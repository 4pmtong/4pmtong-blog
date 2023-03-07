---
title: RSA (cryptosystem)
author: 4pmtong
pubDatetime: 2023-03-03T09:05:51Z
featured: false
draft: false
tags:
  - crypto
  - RSA
ogImage: ""
description: "RSA (cryptosystem)"
---

## Coprime

> [Coprime](https://en.wikipedia.org/wiki/Coprime_integers)
> In number theory, two integers a and b are said to be relatively prime, mutually prime or coprime (also written co-prime) if the only positive integer (factor) that divides both of them is 1. Consequently, any prime number that divides one does not divide the other. This is equivalent to their greatest common divisor (gcd) being 1

**co-prime:**

- Any two prime numbers are co-prime
- **a** is a prime number, **b** is not a multiple of **a**, then **a** and **b** are co-prime
- **1** and any natural number are co-prime
- **p** is an integer greater than **1**, then **p** and **p-1** are co-prime
- **p** is an odd number greater than **1**, then **p** and **p-2** are co-prime
- ...

## congruence relation

Modular arithmetic can be handled mathematically by introducing a congruence relation on the integers that is compatible with the operations on integers: addition, subtraction, and multiplication. For a positive integer **m**, two numbers **a** and **b** are said to be congruent modulo **m**, if their difference **a − b** is an integer multiple of **m** (that is, if there is an integer **k** such that **a − b = km**). This congruence relation is typically considered when **a** and **b** are integers, and is denoted

$$a \equiv b \ (mod \ m)$$

#### compatibility with multiplication：

if $$a \equiv b \ (mod \ m)$$，$$c \equiv d \ (mod \ m)$$，then
$$ac \equiv bd \ (mod \ m)$$

Proof：

$$
    \begin{array}{lr}
        a-mp = b-mq \\
        c-mr = d-ms \\
        (a-mp)(c-mr) = (b-mq)(d-ms) \\
        ac - m(ar+pc-mpr) = bd - m(bs+qd-mqs) \\
        ac - bd = m(ar+pc-mpr - bs-qd+mqs) \\
        ac \equiv bd \ (mod \ m)
    \end{array}
$$

#### division rules:

and
if $$ac \equiv bc \ (mod \ m)$$, and **c**, **m** are co-prime，then:
$$ a \equiv b \ (mod \ m) $$

Proof：

$$
    \begin{matrix}
    ac - mp = bc - mq \\
    ac - bc = mp - mq \\
    (a - b)c = m(p - q) \\
    \end{matrix}
$$

Since **c**, **m** are co-prime, $$a - b$$ has a factor of **m** , then：
$$ a \equiv b \ (mod \ m) $$

## Fermat's little theorem

> [Fermat's little theorem](https://en.wikipedia.org/wiki/Fermat%27s_little_theorem)

Fermat's little theorem states that if **p** is a prime number, then for any integer **a**, the number $$a^{p} − a$$ is an integer multiple of **p**. In the notation of modular arithmetic, this is expressed as
$$ a^{p} \equiv a \ (mod \ p) $$

If **a** is not divisible by **p**, Fermat's little theorem is equivalent to the statement that $$a^{p − 1} − 1$$ is an integer multiple of **p**, or in symbols:

$$
a^{p-1}\equiv 1 \,(mod\ p)
$$

Simple proof:

we get a arbitrary prime number, such as **7**, a given number set **{ 1,2,3,4,5,6 }**, multiply these numbers by a number that is co-prime with **7**, such as **3**, then we get a number set **{ 6,12,18,24,30,36 }**, for modulo **7**, the set is congruence relation with **{ 6,5,4,3,2,1 }**, acturally, these remainders are number set **{ 1,2,3,4,5,6 }**,

then we factor these numbers, we get:

$$6!$$
and factor the number set **{ 6,12,18,24,30,36 }** also，extraction of common factors **3**，we get:
$$3^{6} \times 6!$$

then:

$$
3^{6} \times 6! \equiv 6! \ (mod\ 7)
$$

since $6!$ and 7 are co-prime，from the above **compatibility with multiplication, division rules** available，then:

$$
3^{6} \equiv 1\,(mod\ 7)
$$

use **p** instead of **7**，use **a** instead of **3**，then we get **Fermat's little theorem**

$$
a^{p-1} \equiv 1\,(mod\ p)
$$

## Euler's totient function

> [Euler's totient function](https://en.wikipedia.org/wiki/Euler%27s_totient_function)

In number theory, Euler's totient function counts the positive integers up to a given integer **n** that are relatively prime to **n**
$$\varphi(n)$$

if **n** is a prime number，then $$\varphi(n) = n - 1$$

## Euler's theorem

> [Euler's theorem](https://en.wikipedia.org/wiki/Euler%27s_theorem)

In number theory, Euler's theorem (also known as the Fermat–Euler theorem or Euler's totient theorem) states that if n and a are coprime positive integers, then：
$$ a^{\varphi(n)} \equiv 1 \ (mod \ n) $$

where $$\varphi(n)$$ is Euler's totient function.

The theorem is a generalization of Fermat's little theorem,

when **n** is a prime number，then we get **Fermat's little theorem**:

$$
a^{n-1} \equiv 1\,(mod\ n)
$$

## Modular multiplicative inverse

> [Modular multiplicative inverse](https://en.wikipedia.org/wiki/Modular_multiplicative_inverse)

If two positive integers **a** and **n** are co-prime，then there must be a integer **b**，which is satisfied that **ab - 1** can be divisible by **n**.

Proof:
Since **Euler's theorem**：
$$ a^{\varphi(n)} \equiv 1 \ (mod \ n) $$
then:
$$ a · a^{\varphi(n)-1} \equiv 1 \ (mod \ n) $$
then:
$$ b = a^{\varphi(n)-1}$$

## RSA

> [rsa](https://en.wikipedia.org/wiki/RSA_%28cryptosystem%29)

#### step：

1 - generate two random unequal **large prime numbers** **p** and **q**, whose product number of $$n = p \ · q$$ is the bit of the key
Number, usually set the number of bits is 1024, 2048, 3072, 4096, etc.

2 - calculate the product of **p** and **q** **n**

3 - calculate the Euler function $$\varphi(n)=(p-1)(q-1)$$ of n, and get $$\varphi(n)=(p-1)(q-1)$$

4 - randomly select an integer **e**, with the condition **1 < e < $$\varphi(n)$$**, and **e** and $$\varphi(n)$$

> _In openssl $$e$$ is fixed at 65537_ > [***point***] **Fermat number**: For **e**, **'3, 5, 17, 257 and 65537'** are usually available.Because they are all prime numbers, and only the second bit in the binary are 1, which can speed up the calculation of **d**. The optional values of **e** are actually the first 5 numbers of the **Fermat number**, and the Fermat number is defined as $$F_x = 2^{2^{x}}+1$$, $$F_0$$ to $$F_4$$ are prime numbers, but starting with $$F_5$$ is not a prime number. For example: $$F_5 = 4294967297 = 641 \times 6700471$$, in practice, $$F_4=65537$$ is usually selected as $$e$$.

5 - calculate Modular multiplicative inverse **d** of **e** to $$\varphi(n)$$

$$
        e · d \equiv 1 \ (mod \ \varphi(n))
$$

6 - **n** and **e** are encapsulated into a public key, and **n** and **d** are encapsulated into a private key.

$$
        \begin{array}{lr}
            (n, e) => (21, 5) \\
            (n, d) => (21, 17)
        \end{array}
$$

7 - for the information $m(0 \le m<n)$ , the encryption and decryption functions are as follows:

- public key **n, e** encryption:
  $$
      c = RsaPublic(m) = m^e \ mod \ n
  $$
- private key **n, d** decryption:
  $$
      m = RsaPrivate(c) = c^d \ mod \ n
  $$

we need to proof:

$$
        \begin{array}{lr}
            m = RsaPrivate(RsaPublic(m)) \\
            m = RsaPublic(RsaPrivate(m))
        \end{array}
$$

#### Example

1：$$p = 3, q = 7$$

2：$$n = p * q = 21$$

3：$$\varphi(n)=(p-1)(q-1)= 2 * 6 = 12$$

4：$$e = 5$$

5：$$d = 17$$

6：public key$$(n, e)=(21, 5)$$, private key$$(n, d)=(21, 17)$$

7：Assuming $$m = 2$$, substituting the formula:

$$
    \begin{array}{lr}
        c = m^e \ mod \ n = 2^5 \ mod \ 21 = 11 \\
        m = c^d \ mod \ n = 11^17 \ mod \ 21 = 2
    \end{array}
$$

#### Reliability

number: $$\ p \ q \ n \ \varphi(n) \ e \ d$$

public key: ( **n** 和 **e** )

private key: ( **n** 和 **d** )

So **d** can be derived if **n** and **e** are known?

1. $$e \ ·d \equiv 1 \ (mod \ \varphi(n))$$, only $$e$$ and $$\varphi(n)$$ can be used to calculate $$d$$;
2. $$\varphi(n)=(p-1)(q-1)$$，only $$p$$ and $$q$$ can be used to calculate $$\varphi(n)$$;
3. $$n=p \ ·q$$，only factor $$n$$ to calculate $$p$$ and $$q$$.

solution：If $$n$$ can be factored，then $$d$$ can be calculated，which means that the private key is cracked.

> [Fundamental theorem of arithmetic](https://en.wikipedia.org/wiki/Fundamental_theorem_of_arithmetic)：In number theory, the fundamental theorem of arithmetic, also called the unique factorization theorem or the unique-prime-factorization theorem, states that every integer greater than 1 either is a prime number itself or can be represented as the product of prime numbers and that, moreover, this representation is unique, up to (except for) the order of the factors.
>
> [Integer factorization](https://en.wikipedia.org/wiki/Integer_factorization)

#### Proof

$$
    \begin{array}{lr}
        m = RsaPrivate(RsaPublic(m)) \\
        m = RsaPublic(RsaPrivate(m)) \\
    \end{array}
$$

Proof one of these：

$$
    \begin{array}{lr}
        m = (m^e \ mod \ n)^d \ mod \ n \ (0 \le m < n)
    \end{array}
$$

proof：

$$
    \begin{array}{lr}
        m = (m^e \ mod \ n)^d \ mod \ n  \\
        => m = m^{ed} \ mod \ n \\
        => m^{ed} \equiv m \ (mod \ n)
    \end{array}
$$

since:

$$
    \begin{array}{lr}
    ed ≡ 1 \ (mod  \ φ(n)) \\
    => ed = k \ ·  φ(n)+1
    \end{array}
$$

1. assume $$m$$ and $$n$$ are co-prime:
   since Euler's theorem:
   $$
    m^{φ(n)} ≡ 1 \ (mod \ n)
   $$
   then:
   $$
        \begin{array}{lr}
            (m^{φ(n)})^k ≡ 1 \ (mod \ n) \\
            m ≡ m \ (mod \ n) \\
            \qquad \qquad \Downarrow  \\
            (m^{φ(n)})^k · m ≡ m \ (mod \ n) \\
            m^{k ·  φ(n)+1} ≡ m \ (mod \ n) \\
            m^{ed} \equiv m \ (mod \ n)
        \end{array}
   $$
2. assume $$m$$ and $$n$$ are not co-prime:
   since $$n$$ is equal to the product of prime numbers $$p$$ and $$q$$，so $$m$$ must equal to $$hp$$ or $$hq$$ ($$h$$ is an integer)，Assume $$m=hp$$，since $$hp$$ and $$q$$ must be co-prime，since Fermat's little theorem, we get:

   $$
        \begin{array}{lr}
            (hp)^{q-1} ≡ 1 \ (mod \ q) \\
            => ((hp)^{q-1})^{k·(p-1)} ≡ 1 \ (mod \ q) \\
            => (hp)^{k·φ(n)}≡ 1 \ (mod \ q) \\
            \qquad \qquad \Downarrow  \\
            (hp)^{k·φ(n)}\ · hp ≡ hp \ (mod \ q) \\
            (hp)^{ed} ≡ hp \ (mod \ q) \\
            \qquad \qquad \Downarrow  \\

            (hp)^{ed} = tq + hp
        \end{array}
   $$

   At this time, $$t$$ must be divisible by $$p$$, that is, $$t=t'p$$, then:

   $$
    (hp)^{ed} = t'pq + hp
   $$

   since $$m=hp$$，$$n=pq$$，then:

   $$
        \begin{array}{lr}
             m^{ed} = t'n + m \\
             m^{ed} \equiv m \ (mod \ n)
        \end{array}
   $$

## Challenge from quantum computing

The premise of the RSA encryption system to ensure security is that no computer can decompose a very large integer in an acceptable time, even a supercomputer takes several years.。

Based on the quantum computer-based prime factor decomposition algorithm, the Shor algorithm, the most attractive feature of this algorithm is that it can reduce the complexity of the prime factor decomposition problem from exponential difficulty to near polynomial difficulty.

> [shor](http://intheworld.win/2019/06/22/%E9%87%8F%E5%AD%90%E8%AE%A1%E7%AE%97shor%E7%AE%97%E6%B3%95/)

> [Shor's algorithm](https://en.wikipedia.org/wiki/Shor%27s_algorithm)
