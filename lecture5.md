* if |H|=M finite,N large enough,for whatever g picked by A,
	$$E_{out}(g)\approx E\_{in}(g)$$

将平面上的点进行分类的直线的种类并不是无限多的，对N个人来说虽然可能的分法有2^N种但是实际上考虑到线性可分，结果是有限的。  

*  $$定义growth \, function \,成长函数\,m_{H}=max|H(x\_{1},x\_{2},...,x\_{N})(max\, number of dichotomies)$$

	H(x1,x2,...,xN)意思是对这一组的X的划分的可能的种数如两个点x1,x2可能分成xx,xo,oo,ox四种，考虑到共点得情况下没有这么多，当考虑成长函数的时候取得是使得划分最多的那组X
*  $$bounding \, function \, B(N,k):$$
$$maximum\,  possible\,  m_{H}(N)\,when\, break\, point=k $$
* Table of **Bounding Function** B(N,k)(N是点数k是break point数目)

|  |  |  | k |  |
| - | - | - | - | - |
| B(N,k) | 1 | 2 | 3 | 4 |
| 1 | 1 | 2 | 2 | 2 |
| 2 | 1 | 3 | 4 | 4 |
| 3 | 1 | 4 | 7 | 8 |
| 4 | 1 | |   | 15 |
| 5 | 1 | | |
| 6 | 1 | |  | |

* `Bounding Function` : The Theorem

$$递推公式B(N,k)\le B(N-1,k)+B(N-1,k-1)(实际是等号)$$
$$B(N,k)\le\sum\_{i=0}^{k-1}(^{N}_{i})最高次幂为N^{k-1}$$

$$for\, N\ge 2,k\ge3,m\_{H}(N)\le B(N,k)=\sum\_{i=0}^{j-1}(\_{i}^{N})\le N^{k-1}$$
###Recap:More on Vapnik-Chervonenkis(VC) Bound
*对任意的g属于H都有

$$P\_{D}[|E\_{in}(g)-E\_{out}(g)|>\epsilon]$$
$$\le 4m\_{H}(2N)exp(-1/8\epsilon^2N)$$
$$\le 4(2N)^{k-1}exp(-1/8\epsilon^2N)(if \,k\, exists)$$

* $$VC \, dimension \,of\,H,dented\, d_{vc}(H)\, is$$

$$largest\, N \, for\, which\, m_{H}(N)=2^N(既是最大non-break\, point)$$
$$d\_{vc}='minimum\, k'-1$$
$$for \, k-D\, perceptrons:d\_{vc}=k+1$$

`note`由于得到的不等式是一个很上界的上界，理论上也许需要N为dvc的一万倍才能取得较好的效果，但是实际上，N只需要是dvc的十倍就够了