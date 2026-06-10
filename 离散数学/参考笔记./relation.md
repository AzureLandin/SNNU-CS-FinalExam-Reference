# 离散数学 · 关系 学习笔记

##  目录

| 章节 | 标题 | 内容概要 |
|------|------|----------|
| **1** | **有序对与笛卡尔积** | 有序对的集合论定义、n 元组、笛卡尔积及其代数性质 |
| **2** | **关系的基本概念** | 关系的严格定义、定义域/值域/域、表示方法（矩阵与有向图） |
| **3** | **关系的运算** | 逆关系、限制、像与逆像、复合运算、关系的幂 |
| **4** | **关系的性质** | 自反/反自反、对称/反对称、传递、连接/三歧性，以及性质的等价刻画 |
| **5** | **关系的闭包**  | 自反闭包、对称闭包、传递闭包的定义与构造方法、Warshall 算法、闭包组合 |
| **6** | **等价关系与划分** | 等价关系三要素、等价类、商集、划分的严格定义、等价关系与划分的一一对应 |
| **7** | **偏序关系（简要引入）** | 偏序集、Hasse 图概念预告 |
| **8** | **总结** | 核心概念层级图，注意 |

---

## 1. 有序对与笛卡尔积

### 1.1 有序对

在集合论中，**有序对**是二元关系的基础构件。直观上，$(a, b)$ 与 $(b, a)$ 不同（当 $a \neq b$ 时），这区别于无序的集合 $\{a, b\}$。

**核心性质（有序对的本质特征）：**

$$(a, b) = (c, d) \iff a = c \land b = d$$

历史上，有两种经典的纯集合论定义：

#### Wiener 定义（1914）

$$(a, b) \triangleq \{\{\{a\}, \varnothing\}, \{\{b\}\}\}$$

#### Kuratowski 定义（1921，现行标准）

$$(a, b) \triangleq \{\{a\}, \{a, b\}\}$$

**定理（Kuratowski 有序对满足核心性质）：**

$$\{\{a\}, \{a, b\}\} = \{\{c\}, \{c, d\}\} \iff a = c \land b = d$$

> **证明思路**：由两个双元素集合相等，展开为四种析取情形，逐一分析四种情形，消去矛盾分支，最终得出 $a = c$ 且 $b = d$。

**常见误区**：初学者常将 $(a, b)$ 与 $\{a, b\}$ 混淆。请牢记：$(a, b)$ 不是集合意义上的无序对——尽管它可以用集合来编码，但编码后的结构保证顺序信息被完整保留。

---

### 1.2 n 元组

有序对可以递归地推广到任意有限长度：

**定义：**

$$\begin{aligned}
(x, y, z) &\triangleq ((x, y), z) \\
(x_1, x_2, \ldots, x_{n-1}, x_n) &\triangleq ((x_1, x_2, \ldots, x_{n-1}), x_n)
\end{aligned}$$

**定理：**

$$(x_1, \ldots, x_n) = (y_1, \ldots, y_n) \iff x_1 = y_1 \land \cdots \land x_n = y_n$$

> 通过对 $n$ 进行数学归纳法可证明。

---

### 1.3 笛卡尔积

**定义（二元笛卡尔积）：**

$$A \times B \triangleq \{(a, b) \mid a \in A \land b \in B\}$$

**记号：**

$$X^2 \triangleq X \times X$$

**定义（n 元笛卡尔积）：**

$$\begin{aligned}
X_1 \times X_2 \times X_3 &\triangleq (X_1 \times X_2) \times X_3 \\
X_1 \times X_2 \times \cdots \times X_n &\triangleq (X_1 \times \cdots \times X_{n-1}) \times X_n \\
X^n &\triangleq \underbrace{X \times \cdots \times X}_{n \text{ 个}}
\end{aligned}$$

---

### 1.4 笛卡尔积的运算性质

**定理（分配律）：**

$$\begin{aligned}
A \times (B \cap C) &= (A \times B) \cap (A \times C) \\
A \times (B \cup C) &= (A \times B) \cup (A \times C) \\
A \times (B \setminus C) &= (A \times B) \setminus (A \times C)
\end{aligned}$$

