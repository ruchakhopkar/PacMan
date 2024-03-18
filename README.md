# PacMan
Using Deep Convolutional Q-Learning to train a model for PacMan


[Trained PacMan agent](https://github.com/ruchakhopkar/PacMan/assets/70127769/0f94b886-c179-4177-9d2b-697e145c5858)

We do see that the agent converges at a local minima.
However, with more compute and time, we can train the agent to reach the global minima.

EDIT: Increased the LR to achieve a better convergence.



https://github.com/ruchakhopkar/PacMan/assets/70127769/aea95aca-b7d0-4c50-884b-7f902c7be606

<br> I have used one of the environments from [gymnasium](https://gymnasium.farama.org/content/basic_usage/) called MsPacmanDeterministic-v0, in which some of the actions of the villains are deterministic and many other actions are non-deterministic.
<br> I built a neural network containing convolutional and linear layers which gives as output, the action values(size 9). 
<br> The input in this case is an RGB image of dimension 210 * 160.
<br> I then create an agent with 2 functions: act and learn(step)
<br> In the act function, given a state the agent will take some action based on the output from the neural network. The action is chosen based on a epsilon greedy policy for exploration-exploitation.
<br> In the step function, the agent actually learns. We get the current Q values from the local network and the target Q values from the target network. Having 2 networks helps to stabilize the learning process. Since the environment of the agent is continuously changing, it is good to have a target network which is only updated once in a few steps. The loss is calculated as the MSE loss between the target Q values and the expected Q values. 
<br> I used Adam as an optimizer. 
<br> I also maintain a memory that holds the experiences of the agent. When the agent learns, we can uniformly sample mini batch size number of experiences from this memory to train the agent on. This ensures we are not biasing the agent on tasks that occur frequently. 

