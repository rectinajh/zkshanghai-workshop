1,KZG 多项式承诺方案在 Setup 阶段涉及到计算对秘密评估点 τ 的幂的承诺，这被称为“可信设置”，通
常在被称为“Powers of Tau”的仪式中利用多方计算生成。假如说有一天，你在一张纸条上找到了 τ 的值。
你怎么能用它来制作一个假的 KZG 证明呢？

答：我们知道在 Setup 阶段的 τ 值，原来的三个步骤：

<img width="833" alt="image" src="https://github.com/rectinajh/zkshanghai-workshop/assets/3462559/e332c852-6c82-4624-a25b-11c78c57fd32">

2,从 KZG 多项式承诺方案构造一个向量承诺方案。（提示：对于向量 m = (m1, . . . , mq )，是否存在一个
“插值多项式”I(X) 使得 I (xi) = yi？）
有趣的事实：Verkle 树 [1] 是一种使用向量承诺而不是哈希函数的 Merkle 树。使用 KZG 向
量承诺方案，您能看出为什么 Verkle 树更高效吗？

答：现在要对向量 m = (m1, m2, · · · , mq ) 进行承诺，也就是允许证明任意位置 i 对应 mi。首先通过拉
格朗日插值，使得一个多项式 f (X) 对任意 i 都有 f (i) = mi，根据插值公式，得到
<img width="375" alt="image" src="https://github.com/rectinajh/zkshanghai-workshop/assets/3462559/e16f04fc-df9d-4a31-baa2-95043a13a0f0">


接着，KZG 对该多项式 f (X) 进行承诺就可以了。
如果证明一个元素，Merkle 树需要 O(log2 n) 大小来证明，而这里可以看到只需要 O(1) 就可以。论文
[1] 中给出了与 Merkle 树证明大小的比较：

<img width="694" alt="image" src="https://github.com/rectinajh/zkshanghai-workshop/assets/3462559/61d2203d-3b5a-42ed-a4ad-b3bfdd2b0ef5">


3,KZG 多项式承诺方案对关系 p(x) = y 进行披露证明 π。你能扩展这个方案来产生一个多重证明 π，让我
们相信 p (xi) = yi 对于点列表和评估 (xi, yi) ？（提示：假设您有一个插值多项式 I(X) 使得 I (xi) = yi）。

<img width="823" alt="image" src="https://github.com/rectinajh/zkshanghai-workshop/assets/3462559/52f34279-31b2-43ca-8a0a-f86cfc604944">

