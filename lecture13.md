###Hazard of Overfitting
- The role of Noise and Data Size
	- 越高维的hypothesis就有越大的model complexity,所以在资料量比较小的情况下用高维函数而不是低维函数去拟合的时候虽然$E_{in}$比较小，但是$E_{out}$却比较大（即使target function的维数很高）。（这与有没有noise无关）
- Deterministic Noise
	- $y=f(x)+\epsilon$
		$\sim Gaussian(\underbrace{\sum_{q=0}^{Q_{f}}\alpha_{q}x^q}_{f(x)},\sigma^2)$
		- Gaussian iid noise $\epsilon$ with level $\sigma^2$
	- called impact of $\sigma^2$ stochastic noise.
	- called impact of $Q_{f}$ deterministic noise.
	- 容易发生overfitting的四个因素:
		1. data size N太小
		2. stochastic noise 太大
		3. deterministic noise 太大
		4. excessive power（hypothesis 维度比target function 大，这时候又存在noise时noise会被错误拟合）
	- 如果targer function f不在假设集中（维度太高之类的），那总是有不能拟合的部分
	- `deterministic noise `:difference between best $h^*\in \mathcal{H}$ and f
- Dealing with Overfitting
	1. 从简单的模型做起
	2. 处理一下数据减少杂讯
	3. data cleaning/pruning 
	4. data hinting
	5. regularization
	6. validation
	- data cleaning/pruning
		- 把错误的数据改成对的(data cleaning)
		- 把错误的数据去掉(data pruning)
	- data hinting
		- 利用已有的数据产生更多的数据（如手写体数字的旋转）（注意distribution）

