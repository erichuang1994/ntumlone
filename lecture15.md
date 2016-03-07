##Validation
####Model Selection Problem
 - 没讲啥
 
####Validation 
- 在实际上我们训练模型的时候，由于out-of-sample不可以马上获得，我们不能知道所得到的基于in-of-sample得到的g是否是好的。
- 作为一种折衷，由于我们的训练集是符合distribution的一个数据集，我们可以从中选出一小部分作为测试集，剩下的作为训练集，把在训练集上得到的多个$g^{-}$在测试集上作测试选出$E_{val}(h)$(直觉上我们认为$E_{val}(h)$与$E_{out}(h)$应该是接近的）最好的那一个$g^{-}$然后把这个hypothesis在完整的数据集上做一次train得到g(直觉上可以认为对于同一个model用越多的数据得到的g更好).
- 把完整的已有数据集记为$\mathcal{D}$在其上直接得到的g记为$g_{m}=\mathcal{A}_{m}(\mathcal{D})$
- 减去测试集后的训练集记为$\mathcal{D}_{train}$,其上训练得到的g记为$g_{m}^{-1}=\mathcal{A}_{m}(\mathcal{D}_{train})$
- $\mathcal{D}_{val}\subset \mathcal{D}$:called **validation set** -'on-hand' simulation of test set
- 测试集记为$\mathcal{D}_{val}$大小为K
- 则有$\mathcal{D}\rightarrow \mathcal{D}_{train}\cup\mathcal{D}_{val}$
- to connect $E_{val}$ with $E_{out}$:
	$$\mathcal{D}_{val}\overset{iid}{\tilde{}}P(x,y)\Leftarrow select\,K\,examples\,from\,\mathcal{D}\,at\,random$$
- $E_{out}(g_{m}^{-})\le E_{val}(g_{m}^{-})+O(\sqrt{\frac{logM}{K}})$
- 比起把训练集也当做测试集这是一个更好的方法，因为训练数据在训练时就已经被使用了。
- Model Selection by Best $E_{val}$
	- $$m^*=\underset{1\le m\le M}{argmin}(E_{m}=E_{val}(\mathcal{A}_{m}(\mathcal{D}_{train})))$$
	- generalization guarantee for all m:
		$$E_{out}(g_{m^*})\le E_{out}(g_m^-)\le E_{val}(g_m^-)+O(\sqrt{\frac{logM}{K}})$$
- The Dilemma about K
	$$E_{out}(g)\underset{small \,K}{\approx}E_{out}(g^-)\underset{large\,K}{\approx}E_{val}(g^-)$$

####Leave-One-Out Cross Validation
- LOOCV：这个方法的内容比较简单就是对于一个size为N的资料，依次把第1,2,3,...N作为测试数据剩余的当做训练集得到$g_n^-$(所以是N次试验）再用拿出的那一个点当测试集求err，则这个err的期望值与$E_{out}$的期望值相等
- $$\begin{align}\underset{\mathcal{D}}{\mathcal{E}}E_{LOOCV}(\mathcal{H},\mathcal{A})=\underset{\mathcal{D}}{\mathcal{E}}\frac{1}{N}\sum_{n=1}^{N}e_{n}&=\frac{1}{N}\sum_{n=1}^{N}\underset{\mathcal{D}}{\mathcal{E}}e_{n}\\&=\frac{1}{N}\sum_{n=1}^{N}\underset{\mathcal{D}_{n}}{\mathcal{E}}\underset{(x_{n},y_{n}}{\mathcal{E}}err(g_{n}^-(x_{n}),y_n)\\&=\frac{1}{N}\sum_{n=1}^N\underset{\mathcal{D}_{n}}{\mathcal{E}}E_{out}(g_n^-)\\&=\overline{E_{out}}(N-1)\end{align}$$

####V-Fold Cross Validation
- LOOCV的方法需要的运算量太大了，而且对于0/1分类的时候一次的err显得也绝对了。
- 作为一个折衷的方案，将数据集分成V份（iid随机分），一次用一份做测试集，可以想见这样也可以得到不错的结果。实际上通常分成10份就差不多了。
- $$E_{cv}(\mathcal{H},\mathcal{A})=\frac{1}{V}\sum_{v=1}^{V}E_{val}^{(v)}(g_{v}^-)$$