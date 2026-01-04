# Greatest Common Divisor and Least Common Multiple: The Building Blocks of Number Theory

The Greatest Common Divisor (GCD) and Least Common Multiple (LCM) are fundamental concepts that appear everywhere in mathematics and cryptography. Think of them as the mathematical tools that help us understand how numbers relate to each other – and they're absolutely essential for everything from simplifying fractions to generating cryptographic keys. Let's explore these elegant concepts that have been fascinating mathematicians for over 2000 years.

## The Greatest Common Divisor: Finding Common Ground

### Definition and Intuition

The **Greatest Common Divisor** of two integers $a$ and $b$ is the largest positive integer that divides both numbers evenly.

**Notation:** We write this as $\gcd(a, b)$ or sometimes $(a, b)$.

**Formal Definition:** For integers $a$ and $b$ (not both zero):

$$\gcd(a, b) = \max\{d \in \mathbb{Z}^+ : d \mid a \text{ and } d \mid b\}$$

**Examples:**
- $\gcd(12, 18) = 6$ because $6$ is the largest number that divides both $12$ and $18$
- $\gcd(17, 19) = 1$ because $17$ and $19$ are both prime
- $\gcd(0, 5) = 5$ because every integer divides $0$

### Fundamental Properties

The GCD has several beautiful properties that make it incredibly useful:

**Property 1 (Symmetry):**
$$\gcd(a, b) = \gcd(b, a)$$

**Property 2 (Sign Independence):**
$$\gcd(a, b) = \gcd(|a|, |b|)$$

**Property 3 (Zero Property):**
$$\gcd(a, 0) = |a| \quad \text{for } a \neq 0$$

**Property 4 (Linear Combination):**
$$\gcd(a, b) = \gcd(a + kb, b) \quad \text{for any integer } k$$

**Property 5 (Divisibility):**
$$\gcd(a, b) = \gcd(a \bmod b, b)$$

**Proof of Property 4:** Let $d = \gcd(a, b)$. Then $d \mid a$ and $d \mid b$, so $d \mid (a + kb)$. Conversely, if $d' \mid (a + kb)$ and $d' \mid b$, then $d' \mid a$. Therefore, the common divisors of $(a, b)$ and $(a + kb, b)$ are identical. $\square$

### The Euclidean Algorithm: Ancient Efficiency

The **Euclidean Algorithm**, dating back to Euclid's *Elements* (circa 300 BCE), remains the most efficient method for computing GCDs.

**Algorithm:**
```
function gcd(a, b):
    while b ≠ 0:
        temp = b
        b = a mod b
        a = temp
    return |a|
```

**Mathematical Foundation:** The algorithm is based on the fundamental property:

$$\gcd(a, b) = \gcd(b, a \bmod b)$$

**Why It Works:** At each step, we replace the pair $(a, b)$ with $(b, a \bmod b)$. Since $a \bmod b < b$, the second number decreases at each step, ensuring termination.

**Complexity Analysis:** The algorithm terminates in at most $O(\log \min(a, b))$ steps, making it remarkably efficient even for very large numbers.

### Detailed Example: Computing $\gcd(252, 105)$

Let's trace through the algorithm step by step:

$$\begin{align}
252 &= 2 \times 105 + 42 & \gcd(252, 105) &= \gcd(105, 42) \\
105 &= 2 \times 42 + 21 & \gcd(105, 42) &= \gcd(42, 21) \\
42 &= 2 \times 21 + 0 & \gcd(42, 21) &= \gcd(21, 0) = 21
\end{align}$$

Therefore, $\gcd(252, 105) = 21$.

**Verification:** $252 = 21 \times 12$ and $105 = 21 \times 5$, and $\gcd(12, 5) = 1$. ✓

### The Extended Euclidean Algorithm: Finding Linear Combinations

The **Extended Euclidean Algorithm** not only computes $\gcd(a, b)$ but also finds integers $x$ and $y$ satisfying **Bézout's Identity**:

$$ax + by = \gcd(a, b)$$

**Algorithm:**
```python
def extended_gcd(a, b):
    if b == 0:
        return a, 1, 0
    else:
        gcd, x1, y1 = extended_gcd(b, a % b)
        x = y1
        y = x1 - (a // b) * y1
        return gcd, x, y
```

**Mathematical Justification:** We maintain the invariant that at each recursive call, we can express the GCD as a linear combination of the current arguments.

