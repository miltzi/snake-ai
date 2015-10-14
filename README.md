## Snake AI Competition

### Notices

- _**09/10/2015: Even more bug fixes - redownload to get the latest fixes**_
- _04/10/2015: Bug fixes - If you have already downloaded the Snake Visualiser, please redownload and continue to work with this latest version_
- In order to submit you must have a Wits Moodle account. If you don't have one, email dean.wookey@students.wits.ac.za with your username (student number if student).

The Snake interactive challenge is an AI programming challenge open to any Wits student or staff member. The goal is simple: create a program which controls a snake such that it grows to a length longer than any other snake by eating red apples and trapping opposing players. There will be two categories for final judging which are the open category, open to anyone, and a category for the first and second years only.   
  
  
  

### Languages

Currently the challenge supports two languages: Python (version 2.6) and Java (1.7). The submission system allows you to upload 1 file only. If you're using java, this must be an executable .jar file containing your compiled snake.

### Implementation

At each step in the game, a Gamestate string is generated and sent to all the agents playing the game via Standard Input. The agents should then respond with a single number representing the move they wish to make via Standard Output. Each agent is given 50 milliseconds in which to output a move. If a move is not output in that time, the snake will move forward. If multiple moves are output in that time, only the most recently made move will be counted.

#### Initialisation

When the game first starts, an initialisation string will be sent to each agent indicating the number of snakes in the game, the play area width and height and lastly, the game mode. You can assume that the width and height will always be 50 units, the number of snakes will always be 4, and the game mode will be 1 (grow mode, snake that grew to the longest length by the end wins).   
  
Example initalisation string:

4 50 50 1

#### Game State Updates

At each step of the game, the current game state will be sent to each agent. Each state update will take the following form:

Blue Apple Position given as x and y coordinates (0,0 being top left).
Red Apple Position given as x and y coordinates (0,0 being top left).
Your snake number (0-3)
Snake0
Snake1
Snake2
Snake3
Each snake line will take the following form:

alive/dead/power length kills headX,headY bodyX,bodyY bodyX,bodyY ... tailX,tailY
As an example:

7 12
8 16
0
alive 26 2 10,12 15,12 15,7 5,7 5,2
dead 6 6 14,13 19,13
alive 2 1 12,13 12,14
power 10 8 10,2 15,2 15,6 16,6
In this example, the blue apple is at x position 7 and y position 12, and the red apple is at x position 8 and y position 16 where 0,0 is the top left corner of the play area. On the following line, the 0 means that the first snake in the following list of snakes is the one corresponding to your snake. If yours were the 4th snake, it would be a 3.   
  
The next 4 lines will contain descriptions of each snake in the game. The first word is either alive, dead or power. Dead snakes do not display in the game, so they should be ignored. After this is the length of that snake followed then by the number of other snakes that snake has killed. Lastly the snake's coordinate chain is given. Snakes can become power snakes by eating the blue apple, which gives them the ability to cut other snakes.   
  
The coordinate chain is made up of x,y coordinates representing points of interest in the snake's body. The first coordinate is the snake's head, the next represents the first kink in the snake. There can be any number of kinks in the snake which are all listed in order. Finally, the last coordinate represents the tail of the snake. As an example, the 3rd snake has the following description:

alive 2 1 12,13 12,14
This snake is alive, it has length 2, it has 1 kill. Its head is at position x=12 y=13 and its tail is at x=12 y=14. From this we can see that the snake is traveling upwards since the head is higher than the tail (y=0 is the top of the play area).

#### Game Over

When the game is over, instead of a gamestate, a single line containing the words "Game Over" will be sent to each agent. This gives agents the opportunity to write files etc. before they are shut down. If an agent does not exit after 500 milliseconds, it will be killed.

#### Moves

Once the gamestate has been read in, your agent should use that information to choose its next move. A move is made simply by outputting an integer in the range 0-6.  
The available moves are as follows:  
  

- 0: Up (Relative to the play area - north)
- 1: Down (Relative to the play area - south)
- 2: Left (Relative to the play area - west)
- 3: Right (Relative to the play area - east)
- 4: Left (Relative to the head of your snake)
- 5: Straight (Relative to the head of your snake)
- 6: Right (Relative to the head of your snake)

### Game Mechanics

#### Apple

