###Logistic Regression Problem
- 逻辑回归处理的问题是：想知道某个患者在一定条件（输入$\vec{\textbf{x}}$）下发病的概率（发病记为1不发病记为-1）,即是求函数h使得$h(\vec{x})=P(+1|\vec{x})$(理想情况)
- Logistic Function
- $$\theta(s)=\frac{e^s}{1+e^s}=\frac{1}{1+e^{-s}}$$
- logistic regression:use$$h(x)=\frac{1}{1+exp(-\textbf{w}^Tx)}$$to approximate target function $f(x)=P(y|x)$
- $$err(w,x,y)=ln(1+exp(-y\color{red}{\textbf{w}}^Tx))$$
- $$\min_{w}E_{in}(w)=\frac{1}{N}\sum_{n=1}^{N}ln(1+exp(-y_{n}w^Tx_{n}))$$
- $$\nabla E_{in}(\textbf{W})=\frac{1}{N}\sum_{n=1}^{N}\theta(-y_{n}\textbf{W}^Tx_{n})(-y_{n}x_{n})$$
- `Logistic Regression Algorithm(Gradient Descent)`
	* initialize $\textbf{w}_{0}$ for t=0,1,...
	* compute$$\nabla E_{in}(W_{t})=\frac{1}{N}\sum_{n=1}^{N}\theta(-y_{n}W_{t}^Tx_{n})(-y_{n}x_{n})$$
	* updated by
	$$W_{t+1}\leftarrow W_{t}-\eta\nabla E_{in}(W_{t})$$
	* until $\nabla E_{in}(W_{t+1})\approx0$ or enough iterations return last $W_{t+1}$ as g
