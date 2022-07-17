# Homework 11 -- Fun with OpenAI Gym!

## To Turn In
You should save at least one video showing your first, last, and an intermediary episode of the training process. Also save a couple videos from the testing process that runs at the end of the training.

Upload at least one of the videos to Cloud Object Storage and provide links using the instructions below. Also upload your highest scoring model.

Submit a write-up of the tweaks you made to the model and the effect they had on the results.
Questions to answer:
1) What parameters did you change, and what values did you use?
- Modified `density_first_layer` to `256`.
- Modified `density_second_layer` to `128`.

2) Did you try any other changes (like adding layers or changing the epsilon value) that made things better or worse?
- Attempted to adjust learning rate to `0.01` and the model average reward was unstable and diverged.
- Modified batch size to 128, and achieved similar results.
- I left all epsilon parameters untouched as they seemed reasonable.

3) Describe how your changes improve or degrade the model? How close did you get to a test run with 100% of the scores above 200?
- Adjusting the dense layer node counts seemed to have improved the model significantly.  The default parameters likely yielded too
simple of a network that could not observe patterns from samples in the memory buffer.
- The model, on average, attained a reward of 240, where 90% of the test runs were over 200.

4) Based on what you observed, what conclusions can you draw about the different parameters and their values?
- Adjusting certain parameters can make a break the model.  Adjusting epsilon can drastically change the outcome in training the model due to the classic
exploration vs. exploitation problem.  Making the model too simple would result in a poor ability to learn from the state space and outcomes, and too complex would result in overfitting.  Altered epsilon values can also cause the model to converge on a local minima and poor generalization to less familiar outcomes in test runs.

5) What is the purpose of the epsilon value?
- The epsilon value allows the agent to take random actions in order to add variability to potentially discover a better reward in a different sequence of actions.
This is known as exploration, which is crucial for the model to escape local minima, exploring different state spaces based on randomness induced in the actions taken.
- Allowing a high enough epsilon during certain stages of training will ensure that the agent has seen different variations in the outcome of the random actions taken.

6) Describe "Q-Learning".
- Q-Learning refers to the ability for an agent to learn what actions to take in an environment based on penalties and awards applied after running various simulations. By applying a policy gradient based on an agent's decision within the environment, an agent can learn much like a human; learn from mistakes, and improve from awards.

## Training
```
DQN Training Complete...
Starting Testing of the trained model...
99 	: Episode || Reward:  266.4447558468209
Average Reward:  266.4447558468209
Total tests above 200:  1
```

## Testing
```
0 	: Episode || Reward:  264.7423329399835
1 	: Episode || Reward:  263.6451523899568
2 	: Episode || Reward:  274.18411348406613
...
96 	: Episode || Reward:  252.68194324376984
97 	: Episode || Reward:  235.75955281468518
98 	: Episode || Reward:  192.43313003289043
99 	: Episode || Reward:  244.672167818836
Average Reward:  240.19444699289454
Total tests above 200:  86
```

## Videos
Train: https://ucb-mids-251-homework-3.s3.amazonaws.com/episode400.mp4  
Test: https://ucb-mids-251-homework-3.s3.amazonaws.com/testing_run50.mp4
