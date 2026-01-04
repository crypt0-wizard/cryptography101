# Modular Arithmetic: The Mathematics of Finite Systems

Modular arithmetic is the mathematical foundation that makes modern cryptography possible. Think of it as "clock arithmetic" – when you go past 12 on a clock, you wrap around to 1. This simple concept leads to profound mathematical structures that protect everything from your credit card transactions to secure messaging.

## The Fundamental Concept: Congruence

### Definition and Intuition

For integers $a$, $b$, and positive integer $n$, we say $a$ is **congruent** to $b$ modulo $n$, written as:

$$a \equiv b \pmod{n}$$

if and only if $n$ divides $(a - b)$, which we write as $n \mid (a - b)$.

**Equivalent characterizations:**

$$a \equiv b \pmod{n} \iff \exists k \in \mathbb{Z} : a = b + kn$$

$$a \equiv b \pmod{n} \iff a \bmod n = b \bmod n$$

**Examples:**
- $17 \equiv 5 \pmod{12}$ because $17 - 5 = 12$ and $12 \mid 12$
- $-3 \equiv 9 \pmod{12}$ because $-3 - 9 = -12$ and $12 \mid (-12)$
- $100 \equiv 4 \pmod{8}$ because $100 = 12 \times 8 + 4$

### The Division Algorithm

The mathematical foundation of modular arithmetic rests on the **Division Algorithm**:

**Theorem:** For any integer $a$ and positive integer $n$, there exist unique integers $q$ (quotient) and $r$ (remainder) such that:

$$a = qn + r \quad \text{where} \quad 0 \leq r < n$$

The remainder $r$ is denoted $a \bmod n$, and we have $a \equiv r \pmod{n}$.

## Properties of Congruence Relations

Congruence modulo $n$ is an **equivalence relation**, satisfying three fundamental properties:

### Reflexivity

$$\forall a \in \mathbb{Z}: \quad a \equiv a \pmod{n}$$

**Proof:** Since $a - a = 0$ and $n \mid 0$, we have $a \equiv a \pmod{n}$. $\square$

### Symmetry

$$a \equiv b \pmod{n} \implies b \equiv a \pmod{n}$$

**Proof:** If $n \mid (a - b)$, then $a - b = kn$ for some $k \in \mathbb{Z}$. Thus $b - a = -kn = (-k)n$, so $n \mid (b - a)$. $\square$

### Transitivity

$$a \equiv b \pmod{n} \land b \equiv c \pmod{n} \implies a \equiv c \pmod{n}$$

**Proof:** If $a - b = k_1 n$ and $b - c = k_2 n$, then:

$$a - c = (a - b) + (b - c) = k_1 n + k_2 n = (k_1 + k_2)n$$

Therefore $n \mid (a - c)$. $\square$

## Arithmetic Operations

### Addition and Subtraction

**Theorem:** If $a \equiv a' \pmod{n}$ and $b \equiv b' \pmod{n}$, then:

$$a + b \equiv a' + b' \pmod{n}$$

$$a - b \equiv a' - b' \pmod{n}$$

**Computational formula:**

$$(a + b) \bmod n = \big((a \bmod n) + (b \bmod n)\big) \bmod n$$

**Example:**

$$(23 + 17) \bmod 10 = (3 + 7) \bmod 10 = 10 \bmod 10 = 0$$

### Multiplication

**Theorem:** If $a \equiv a' \pmod{n}$ and $b \equiv b' \pmod{n}$, then:

$$a \cdot b \equiv a' \cdot b' \pmod{n}$$

**Proof:** Let $a = a' + k_1 n$ and $b = b' + k_2 n$. Then:

$$ab = (a' + k_1 n)(b' + k_2 n) = a'b' + n(a'k_2 + b'k_1 + k_1 k_2 n)$$

Therefore $ab \equiv a'b' \pmod{n}$. $\square$

### Exponentiation

**Theorem:** If $a \equiv b \pmod{n}$, then for any positive integer $k$:

$$a^k \equiv b^k \pmod{n}$$

## The Ring Structure: $\mathbb{Z}/n\mathbb{Z}$

### Equivalence Classes

The congruence relation partitions $\mathbb{Z}$ into $n$ equivalence classes:

$$[0] = \{\ldots, -2n, -n, 0, n, 2n, \ldots\}$$