> **以第一条为例的证明**：对任意有序对 $(a, b)$，
> $$\begin{aligned}
(a, b) \in A \times (B \cap C)
&\iff a \in A \land b \in (B \cap C) \\
&\iff a \in A \land b \in B \land b \in C \\
&\iff (a \in A \land b \in B) \land (a \in A \land b \in C) \\
&\iff (a, b) \in A \times B \land (a, b) \in A \times C \\
&\iff (a, b) \in (A \times B) \cap (A \times C)
\end{aligned}$$

**重要注意事项：**

- $X \times \varnothing = \varnothing \times X = \varnothing$（与空集的笛卡尔积为空）
- **一般不交换**：$X \times Y \neq Y \times X$（除非 $X = Y$ 或其中之一为空）
- **一般不结合**：$(X \times Y) \times Z \neq X \times (Y \times Z)$（例如 $A = \{1\}$ 时，$((1,1),1) \neq (1,(1,1))$）

---

## 2. 关系的基本概念

### 2.1 关系的定义

**定义：**

> 设 $A, B$ 为集合。从 $A$ 到 $B$ 的一个**关系** $R$ 是笛卡尔积 $A \times B$ 的一个子集：
> $$R \subseteq A \times B$$
> 当 $A = B$ 时，称 $R$ 为 **$A$ 上的关系**。

**记号：**

$$(a, b) \in R \quad\text{记为}\quad aRb$$
$$(a, b) \notin R \quad\text{记为}\quad a\not\!R\,b$$

**核心理解**：关系就是有序对的集合——这是一个极其精炼的集合论还原。任何满足“某些对象之间存在某种关联”的直觉，都可以形式化为笛卡尔积的适当子集。

**典型例子：**

1. 全域关系 $A \times B$ 和空关系 $\varnothing$ 都是关系
2. 小于关系：$< \; = \{(a, b) \in \mathbb{R} \times \mathbb{R} \mid a \text{ is less than } b\}$
3. 整除关系：$D = \{(a, b) \in \mathbb{N} \times \mathbb{N} \mid \exists q \in \mathbb{N}.\; a \cdot q = b\}$
4. 亲属关系（设 $P$ 为所有人的集合）：
   - $M = \{(a, b) \in P \times P \mid a \text{ is the mother of } b\}$
   - $B = \{(a, b) \in P \times P \mid a \text{ is the brother of } b\}$

**三大重要关系类型（预告）：**
- **等价关系**（本章重点）
- **序关系**（后续）
- **函数**（后续，函数是特殊的关系：单值性）

---

### 2.2 定义域、值域和域

**定义：**

$$\begin{aligned}
\text{定义域（Domain）：}\quad &\operatorname{dom}(R) = \{a \mid \exists b.\; (a, b) \in R\} \\
\text{值域（Range）：}\quad &\operatorname{ran}(R) = \{b \mid \exists a.\; (a, b) \in R\} \\
\text{域（Field）：}\quad &\operatorname{fld}(R) = \operatorname{dom}(R) \cup \operatorname{ran}(R)
\end{aligned}$$

**示例：**

- $R = \{(x, y) \mid x = y\} \subseteq \mathbb{R} \times \mathbb{R}$：
  $\operatorname{dom}(R) = \operatorname{ran}(R) = \operatorname{fld}(R) = \mathbb{R}$

- $R = \{(x, y) \mid x^2 + y^2 = 1\} \subseteq \mathbb{R} \times \mathbb{R}$：
  $\operatorname{dom}(R) = \operatorname{ran}(R) = \operatorname{fld}(R) = [-1, 1]$

**定理（定义域、值域与并集的关系）：**

$$\operatorname{dom}(R) \subseteq \bigcup\bigcup R, \qquad \operatorname{ran}(R) \subseteq \bigcup\bigcup R$$

> 这一定理揭示了关系的集合论编码下，定义域中的元素确实可以从集合的迭代并集中“检索”出来。

---

### 2.3 关系的表示方法

#### 2.3.1 关系矩阵

设 $A = \{a_1, a_2, \ldots, a_m\}$，$B = \{b_1, b_2, \ldots, b_n\}$，$R \subseteq A \times B$。定义 **关系矩阵** $M_R = (m_{ij})_{m \times n}$：

$$m_{ij} = \begin{cases}
1, & \text{若 } (a_i, b_j) \in R \\
0, & \text{若 } (a_i, b_j) \notin R
\end{cases}$$

**示例**：$A = \{1, 2, 3\}$，$R = \{(1, 1), (1, 3), (2, 1), (2, 2), (3, 3)\}$

