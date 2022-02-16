# TD2 Reinforcement Learning 

#### Due date
:calendar: **21/02/2021**  


## :books: Subject of the TD  
:mountain_cableway: [CartPole-v0](https://gym.openai.com/envs/CartPole-v0/)

## :runner: Running the code
### Run code 

An interactive .ipynb notebook: ``TD2_RL_Ariane_Dalens.ipynb`` shows the results 

In the ``./video`` folder you will find the .mp4 file with the result of our DQN

![CartPole](https://raw.githubusercontent.com/ArianeDlns/rl-practice/master/TD2_cartpole_DQNN/videos/openaigym.video.0.77186.video000000.gif)

## :package: Organisation of the project

### Structure

```bash 
.
├── README.md
├── videos
│   ├── openaigym.video.0.77186.video000000.gif
│   └── openaigym.video.0.77186.video000000.mp4
├── TD2_RL_Ariane_Dalens.ipynb
└── img
    └── phase_plot.png
```

## Theoretical Explanation: Deep Q-Learning 

$test$

Deep Q-Learning uses a neural network to approximate $Q$ functions. Hence, we usually refer to this algorithm as DQN (for *deep Q network*).

The parameters of the neural network are denoted by $\theta$. 
*   As input, the network takes a state $s$,
*   As output, the network returns $Q_\theta [a | s] = Q_\theta (s,a) = Q(s, a, \theta)$, the value of each action $a$ in state $s$, according to the parameters $\theta$.


The goal of Deep Q-Learning is to learn the parameters $\theta$ so that $Q(s, a, \theta)$ approximates well the optimal $Q$-function $Q^*(s, a) \simeq Q_{\theta^*} (s,a)$. 

In addition to the network with parameters $\theta$, the algorithm keeps another network with the same architecture and parameters $\theta^-$, called **target network**.

The algorithm works as follows:

1.   At each time $t$, the agent is in state $s_t$ and has observed the transitions $(s_i, a_i, r_i, s_i')_{i=1}^{t-1}$, which are stored in a **replay buffer**.

2.  Choose action $a_t = \arg\max_a Q_\theta(s_t, a)$ with probability $1-\varepsilon_t$, and $a_t$=random action with probability $\varepsilon_t$. 

3. Take action $a_t$, observe reward $r_t$ and next state $s_t'$.

4. Add transition $(s_t, a_t, r_t, s_t')$ to the **replay buffer**.

4.  Sample a minibatch $\mathcal{B}$ containing $B$ transitions from the replay buffer. Using this minibatch, we define the loss:

$$
L(\theta) = \sum_{(s_i, a_i, r_i, s_i') \in \mathcal{B}}
\left[
Q(s_i, a_i, \theta) -  y_i
\right]^2
$$
where the $y_i$ are the **targets** computed with the **target network** $\theta^-$:

$$
y_i = r_i + \gamma \max_{a'} Q(s_i', a', \theta^-).
$$

5. Update the parameters $\theta$ to minimize the loss, e.g., with gradient descent (**keeping $\theta^-$ fixed**): 
$$
\theta \gets \theta - \eta \nabla_\theta L(\theta)
$$
where $\eta$ is the optimization learning rate. 

6. Every $N$ transitions ($t\mod N$ = 0), update target parameters: $\theta^- \gets \theta$.

7. $t \gets t+1$. Stop if $t = T$, otherwise go to step 2.


## References 
[1] Mnih, V., Kavukcuoglu, K., Silver, D., Rusu, A., Veness, J., Bellemare, M., Graves, A., Riedmiller, M., Fidjeland, A., Ostrovski, G., Petersen, S., Beattie, C., Sadik, A., Antonoglou, I., King, H., Kumaran, D., Wierstra, D., Legg, S., & Hassabis, D. (2015). [Human-level control through deep reinforcement learning](http://dx.doi.org/10.1038/nature14236). Nature, 518(7540), 529–533.  
[2] https://towardsdatascience.com/deep-q-network-with-pytorch-146bfa939dfe  
[3] https://pytorch.org/tutorials/intermediate/reinforcement_q_learning.html   
[4] [Deep Q Learning w/ DQN - Reinforcement Learning](https://www.youtube.com/watch?v=t3fbETsIBCY), Sentdex, YouTube   
[5] [GitHub](https://github.com/gle-bellier/dueling-network-architectures/blob/8519a0932d6e55d0f5cf40dd841ad11dbc7edad5/notebooks/Deep_Q_Learning.ipynb)  
[6] [GitHub](https://github.com/amathsow/machine-learning/blob/master/DQN.ipynb)  
[7] [GitHub](https://github.com/Volviane/Reinforcement-learning/blob/master/Practical_Session_DQN.ipynb)   
[8] https://gsurma.medium.com/cartpole-introduction-to-reinforcement-learning-ed0eb5b58288