$$[1] = \{\ldots, -2n+1, -n+1, 1, n+1, 2n+1, \ldots\}$$

$$\vdots$$

$$[n-1] = \{\ldots, -n-1, -1, n-1, 2n-1, 3n-1, \ldots\}$$

The set $\mathbb{Z}/n\mathbb{Z} = \{[0], [1], \ldots, [n-1]\}$ forms a **commutative ring** with:

| Property | Definition |
|----------|------------|
| Additive identity | $[0]$ |
| Multiplicative identity | $[1]$ |
| Additive inverse of $[a]$ | $[n-a]$ |

## Multiplicative Inverses

### Definition and Existence

An element $[a] \in \mathbb{Z}/n\mathbb{Z}$ has a **multiplicative inverse** if there exists $[b]$ such that:

$$[a] \cdot [b] = [1] \quad \text{i.e.,} \quad ab \equiv 1 \pmod{n}$$

**Fundamental Theorem:** The multiplicative inverse of $a$ modulo $n$ exists if and only if:

$$\gcd(a, n) = 1$$

**Proof ($\Leftarrow$):** If $\gcd(a, n) = 1$, by Bézout's identity there exist $x, y \in \mathbb{Z}$ such that:

$$ax + ny = 1$$

This gives $ax \equiv 1 \pmod{n}$, so $x \equiv a^{-1} \pmod{n}$. $\square$

### The Group of Units

The **group of units** modulo $n$ is:

$$(\mathbb{Z}/n\mathbb{Z})^* = \{[a] \in \mathbb{Z}/n\mathbb{Z} : \gcd(a, n) = 1\}$$

This forms a **multiplicative group** with order:

$$\left|(\mathbb{Z}/n\mathbb{Z})^*\right| = \varphi(n)$$

where $\varphi$ is Euler's totient function.

**Examples:**

$$(\mathbb{Z}/5\mathbb{Z})^* = \{[1], [2], [3], [4]\}, \quad \left|(\mathbb{Z}/5\mathbb{Z})^*\right| = 4$$

$$(\mathbb{Z}/8\mathbb{Z})^* = \{[1], [3], [5], [7]\}, \quad \left|(\mathbb{Z}/8\mathbb{Z})^*\right| = 4$$

## Computing Multiplicative Inverses

### Extended Euclidean Algorithm

To find $a^{-1} \bmod n$, solve for $x$ in:

$$ax + ny = \gcd(a, n) = 1$$

```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    gcd, x1, y1 = extended_gcd(b, a % b)
    x = y1
    y = x1 - (a // b) * y1
    return gcd, x, y

def mod_inverse(a, n):
    gcd, x, _ = extended_gcd(a, n)
    if gcd != 1:
        raise ValueError("Inverse does not exist")
    return x % n
```

**Example:** Find $7^{-1} \bmod 11$

Using the Extended Euclidean Algorithm:

$$11 = 1 \times 7 + 4$$
$$7 = 1 \times 4 + 3$$
$$4 = 1 \times 3 + 1$$

Back-substitution:

$$1 = 4 - 1 \times 3 = 4 - (7 - 4) = 2 \times 4 - 7 = 2(11 - 7) - 7 = 2 \times 11 - 3 \times 7$$

Therefore: $7^{-1} \equiv -3 \equiv 8 \pmod{11}$

### Fermat's Little Theorem Method

For prime $p$ and $\gcd(a, p) = 1$:

$$a^{p-1} \equiv 1 \pmod{p}$$

**Corollary:**

$$a^{-1} \equiv a^{p-2} \pmod{p}$$

## Euler's Totient Function

### Definition

For positive integer $n$, Euler's totient function counts integers coprime to $n$:

$$\varphi(n) = \left|\{k : 1 \leq k \leq n, \gcd(k, n) = 1\}\right|$$

### Key Properties

**For prime $p$:**

$$\varphi(p) = p - 1$$

**For prime power $p^k$:**

$$\varphi(p^k) = p^k - p^{k-1} = p^{k-1}(p - 1)$$

**Multiplicative property:** If $\gcd(m, n) = 1$:

$$\varphi(mn) = \varphi(m) \cdot \varphi(n)$$