$$M_R = \begin{pmatrix}
1 & 0 & 1 \\
1 & 1 & 0 \\
0 & 0 & 1
\end{pmatrix}$$

> 关系矩阵是布尔矩阵（元素仅取 $0, 1$），可以直接用于关系的运算（如复合对应布尔矩阵乘法）。

#### 2.3.2 有向图

若 $R$ 是有限集合 $A$ 上的关系，可以用有向图表示：
- 顶点集 = $A$
- 有向边集 = $R$（即 $(a, b) \in R$ 对应从 $a$ 到 $b$ 的一条有向边）

自反性对应每个顶点有自环，对称性对应所有边为双向边，传递性对应“若存在 $a \to b \to c$ 的路径，则必有直接边 $a \to c$”。

---

## 3. 关系的运算

### 3.1 逆关系

**定义：**

$$R^{-1} = \{(a, b) \mid (b, a) \in R\}$$

**示例：**

- $R = \{(x, y) \mid x = y\} \implies R^{-1} = R$
- $R = \{(x, y) \mid y = \sqrt{x}\} \implies R^{-1} = \{(x, y) \mid y = x^2 \land x > 0\}$
- $\leq \; = \{(x, y) \mid x \leq y\} \implies \;\leq^{-1}\; = \;\geq\; \triangleq \{(x, y) \mid x \geq y\}$

**定理：**

1. $(R^{-1})^{-1} = R$
2. $(R \cup S)^{-1} = R^{-1} \cup S^{-1}$
3. $(R \cap S)^{-1} = R^{-1} \cap S^{-1}$
4. $(R \setminus S)^{-1} = R^{-1} \setminus S^{-1}$

---

### 3.2 限制

**定义（左限制 / Left-Restriction）：** 设 $R \subseteq X \times Y$，$S \subseteq X$。

$$R|_{S}^{\text{left}} = \{(x, y) \in R \mid x \in S\}$$

**定义（右限制 / Right-Restriction）：** 设 $S \subseteq Y$。

$$R|_{S}^{\text{right}} = \{(x, y) \in R \mid y \in S\}$$

**定义（限制 / Restriction）：** 设 $R \subseteq X \times X$，$S \subseteq X$。

$$R|_{S} = \{(x, y) \in R \mid x \in S \land y \in S\}$$

> 限制运算相当于将关系的范围缩小到 $S$ 上。

---

### 3.3 像与逆像

**定义（像 / Image）：**

$$R[X] = \{b \in \operatorname{ran}(R) \mid \exists a \in X.\; (a, b) \in R\}$$

特别地，$R[\{a\}]$ 简记为 $R[a] = \{b \mid (a, b) \in R\}$。

**定义（逆像 / Inverse Image）：**

$$R^{-1}[Y] = \{a \in \operatorname{dom}(R) \mid \exists b \in Y.\; (a, b) \in R\}$$

特别地，$R^{-1}[\{b\}]$ 简记为 $R^{-1}[b] = \{a \mid (a, b) \in R\}$。

**像的运算性质：**

$$\begin{aligned}
R[X_1 \cup X_2] &= R[X_1] \cup R[X_2] \quad \text{（像对并集分配）} \\
R[X_1 \cap X_2] &\subseteq R[X_1] \cap R[X_2] \quad \text{（像对交集仅单向包含！）} \\
R[X_1 \setminus X_2] &\supseteq R[X_1] \setminus R[X_2] \quad \text{（注意方向）}
\end{aligned}$$

> **关键注意**：第二条和第三条仅为包含关系而非相等。这是因为不同的 $a_1 \in X_1, a_2 \in X_2$ 可能映射到同一个 $b$。

---

### 3.4 复合运算

**定义：** 设 $R \subseteq X \times Y$，$S \subseteq Y \times Z$。$R$ 与 $S$ 的**复合**为：

$$R \circ S = \{(a, c) \mid \exists b.\; (a, b) \in S \land (b, c) \in R\}$$



**示例：**

$R = \{(1, 2), (3, 1)\}$，$S = \{(1, 3), (2, 2), (2, 3)\}$

- $R \circ S = \{(1, 1), (2, 1)\}$
- $S \circ R = \{(1, 2), (1, 3), (3, 3)\}$（注意复合不交换！）
- $R^{(2)} \triangleq R \circ R = \{(3, 2)\}$
- $S^{(2)} \triangleq S \circ S = \{(2, 2), (2, 3)\}$

