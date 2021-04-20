# Snake AI

## Version 3.0
Added additional apples and obstacles to original Snake AI

Version 2.0 - Added obstacles to original Snake AI

## Dependencies
There exist three dependencies:

1. numpy
2. pyqt5
3. Python3.6+

To install dependencies, run `pip3 install -r requirements.txt`


## Description
Traditional Snake game: https://www.google.com/search?q=classic+snake+game&oq=classic+snake+&aqs=chrome.0.0i20i263i433j69i57j0j0i20i263j0j46j0l4.1812j0j4&sourceid=chrome&ie=UTF-8

This implementation of the Snake AI game was adapted from Chrispresso (https://github.com/Chrispresso/SnakeAI.git), who has this code licensed under an open-source MIT license. 

In the traditional snake game, you are the snake and use the arrow keys to eat as many apples as you can without dying by crashing into yourself or the walls. In this adaptation of the game, I have coded an AI snake that uses reinforcement learning to learn from its mistakes/failures and progressively get smarter. I have also added a yellow obstacle, as well as another apple (blue) to the game to make it more interesting.


## How the AI Snake Learns
Through reinforcement learning, the AI is able to identify the optimal (shortest) path to pick up all the apples and avoid obstacles without dying. As you can see in the AI videos, the AI snake's initial performance is quite poor, but through back propagation using a 4-layer neural network and a fitness algorithm, it is able to gradually improve and eventually perform as well as (or even better than) humans. 

The snake is also able to learn through a fitness algorithm, which rewarded snakes that picked up more apples and punished ones with a high number of steps. There are 500 parent snakes in Generation 0, which generate 1500 offspring each new generation. There is a slight chance of mutation each round, and the snakes with the best fitness reproduce.

The 4-layer neural network is also integral to the AI Snake's success. The first layer of the neural network has 48 input nodes: 8 for wall vision (NE, NW, SE, SW, N, S, E, W), 8 for self vision, 8 for apple1 vision, 8 for apple2 vision, 4 for head direction (U, D, L, R), 4 for tail direction, and 8 for obstacle vision. There are also 2 hidden layers - the first has 20 nodes, and the second has 12 nodes. The last layer of the neural network has 4 nodes, corresponding to the snake's ultimate head direction (U, D, L, R).

After hundreds of generations and hours of training, the AI snake is able to achieve a score of 63 (high score: 100)! 

An interesting phenomenon is that the AI snake develops a clockwise-like pattern to navigate the map and eat the apples. It also does quite well in picking up the apples together, as well as avoiding the walls and the obstacle we added.


## Applications
This project has numerous real-world, practical applications. For instance, the path of the snake is similar to that of an uber driver using “Uber Pool” - the apples are similar to passengers waiting to be picked up, and the obstacles are similar to roadblocks and traffic jams. Hence, the same reinforcement learning models used to solve this adapted version of “Snake” could also be used to maximize the efficiency of “Uber Pool,” as well as numerous others fascinating applications.


## Future Goals
Additional avenues to explore with our snake AI include:
1. Experiment with fitness formula to train faster
2. Multiple snakes
3. Multiple obstacles
4. Moving apples 
5. Moving obstacles
6. More obstacles & apples as game goes on



## Getting started

Fully adapted from Chrispresso: 
1. Clone the repo or download it in someway
2. The two places you will ever really need to change stuff unless you feel like going crazy are `settings.py`, which control the hyperparameters of the Neural Network and Genetic Algorithm and `snake_app.py`, which is the graphics and GA.
3. Pick some things you would like to test with under `settings.py`. If you change the `board_size` drastically you will probably want to change `SQUARE_SIZE` under `snake_app.py`. The current settings when you first clone are the settings I used for training a snake to solve 10x10 and the 50x50 grids. Play around with this stuff if you want, you can always create another population in a new command window that use different settings. 
4. Head over to `snake_app.py` and adjust `show=True, fps=200` if you would like. `show` controls whether or not to display the snakes learning. FPS in the case of show is capped at your monitor refresh. Definitely faster to train with `show=False, fps=1000`.
5. Go to the area of `# Next generation` and you can print out the fitness if you would like. This is also where you can `save` the snake. Well you can save anywhere I guess, but this is where I saved the best snake from each generation. This can be done with `save_snake('path/to/population/folder', 'snake_name (i.e. best_snake_gen0)', snake, self.settings)`. This saves the snake, the constructor params that were used to create the snake and the `settings.py` file used for hyperparameters. If you load the same snake you saved, the snake will play **exactly** how it did before. The apple locations are based off an initially `apple seed`. So if you load the same snake without modifying the contructor, then the snake will replay what it did. Very helpful for me since I trained without visualizations and needed to go back and record stuff for the video.
6. Run it! However you like, you can run it and get some snakes generating!


## Loading snakes
Also fully adapted from Chrispresso: 

Let's say you have a 50 generations of snakes saved and you want to create a new population with the last 10 generations. You could start a new instance of `snake_app.py` and modify `for _ in range(self.settings['num_parents']):` portion to generate 10 less snakes. Then you can load your 10 best snakes and insert them into the population. This is where you can choose to either modify the constructor of your snake to have a different `apple_seed` or allow the snake to run it's previous course. The choice is up to you and totally dependent on your goals!

If the ability to load snakes is something you want to have an easier time with let me know and I can work on that.