**General formula:** For $n = p_1^{a_1} p_2^{a_2} \cdots p_k^{a_k}$:

$$\varphi(n) = n \prod_{i=1}^{k} \left(1 - \frac{1}{p_i}\right)$$

**Example:**

$$\varphi(12) = \varphi(2^2 \cdot 3) = 12 \cdot \left(1 - \frac{1}{2}\right) \cdot \left(1 - \frac{1}{3}\right) = 12 \cdot \frac{1}{2} \cdot \frac{2}{3} = 4$$

## Euler's Theorem

**Theorem:** If $\gcd(a, n) = 1$, then:

$$a^{\varphi(n)} \equiv 1 \pmod{n}$$

**Corollary:**

$$a^{-1} \equiv a^{\varphi(n)-1} \pmod{n}$$

**Proof sketch:** The set $S = \{r_1, r_2, \ldots, r_{\varphi(n)}\}$ of residues coprime to $n$ satisfies:

$$\prod_{i=1}^{\varphi(n)} r_i \equiv \prod_{i=1}^{\varphi(n)} (ar_i) \equiv a^{\varphi(n)} \prod_{i=1}^{\varphi(n)} r_i \pmod{n}$$

Canceling gives $a^{\varphi(n)} \equiv 1 \pmod{n}$. $\square$

## Efficient Modular Exponentiation

Computing $a^b \bmod n$ efficiently using **binary exponentiation**:

```python
def mod_exp(base, exp, mod):
    result = 1
    base = base % mod
    while exp > 0:
        if exp & 1:
            result = (result * base) % mod
        base = (base * base) % mod
        exp >>= 1
    return result
```

**Complexity:** $O(\log b)$ multiplications

**Example:** Compute $3^{13} \bmod 7$

Binary: $13 = 1101_2$

| Step | exp (binary) | Action | result | base |
|------|--------------|--------|--------|------|
| 1 | 1101 | multiply | $3$ | $3^2 \equiv 2$ |
| 2 | 110 | square only | $3$ | $2^2 \equiv 4$ |
| 3 | 11 | multiply | $3 \times 4 \equiv 5$ | $4^2 \equiv 2$ |
| 4 | 1 | multiply | $5 \times 2 \equiv 3$ | — |

**Result:** $3^{13} \equiv 3 \pmod{7}$

## Chinese Remainder Theorem

### Statement

Let $n_1, n_2, \ldots, n_k$ be pairwise coprime. The system:

$$$
\begin{cases}
x \equiv a_1 \pmod{n_1} \\
x \equiv a_2 \pmod{n_2} \\
\vdots \\
x \equiv a_k \pmod{n_k}
\end{cases}
$$$

has a **unique solution** modulo $N = n_1 n_2 \cdots n_k$.

### Construction

Let $N_i = \dfrac{N}{n_i}$ and find $M_i$ such that $N_i M_i \equiv 1 \pmod{n_i}$.

The solution is:

$$x \equiv \sum_{i=1}^{k} a_i N_i M_i \pmod{N}$$

### RSA Optimization

For RSA with $n = pq$, instead of computing $m \equiv c^d \pmod{n}$:

$$m_p \equiv c^{d \bmod (p-1)} \pmod{p}$$

$$m_q \equiv c^{d \bmod (q-1)} \pmod{q}$$

Combine using CRT for ~4× speedup.

## Quadratic Residues

### Definition

An integer $a$ is a **quadratic residue** modulo $n$ if:

$$\exists x \in \mathbb{Z}: \quad x^2 \equiv a \pmod{n}$$

**Example (mod 7):**

| $x$ | $x^2 \bmod 7$ |
|-----|---------------|
| 1 | 1 |
| 2 | 4 |
| 3 | 2 |
| 4 | 2 |
| 5 | 4 |
| 6 | 1 |

Quadratic residues: $\{1, 2, 4\}$, Non-residues: $\{3, 5, 6\}$

### Legendre Symbol

For odd prime $p$ and $\gcd(a, p) = 1$:

$$$
\left(\frac{a}{p}\right) = \begin{cases}
1 & \text{if } a \text{ is a QR mod } p \\
-1 & \text{if } a \text{ is a QNR mod } p
\end{cases}
$$$

**Euler's Criterion:**

$$\left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p}$$

### Quadratic Reciprocity

