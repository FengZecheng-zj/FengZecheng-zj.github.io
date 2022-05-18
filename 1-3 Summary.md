## Intro
1. What is diiferent with ohter machine learning 
2. What's the difference between **Environment state** and **Agent state**
and **information state**(Markov state)
3. Policy: agent's behaviour function
	1. determinstic
	2. stochastic
4. Value function:How good
	1. state
5. Model:agent's representation of the environment
	What will environment do ?
	1.  $R_{t+1}$
	2. $S_{t+1}$
6.  Categorize RL 
	1. Value/Policy based /Actor critic
	2. Model Based/Model Free
7. Difference between **Learning** and **Planning** 
8. Expolration and Expolitation
9. What's different ?Prediction and Control
## MDP
1. To describe a environment formally
	1. The future is independent of the past given the present$$\mathbb{P}[S_{t+1}|S_t]=\mathbb{P}[S_{t+1}|S_1,...,S_t]$$
	Why it can?
	**Why different complex situation can be described into MDP?**
	My answer is : According to classic physics, if the information about current state is sufficient, it can be Markov.Even if we do not know about what the state is,We can just set a hiddent markov state. Moreover,it is about philosophy ,haha.
2. State Transition Matrix
3. Markov Processes
4. Markov Reward Processes
	1. $S,P,R,\gamma$, What are they?
5. Return
	1. total *discounted* reward
	2. Why discount?
6. Bellman Equation for MRPs
	1. Matrix Form //Solving $O(n^3)$
	2. iterative methods:
		1. DP
		2. Monte-Carlo evaluation
		3. Temporal-Difference learning
7.  Markov Decision Processes
	1. S,A,P,R,$\gamma$,
8. Bellman Expectation Equation
9. What is $v_\pi(s)$
	1.  Value Function $v_\pi(s)$ of an MDP is the expected return starting from state s, and then **following policy** $\pi$ $$v_\pi(s)=\mathbb{E}[G_t|S_t=s]$$
10. What is $q_\pi(s,a)$?
11. **Bellman Expecatation Equation**
	1. What? Please write down.
	2. Matrix Form(solution)
12. Optimal Value Function?$v_*(s)$ 
	1. to certain state s ,for all policy
	2. q*
13. Opimal Policy$$\pi>\pi'\quad if \quad v_{\pi}(s)\ge v_{\pi'}(s),\forall s$$
	1. Is there exists a optimal policy in all condition?Why?
	2. How to find it?
	3. Why we say an MDP is "solved" when we know the optimal value
14. **Bellman Optimality Equation** 
15. Solving the Vellman Optimality Equation
	1. No closed methods
	2. iterativie methods
		1. Sarsa
		2. Q-learning
		3. Policy Iteration
		4. Value Iteration

### Dynamic Programming
1. What is Dynamic Programming?Feature?
2. for what kind of problems? Two properties.
	1. Markov decision processes satisfy both properties.
3. As Planning, DP assumes full knowledge of the MDP
4. For prediction and for control
	1. What is the input and output of predcition and control
5. Iterative Policy Evaluation
	1. How to do it?
	2. Convergence?
6. Why reward is $R_s^a$ not$R_s$ ? ??????????????????????????????? #没懂
	1. In grid world, reward is for state, not for action
	2. Because it is in MDP,in definition. But why can MDP?
7. How to Improve a Policy?(Policy Iteration)
	1. Evaluate the policy
	2. Improve the policy by acting greedily
	3. Prove that.$v_\pi(s)\le v_{\pi'}(s)$  
8. Value Iteration
9. All above is based on state-value function, How can we apply it to action-value function?
10. Contraction 还是没看懂