### Extended Algorithm Example: $\gcd(252, 105)$

Working through our previous example:

$$\begin{align}
252 &= 2 \times 105 + 42 \\
105 &= 2 \times 42 + 21 \\
42 &= 2 \times 21 + 0
\end{align}$$

**Back-substitution:**

$$\begin{align}
21 &= 105 - 2 \times 42 \\
&= 105 - 2 \times (252 - 2 \times 105) \\
&= 105 - 2 \times 252 + 4 \times 105 \\
&= 5 \times 105 - 2 \times 252 \\
&= (-2) \times 252 + 5 \times 105
\end{align}$$

**Result:** $252 \times (-2) + 105 \times 5 = 21 = \gcd(252, 105)$

**Verification:** $252 \times (-2) + 105 \times 5 = -504 + 525 = 21$ ✓

## Coprimality: When Numbers Share Nothing

### Definition

Two integers $a$ and $b$ are **coprime** (or **relatively prime**) if:

$$\gcd(a, b) = 1$$

This means they share no common prime factors.

**Examples:**
- $\gcd(15, 28) = 1$, so $15$ and $28$ are coprime
- $\gcd(12, 18) = 6 \neq 1$, so $12$ and $18$ are not coprime

### Properties of Coprime Numbers

**Theorem:** If $\gcd(a, b) = 1$ and $a \mid bc$, then $a \mid c$.

**Proof:** Since $\gcd(a, b) = 1$, there exist integers $x, y$ such that $ax + by = 1$. Multiplying by $c$:
$$acx + bcy = c$$
Since $a \mid bc$, we have $bc = ak$ for some integer $k$. Substituting:
$$acx + aky = c \implies a(cx + ky) = c$$
Therefore $a \mid c$. $\square$

**Corollary:** If $p$ is prime and $p \mid ab$, then $p \mid a$ or $p \mid b$.

## The Least Common Multiple: Finding Common Multiples

### Definition

The **Least Common Multiple** of two positive integers $a$ and $b$ is the smallest positive integer that is divisible by both $a$ and $b$.

**Notation:** We write this as $\text{lcm}(a, b)$ or $[a, b]$.

**Formal Definition:**

$$\text{lcm}(a, b) = \min\{m \in \mathbb{Z}^+ : a \mid m \text{ and } b \mid m\}$$

**Examples:**
- $\text{lcm}(12, 18) = 36$ because $36$ is the smallest positive multiple of both $12$ and $18$
- $\text{lcm}(7, 11) = 77$ because $7$ and $11$ are coprime

### The Fundamental Relationship

The most important relationship between GCD and LCM is:

$$\gcd(a, b) \times \text{lcm}(a, b) = |a \times b|$$

**Proof:** Let $d = \gcd(a, b)$, so $a = da'$ and $b = db'$ where $\gcd(a', b') = 1$.

Then:
$$\text{lcm}(a, b) = \text{lcm}(da', db') = d \times \text{lcm}(a', b') = d \times a'b' = \frac{ab}{d}$$

Therefore:
$$\gcd(a, b) \times \text{lcm}(a, b) = d \times \frac{ab}{d} = ab$$

This gives us the **computational formula**:

$$\text{lcm}(a, b) = \frac{|a \times b|}{\gcd(a, b)}$$

### Computing LCM Efficiently

**Algorithm:**
1. Compute $\gcd(a, b)$ using the Euclidean algorithm
2. Apply the formula: $\text{lcm}(a, b) = \frac{|ab|}{\gcd(a, b)}$

**Example:** Find $\text{lcm}(252, 105)$

We already know $\gcd(252, 105) = 21$, so:

$$\text{lcm}(252, 105) = \frac{252 \times 105}{21} = \frac{26460}{21} = 1260$$

**Verification:** 
- $1260 = 252 \times 5$ ✓
- $1260 = 105 \times 12$ ✓
- No smaller positive integer is divisible by both $252$ and $105$ ✓

### Properties of LCM

**Property 1 (Symmetry):**
$$\text{lcm}(a, b) = \text{lcm}(b, a)$$

**Property 2 (Associativity):**
$$\text{lcm}(a, \text{lcm}(b, c)) = \text{lcm}(\text{lcm}(a, b), c)$$

**Property 3 (Distributivity with GCD):**
$$\text{lcm}(a, \gcd(b, c)) = \gcd(\text{lcm}(a, b), \text{lcm}(a, c))$$

