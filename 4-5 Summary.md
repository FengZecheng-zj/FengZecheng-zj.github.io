### Model-Free Prediction——MC & TD
1. Summary
	1. Last lecture
		1. **Planning** by dynamic programming
		2. Solve a **known MDP**(What is a known MDP?)
	2. This lecture
		1. Model-free prediction
		2. **Estimate** the value function of an unknown MDP
	3. Next lecture
		1. Model-free control 
		2. **Optimise** the value function of an unknown MDP
2. Monte-Carlo Methods
	1. model-free(meanning?)
	2. no bootstraapping(What is bootstrapping?)
		1. not like TD ,it uses the estimation of it self
	3. Base idea :value = mean return
	4. Caveat: only apply to episodic MDPs
3. Monte-Carlo
	1. first-visit
	2. every-visit
4. Incremental Mean$\mu_k = \mu_{k-1}+\frac1k(x_k-\mu_{k-1})$
	1. Monte-Carlo update formula $V(S_t)\leftarrow V(S_t)+\alpha(G_t-V(S_t))$
5.   TD-Method
	1. Compared to Monte-Carlo methods, What's biggest difference?
		1. By bootstrapping(updates a guess towards a guess)
	2. Update value toward estimated return $R_{t+1}+\gamma V(S_{t+1})$ $$V(S_t)\leftarrow V(S_t)+\alpha(R_{t+1}+\gamma V(S_{t+1})-V(S_t))$$
	3. What is called TD target?
	4. What is called TD error?