**经典示例：**

- $\leq \circ \leq = \leq$
- $\geq \circ \leq = \mathbb{R} \times \mathbb{R}$

**定理（复合的代数性质）：**

1. **逆的分配**：$(R \circ S)^{-1} = S^{-1} \circ R^{-1}$
2. **结合律**：$(R \circ S) \circ T = R \circ (S \circ T)$
3. **对并集的分配**：$(X \cup Y) \circ Z = (X \circ Z) \cup (Y \circ Z)$
4. **对交集的单向包含**：$(X \cap Y) \circ Z \subseteq (X \circ Z) \cap (Y \circ Z)$

---

### 3.5 关系的幂

设 $R \subseteq A \times A$，定义：

$$\begin{aligned}
R^{(1)} &= R \\
R^{(n+1)} &= R^{(n)} \circ R
\end{aligned}$$

（某些教材记 $R^n = R \circ R \circ \cdots \circ R$（$n$ 次），需记号的对应。）

---

## 4. 关系的性质

> 研究关系 $R \subseteq X \times X$（即 $X$ 上的二元关系）的七种核心性质。

### 4.1 自反性与反自反性

**定义（自反性 / Reflexive）：**

$$R \text{ 是自反的} \iff \forall a \in X.\; (a, a) \in R$$

**示例**：$\leq$ 在 $\mathbb{R}$ 上是自反的（因为 $\forall a.\; a \leq a$）。

**定义（反自反性 / Irreflexive）：**

$$R \text{ 是反自反的} \iff \forall a \in X.\; (a, a) \notin R$$

**示例**：$<$ 在 $\mathbb{R}$ 上是反自反的（没有 $a < a$）。

> **注意**：一个关系可以既不自反也不反自反（例如部分元素有自环、部分没有）。

**等价刻画：**

$$R \text{ 是自反的} \iff I_X \subseteq R$$

其中 $I_X = \{(a, a) \mid a \in X\}$ 为 $X$ 上的**恒等关系**。

---

### 4.2 对称性与反对称性

**定义（对称性 / Symmetric）：**

$$R \text{ 是对称的} \iff \forall a, b \in X.\; (aRb \to bRa)$$

由于对称性本身蕴含双向，等价于 $\forall a, b.\; (aRb \leftrightarrow bRa)$。

**示例**：$X = \{1, 2, 3\}$，$R = \{(1, 1), (1, 2), (1, 3), (2, 1), (3, 1), (3, 3)\}$ 是对称的。

**定义（反对称性 / Antisymmetric）：**

$$R \text{ 是反对称的} \iff \forall a, b \in X.\; (aRb \land bRa \to a = b)$$

**示例**：$\geq$ 是反对称的（若 $a \geq b$ 且 $b \geq a$，则 $a = b$）；整除关系 $|$ 在 $\mathbb{N}$ 上是反对称的。

**等价刻画：**

$$R \text{ 是对称的} \iff R^{-1} = R$$

> **辨析**：对称性和反对称性并非互斥——例如 $I_X$（恒等关系）既对称又反对称。

---

### 4.3 传递性（Transitive）

**定义：**

$$R \text{ 是传递的} \iff \forall a, b, c \in X.\; (aRb \land bRc \to aRc)$$

**示例**：$\leq$、$<$、整除关系 $|$ 都是传递的。

**非传递示例**：$R = \{(1, 2), (2, 3), (3, 1)\}$ 不是传递的（$(1, 2) \land (2, 3)$ 成立但 $(1, 3) \notin R$）；$R = \{(1, 3)\}$ 是传递的（前提不成立，蕴含式真空为真）。

**等价刻画：**

$$R \text{ 是传递的} \iff R \circ R \subseteq R$$

> **理解**：$R \circ R$ 恰好是所有“两步可达”的有序对集合；传递性要求所有两步可达的必须已经一步可达。

**定理（对称+传递的等价刻画）：**

$$R \text{ 是对称且传递的} \iff R = R^{-1} \circ R$$

---

### 4.4 连接性与三歧性

**定义（连接性 / Connex）：**

$$R \text{ 是连接的} \iff \forall a, b \in X.\; (aRb \lor bRa)$$

**定义（三歧性 / Trichotomous）：**

$$R \text{ 是三歧的} \iff \forall a, b \in X.\; (\text{exactly one of } aRb, bRa, a = b \text{ holds})$$

