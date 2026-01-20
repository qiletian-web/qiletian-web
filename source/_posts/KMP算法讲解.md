---
title: KMP算法讲解
abbrlink: a7d291d5
date: 2026-01-20 23:25:52
updated: 2026-1-20 23:44:14
categories: arithmetic
tags:
  - - KMP
---

# KMP 算法详解 (Knuth-Morris-Pratt Algorithm)

## 1. 什么是 KMP？

**KMP 算法**是一种改进的字符串匹配算法，由 D.E.Knuth，J.H.Morris 和 V.R.Pratt 同时发现。

* **解决问题**：在一个**文本串 (Text)** 中查找一个**模式串 (Pattern)** 出现的位置。
* **核心优势**：当出现字符串不匹配时，可以知道一部分之前已经匹配的文本内容，利用这些信息避免从头再去做匹配。
    * 暴力解法复杂度：$O(m \times n)$
    * KMP 算法复杂度：$O(m + n)$

---

## 2. 核心思想：拒绝“无脑”回退

在朴素的暴力匹配（Brute Force）中，一旦字符不匹配，文本串的指针 `i` 会回退到上一次开始匹配的下一个位置，模式串的指针 `j` 回退到 0。这导致了大量的重复比较。

**KMP 的聪明之处**在于：
当 `text[i]` 和 `pattern[j]` 不匹配时，KMP 利用已经匹配过的 `pattern[0...j-1]` 这部分信息，**将模式串向右移动“尽可能多”的距离**，而不是只移动一位，并且**文本串指针 `i` 永远不回退**。

---

## 3. 关键概念：前缀表 (Next 数组)

KMP 的灵魂在于 **Next 数组**（也称为前缀表）。它记录了模式串中每一个位置之前的子串中，**最长相等前后缀的长度**。

### 3.1 什么是前缀和后缀？
以字符串 `"aabaaf"` 为例：
* **前缀**：包含第一个字符，不包含最后一个字符的所有子串。
    * `a`, `aa`, `aab`, `aaba`, `aabaa`
* **后缀**：包含最后一个字符，不包含第一个字符的所有子串。
    * `f`, `af`, `aaf`, `baaf`, `abaaf`

### 3.2 最长相等前后缀
对于子串 `"aabaa"`：
* 前缀有：`a`, `aa`, `aab`, `aaba`
* 后缀有：`a`, `aa`, `baa`, `abaa`
* **相等且最长**的是 `"aa"`，长度为 **2**。

### 3.3 Next 数组的含义
`next[j]` 表示：当模式串的第 `j` 个字符匹配失败时，模式串应该跳到哪个位置重新开始匹配（也就是跳到最长相等前后缀的后面）。

**示例：模式串 `aabaaf` 的 Next 数组**

| 下标 j | 子串 | 最长相等前后缀 | 长度 (next[j]) |
| :--- | :--- | :--- | :--- |
| 0 | `a` | 无 | 0 |
| 1 | `aa` | `a` | 1 |
| 2 | `aab` | 无 | 0 |
| 3 | `aaba` | `a` | 1 |
| 4 | `aabaa` | `aa` | 2 |
| 5 | `aabaaf` | 无 | 0 |

*(注：具体的 Next 数组实现有多种写法，有的将数值整体右移，有的减一，但核心原理一致。本文采用“当前子串的最长相等前后缀长度”作为标准)*

---

## 4. 算法流程图解

假设文本串 `S = "aabaabaafa"`，模式串 `P = "aabaaf"`。

![描述](../images/KMP.gif)

1.  **匹配开始**：
    ```text
    S: a a b a a b a a f
       | | | | | |
    P: a a b a a f
    ```
    一直匹配到 `S[5] ('b')` 和 `P[5] ('f')` 不相等。此时 `j = 5`。

2.  **查找 Next 数组**：
    查看 `P` 在 `j-1` (即下标 4) 处的 Next 值。
    子串 `"aabaa"` 的最长相等前后缀是 `"aa"`，长度为 **2**。
    这意味着：`P` 开头的两个字符 `aa` 和 `S` 刚才匹配过的最后两个字符 `aa` 是一样的。

3.  **跳转 (不回退 i)**：
    保持 `i` 不变，将 `j` 移动到 `2` (即 Next 数组的值)。
    ```text
    S: a a b a a b a a f
               |
    P:       a a b a a f
               |
    ```
    此时 `P[2] ('b')` 与 `S[5] ('b')` 继续比较。匹配成功！

---

## 5. 代码实现

### 5.1 JavaScript 版本

```javascript
/**
 * 构建 next 数组
 */
function getNext(pattern) {
    let next = [];
    let j = 0; // j 代表前缀末尾位置，也代表最长相等前后缀的长度
    next[0] = 0;

    for (let i = 1; i < pattern.length; i++) {
        // 1. 前后缀不相同，j 回退
        while (j > 0 && pattern[i] !== pattern[j]) {
            j = next[j - 1];
        }
        // 2. 前后缀相同，j 前进
        if (pattern[i] === pattern[j]) {
            j++;
        }
        // 3. 更新 next 数组
        next[i] = j;
    }
    return next;
}

/**
 * KMP 主算法
 * @return {number} 返回模式串在文本串中首次出现的索引，未找到返回 -1
 */
function strStr(text, pattern) {
    if (pattern.length === 0) return 0;

    const next = getNext(pattern);
    let j = 0; // 模式串的指针

    for (let i = 0; i < text.length; i++) { // 文本串指针 i 从不回退
        // 不匹配时，调整 j 的位置
        while (j > 0 && text[i] !== pattern[j]) {
            j = next[j - 1];
        }
        // 匹配时，j 和 i 同时后移
        if (text[i] === pattern[j]) {
            j++;
        }
        // j 到达模式串末尾，说明完全匹配
        if (j === pattern.length) {
            return i - pattern.length + 1;
        }
    }
    return -1;
}

// 测试
console.log(strStr("hello", "ll")); // 输出 2
console.log(strStr("aaaaa", "bba")); // 输出 -1
```

### 5.2 Java / C++ 风格伪代码

```cpp
void getNext(int* next, const string& s) {
    int j = 0;
    next[0] = 0;
    for(int i = 1; i < s.size(); i++) {
        while(j > 0 && s[i] != s[j]) {
            j = next[j - 1];
        }
        if(s[i] == s[j]) {
            j++;
        }
        next[i] = j;
    }
}
```

---

## 6. 复杂度分析

* **时间复杂度**: $O(n + m)$
    * 其中 $n$ 是文本串长度，$m$ 是模式串长度。
    * 生成 Next 数组需要 $O(m)$。
    * 主循环中，文本串指针 `i` 不回退，模式串指针 `j` 虽然会回退，但整体移动次数也是线性的。
* **空间复杂度**: $O(m)$
    * 需要一个长度为 $m$ 的 Next 数组。

## 7. 总结

KMP 算法之所以快，是因为它 **“记性好”** 。它记住了之前匹配过的内容（通过 Next 数组），在遇到不匹配时，不是从头再来，而是**优雅地后退一步**，找到最佳的接续位置继续战斗。

**适用场景**：
* 大规模字符串匹配。
* 不允许文本串指针回退的场景（如数据流读取）。
* 需要查找字符串重复周期的题目（如 LeetCode 459）。