**Property 4 (Coprime Case):**
$$\text{If } \gcd(a, b) = 1, \text{ then } \text{lcm}(a, b) = ab$$

## Prime Factorization Approach

### GCD via Prime Factorization

If we have the prime factorizations:
$$a = p_1^{a_1} p_2^{a_2} \cdots p_k^{a_k}$$
$$b = p_1^{b_1} p_2^{b_2} \cdots p_k^{b_k}$$

Then:
$$\gcd(a, b) = p_1^{\min(a_1, b_1)} p_2^{\min(a_2, b_2)} \cdots p_k^{\min(a_k, b_k)}$$

$$\text{lcm}(a, b) = p_1^{\max(a_1, b_1)} p_2^{\max(a_2, b_2)} \cdots p_k^{\max(a_k, b_k)}$$

**Example:** Find $\gcd(72, 48)$ and $\text{lcm}(72, 48)$

Prime factorizations:
- $72 = 2^3 \times 3^2$
- $48 = 2^4 \times 3^1$

Therefore:
- $\gcd(72, 48) = 2^{\min(3,4)} \times 3^{\min(2,1)} = 2^3 \times 3^1 = 24$
- $\text{lcm}(72, 48) = 2^{\max(3,4)} \times 3^{\max(2,1)} = 2^4 \times 3^2 = 144$

**Verification:** $\gcd(72, 48) \times \text{lcm}(72, 48) = 24 \times 144 = 3456 = 72 \times 48$ ✓

## Multiple Numbers: Extending the Concepts

### GCD of Multiple Numbers

For $n$ numbers $a_1, a_2, \ldots, a_n$:

$$\gcd(a_1, a_2, \ldots, a_n) = \gcd(\gcd(a_1, a_2), a_3, \ldots, a_n)$$

**Algorithm:**
```python
def gcd_multiple(numbers):
    result = numbers[0]
    for i in range(1, len(numbers)):
        result = gcd(result, numbers[i])
        if result == 1:
            break  # Early termination optimization
    return result
```

### LCM of Multiple Numbers

Similarly:

$$\text{lcm}(a_1, a_2, \ldots, a_n) = \text{lcm}(\text{lcm}(a_1, a_2), a_3, \ldots, a_n)$$

**Important:** The relationship $\gcd \times \text{lcm} = \text{product}$ only holds for **two** numbers!

## Cryptographic Applications

### RSA Key Generation

In RSA cryptography, we need:

1. **Prime Selection:** Choose primes $p$ and $q$
2. **Totient Computation:** $\varphi(n) = (p-1)(q-1)$ where $n = pq$
3. **Public Exponent:** Choose $e$ such that $\gcd(e, \varphi(n)) = 1$
4. **Private Exponent:** Find $d$ such that $ed \equiv 1 \pmod{\varphi(n)}$

The Extended Euclidean Algorithm is used in step 4 to find the modular inverse.

### Modular Arithmetic

**Finding Multiplicative Inverses:** To find $a^{-1} \bmod n$:

1. Use Extended Euclidean Algorithm to find $x, y$ such that $ax + ny = \gcd(a, n)$
2. If $\gcd(a, n) = 1$, then $x \equiv a^{-1} \pmod{n}$
3. If $\gcd(a, n) \neq 1$, the inverse doesn't exist

### Chinese Remainder Theorem

The CRT requires pairwise coprime moduli. We use GCD to verify:

$$\gcd(n_i, n_j) = 1 \quad \text{for all } i \neq j$$

### Diffie-Hellman Key Exchange

When selecting parameters for Diffie-Hellman:

1. Choose prime $p$
2. Find primitive root $g$ modulo $p$
3. Verify $\gcd(g^{(p-1)/q}, p) = 1$ for security

## Advanced Topics

### Stein's Algorithm (Binary GCD)

For computer implementation, **Stein's Algorithm** can be more efficient as it uses only subtraction and bit shifts:

```python
def binary_gcd(a, b):
    if a == 0: return b
    if b == 0: return a
    
    # Remove common factors of 2
    shift = 0
    while ((a | b) & 1) == 0:
        a >>= 1
        b >>= 1
        shift += 1
    
    # Remove remaining factors of 2 from a
    while (a & 1) == 0:
        a >>= 1
    
    while b != 0:
        # Remove factors of 2 from b
        while (b & 1) == 0:
            b >>= 1
        
        # Ensure a ≤ b
        if a > b:
            a, b = b, a
        
        b = b - a
    
    return a << shift
```

