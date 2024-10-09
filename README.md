<br />
<p align="center">
  <a href="/Images/AI_Image.jpg">
    <img src="/Images/AI_Image.jpg" alt="Logo" height=150 >
  </a>
  <h1 align="center">
    SC3000 Artificial Intelligence Lab Assignments
  </h1>
</p>

# Overview

This repository contains the lab assignments for NTU SC3000 Artificial Intelligence (AY24/25 SEM1)
There are mainly two lab assignments for this course.

# Lab Asssignment 1

## Reinforcement Learning Algorithm

Students are tasked to implement and evaluate on of the Reinforcement Learning (RL) Algorithms to solve the CliffBoxPushing grid-world game.

<img src="/Images/Cliff_Box_Pushing_Grid_World.png" width="700">
<h4 align = "center">
<u>Fig.1 The Cliff Box Pushing Grid World<u>
</h4>

The environment is a 2D grid world as shown in Fig. 1. The size of the environment is 6×14. In Fig. 1,
**A** indicates the agent, **B** stands for the box, **G** is the goal, and **x** means cliff. You need to write code
to implement one of the RL algorithms and train the agent to push the box to the goal position. The
game ends under three conditions:

1. The agent or the box steps into the dangerous region (cliff).
2. The current time step attains the maximum time step of the game.
3. The box arrives at the goal.

The MDP formulation is described as follows:

- **State**: The state consists of the position of the agent and the box. In Python, it is a tuple, for
  example, at time step 0, the state is ((5, 0), (4, 1)) where (5, 0) is the position of the agent
  and (4, 1) is the position of the box.
- **Action**: The action space is [1,2,3,4], which is corresponding to [up, down, left, right]. The
  agent needs to select one of them to navigate in the environment.
- **Reward**: The reward consists of

1. the agent will receive a reward of -1 at each timestep
2. the negative value of the distance between the box and the goal
3. the negative value of the distance between the agent and the box
4. the agent will receive a reward of -1000 if the agent or the box falls into the cliff.
5. the agent will receive a reward of 1000 if the box reaches the goal position.

- **Transition**: Agent’s action can change its position and the position of the box. If a collision with a
  boundary happens, the agent or the box would stay in the same position. The transition can be
  seen in the step() function of the environment.

There are 2 main componenets left for students to implement, namely:

1. The RLAgent class
2. Visualization of learned V-table (the average Q-values of each agent position) and policy

## Choosing the optimal RL

In the course of SC3000, 3 RL algorithms were taught - Monte Carlo, Q-learning, and Deep Q-Network. Below is a brief analysis of the suitability of each RL algorithm for the assignment:

1. **Monte Carlo (MC)**:
   The main idea behind MC is to use randomness to solve a problem - generating
   suitable random numbers and observing the fraction of numbers obeying some
   properties. MC methods require episodic tasks and only update values at the end of
   each episode. In this assignment, waiting until the end of the episode for updates
   could be inefficient and lead to poor performance during training.
2. **Q-Learning**:
   Q-learning is an example of bootstrapping, leveraging the estimates of future rewards
   to update the Q-values of the current state-action pair. Q-learning is a good fit for this
   assignment because it updates the Q-value at each step, allowing the agent to learn
   to avoid dangerous cliffs faster. It can also handle the reward structure, learning to
   push the box while avoiding the cliff by continuously updating values during each
   step.
3. **Deep Q-Network (DQN)**:
   DQN uses a neural network the approximate the Q-values, and is generally used for
   larger or continuous state spaces. Since the grid is relatively small (6x14), the extra
   power that comes with the complexity of DQN may not be necessary

## Final Seclection

I have decided to use Q-learning for this specific problem due to the manageable size of the
grid-world and the need for step-by-step updates, which helps the agent learn to avoid cliffs
and push the box to the goal efficiently. DQN would introduce unnecessary complexities,
while MC might be inefficient due to delayed updates

The Q-learning formula is as shown below (adapted from Lecture Notes).
<img src="/Images/Q_ learning_formula.png" width="700">

<h4 align = "center">
<u>Fig.2 Q-learning formula<u>
</h4>

In this assignment, the learning rate (**alpha value**) has been set to 0.1, the discount factor
(**gamma value**) has been set to 0.99.
The learning rate determines how quickly the agent learns from new experiences, while the
discount factor discounts the future rewards compared to immediate rewards (money is
worth more today than tomorrow). **Alpha=0.1** means that only 10% of the new experiences
is based on the Q-value, and 90% is based on the old Q-value. **Gamma=0.99** means that
the agent places more emphasis on future rewards, considering long-term rewards when
making decisions.
Q-learning helps the agent to improve his decision-making by continuously adjusting its
Q-values based on the maximum expected reward it can achieve in each given state by
following the optimal policy.
