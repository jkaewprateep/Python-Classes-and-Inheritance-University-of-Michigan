# Python-Classes-and-Inheritance-University-of-Michigan
Python Classes and Inheritance University of Michigan

<p align="center" width="100%">
    <img width="47%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/Screenshot%202024-08-28%20112743.png">
    <img width="40%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/kid_07.jpg"> </br>
    <b> Pictures from the Internet </b> </br>
</p>

[Applied Data Science with Python]( https://coursera.org/share/99b989f079284ca6cae2bb8981f58dfa ) </br>
[Python 3 Programming Specialization]( https://coursera.org/share/ba047d1c5738f9bba3b08a5ac883569d ) </br>
[Google IT Automation with Python]( https://coursera.org/share/4ce05eb064193ff87071baedb37f1c9e ) </br>
[HackerRank Python (Basic)]( https://www.hackerrank.com/certificates/e063e97d9d72 ) </br>
[DeepLearning.AI TensorFlow Developer]( https://coursera.org/share/72d845ca7058700e2ff783ecd9e6b710 ) </br>

## Understand the assignment #1 Puzzles guessing word character from a random fortune-wheel with computer player ##

🧸💬 There are human player and computer player, start the game with an amount of money 0$, and the goal is to guess characters in word composing. The games is playing as a turn-based game each player has to spin the wheel and define an amount for each turn with valid of three actions (1) Guessing a letter that does not mean guessing in the game and the minimum prize for the vowel is at least 250$ the game turn play will return the prize to the player in turn by the number of character guessing correct times the prizes of money the player determined in each turn base. (2) Guess to win the game by each turn and correct phase to win the games and (3) Turn pass by say pass.

<p align="center" width="100%">
    <img align="left" width="36%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/kid_08.jpg" alt="image" />
    <p align="middle">
    <b>  </b> </br>
    <img align="top" width="33%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/puzzles2.jpg" alt="image" />
    <img align="top" width="25%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/puzzles3.jpg" alt="image" />
    <b>  </b> </br>
    <img align="top" width="30%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/puzzles.jpg" alt="image" /> 
    <img align="down" width="30%" src="https://github.com/jkaewprateep/Python-Classes-and-Inheritance-University-of-Michigan/blob/main/hangmangames.jpg" alt="image" /> </br>
    </p>
    <b>  </b> </br>
</p>
<p align="center" width="100%">
    <b> Pictures from the Internet </b> </br>
</p>

### Select random text ###

🧸💬 Selecting random text by utilizing randoms function, this implementation is when over start the running project but for random instant required to a specific random number or create a random identity to tell random sample of a new random object. </br>
👧💬 🎈 Implementation in an open environment will require random functions because of environment adjustment and boost learning faster in the development area. Learning function and perform immediately but as in open environment problem to create a smooth response and evaluation random function still required similar to a bouncing ball on the floor the basketball players can play it but warm-up methods allowed them to play better with a confidence level. </br>

```
import random

rand_number = random.randint(1, 10)
print('Random number between 1 and 10: {}'.format(rand_number))

letters = [letter for letter in 'ABCDEFGHIJKLMNOPQRSTUVWXYZ']
rand_letter = random.choice(letters)
print('Random letter: {}'.format(rand_letter))
```

🧸💬 We’re going to define a few useful methods for you:  </br>
        (1) getNumberBetween(prompt, min, max)) validate number of prompts input and minimum and maximum values.  </br>
        (2) spinWheel() simulates spinning the wheel and returns a dictionary with a random prize.  </br>
        (3) getRandomCategoryAndPhrase() returns a tuple with a random category and phrase for players to guess  </br>
        (4) obscurePhrase(phrase, guessed) returns a tuple with a random category and phrase for players to guess  </br>

```
import json
import random
import time

LETTERS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

# Repeatedly asks the user for a number between min & max (inclusive)
def getNumberBetween(prompt, min, max):
    userinp = input(prompt) # ask the first time

    while True:
        try:
            n = int(userinp) # try casting to an integer
            if n < min:
                errmessage = 'Must be at least {}'.format(min)
            elif n > max:
                errmessage = 'Must be at most {}'.format(max)
            else:
                return n
        except ValueError: # The user didn't enter a number
            errmessage = '{} is not a number.'.format(userinp)

        # If we haven't gotten a number yet, add the error message
        # and ask again
        userinp = input('{}\n{}'.format(errmessage, prompt))

# Spins the wheel of fortune wheel to give a random prize
# Examples:
#    { "type": "cash", "text": "$950", "value": 950, "prize": "A trip to Ann Arbor!" },
#    { "type": "bankrupt", "text": "Bankrupt", "prize": false },
#    { "type": "loseturn", "text": "Lose a turn", "prize": false }
def spinWheel():
    with open("wheel.json", 'r') as f:
        wheel = json.loads(f.read())
        return random.choice(wheel)

# Returns a category & phrase (as a tuple) to guess
# Example:
#     ("Artist & Song", "Whitney Houston's I Will Always Love You")
def getRandomCategoryAndPhrase():
    with open("phrases.json", 'r') as f:
        phrases = json.loads(f.read())

        category = random.choice(list(phrases.keys()))
        phrase   = random.choice(phrases[category])
        return (category, phrase.upper())

# Given a phrase and a list of guessed letters, returns an obscured version
# Example:
#     guessed: ['L', 'B', 'E', 'R', 'N', 'P', 'K', 'X', 'Z']
#     phrase:  "GLACIER NATIONAL PARK"
#     returns> "_L___ER N____N_L P_RK"
def obscurePhrase(phrase, guessed):
    rv = ''
    for s in phrase:
        if (s in LETTERS) and (s not in guessed):
            rv = rv+'_'
        else:
            rv = rv+s
    return rv

# Returns a string representing the current state of the game
def showBoard(category, obscuredPhrase, guessed):
    return """
Category: {}
Phrase:   {}
Guessed:  {}""".format(category, obscuredPhrase, ', '.join(sorted(guessed)))

category, phrase = getRandomCategoryAndPhrase()

guessed = []
for x in range(random.randint(10, 20)):
    randomLetter = random.choice(LETTERS)
    if randomLetter not in guessed:
        guessed.append(randomLetter)

print("getRandomCategoryAndPhrase()\n -> ('{}', '{}')".format(category, phrase))

print("\n{}\n".format("-"*5))

print("obscurePhrase('{}', [{}])\n -> {}".format(phrase, ', '.join(
        ["'{}'".format(c) for c in guessed]), obscurePhrase(phrase, guessed)))

print("\n{}\n".format("-"*5))

obscured_phrase = obscurePhrase(phrase, guessed)
print("showBoard('{}', '{}', [{}])\n -> {}".format(phrase, obscured_phrase, ','.join(
        ["'{}'".format(c) for c in guessed]), showBoard(phrase, obscured_phrase, guessed)))

print("\n{}\n".format("-"*5))

num_times_to_spin = random.randint(2, 5)
print('Spinning the wheel {} times (normally this would just be done once per turn)'.format(num_times_to_spin))

for x in range(num_times_to_spin):
    print("\n{}\n".format("-"*2))
    print("spinWheel()")
    print(spinWheel())


print("\n{}\n".format("-"*5))

print("In 2 seconds, will run getNumberBetween('Testing getNumberBetween(). Enter a number between 1 and 10', 1, 10)")

time.sleep(2)

print(getNumberBetween('Testing getNumberBetween(). Enter a number between 1 and 10', 1, 10))
```

🐑💬 ➰ Beginning the games by running the Python codes provided, and the games display as in the context box next below. </br>

```
# Given a phrase and a list of guessed letters, returns an obscured version
# Example:
#     guessed: ['L', 'B', 'E', 'R', 'N', 'P', 'K', 'X', 'Z']
#     phrase:  "GLACIER NATIONAL PARK"
#     returns> "_L___ER N____N_L P_RK"
```

## Part A: WOFPlayer ##

🐑💬 ➰ We define the player instance for the collection of these values as a class name ```WOFPlayer```. </br>
    ```.name```: The name of the player (should be passed into the constructor) </br>
    ```.prizeMoney```: The amount of prize money for this player (an integer, initialized to 0) </br>
    ```.prizes```: The prizes this player has won so far (a list, initialized to []) </br>

### Sample output ###

```
Steve has $200

Category: Places
Phrase: _L___ER N____N_L P_RK
Guessed: B, E, K, L, N, P, R, X, Z

Guess a letter, phrase, or type 'exit' or 'pass':
```