The red apple spawns in random locations each time it is eaten or disappears. Occasionally, a blue apple will spawn on the game board. This apple turns the snake into a super snake, which can cut other snakes by crashing into them. The victim will be reduced in size, as its body will now only consist of the segments between its head and the point at which the super snake crashed into it. The power can only be used once, so the super snake will become a normal snake after the impact. The power is also time limited and will wear off after 100 time steps. Note that if the super snake crashes into itself, it will cut its own length. \\\\ The blue apple will spawn once for every ten red apple spawns during which there is no super snake. This means that when there is a super snake, the spawn counter does not run. When there is no super snake, the counter increments when a red apple spawns and when it reaches 10, a blue apple spawns.

#### Scoring

Throughout each game, the longest length achieved by each snake is recorded. The snake with the longest length in the end comes first. In case of a tie, kills made during that game are used to determine order.

#### Kills

A kill is awarded to a player when another player crashes into one of its body segments. No kill is awarded if the snake died at the same time another snake crashed into it. In other words, in the case of a head-on collision, neither snake receives a kill.

#### Respawning

When a snake dies in 'grow mode', it is randomly positioned somewhere in the play area with a starting length of 5 units. Snake agents whose program crashes will not be respawned.

#### Leagues

The game is split into 5 minute rounds, each made up of multiple games. Players are split into groups of 4 players according to their current league ranking. In the case where a game cannot be filled by submitted agents, it is filled with built-in agents. The games are then run and scored as above. Players who come first in their game advance to a higher league, whilst players who come last get relegated to a lower league. The highest league is 0.

#### Points

The points table gives the average rank of each player where the rank is counted from 0 being the last player in the league, 1 being the second last etc.

### Submitting

In order to submit you must have a moodle account. If you don't have one you can email dean.wookey@students.wits.ac.za. Once you have written your code in either Java or python, you can upload it on moodle. If you are unsure of how to do this, email me. If you have an agent already running, it will be removed from the rankings at the end of the current round and replaced with the new agent. Please note that java programs must be submitted as .jar files.

### Testing

To test your program without submitting, you can download the [standalone snake server](http://lamp.ms.wits.ac.za/snake/SnakeVisualiser2015.jar). To run the server your computer must have java installed. Note that to test your program using the tester, you must create a .jar file from your code. If you need to know how to create a **runnable** jar file from your Eclipse project, please google this. If you get horribly stuck, email pravesh.ranchod@wits.ac.za. Once you have a .jar file, you can test your code with the following command:

java -jar SnakeVisualiser2015.jar [-j javaprogram.jar] [-p pythonprogram] [-h wsad|normal] [-s movedelay] [-d duration]
For example if your SnakeVisualiser2015.jar is in the same folder as your java program which is called mysnake.jar, then you could use the following line to test it:

java -jar SnakeVisualiser2015.jar -j mysnake.jar
You can run up to 4 snakes in one game. If you specify less than 4 snakes, then the game will be filled up with built-in snakes. The other options do the following things:

- -j or -java followed by the path of a .jar file runs that .jar as a snake.
- -p or -python followed by the path of a python file runs that file as a snake.
- -h or -human followed by either 'wsad' or 'normal' to specify a human player using the WSAD keys or direction keys respectively to control the snake. 2 players can play at once.
- -s or -speed followed by an integer to set the millisecond delay between snake moves. Default is 50.
- -d or -duration followed by the time in seconds the game should last. Default is 300 (5 minutes).
Another example command:

java -jar SnakeVisualiser2015.jar -j /home/bob/aaa/mysnake/dist/mysnake.jar -h wsad -h normal -speed 25
This would start a game with 1 java player, a human player using the WSAD keys, a human player using the normal arrow keys, and 25 (double the normal) speed.

#### Debugging

In order to enable some form of debugging, the snake game creates 2 files when it is run that should aid in debugging. The files will be located in the same directory as the java or python program you're running. The first file is an error file which will list all the runtime errors your code triggers, and the second is a log file which allows your program to save output. To save output, your program should print "log message" and "message" will be appended to the end of the log file. Anything beginning with "log " will not be treated as a game move.

### Sample Agents

A randomly playing [python agent](http://lamp.ms.wits.ac.za/snake/randomsnake.py) and [java agent](http://lamp.ms.wits.ac.za/snake/ExampleSnake.java) are provided as examples. These agents read in the game state and output a random move.