> 连接性（又称“完全性”）加上反对称性和传递性构成**全序关系**的特征。

---

### 4.5 性质的综合判断方法

对于有限集上的关系 $R$，可以通过**关系矩阵**或**有向图**直观判断：

| 性质 | 关系矩阵特征 | 有向图特征 |
|------|-------------|-----------|
| **自反性** | 主对角线全为 $1$ | 每个顶点有自环 |
| **反自反性** | 主对角线全为 $0$ | 每个顶点无自环 |
| **对称性** | $M_R = M_R^T$（对称矩阵） | 所有边为双向边 |
| **反对称性** | $m_{ij} = 1 \land m_{ji} = 1 \implies i = j$ | 无双向边（除自环） |
| **传递性** | $M_R^2 \leq M_R$（布尔矩阵意义下） | 长度为2的路径必被直接边替代 |

---

## 5. 关系的闭包

> 本部分为参考课程所缺，但属于关系理论的核心内容，此处参照国内外教材进行补充。

### 5.1 闭包的概念

**直观理解**：给定关系 $R$，若 $R$ 不满足某一性质 $P$，我们希望向 $R$ 中添加**尽可能少**的有序对，使其满足 $P$。这样得到的新关系称为 $R$ 的 **$P$-闭包**。

**严格定义**：设 $R \subseteq A \times A$，$P$ 为某种关系性质（自反、对称、传递）。$R$ 关于性质 $P$ 的**闭包** $C(R)$ 满足：

1. $C(R)$ 具有性质 $P$（即 $C(R)$ 满足 $P$）
2. $R \subseteq C(R)$（闭包包含原关系）
3. 对任意具有性质 $P$ 的关系 $S$，若 $R \subseteq S$，则 $C(R) \subseteq S$（$C(R)$ 是最小的）

---

### 5.2 自反闭包

**定义：** $R$ 的**自反闭包**，记为 $r(R)$，是包含 $R$ 的最小自反关系。

**构造方法：**

$$r(R) = R \cup I_A$$

其中 $I_A = \{(a, a) \mid a \in A\}$。

**示例**：$A = \{1, 2, 3\}$，$R = \{(1, 2), (2, 3)\}$，则：

$$r(R) = \{(1, 2), (2, 3), (1, 1), (2, 2), (3, 3)\}$$

**关系矩阵视角**：将 $M_R$ 的主对角线全改为 $1$。

---

### 5.3 对称闭包

**定义：** $R$ 的**对称闭包**，记为 $s(R)$，是包含 $R$ 的最小对称关系。

**构造方法：**

$$s(R) = R \cup R^{-1}$$

**示例**：$R = \{(1, 2), (2, 3)\}$，则：

$$R^{-1} = \{(2, 1), (3, 2)\}$$
$$s(R) = \{(1, 2), (2, 3), (2, 1), (3, 2)\}$$

**关系矩阵视角**：$M_{s(R)} = M_R \lor M_R^T$（布尔“或”运算）。

---

### 5.4 传递闭包

**定义：** $R$ 的**传递闭包**，记为 $t(R)$ 或 $R^+$，是包含 $R$ 的最小传递关系。

**构造方法（基于关系幂的并集）：**

$$t(R) = \bigcup_{n=1}^{\infty} R^{(n)} = R \cup R^{(2)} \cup R^{(3)} \cup \cdots$$

若 $A$ 为有限集且 $|A| = n$，则：

$$t(R) = \bigcup_{k=1}^{n} R^{(k)}$$

**连通性解释**：$(a, b) \in t(R)$ 当且仅当在 $R$ 的有向图中存在从 $a$ 到 $b$ 的路径（长度 $\geq 1$）。

**示例**：$A = \{1, 2, 3, 4\}$，$R = \{(1, 2), (2, 3), (3, 4)\}$

$$\begin{aligned}
R^{(1)} &= \{(1, 2), (2, 3), (3, 4)\} \\
R^{(2)} &= \{(1, 3), (2, 4)\} \\
R^{(3)} &= \{(1, 4)\} \\
R^{(4)} &= \varnothing \\
t(R) &= \{(1, 2), (2, 3), (3, 4), (1, 3), (2, 4), (1, 4)\}
\end{aligned}$$

**重要的闭包公式：**

$$R^* \; (\text{自反传递闭包}) = t(r(R)) = r(t(R)) = \bigcup_{k=0}^{\infty} R^{(k)} = I_A \cup R \cup R^{(2)} \cup \cdots$$

