# reinforcement-learning-cat-mouse-cheese
Found this excellent Java project which demonstrates Reinforcement Learning with Cat and Mouse game.
The complete lesson is very well written. Please read https://www.cse.unsw.edu.au/~cs9417ml/RL1/index.html

I have merely taken the sample project from that site, cleaned it a bit, made it Eclipse friendly.

To run: Run SwingApplet.java


COPIED VERBATIM FROM: https://www.cse.unsw.edu.au/~cs9417ml/RL1/applet.html
=========

Rules of the Game

The rules of the Cat and Mouse game are:

Both the cat and mouse have 8 degrees of movement. Up, down, left and right, as well as the four diagonals.
The mouse scores a point for getting the cheese. The mouse gets the cheese when it is in the same square as the cheese.
The cat scores a point for catching the mouse, by simply moving to the same square as the mouse.
If the mouse gets the cheese, a new piece is placed randomly while the cat and mouse keep their positions.
The game is over when the cat catches the mouse. The scores are then updated and a new game can begin.


  Applet Controls and Parameters

While on the playing screen, you will see a number of controls.

The slider below the game square controls the speed the game is played at.
The granularity of the performance graph can be adjusted with the slider underneath it. Setting it to coarse produces a scatter plot, while using smooth draws a smooth line.
The Reset Scores button will reset the mouse and cat scores to zero.
The continuous checkbox determines whether a new game starts automatically after the mouse gets caught. Selecting continuous means the Start button does not have to be pressed to start a new game.
Lastly, the mouse brain can be one of two choices. Greedy Mouse, where the mouse just goes straight for the cheese taking no notice of the cat. Or, Smart Mouse, which uses the policy that has been learned in training.
The training screen has a number of parameters that can be adjusted. The Death Penalty and Cheese Reward are the rewards associated with the mouse getting caught or getting the cheese. Alpha, Gamma and Epsilon are embedded in the reinforcement learning algorithms. For a more detailed explanation of what they do, refer to the Algorithms page. The action selection method determines the way an action is selected from the Q-Values table, more detail on the TD-Learning page. The learning method can also be specified, for more detail on Q-Learning and Sarsa, refer again to the Algorithms page. The number of epochs (games) to train for can be entered in also.

Sensible defaults have been chosen for each of these parameters, so there is no need to adjust any of them before starting initial training.



  Tutorial

Following is a series of interactive experiments to help explain the operation of a reinforcement based learner.

If you haven't done so already, open the applet by clicking on the following button:

Part 1: Understanding the applet
The first screen presents you with options to select a world, or board, to play on. After you choose a board you can continue and use the applet, however to select another world you will have to close the applet and open it again by clicking on the button above.
Select the 'Wall' world and click on the start button.
The next panel presented is the game panel. From this panel a game can be started and you can observe the behaviour of the agent (the mouse), and performance statistics. The graph in the top right corner shows a graph of the performance of the mouse, which is measured as the number of points collected by the mouse compared to the number of points collected by the cat (the rules are given above on this page).
Select 'Greedy Mouse' and click Start
The game will start, you can see the score in the middle frame on the right, and a graph of the performance above. The greedy mouse does not use the reinforcement learning algorithm but tries to run straight for the cheese, disregarding the cat and paying the price..
Move the slider below the game board to 'Fast'. You can stop the game at any point by clicking on the 'Continuous' checkbox, which is currently selected.
In the graph window you will see a series of blue dots. There will be some slight variation in the performance graph but generally the points in the plot will range between about 1/4 to 2/3 of the height of the window. Below the graph next to the scores is a percentage value showing the aggregate score, measured as the percentage of all points collected by the mouse. This is an average of all the points shown in the graph.
Move the slider below the graph close to 'Smooth'
Smoothing the graph averages the values and shows the longer-term trend. You can see the performance of the greedy mouse is fairly constant.
Stop the game. Click 'Reset Scores', then select 'Smart Mouse' and start the game again. You will have to select 'Continuous' to have games proceed one after another.
In the performance window you should see the graph drop to a very low value. If you slow down the game you will see the mouse moving about aimlessly and being ruthlessly hunted down by the cat. The reason why the mouse is not performing well is because it has not been trained. In this applet the training and the playing (using the training information) has been seperated. In some reinforcement learning situations training and performing is mixed, so the agent learns from its experience in the world. Due to the nature of the problem and for explaining the algorithm we have seperated the two stages.
While playing the game the reinforcement learner simply exploits the information it has gained in the past and selects the best possible action. While learning the job of the agent is to explore the benefits of performing different actions in different situations, so tends to try new things more than exploit the information it has already gained.

Stop the game and select the 'Train' tab at the top of the window. (You can stop the game by clicking on the 'Continuous' check box)
This window provides fields for setting the parameters of the learner. These parameters will do fine for the moment. Click on 'Begin Training'. Depending on the speed of the computer it will take between a few seconds and a few minutes to train the learner for 50,000 epochs. One epoch is one game, we are training the agent by having it play 50,000 games in the background. While it is training we can observe how the performance of the agent changes by playing games as it trains.
Click on the 'Play' tab and start the game (make sure 'Continuous' is selected). Set the game speed to 'Fast'.
In the graph window you should see the performance of the agent rise as the training progresses. Once training is finished the performance graph will level as the agent is not learning from the games played in this window.
Slow down the game and observe the behaviour of the mouse
You should see the mouse stalking behind the wall and waiting for the cat to go around one side. It has learned to use the wall as a barricade and value it's life above a silly dash for a piece of cheese. Occasionally however the mouse does get caught.
Part 2: Learning Settings
Close the applet and open it again.
Select 'Random World', set the Rows and Columns to 5, and the number of obstacles to 1. This will create a mostly empty board.

