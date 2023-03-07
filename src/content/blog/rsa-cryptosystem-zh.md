---
title: RSA 数论背景&证明
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

## 互质

> 若 **a** 和 **b** 的最大公因子为 **1**，则称 **a** 和 **b** 互质。

**互质关系有:**

- 任意两个质数互质
- **a** 是质数，**b** 不为 **a** 的倍数，则 **a** 与 **b** 互质
- **1** 和任意自然数互质
- **p** 是大于 **1** 的整数，则 **p** 和 **p-1** 互质
- **p**是大于 **1** 的奇数，则 **p** 和 **p-2** 互质
- ...

## 同余

> 当两个整数除以同一个正整数，若得相同余数，则二整数同余

两个整数**a**, **b**若它们除以正整数**m**所得的余数相等，则称**a**, **b**对于模**m**同余，记作：
$$a \equiv b \ (mod \ m)$$

#### 相乘：

若 $$a \equiv b \ (mod \ m)$$，$$c \equiv d \ (mod \ m)$$，则
$$ac \equiv bd \ (mod \ m)$$

证明：

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

#### 除法原理一:

若 $$ac \equiv bc \ (mod \ m)$$,且**c**, **m**互质，则:
$$ a \equiv b \ (mod \ m) $$

证明：

$$
    \begin{matrix}
    ac - mp = bc - mq \\
    ac - bc = mp - mq \\
    (a - b)c = m(p - q) \\
    \end{matrix}
$$

由于**c**, **m**互质，则 $$a - b$$ 有因子**m**,即：
$$ a \equiv b \ (mod \ m) $$

## 费马小定理

