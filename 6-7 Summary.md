#### Value function Approximation
1. Why need value function approximation?
	1. Continuous situation. Large-scale states....
2. What is value funtion Approximation?
	1. Estimate value function with function approximation$$\begin{aligned}\hat{v}(s, \mathbf{w}) & \approx v_{\pi}(s) \\\text { or } \hat{q}(s, a, \mathbf{w}) & \approx q_{\pi}(s, a)\end{aligned}$$
	2. Generlise from seen states to unseen states
	3. Update parameter $w$ using MC or TD learning.
3. !Be contious that: using FA ,value function has not $w$ ,unlike $v_\pi(s)$  and  $q_\pi(s,a)$ .Because previous value evaluation always depends on policy $\pi$  .I think in FA, the value function is also based on policy ?????? #没懂 
4. Three types of FA:
5. Function Approximator:
	1. Linear
	2. Neural netwrok
	3. Decision Tree...
6. Does stochastic gradient deescent equal to full gradient update(No, only expected is)
7. $\hat{V}(S,w) = x(S)^Tw$
8. Why does stochastic gradient descent converges on global optimum?
	1. Because it's linear, if it's not golobal opimum, the gradient is not zero
9. Update rule:Upadate = Step-size × prediction erros × featrue value$$\begin{aligned} {\triangledown_w \hat{v}(S,w)=x(S)}\\\Delta w=\alpha(v_\pi(S)-\hat{v}(S,w))x(S) \end{aligned}$$
10. Convergence: MC or Table-Lookup or (Linear and On-policy)
11. Why batch methods?
12. Least squares Prediction: choose square erros as loss function
13. About Linear lests squares predicrtion:
	1. it can find , but take many iterations
	2. it can be solved directly
14. LSMC/LSTD/LSTD($\lambda$) can be directly solved :
	1. 公式略
15. Least Squares Control:
	1. Idea: for control ,we also want to improve policy ,which results in different policy while learning.
	2. So to evaluate $q_\pi(S,A)$ we must learn **off-policy**
16. how LSTDQ work?
17. DQN:
	1. Main features:
		1. experience replay 
		2. fixed Q-targets
	2. procedures:
		1. Take action accroding to $\epsilon$-greedy policy
		2. Store transition in replay policy
		3. Sample random mini-batch of transisions 
		4. compute-Q-learning targets
		5. opimise MSE between Q-network and Q-learning targets


#### Policy Gradient
1. Why in Policied-Based, value function does not need subscript $\pi$ The reason is $\theta$ represents the policy
2. Why?
	1. Better **convergence**
	2. **effective** in high-dimentional or continuous action spaces(**Be catious!** Only in high dimentional situation )
	3. can learn stochastic policies
3. Disadvantage:
	1. typically converge to a **local** rather than global optimum
	2. with high variance ,thus ineffcient
4. Good Example!(Inspiring!)![[Pasted image 20220514144333.png]]
	1. If choose value vased method , the final optimal determinstic policy will be like this,![[Pasted image 20220514144707.png]]thus it will traverse the corridor for a long time
	2. But if we use policy based method, an optimal stochastic policy will randomly move,just like below:![[Pasted image 20220514144849.png]]it will  reach the goal in a few steps with high probabilities.
	3. **Furthermore(My thingking):** it give me a very good example. If we throw out Markov properties, we can use previous state to estimate current state.In short, I think we describe all situation as MDP can missing something, maybe there is a method to better utilize information like this. Using policy method is somewhat a solution, but obvious it's not the optimum, in this simple example. 
5.  Policy Objective Function(策略目标函数)
	1. To measure the quality of policy $\pi_\theta$ 
	2. In episodic environments, we can use the **start value**:$J_1(\theta) = V^{\pi_\theta}(s_1)=\mathbb{E}_{\pi_\theta}[v_1]$
	3.  In continuous environments ,we can use average value:$J_{a v V}(\theta)=\sum_{s} d^{\pi_{\theta}}(s) V^{\pi_{\theta}}(s)$
6. Policy optimisation: find $\theta$ maximises $J(\theta)$
	1. Methods: Hill climbing,genetic algorithms,gradient descent, conjugate gradient....
7. computing Gradients By Finite Differences: 
	1. simple ,noise ,but inefficient,but sometimes effective
8. Score function.............................................