6.  Why in next Chapter(Model free control,we use Q and say we are optimize value funtion not estimate?What's difference?)
7. In driving home example,What is State,what is value function,what is reward?
8. Concept of **online learning** and **off-line learning**,and what is on-policy and off-policy?
9. Comparision of TD and MC:
	1. TD can learn without and before final outcome:
		1. Thus it can learn online(update in every step)
		2. Can learn in imcomplete episode
		3. Can work in continuing environments
	2. Bias and Variance trade-off
		1. MC target is unbiased estimate ,but TD target is biased(True TD target is not)
			1. What is True TD target
		2. TD target is much lower variance than return G_t
			1. Why? 
				1. Return depends on many random actions,transitions,rewards
				2. TD target depedns on one random action,transition,reward.Thus it's more efficient
	3. MC has high variance,zero bias, not sensitive to initial value
	4. TD has low variance, some bias.more efficient,more sensitive to initial value.TD(0) converges to $v_\pi(s)$
	5. Why low variance cause faster convergence?
	6. Certainty Equivalence
		1. MC converges to solution with minimum mean-squared error
		2. TD(0) converges to solution of max likelihood Markov model
			1. Does TD($\lambda$) has the same result?????????? #没懂 
			2. I think is ,but not sure.
	7. Whether to exploits Markov property
	8. Whether it is bootstrap
	9. Bakup
		1. Monte-Carlo![[Pasted image 20220416151059.png]]
		2. TD:![[Pasted image 20220416151146.png]]
		3. DP:![[Pasted image 20220416151202.png]]
		4. Unified view of Reinforcement Learning:![[Pasted image 20220416151314.png]]
10. n-step TD
	1. 基础迭代公式
		1. $$
G_{t}^{(n)}=R_{t+1}+\gamma R_{t+2}+\ldots+\gamma^{n-1} R_{t+n}+\gamma^{n} V\left(S_{t+n}\right)
$$
		2. $$V(S_t)\leftarrow V(S_t)+\alpha(G_t^{(n)}-V(S_t))$$
	2. TD($\lambda$):Averaging n-step return
		1. Using weight $(1-\lambda)\lambda^{n-1}$:$$G_t^\lambda=((1-\lambda)\sum_{n=1}^\infty\lambda^{n-1}G_t^{n}$$
		2. $$V(S_t)\leftarrow V(S_t)+\alpha(G_t^{\lambda}-V(S_t))$$
		3. Forward-view
			1. looks into the future to compute $G_t^\lambda$
			2. What is forward-view TD($\lambda$) mean?
			3. Does it needs complete episodes?
		4. Backward-view
			1. Update online,every step,from incomplite sequences.
		5. What is Eligibility Traces?
			1. why?
		6. What is $\delta_t$ What is $E_t(s)$
11. Relationship between Forward and backward TD
	1. The sum of offline updates is identical for forward-view and backward-view $TD(\lambda)$ $$
\sum_{t=1}^{T} \alpha \delta_{t} E_{t}(s)=\sum_{t=1}^{T} \alpha\left(G_{t}^{\lambda}-V\left(S_{t}\right)\right) \mathbf{1}\left(S_{t}=s\right)
$$
	2. Over the course of an episode, total update for TD(1) is the same as total update for MC. So TD(1) is exactly the same as MC if offline. ohterwise ,it's roughly the same
	3. Summary:![[Pasted image 20220416160039.png]]


### Model-Free Control
1. What is control problem about?
	1. **control probelm** is aiming to get optimal policy $\pi_*$and optimal value function$v_*$
	2. Unlike prediction problem,it just get value function(last chapter)    REF:[[1-3 Summary]] search control
2. What's difference **On-policy** learning & **Off-line** learning
	1. On-policy: Learn on the job:Learn about policy $\pi$ from experience sampled from $\pi$ 
	2. Off-policy :Look about policy$\pi$ from experience sampled from $\mu$
3. Policy iteration: 2 step
	1. policy evalutaion :Estimate $v_\pi$
	2. policy improvement :Generate $\pi' \ge \pi$
4. If with Monte-Carlo Evalution,there exists two problems:
	1. Whether $V=v_\pi$?
	2. Greedy ?
5. Why model-free Policy Iteration needs to use action-value function?(Not state value function)
	1. Greedy **policy improvement** over $V(s)$ requires model of MDP$$\pi^{\prime}(s)=\underset{a \in \mathcal{A}}{\operatorname{argmax}} \mathcal{R}_{s}^{a}+\mathcal{P}_{s s^{\prime}}^{a} V\left(s^{\prime}\right)$$
	2.  Greedy **policy improvement** over $Q(s,a)$ is model free:$$
\pi^{\prime}(s)=\underset{a \in \mathcal{A}}{\operatorname{argmax}} Q(s, a)$$
6. Elaborate $\epsilon$ greedy exporation:
	1.$$\pi(a \mid s)= \begin{cases}\epsilon / m+1-\epsilon & \text { if } a^{*}=\underset{a \in \mathcal{A}}{\operatorname{argmax}} Q(s, a) \\ \epsilon / m & \text { otherwise }\end{cases}$$
	2. With probability $1-\epsilon$ choose the greedy action
	3. With probability $\epsilon$ choose greedy
7. Therom:  
	1. Using $\epsilon$ policy improvement ,$v_{\pi'}(s) \ge v_\pi(s)$
8. Using TD control,Advantages:
	1. Online(Incomplete sequences),can update every time-step
9. SARSA:(TD method of control)$$Q(s,a)\leftarrow Q(s,a)+\alpha(R+\gamma Q(S',A')-Q(S,A))$$
10. n-step Sarsa: just like n-step TD 
11. Backward View Sarsa...
12. **Off-policy Learning**:Advantages:(taking policy 1 to evaluate policy 2 )**Efficient**
	1. can learn from optimal policy while following exploratory policy
	2. Learn multiple polices while following one policy
	3. Re-use experience from old policy
	4. Learn from humans and other angets
13. Importance Sampling
	1. Estimate the expectation of a different distribution
	2. $$\begin{aligned}\mathbb{E}_{X \sim P}[f(X)] &=\sum P(X) f(X) \\&=\sum Q(X) \frac{P(X)}{Q(X)} f(X) \\&=\mathbb{E}_{X \sim Q}\left[\frac{P(X)}{Q(X)} f(X)\right]\end{aligned}$$
14. Importance Sampling for Off-Policy Monte-Carlo
	1. Idea:Use returns generated from $\mu$ to evalutate $\pi$
	2. ***Weight return* $G_t$ accroding to similarity between policies**
	3. Multiply importance sampling corrections along whole episode.$$G_{t}^{\pi / \mu}=\frac{\pi\left(A_{t} \mid S_{t}\right)}{\mu\left(A_{t} \mid S_{t}\right)} \frac{\pi\left(A_{t+1} \mid S_{t+1}\right)}{\mu\left(A_{t+1} \mid S_{t+1}\right)} \ldots \frac{\pi\left(A_{T} \mid S_{T}\right)}{\mu\left(A_{T} \mid S_{T}\right)} G_{t}$$
	4. Update value toward corrected return$$V(s_t)\leftarrow V(S_t)+\alpha(G_t^{\pi/\mu}-V(S_t))$$
15. Importance Sampling for Off-Policy TD
	1. Use TD targets generated from $µ$ to evaluate $π$
	2. Weight TD target$R + γV(S')$ by importance sampling
	3. Advantages:
		1. lower variance
		2. policies only need to be similar over a single step
16. **Q-Learning**
	1. $$Q(S_t,A_t)\leftarrow Q(S_t,A_t)+\alpha {(R_{t+1}+\gamma Q(S_{t+1},A')}-Q(S_t,A_t))$$