其中 $R^{(0)} = I_A$。

---

### 5.5 Warshall 算法（求传递闭包的高效算法）

对于有限集 $A = \{a_1, a_2, \ldots, a_n\}$ 上的关系 $R$，直接计算所有关系幂的并集复杂度较高（布尔矩阵乘法每次 $O(n^3)$，共需 $O(n^4)$）。**Warshall 算法**在 $O(n^3)$ 时间内求出传递闭包。

**算法思想**（动态规划）：逐步允许中间顶点通过 $a_1, a_2, \ldots, a_k$ 来构造路径。

**算法描述**（设 $W = M_R$）：

```python
# Warshall 算法求传递闭包
# 输入：关系矩阵 W（n×n 布尔矩阵）
# 输出：传递闭包的关系矩阵

for k in range(n):
    for i in range(n):
        for j in range(n):
            W[i][j] = W[i][j] or (W[i][k] and W[k][j])
```

第 $k$ 轮迭代后，$W[i][j] = 1$ 当且仅当存在从 $a_i$ 到 $a_j$ 的路径，且所有中间顶点均来自 $\{a_1, \ldots, a_k\}$。

**示例演示**：

$$M_R = \begin{pmatrix}
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0
\end{pmatrix}$$

经过 Warshall 算法处理后：

$$M_{t(R)} = \begin{pmatrix}
0 & 1 & 1 & 1 \\
0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 \\
0 & 0 & 0 & 0
\end{pmatrix}$$

---

### 5.6 多种闭包的组合

**定理（闭包的交换性与包含关系）：**

设 $R \subseteq A \times A$。

1. $r(s(R)) = s(r(R))$（自反闭包与对称闭包可交换）
2. $r(t(R)) = t(r(R))$（自反闭包与传递闭包可交换）
3. $s(t(R)) \subseteq t(s(R))$（注意方向：先对称闭包再传递闭包更大！）

**举例说明第 3 条**：$R = \{(1, 2)\}$ 在 $A = \{1, 2, 3\}$ 上：

- $s(R) = \{(1, 2), (2, 1)\}$，$t(s(R)) = \{(1, 2), (2, 1), (1, 1), (2, 2)\}$
- $t(R) = \{(1, 2)\}$，$s(t(R)) = \{(1, 2), (2, 1)\}$

可见 $s(t(R)) \subsetneq t(s(R))$。

> 若需要同时满足对称性和传递性，**应先求对称闭包再求传递闭包**，否则可能得不到正确结果。

---

## 6. 等价关系与划分

### 6.1 等价关系的定义

**定义（等价关系）：**

$R \subseteq X \times X$ 是 $X$ 上的**等价关系**，当且仅当 $R$ 同时满足：

1. **自反性**：$\forall a \in X.\; aRa$
2. **对称性**：$\forall a, b \in X.\; (aRb \leftrightarrow bRa)$
3. **传递性**：$\forall a, b, c \in X.\; (aRb \land bRc \to aRc)$

**经典示例**：

- $=$ 在 $\mathbb{R}$ 上（相等关系）
- $\parallel$ 在直线集合 $L$ 上（平行关系）
- **模 $k$ 同余**：$R = \{(x, y) \mid x \equiv y \pmod{k}\} \subseteq \mathbb{Z} \times \mathbb{Z}$




> 等价关系提供了“视为相同”的形式化手段——它将集合中的元素按照某种共同特征进行分组，从而实现对具体差异的**抽象**。这是数学中构造新对象（如从 $\mathbb{N}$ 构造 $\mathbb{Z}$、从 $\mathbb{Z}$ 构造 $\mathbb{Q}$）的核心工具。

---

### 6.2 等价类

**定义：**

$$[a]_R = \{b \in X \mid aRb\}$$

称 $[a]_R$ 为 $a$ 关于 $R$ 的**等价类**，$a$ 称为该等价类的**代表元**。

**关键定理：**

$$\forall a, b \in X.\; ([a]_R = [b]_R \leftrightarrow aRb)$$

> **证明**：若 $aRb$，由对称和传递可证两个等价类互为子集；若等价类相等，则 $b \in [b]_R = [a]_R$，故 $aRb$。

**等价类的本质性质（划分性质）：**

$$\forall a, b \in X.\; [a]_R \cap [b]_R = \varnothing \lor [a]_R = [b]_R$$