> [费马小定理](https://zh.wikipedia.org/wiki/%E8%B4%B9%E9%A9%AC%E5%B0%8F%E5%AE%9A%E7%90%86)

假如 **a** 是一个整数，**p** 是一个质数，那么 $$a^{p} - a$$ 是 **p** 的倍数，可以表示为
$$ a^{p} \equiv a \ (mod \ p) $$

如果 **a** 不是 **p** 的倍数，这个定理也可以写成

$$
a^{p-1}\equiv 1 \,(mod\ p)
$$

简单证明:

任意取一个质数，比如 **7**，给定数集 **{ 1,2,3,4,5,6 }** ，给这些数都乘上一个与 **7** 互质的数，比如 **3**，
得到 **{ 6,12,18,24,30,36 }**, 对于模 **7** 来说，这些数同余于 **{ 6,5,4,3,2,1 }** ， 这些余数实际上就是集合 **{ 1,2,3,4,5,6 }**

把 **{ 1,2,3,4,5,6 }** 做阶乘，得到
$$6!$$
把 **{ 6,12,18,24,30,36 }** 做阶乘，提取公因子**3**，乘积就是
$$3^{6} \times 6!$$

得:

$$
3^{6} \times 6! \equiv 6! \ (mod\ 7)
$$

由于 $$6!$$ 和 7 互质，由上面**同余 除法原理一** 可得，

$$
3^{6} \equiv 1\,(mod\ 7)
$$

如果用 **p** 代替 **7**，用 **a** 代替 **3**，就得到 **费马小定理**

$$
a^{p-1} \equiv 1\,(mod\ p)
$$

## 欧拉函数

> [欧拉函数](https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%87%BD%E6%95%B0)
> 小于或等于 n 的正整数中与 n 互质的数的数目 $$\varphi(n)$$

若 **n** 为一个质数，那么 $$\varphi(n) = n - 1$$

## 欧拉定理

> [欧拉定理](<https://zh.wikipedia.org/wiki/%E6%AC%A7%E6%8B%89%E5%AE%9A%E7%90%86_(%E6%95%B0%E8%AE%BA)>)
> 如果两个正整数 **a** 和 **n** 互质，则 **n** 的欧拉函数 $$\varphi(n)$$ 可以让下面的等式成立：
> $$ a^{\varphi(n)} \equiv 1 \ (mod \ n) $$

欧拉定理中的一种特殊情况，当 **n** 为质数时，可得 **费马小定理**:

$$
a^{n-1} \equiv 1\,(mod\ n)
$$

## 模反元素

> [模反元素](https://zh.wikipedia.org/wiki/%E6%A8%A1%E5%8F%8D%E5%85%83%E7%B4%A0)
> 如果两个正整数 **a** 和 **n** 互质，那么一定可以找到整数 **b**，使得 **ab - 1** 被 **n** 整除.

证明:
由 **欧拉定理** 可得：
$$ a^{\varphi(n)} \equiv 1 \ (mod \ n) $$
则:
$$ a · a^{\varphi(n)-1} \equiv 1 \ (mod \ n) $$
可得:
$$ b = a^{\varphi(n)-1}$$

## RSA 加密算法

#### 步骤：

- 第一步，生成两个随机的不相等的**大质数** **p** 和 **q**，它们的积  $$n = p \ · q$$ 的二进制位数就是密钥的位数，通常设置的位数有 1024，2048，3072，4096 等
- 第二步，计算 **p** 和 **q** 的乘积 **n**
- 第三步，计算 n 的欧拉函数$$\varphi(n)$$, 得 $$\varphi(n)=(p-1)(q-1)$$
- 第四步，随机选择一个整数 **e**，条件是 **1 < e < $$\varphi(n)$$**, 且 **e** 与 $$\varphi(n)$$ 互质

> _在 openssl 中  $$e$$ 固定为 65537_ > [知识点]费马数: 对于 $$e$$，通常可选 3, 5, 17, 257 和 65537。因为它们都是质数，且二进制中只有 2 位是 1，可以加快 d 的计算。这几个 e 的可选值实际是费马数的前 5 个数，费马数定义是$$F_x =2^{2^{x}}+1$$, $$F_0$$ 到 $$F_4$$ 都是质数，但是从 $$F_5$$ 开始就不是质数了。 例如：$$F_5 = 4294967297 = 641 \times 6700471$$，实际应用中通常选择$$F_4=65537$$ 作为 $$e$$.

- 第五步，计算 **e** 对于 $$\varphi(n)$$ 的模反元素 **d**

  $$
      e · d \equiv 1 \ (mod \ \varphi(n))
  $$

- 第六步，将 **n** 和 **e** 封装成公钥，**n** 和 **d** 封装成私钥
  $$
      \begin{array}{lr}
          (n, e) => (21, 5) \\
          (n, d) => (21, 17)
      \end{array}
  $$
- 第七步，定义好了公私钥，则对信息 $$m(0 \le m<n)$$ ，加密和解密函数如下：

  - 公钥 **n, e** 加密:
    $$
        c = RsaPublic(m) = m^e \ mod \ n
    $$
  - 私钥 **n, d** 解密:
    $$
        m = RsaPrivate(c) = c^d \ mod \ n
    $$

  需要证明:

  $$
      \begin{array}{lr}
          m = RsaPrivate(RsaPublic(m)) \\
          m = RsaPublic(RsaPrivate(m))
      \end{array}
  $$

1. 常用于客户端公钥加密数据然后服务端私钥解密获取原始数据
2. 常用于服务端私钥加密签名数据，客户端公钥解密获取签名数据并校验签名

#### 实例

- 第一步：$$p = 3, q = 7$$
- 第二步：$$n = p * q = 21$$
- 第三步：$$\varphi(n)=(p-1)(q-1)= 2 * 6 = 12$$
- 第四步：$$e = 5$$
- 第五步：$$d = 17$$
- 第六步：公钥$$(n, e)=(21, 5)$$, 私钥$$(n, d)=(21, 17)$$
- 第七步：假定 $$m = 2$$, 代入公式：
  $$
      \begin{array}{lr}
          c = m^e \ mod \ n = 2^5 \ mod \ 21 = 11 \\
          m = c^d \ mod \ n = 11^17 \ mod \ 21 = 2
      \end{array}
  $$

#### 可靠性

使用数字: $$\ p \ q \ n \ \varphi(n) \ e \ d$$
公钥: ( **n** 和 **e** )
私钥: ( **n** 和 **d** )
那么已知 **n** 和 **e** 的情况下，可以推导出 **d** 吗？

1. $$e \ ·d \equiv 1 \ (mod \ \varphi(n))$$, 只有知道 $$e$$ 和 $$\varphi(n)$$ 才能算出 $$d$$;
2. $$\varphi(n)=(p-1)(q-1)$$，只有知道 $$p$$ 和 $$q$$，才能算出 $$\varphi(n)$$;
3. $$n=p \ ·q$$，只能将 $$n$$ 因数分解，才能算出 $$p$$ 和 $$q$$.

结论：如果 $$n$$ 可以被因数分解，$$d$$ 就可以算出，也就意味着私钥被破解。

> 唯一质数分解定理：任何一个大于 1 的正整数 n 都可以   唯一分解   为一组质数的乘积，其中$$e_1,e_2...e_k$$都是自然数(包括 0)
> 大数质因数分解

#### 证明

$$
    \begin{array}{lr}
        m = RsaPrivate(RsaPublic(m)) \\
        m = RsaPublic(RsaPrivate(m)) \\
    \end{array}
$$

证明其一即可，即证：

$$
    \begin{array}{lr}
        m = (m^e \ mod \ n)^d \ mod \ n \ (0 \le m < n)
    \end{array}
$$

证明：

$$
    \begin{array}{lr}
        m = (m^e \ mod \ n)^d \ mod \ n  \\
        => m = m^{ed} \ mod \ n \\
        => m^{ed} \equiv m \ (mod \ n)
    \end{array}
$$

由于

$$
    \begin{array}{lr}
    ed ≡ 1 \ (mod  \ φ(n)) \\
    => ed = k \ ·  φ(n)+1
    \end{array}
$$

1. 假设: $$m$$ 与 $$n$$ 互质:
   由欧拉定理有:

   $$
    m^{φ(n)} ≡ 1 \ (mod \ n)
   $$

   由此：

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

   得证。

2. 假设: $$m$$ 与 $$n$$ 不是互质关系:
   此时，由于 $$n$$ 等于质数 $$p$$ 和 $$q$$ 的乘积，所以 $$m$$ 必然等于 $$hp$$ 或 $$hq$$，假设 $$m=hp$$，由于 $$hp$$ 必然与 $$q$$ 互质，由费马小定理得:

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

   这时 t 必然能被 $$p$$ 整除，即 $$t=t'p$$, 得:

   $$
    (hp)^{ed} = t'pq + hp
   $$

   由 $$m=hp$$，$$n=pq$$，得:

   $$
        \begin{array}{lr}
             m^{ed} = t'n + m \\
             m^{ed} \equiv m \ (mod \ n)
        \end{array}
   $$

   得证。

证毕。

## 来自量子计算的挑战

RSA 加密系统能够确保安全的前提是，没有一个计算机能够在可接受的时间内分解一个极大整数，即使是超级计算机也要花费数年的时间。

基于量子计算机的质因数分解算法——Shor 算法，这种算法最吸引人的地方是，它能够将质因数分解问题的复杂度，从指数难度降低到近多项式难度

> [shor 算法](http://intheworld.win/2019/06/22/%E9%87%8F%E5%AD%90%E8%AE%A1%E7%AE%97shor%E7%AE%97%E6%B3%95/)
> Grover 量子搜索算法

参考：
[RSA](https://zh.wikipedia.org/wiki/RSA%E5%8A%A0%E5%AF%86%E6%BC%94%E7%AE%97%E6%B3%95)
[互质](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%B3%AA)
[同余](https://zh.wikipedia.org/wiki/%E5%90%8C%E9%A4%98)
[费马小定理](https://zh.wikipedia.org/wiki/%E8%B4%B9%E9%A9%AC%E5%B0%8F%E5%AE%9A%E7%90%86)
[唯一质数分解定理](https://zh.wikipedia.org/wiki/算术基本定理)
[整数分解](https://zh.wikipedia.org/wiki/%E6%95%B4%E6%95%B0%E5%88%86%E8%A7%A3)
[RSA 算法原理全面解析](https://www.jianshu.com/p/6aa7b59be872)
