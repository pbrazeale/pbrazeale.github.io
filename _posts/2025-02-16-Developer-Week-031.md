## NeetCode SQL for Beginners (59/75)


## Projects
### 100 Days of Code: The Complete Python Pro Bootcamp (7/100)
https://www.udemy.com/course/100-days-of-code/

This came across my feed as a recommendation when I was looking for Python books, and I was able to snag it on sale, so it seemed a no brainer. The simple act of dedicated focus and building projects publicly should prove well worth the price of admission.

Full journal can be read here:
https://github.com/pbrazeale/100-Days-of-Code

#### Day 005
Built a CLI that takes in a password_length between 12 - 20, randomly assigns the number of letters, characters, and symbols. And then randomizes the sequence to produce a randomized password. This was beyond the lesson itself, and really helped to solidify the use of random's built in functions.
https://github.com/pbrazeale/100-Days-of-Code/blob/main/Day_005_Password_Generator/upgraded_password_generator.py

#### Day 006
Solved the maze problem with code, using the follow right path algorithm. Gave me flashbacks to the early 2000s and watching the maze screen saver for Windows XP. I need to spend a little time thinking through edge cases. I failed to consider what happens when the robot reached an empty square space, because I didn't encounter it when I tested my code. "Works on my machine" is not an acceptable mindset.

#### Day 009
Built a CLI for blind auctions. It was a simple solution using a nested list inside a dictionary. Didn't need the video to solve the problem which I'm proud of.

#### Day 011
Built a CLI Blackjack game. This was a capstone project, so I watched the intro to understand the application requirements and then built the game without any reference to the course, nor outside google searches.
https://github.com/pbrazeale/100-Days-of-Code/blob/main/Day_011_Blackjack/blackjack.py

Not sure if it's optimal, but I used `random` to shuffle my deck list and then delt by indexing into the deck. It's a total of 101 lines of code, which seems suboptimal, but I was able to build it in about an hour, so that was fun. Ran into the odd syntax error, and had to add in conditional check for dealer having 21 before entering the "hit()" phase of the game for the player, but otherwise everything worked as planned.

#### Day 012
Built a CLI number guessing game.
https://github.com/pbrazeale/100-Days-of-Code/blob/main/Day_012_Number_Guessing_Game/task1.py
Watched the first video, and built the game in ~30 minutes. ~10 minutes for working prototype and ~20 testing edge cases and refactoring.
