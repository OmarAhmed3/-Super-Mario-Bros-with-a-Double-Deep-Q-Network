# -Super-Mario-Bros-with-a-Double-Deep-Q-Network
Reinforcement project For Super Mario Bros Game Using a Double Deep Q-Network 

# CONTENTS
## 1.	INTRODUCTION TO REINFORCEMENT LEARNING
## 2.	THE SUPER MARIO BROS (NES) ENVIRONMENT
## 3.	BUILDING AN AGENT THAT CAN GET THROUGH THIS ENVIRONMENT

# What is Reinforcement learning?
## REINFORCEMENT LEARNING IS THE FAMILY OF LEARNING ALGORITHMS IN WHICH AN AGENT LEARNS FROM ITS ENVIRONMENT BY INTERACTING WITH IT. 
## WHAT DOES IT LEARN? INFORMALLY, AN AGENT LEARNS TO TAKE ACTIONS THAT BRING IT FROM ITS CURRENT STATE TO THE BEST (OPTIMAL) REACHABLE STATE.
I FIND THAT EXAMPLES ALWAYS HELP. EXAMINE THE FOLLOWING 3×3 GRID:

![image](https://user-images.githubusercontent.com/101157505/184281285-82305127-2e07-4825-8175-db070c88c52e.png)

## This grid is our agent's environment. Each square in this environment is called a state, and an environment will always have a start and end state which you can see highlighted in green and red, respectively. Much like a human, our agent will learn from repetition in a process called an episode. At the start of an episode, an agent will begin at the start state, and it will keep making actions until it arrives at the end state. Once the agent makes it to the end state the episode will terminate, and a new one will begin with the agent once again beginning from the start state.

## Here I've just given you a grid, but you can imagine more realistic examples. Imagine you're in a grocery store and you look at your shopping list: you need to buy dried rosemary. Your start state would be your location when you enter the store. The first time you try to find rosemary you might be a bit lost, and you probably won't move the most direct way through the store to find the "Herbs and Spices" aisle. But on each subsequent visit, you'll get better and better at finding it, until you reach the point where you can move directly to the correct aisle when you walk in.

## When an agent lands on a state it accumulates the reward associated with that state, and a good agent wants to maximize the accumulated discounted reward along an episode (I'll explain what discounted means later). Suppose our agent can move vertically, horizontally, and diagonally. Based on this information, you can see that the best way for the agent to make it to the end state is to move diagonally (directly towards it) since it would accumulate a reward of -1 + 0 = -1. If the agent would move in any other way towards the end state, it would accumulate a reward less than -1. For example, if the agent were to move right, right, up, and then up once more, it would get a reward of -1 + (-1) + (-1) + 0 = -3, which is less than -1.  Moving diagonally is therefore called the optimal policy π*, where π is a function that takes in a state and outputs the action the agent will take from that given state. You can logically deduce the best policy for this simple grid, but how would we solve this problem using reinforcement learning? 

# Double Q-Learning
## There is one major issue with Q-learning that we need to deal with: over-estimation bias, which means that the Q-values learned are higher than they should be. Mathematically, maxaQ (st+1, a) converges to E (maxaQ(st+1, a)), which is higher than maxa(E(Q(st+1, a)), the true Q-value (I won't prove that here). To get more accurate Q-values, we use something called double Q-learning. In double Q-learning, we have two Q-tables: one which we use for taking actions, and another specifically for use in the Q-update equation. The double Q-learning update equation is:
## Q*(st, at) ←Q*(st, at) + α(rt+1 + γ maxa QT(st+1, a) - Q*(st, at))
## where Q* is the Q table that gets updated, and QT is the target table. QT copies the values of Q* every n step.


# Super Mario Bros (NES)
## 	Now that you have a brief overview of reinforcement learning, let's build our agent that can make it through the first level of Super Mario Bros (NES). We will be using the gym-super-Mario-bros library, built on top of the Open AI gym. For those not familiar with gyms.

# 	Wrappers 
## •	PreprocessFrames Class make (resize image - convert to nparray - move axis(reshape) - scale values from 0-1)
## •	CustomStep Class make (repeats the same action in 'n' skipped frames to compute faster - takes a maximum of 2 frames)
## •	StackFrames Class make (on reset() returns first 'observation' STACKED 'stack_size' times - observation() returns current 'observation' STACKED with 'stack_size-1' previous 'observation')
## •	CustomReward Class make (give reward for agent)

# 	ReplayBuffer 
## •	Store Transitions in Buffer
## •	UNIFORMLY SAMPLES 'BUFFER' AND RETURNS A 'BATCH' OF Batch_Size


# 	Network
## •	DuelingDeepQNetwork (build model with CNN and Layer)
## •	Forward (make forward propagation)
## •	caculate_conv_output_dims (calculate output dimensions)
## •	save_model (Save model)
## •	load_model (Load model)

# 	Agent
## •	DuelingDDQNAgent (MEM PARAMS - MODEL PARAMS - e-GREEDY POLICY – learn function )

	 Training
![image](https://user-images.githubusercontent.com/101157505/184281620-f52968d0-2d85-4572-b6db-fcc9254c8ccd.png)

# 	Testing
![image](https://user-images.githubusercontent.com/101157505/184281669-1d3781d3-6f1e-4634-844a-4c5a978ddc56.png)

![image](https://user-images.githubusercontent.com/101157505/184281680-eee406ae-7d47-4c7f-9412-b0ebb842e5f1.png)