For distinct odd primes $p$ and $q$:

$$\left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{(p-1)(q-1)}{4}}$$

**Supplementary laws:**

$$\left(\frac{-1}{p}\right) = (-1)^{\frac{p-1}{2}}$$

$$\left(\frac{2}{p}\right) = (-1)^{\frac{p^2-1}{8}}$$

## Primitive Roots

### Definition

An integer $g$ is a **primitive root** modulo $n$ if:

$$\text{ord}_n(g) = \varphi(n)$$

where $\text{ord}_n(g)$ is the smallest positive $k$ such that $g^k \equiv 1 \pmod{n}$.

### Existence

Primitive roots exist modulo $n$ if and only if:

$$n \in \{1, 2, 4, p^k, 2p^k\}$$

where $p$ is an odd prime.

### Properties

If $g$ is a primitive root modulo prime $p$:

$$\{g^0, g^1, g^2, \ldots, g^{p-2}\} = (\mathbb{Z}/p\mathbb{Z})^*$$

Number of primitive roots modulo $p$: $\varphi(p-1)$

## The Discrete Logarithm Problem

Given $g$, $h$, and prime $p$ where $g$ is a primitive root, find $x$ such that:

$$g^x \equiv h \pmod{p}$$

We write $x = \log_g h$.

**Cryptographic significance:** The security of Diffie-Hellman, ElGamal, and DSA relies on the computational difficulty of this problem.

## Cryptographic Applications

### RSA Cryptosystem

**Key generation:**
1. Choose large primes $p, q$
2. Compute $n = pq$ and $\varphi(n) = (p-1)(q-1)$
3. Choose $e$ with $\gcd(e, \varphi(n)) = 1$
4. Compute $d \equiv e^{-1} \pmod{\varphi(n)}$

**Operations:**

$$\text{Encrypt: } c \equiv m^e \pmod{n}$$

$$\text{Decrypt: } m \equiv c^d \pmod{n}$$

**Why it works:** By Euler's theorem:

$$c^d = m^{ed} = m^{1 + k\varphi(n)} = m \cdot (m^{\varphi(n)})^k \equiv m \pmod{n}$$

### Diffie-Hellman Key Exchange

**Public parameters:** Prime $p$, primitive root $g$

**Protocol:**

$$\text{Alice: } A \equiv g^a \pmod{p}$$

$$\text{Bob: } B \equiv g^b \pmod{p}$$

$$\text{Shared secret: } K \equiv g^{ab} \equiv A^b \equiv B^a \pmod{p}$$

### ElGamal Encryption

**Keys:** Private $x$, Public $y \equiv g^x \pmod{p}$

**Encrypt message $m$:**

$$c_1 \equiv g^k \pmod{p}, \quad c_2 \equiv m \cdot y^k \pmod{p}$$

**Decrypt:**

$$m \equiv c_2 \cdot (c_1^x)^{-1} \pmod{p}$$

## Summary of Key Formulas

| Concept | Formula |
|---------|---------|
| Congruence | $a \equiv b \pmod{n} \iff n \mid (a-b)$ |
| Inverse exists | $\gcd(a,n) = 1$ |
| Fermat's Little Theorem | $a^{p-1} \equiv 1 \pmod{p}$ |
| Euler's Theorem | $a^{\varphi(n)} \equiv 1 \pmod{n}$ |
| Totient (prime) | $\varphi(p) = p-1$ |
| Totient (general) | $\varphi(n) = n\prod_{p \mid n}\left(1 - \frac{1}{p}\right)$ |
| Euler's Criterion | $\left(\frac{a}{p}\right) \equiv a^{\frac{p-1}{2}} \pmod{p}$ |

## Practice Problems

1. Compute $17^{-1} \bmod 43$ using the Extended Euclidean Algorithm
2. Find all solutions to $x^2 \equiv 2 \pmod{7}$
3. Solve the system: $x \equiv 2 \pmod{3}$, $x \equiv 3 \pmod{5}$, $x \equiv 2 \pmod{7}$
4. Find a primitive root modulo $13$
5. Compute $2^{1000} \bmod 13$ using Fermat's Little Theorem

The elegant mathematics of modular arithmetic forms the backbone of modern cryptography, transforming ancient number theory into the security infrastructure that protects our digital world.