> 即两个等价类要么完全不相交，要么完全相同。

---

### 6.3 商集

**定义：**

$$X/R = \{[a]_R \mid a \in X\}$$

$X/R$ 称为 $X$ 模 $R$ 的**商集**，它是所有等价类构成的集合（集合的集合）。

**示例**：

- 对 $=$ 在 $\mathbb{R}$ 上：$\mathbb{R}/= \; = \{\{x\} \mid x \in \mathbb{R}\}$（孤立点集族）
- 对模 $k$ 同余在 $\mathbb{Z}$ 上：$\mathbb{Z}/\equiv_k \; = \{[0], [1], \ldots, [k-1]\}$

**定理：** $X/R$ 是 $X$ 的一个划分。

---

### 6.4 划分

**定义（划分的严格表述）：**

集族 $\Pi = \{A_\alpha \mid \alpha \in I\}$ 是 $X$ 的一个**划分**，当且仅当：

1. **非空性**：$\forall \alpha \in I.\; A_\alpha \neq \varnothing$
2. **覆盖性**：$\bigcup_{\alpha \in I} A_\alpha = X$（即 $\forall x \in X.\; \exists \alpha \in I.\; x \in A_\alpha$）
3. **互不相交性**：$\forall \alpha, \beta \in I.\; A_\alpha \cap A_\beta \neq \varnothing \to A_\alpha = A_\beta$

（第三条亦可表述为：$\forall \alpha, \beta \in I.\; A_\alpha \cap A_\beta = \varnothing \lor A_\alpha = A_\beta$）

---

### 6.5 等价关系与划分的一一对应



**定理（等价关系 $\Rightarrow$ 划分）：**

若 $R$ 是 $X$ 上的等价关系，则商集 $X/R = \{[a]_R \mid a \in X\}$ 构成 $X$ 的一个划分。

**定理（划分 $\Rightarrow$ 等价关系）：**

若 $\Pi$ 是 $X$ 的一个划分，定义关系 $R_\Pi$：

$$(a, b) \in R_\Pi \iff \exists S \in \Pi.\; a \in S \land b \in S$$

则 $R_\Pi$ 是 $X$ 上的等价关系。

**结论：**

$$ \text{等价关系} \;\longleftrightarrow\; \text{划分} $$

两者之间存在**双射**，每个等价关系唯一确定一个划分，反之亦然。

---

## 7. 偏序关系（简要引入）



**定义（偏序关系）：**

$R \subseteq X \times X$ 是 $X$ 上的**偏序关系**，若 $R$ 满足：

1. **自反性**
2. **反对称性**
3. **传递性**

偏序集记作 $(X, \preccurlyeq)$。若额外满足**连接性**（$\forall a, b.\; a \preccurlyeq b \lor b \preccurlyeq a$），则为**全序关系**。

**Hasse 图**是表示有限偏序集的精简有向图，用于后续深入研究序结构。

---

## 8. 总结



```
有序对 → 笛卡尔积 → 关系（= 笛卡尔积子集）
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
        关系运算        关系性质          关系闭包
      (逆/限制/像/     (自反/对称/      (自反闭包/
       复合/幂)         传递等)         对称闭包/
                                        传递闭包)
                            │
                            ▼
                      等价关系
                            │
                            ▼
                    等价类 + 商集
                            │
                            ▼
                         划分
                            │
                            ▼
                  应用：构造 ℤ, ℚ
```

### 注意

1. **对称性与反对称性不是互斥的**：恒等关系 $I_X$ 既对称又反对称。
2. **传递性与“真空满足”**：若前提 $aRb \land bRc$ 从不成立（如仅有一个有序对的关系），传递性自动成立。
3. **$R \circ S$ 的顺序**：课件中 $(a, c) \in R \circ S$ 要求 $(a, b) \in S$ 且 $(b, c) \in R$。这与函数复合的记号习惯一致（先应用 $S$ 再应用 $R$），但部分教材反过来定义，务必确认。
4. **像运算对交集不保持相等**：$R[X_1 \cap X_2] \subseteq R[X_1] \cap R[X_2]$ 仅为包含，反例：$R = \{(1, 3), (2, 3)\}$，$X_1 = \{1\}, X_2 = \{2\}$。
5. **闭包的顺序至关重要**：$s(t(R)) \neq t(s(R))$ 一般而言，先对称后传递才是正确的“等价闭包”求法。