### Computational Complexity

| Algorithm | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Euclidean | $O(\log \min(a,b))$ | $O(1)$ |
| Extended Euclidean | $O(\log \min(a,b))$ | $O(\log \min(a,b))$ |
| Binary GCD | $O(\log^2 \min(a,b))$ | $O(1)$ |
| Prime Factorization | $O(\sqrt{\max(a,b)})$ | $O(\log \max(a,b))$ |

### Bézout's Identity and Linear Diophantine Equations

The equation $ax + by = c$ has integer solutions if and only if $\gcd(a, b) \mid c$.

**General Solution:** If $(x_0, y_0)$ is a particular solution to $ax + by = \gcd(a, b)$, then all solutions to $ax + by = c$ are:

$$x = x_0 \cdot \frac{c}{\gcd(a, b)} + k \cdot \frac{b}{\gcd(a, b)}$$

$$y = y_0 \cdot \frac{c}{\gcd(a, b)} - k \cdot \frac{a}{\gcd(a, b)}$$

for any integer $k$.

## Practical Examples and Applications

### Example 1: Simplifying Fractions

To simplify $\frac{252}{105}$:

$$\frac{252}{105} = \frac{252 \div \gcd(252, 105)}{105 \div \gcd(252, 105)} = \frac{252 \div 21}{105 \div 21} = \frac{12}{5}$$

### Example 2: Finding Common Denominators

To add $\frac{5}{12} + \frac{7}{18}$, we need $\text{lcm}(12, 18)$:

$$\gcd(12, 18) = 6, \quad \text{lcm}(12, 18) = \frac{12 \times 18}{6} = 36$$

$$\frac{5}{12} + \frac{7}{18} = \frac{15}{36} + \frac{14}{36} = \frac{29}{36}$$

### Example 3: Cryptographic Key Validation

In RSA with $p = 61, q = 53$:

$$n = pq = 3233, \quad \varphi(n) = (p-1)(q-1) = 60 \times 52 = 3120$$

Choose $e = 17$. Check: $\gcd(17, 3120) = \gcd(17, 3120 \bmod 17) = \gcd(17, 8) = 1$ ✓

Find $d$: $17d \equiv 1 \pmod{3120}$

Using Extended Euclidean Algorithm: $d = 2753$

**Verification:** $17 \times 2753 = 46801 = 15 \times 3120 + 1$ ✓

## Summary of Key Formulas

| Concept | Formula |
|---------|---------|
| GCD-LCM Relationship | $\gcd(a,b) \times \text{lcm}(a,b) = \|ab\|$ |
| LCM Computation | $\text{lcm}(a,b) = \frac{\|ab\|}{\gcd(a,b)}$ |
| Bézout's Identity | $ax + by = \gcd(a,b)$ |
| Coprimality | $\gcd(a,b) = 1$ |
| Euclidean Step | $\gcd(a,b) = \gcd(b, a \bmod b)$ |

## Practice Problems

1. **Basic Computation:** Find $\gcd(1071, 462)$ and $\text{lcm}(1071, 462)$

2. **Extended Algorithm:** Find integers $x, y$ such that $1071x + 462y = \gcd(1071, 462)$

3. **Cryptographic Application:** For RSA with $p = 17, q = 19$, find a valid public exponent $e$ and corresponding private exponent $d$

4. **Multiple Numbers:** Find $\gcd(48, 72, 96)$ and $\text{lcm}(48, 72, 96)$

5. **Diophantine Equation:** Solve $15x + 25y = 5$ for integers $x, y$

### Solutions

1. **Solution:**
   ```
   1071 = 2 × 462 + 147
   462 = 3 × 147 + 21
   147 = 7 × 21 + 0
   
   gcd(1071, 462) = 21
   lcm(1071, 462) = (1071 × 462) ÷ 21 = 23562
   ```

2. **Solution:** Working backwards from the Euclidean algorithm:
   ```
   21 = 462 - 3 × 147
   21 = 462 - 3 × (1071 - 2 × 462)
   21 = 7 × 462 - 3 × 1071
   
   Therefore: x = -3, y = 7
   ```

The beauty of GCD and LCM lies in their fundamental simplicity combined with their profound applications. From ancient Greek mathematics to modern cryptographic systems, these concepts continue to be essential tools for understanding the deep structure of numbers and building secure digital systems.
