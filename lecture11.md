###Linear Models for Classification 
######Error Functions Revisited
- linear scoring function:$s=W^Tx$for binary classification $y\in \{-1,+1\}$
- linear classification
	* $h(x)=sign(s)$
	* $err(h,x,y)=[h(x)\ne y]$
	* $\begin{align} & err_{0/1}(s,y)=[sign(s)\ne y] \end{align}$
- linear regression
	$$h(x)=s \\\ err(h,x,y)={(h(x)-y)}^2 \\\ err_{SQR}(s,y)={(s-y)}^2={(ys-1)}^2$$
- logistic regression
	$$h(x)=\theta (s) \\\ err(h,x,y)=-ln{h(yx)} \\\ err_{CE}(s,y)=ln(1+exp(-ys))$$
- ys越大则可以认为预测的结果越准

######Two iterative Optimization Schemes
1. stochastic gradient
	- Logistic Regression每次迭代时都要遍历全部的点，运算效率太慢，作为一种折中的方法，可以抽样来降低复杂度，每次抽取一个点来计算梯度然后做梯度下降.
	- SGD logistic regression:$$w_{t+1}\leftarrow w_{t}+\eta*\theta(-y_{n}w_{t}^Tx_{n})(y_{n}x_{n})$$
	- PLA:$$w_{t+1}\leftarrow w_{t}+1[y_{n}\ne sign(w_{t}^{T}x_{n})](y_{n}x_{n})$$
	- SGD logistic regression$\approx$'soft' PLA
	- PLA$\approx$SGD logistic regression with $\eta=1$ when $w_{t}^Tx_{n}$ large
	- two practical rule-of-thumb:
		* stopping condition?t large enough
		* $\eta$?0.1 when **x** in proper range
		
######One-Versus-ALL Decomposition
- 本节的内容是多分类器的问题，对于有K个类别的样本数据，不能简单的执行K次binary classification得到K个分类器多每个待预测的数据执行K次。这可能会遇到同一个数据被分到多个类别或者没被分到任何一个类中.
- 一个简单的解决方案是采用logistic regression。取待测数据在K个分类器下概率最高的那一个（注意这时候概率总和不是1）

######Multiclass via Binary Classification
- 作为在特定情况下的可能更优的做法OVO算法的思想是采用更多的分类器($C_{n}^{2}$个)，每次只取出样本中的两个类来训练出一个分类器，这样子虽然需要的分类器数量变多了，但是只要类别没那么多（通常情况下符合），样本分布较均匀，可以想见实际的运算量比OVA要来的小。预测时类似投票，把待测数据在每个分类器上试一遍计算得分取得分最高的那个类别。
	* One-versus-one(OVO) Decomposition
	