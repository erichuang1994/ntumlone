##<center>Regularization<center/>
######6 Nov,2015
####Regularized Hypothesis Set
- $$\mathcal{H}_{2}^{'}\equiv\begin{equation} \begin{cases}w\in \mathbb{R}^{10+1}\, while\ge8\, of w_{q}=0\end{cases}\end{equation}$$
regression with $\mathcal{H}_{2}^{'}$:
$$\min_{w\in\mathbb{R}^{10+1}}E_{in}(w)$$
s.t$\sum\limits_{q=0}^{10}[\![H(x_i)\neq y_i ]\!]\le3$
- $\mathcal{H}_{2}\subset\mathcal{H}_{2}^{'}\subset\mathcal{H}_{10}$
- 所以$\mathcal{H}_{2}^{'}$比起$\mathcal{H}_{2}$有更好的自由度又没有$\mathcal{H}_{10}$那么容易overfitting。但是遗憾的是这也是NP-HARD的（因为bool函数是离散的？）。
- Regression with Softer Constraint
	- $H_{C}\equiv
\begin{equation}
\begin{cases}
w\in\mathbb{R}^{10+1}while{||w||}^2\le C
\end{cases}
\end{equation}$
	regression with $\mathcal{H}(C)$:
	$$\min_{w\in\mathbb{R}^{10+1}}E_{in}(w)s.t.\sum_{q=0}^{10}w_{q}^2\le C$$
	- $\mathcal{H}(C)$:overlaps but not exactly the same as $\mathcal{H}_{2}^{'}$
	- soft and smooth structure over $C\ge 0$:
	$$\mathcal{H}(0)\subset\mathcal{H}(1.126)\subset...\subset\mathcal{H}(1126)\subset...\subset\mathcal{H}(\infty)=\mathcal{H}_{10}$$
	- 这是一种较好的Hypothesis set构造方式，在这种方式下找到的好的W叫做$W_{REG}$

####Weight Decay Regularization
- question：为什么大部分的情况下解在球体的边缘上？
- The Larange Multiplier
	- $\min\limits_{w\in\mathbb{R}^{Q+1}}E_{in}(w)=\frac{1}{N}(Zw-y)^T(Zw-y)s.t.w^Tw\le C$
	- solving $\nabla E_{in}(W_{REG})+\frac{2\lambda}{N}W_{REG}=0$
		$$\frac{2}{N}(Z^TZW_{REG}-Z^Ty)+\frac{2\lambda}{N}W_{REG}=0$$
	- optimal solution:
		$$W_{REG}\leftarrow{(Z^TZ+\lambda I)}^{-1}Z^Ty$$
		--called **ridge regression** in Statistics
	- Aygmented Error
		- if oracle tells you $\lambda >0$,then
			solving$\nabla E_{in}(W_{REG})+\frac{2\lambda}{N}W_{REG}=0$
			equivalent to minimizing $\underbrace{E_{in}(w)+\frac{\lambda}{N}\overbrace{w^Tw}^{regulaizer}}_{augmented\,error\, E_{aug}(w)}$
		- regularization with augmented error instead of constrained $E_{in}$
			$$w_{REG}\leftarrow \underset{w}{argmin}E_{aug}(w)\, \,for\,given\,\lambda>0\,or\,\lambda =0$$
		- 所以当$\lambda=0$的时候就相当于没有约束的情况（即C无穷大），$\lambda$越大则对应C越小的情况。
	- call '$+\frac{\lambda}{N}w^Tw$'weight-decay regularization:
		$$\begin{align}larger\,\lambda&\Leftrightarrow prefer\,shorter\,w \\&\Leftrightarrow effectively\,smaller\,C\end{align}$$
		--go with 'any' transform+linear model

####Regularization and VC theory
- Augmented Error:
	$$E_{aug}(w)=E_{in}(w)+\frac{\lambda}{N}w^Tw$$
- VC Bound:
	$$E_{out}(w)\le E_{in}(w)+\Omega(\mathcal{H})$$
- regularizer$w^Tw=\Omega(w)$:complexity of a single hypothesis
- generalization price $\Omega(\mathcal{H})$:complexity of a hypothesis set
- if $\frac{\lambda}{N}\Omega(w)$'represents' $\Omega(\mathcal{H})$ well,
	$E_{aug}$ is a better proxy of $E_{out}$ than $E_{in}$
- minimizing $E_{out}$:
	(heuristically) operating with the better proxy
	(technically) enjoying flexibility of whole $\mathcal{H}$
- Effective VC Dimension
	$$\min_{w\in\mathbb{R}^{\tilde{d}+1}}E_{aug}(w)=E_{in}(w)+\frac{\lambda}{N}\Omega(w)$$
	- $d_{vc}(\mathcal{H})=\tilde{d}+1$因为其w没有被限制，而$d_{vc}(\mathcal{H}(C))$因为受到了C的限制，不能包含所有可能的Hypothesis set.所以他的vc dimension没有那么大。
	- $d_{vc}(\mathcal{H}(C))$:
		effective VC dimension $d_{EFF}(\mathcal{H},\underbrace{\mathcal{A}}_{\min E_{aug}})$
	- explanation of regularization:$d_{vc}(\mathcal{H})$large,while $d_{EFF}(\mathcal{H},\mathcal{A})$small if $\mathcal{A}$ regularized.

####General Regularizers
- 提到了Reugularizer时候的一些技巧，比如利用图像的一些性质（可以是观察出来的，可以是给出的）来特定一些constraint(比如对称性之类的，w的各位绝对值求和)
- $$(X^TX+\lambda)^{-1}X^Ty$$