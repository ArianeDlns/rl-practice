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

Deep Q-Learning uses a neural network to approximate <img src="https://render.githubusercontent.com/render/math?math=Q"> functions. Hence, we usually refer to this algorithm as DQN (for *deep Q network*).

The parameters of the neural network are denoted by ">\theta">. 
*   As input, the network takes a state <img src="https://render.githubusercontent.com/render/math?math=s">,
*   As output, the network returns <img src="https://render.githubusercontent.com/render/math?math=Q_\theta [a | s] = Q_\theta (s,a) = Q(s, a, \theta)">, the value of each action <img src="https://render.githubusercontent.com/render/math?math=a"> in state <img src="https://render.githubusercontent.com/render/math?math=s">, according to the parameters <img src="https://render.githubusercontent.com/render/math?math=\theta">.


The goal of Deep Q-Learning is to learn the parameters <img src="https://render.githubusercontent.com/render/math?math=\theta"> so that <img src="https://render.githubusercontent.com/render/math?math=Q(s, a, \theta)"> approximates well the optimal <img src="https://render.githubusercontent.com/render/math?math=Q">-function <img src="https://render.githubusercontent.com/render/math?math=Q^*(s, a) \simeq Q_{\theta^*} (s,a)">. 

In addition to the network with parameters <img src="https://render.githubusercontent.com/render/math?math=\theta">, the algorithm keeps another network with the same architecture and parameters <img src="https://render.githubusercontent.com/render/math?math=\theta^-">, called **target network**.

The algorithm works as follows:

1.   At each time <img src="https://render.githubusercontent.com/render/math?math=t">, the agent is in state <img src="https://render.githubusercontent.com/render/math?math=s_t"> and has observed the transitions <img src="https://render.githubusercontent.com/render/math?math=(s_i, a_i, r_i, s_i')_{i=1}^{t-1}">, which are stored in a **replay buffer**.

2.  Choose action <img src="https://render.githubusercontent.com/render/math?math=a_t = \arg\max_a Q_\theta(s_t, a)"> with probability <img src="https://render.githubusercontent.com/render/math?math=1-\varepsilon_t">, and <img src="https://render.githubusercontent.com/render/math?math=a_t">=random action with probability <img src="https://render.githubusercontent.com/render/math?math=\varepsilon_t">. 

3. Take action <img src="https://render.githubusercontent.com/render/math?math=a_t">, observe reward <img src="https://render.githubusercontent.com/render/math?math=r_t"> and next state <img src="https://render.githubusercontent.com/render/math?math=s_t'">.

4. Add transition <img src="https://render.githubusercontent.com/render/math?math=(s_t, a_t, r_t, s_t')"> to the **replay buffer**.

4.  Sample a minibatch <img src="https://render.githubusercontent.com/render/math?math=\mathcal{B}"> containing <img src="https://render.githubusercontent.com/render/math?math=B"> transitions from the replay buffer. Using this minibatch, we define the loss:

```math
L(\theta) = \sum_{(s_i, a_i, r_i, s_i') \in \mathcal{B}}
\left[
Q(s_i, a_i, \theta) -  y_i
\right]^2
```

where the <img src="https://render.githubusercontent.com/render/math?math=y_i"> are the **targets** computed with the **target network** <img src="https://render.githubusercontent.com/render/math?math=\theta^-">:

```math
y_i = r_i + \gamma \max_{a'} Q(s_i', a', \theta^-).
```

5. Update the parameters <img src="https://render.githubusercontent.com/render/math?math=\theta"> to minimize the loss, e.g., with gradient descent (**keeping <img src="https://render.githubusercontent.com/render/math?math=\theta^-"> fixed**): 
```math
\theta \gets \theta - \eta \nabla_\theta L(\theta)
```
where <img src="https://render.githubusercontent.com/render/math?math=\eta"> is the optimization learning rate. 

6. Every <img src="https://render.githubusercontent.com/render/math?math=N"> transitions (<img src="https://render.githubusercontent.com/render/math?math=t\mod N"> = 0), update target parameters: <img src="https://render.githubusercontent.com/render/math?math=\theta^- \gets \theta">.

7.<img src="https://render.githubusercontent.com/render/math?math=t \gets t+1">. Stop if <img src="https://render.githubusercontent.com/render/math?math=t = T">, otherwise go to step 2.


## References 
[1] Mnih, V., Kavukcuoglu, K., Silver, D., Rusu, A., Veness, J., Bellemare, M., Graves, A., Riedmiller, M., Fidjeland, A., Ostrovski, G., Petersen, S., Beattie, C., Sadik, A., Antonoglou, I., King, H., Kumaran, D., Wierstra, D., Legg, S., & Hassabis, D. (2015). [Human-level control through deep reinforcement learning](http://dx.doi.org/10.1038/nature14236). Nature, 518(7540), 529–533.  
[2] https://towardsdatascience.com/deep-q-network-with-pytorch-146bfa939dfe  
[3] https://pytorch.org/tutorials/intermediate/reinforcement_q_learning.html   
[4] [Deep Q Learning w/ DQN - Reinforcement Learning](https://www.youtube.com/watch?v=t3fbETsIBCY), Sentdex, YouTube   
[5] [GitHub](https://github.com/gle-bellier/dueling-network-architectures/blob/8519a0932d6e55d0f5cf40dd841ad11dbc7edad5/notebooks/Deep_Q_Learning.ipynb)  
[6] [GitHub](https://github.com/amathsow/machine-learning/blob/master/DQN.ipynb)  
[7] [GitHub](https://github.com/Volviane/Reinforcement-learning/blob/master/Practical_Session_DQN.ipynb)   
[8] https://gsurma.medium.com/cartpole-introduction-to-reinforcement-learning-ed0eb5b58288