Train the mouse with the current settings for 50,000 epochs
Before starting the game, what sort of performance value do you expect the mouse to get?
Set the game speed to 'Fast' and start the game.
You can see the performance is not very good. The mouse performs at about 20-30%.
Reset the scores. Select 'Greedy Mouse' and start the game.
This time the mouse scores about 40-45%. Why is our smart mouse doing worse than the greedy mouse? Perhaps we have not trained it enough?
Go to the training panel and traing the mouse for a further 50,000 or 100,000 epochs. Start the game again (reset the scores).
Even after further training the mouse still will not perform as well as the greedy mouse (about 30%). Surely the reinforcement learning technique converges on the optimum policy and should perform at least as well as the greedy mouse? How do you think we can improve the learner? In this case the problem is the way rewards and penalties are being defined. The mouse has been instructed to stay alive as a higher priority to getting the cheese (100 penalty vs 50 reward), so it tries to avoid the cat. This is generally a good strategy however in this world there is no method where the mouse can protect itself. There is nothing to hide behind (one obstacle is too small) so the strategy of the mouse is not working well. In this situation the strategy that provides the best score (note that the score is independant of the reward function. The reward function is internal to the learner) is to run straight for the cheese with no consideration for preserving the life of the mouse, ie the action taken by the greedy mouse.
In the training panel, undo the current training. Set the 'Death Penalty' value to 10 and train for 50,000 to 100,000 epochs. Start a new game (reset scores).
By lowering the death penalty we have encouraged the mouse to go for the cheese, and it now succeeds in gaining a score of roughly 45-50%. (It gets the cheese about half the time, the cat always gets it). This is even slightly better than the greedy mouse. How is it doing better than the greedy mouse? (slow the game down to observe behaviour)
Restart the applet and select any world. Play around with the learning settings, as well as the different learning types to get a feel for what they do. Typically the other parameters will not give very observable results, they will simply affect the rate of learning of the algorithm but not the final behaviour. Changing the reward policy will affect the final behaviour of the agent which may need to be customised depending on the situation (penalty 100 and reward 50 should be optimal for most situations created in the cat and mouse world).

What happens if you set the penalty and reward to negative values? (the mouse runs away from the cheese and straight to the cat!)
Part 3: Showing Off
Restart the applet with the 'Corridors' world. Train the mouse for 50,000 epochs.
Run the game on Fast for a while to get an idea of the performance, and then slow it down to watch the mouse. In this world the mouse can easily exploit the corridors to its advantage, waiting for the cat to come down one end and then running out the other end of the corridor. It learns some very clever tactics like luring the mouse out one side and letting the cat chase it as it goes and gets the cheese.
Occasionally the mouse gets caught. In what situations does this occur?
Sometimes the mouse gets caught in a corner, gets caught out being greedy or even appears to get run down by the cat. Is this a limit of the learner?
Train the agent for a further 50,000 epochs.
After starting the game again take a note of the performance. It may not update regularly as it only updates at the end of a game, which is when the cat finally catches the mouse. By slowing the game down you should see the mouse taking complete control of the game. It just needed a bit more training to learn what to do in certain situations. This world lends itself well to the mouse, which can clearly exploit the situation to its advantage.
Restart the applet and select the 'Trap' world. Train for 50,000 epochs.
This world is a bit more difficult- when the cat is in the 'trap' and the cheese is outside everything is fine for the mouse, however if the cheese ends up inside with the cat the mouse often gets caught out. (Occasionally in this world the agent may end up in a stale-mate situation where the mouse keeps moving between a few squares back and forth. The cat is not smart and gets trapped in a similar situation and neither of them gets anywhere. To get out of this situation set the learner to 'Greedy Mouse' to get it out of the loop and then switch back to 'Smart Mouse'). Typically the mouse will score about 60%. Is there room for improvement?
Try training for a further 50,000 to 100,000 epochs, or more if you have time..
If you want to watch the progess of the learner you can run a game while it is learning and watch the graph, however this slows down the learner quite significantly so it might be best to run a game slightly slower than the maximum. To get an updated measure of the performance reset the scores.
You may want to train it a bit more....
This is a difficult situation, but after about 200,000 to 400,000 epochs it should have learnt well enough to be up there with the best of them. The mouse needs to learn to draw the cat out from the trap and have it chase it right around the trap and use the block as a barricade. This takes a lot of training as it must be very sure about what it is doing if it is to be chased- one indecision will lead to the cat gaining on it and the mouse will be caught. With enough training the mouse can get a score of above 95% in this world.
You should be able to see the limitations of the reinforcement learner- it does very well on small worlds with enough training, but how much longer does it take to train on an 8x8 world compared to a 5x5 world? Imagine applying a basic learner like this to a world with more possibilities, how much would it increase the learning time and space needed? What effect would you expect if you expanded the domain to a situation with say 10 independent variables instead of 3 (the positions of the cheese, mouse and cat)? It took a long time to reach an optimal solution for a world such as the trap world; it develops very complicated behaviour but this can take a lot of computation!



  Hints for Using the Applet

The game may take a little while to start after clicking the Click here to start! button, be patient. Particularly with the 8x8 worlds.
While training, it is best to reduce the speed of the game or stop it from playing altogether. Running the game quickly uses some CPU time that the training could otherwise benefit from.
