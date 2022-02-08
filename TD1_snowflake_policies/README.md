# TD1 Reinforcement Learning 

## Students

[Ariane Dalens](https://gitlab-student.centralesupelec.fr/ariane.dalens)   

#### Due date
:calendar: **28/01/2021**  


## :books: Subject of the TD  
:snowflake: [FrozenLake](https://gym.openai.com/envs/FrozenLake-v0/)


Winter is here. You and your friends were tossing around a frisbee at the park when you made a wild throw that left the frisbee out in the middle of the lake. The water is mostly frozen, but there are a few holes where the ice has melted. If you step into one of those holes, you'll fall into the freezing water. At this time, there's an international frisbee shortage, so it's absolutely imperative that you navigate across the lake and retrieve the disc. However, the ice is slippery, so you won't always move in the direction you intend.

The surface is described using a grid like the following:

````
SFFF       (S: starting point, safe)
FHFH       (F: frozen surface, safe)
FFFH       (H: hole, fall to your doom)
HFFG       (G: goal, where the frisbee is located)
````

The episode ends when you reach the goal or fall in a hole. You receive a reward of 1 if you reach the goal, and zero otherwise.


## :runner: Running the code
### Check environement 
````
python3 check_env.py 
````
### Run code 

```bash
python3 discover.py # interactive source code debugger
python3 solution_ariane_dalens.py
```

An interactive .ipynb notebook: ``TD1_RL_Ariane_Dalens.ipynb`` shows the results 
## :package: Organisation of the project

### Structure

```bash 
.
├── README.md
├── check_env.py
├── discover.py
├── hint_question3.py
├── notebook
│   └── TD1_RL_Ariane_Dalens.ipynb # Interactive notebook with answers
├── requirement.txt
├── solution_ariane_dalens.py # Script with answers
└── td1.pdf # Subject of the project
```

### Requirements 
```bash
pip3 install -r requirements.txt 
```

``numpy == 1.21.4 | gym == 0.21.0 | matplotlib == 3.5.0``

## References
[1] https://towardsdatascience.com/value-iteration-to-solve-openai-gyms-frozenlake-6c5e7bf0a64d  
[2] https://reinforcement-learning4.fun/2019/06/16/gym-tutorial-frozen-lake/
