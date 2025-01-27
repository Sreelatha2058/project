# project
import random

# List of words to choose from
word_list = ['python', 'hangman', 'developer', 'github', 'computer', 'programming', 'challenge', 'algorithm']
# Pick a random word from the list
word = random.choice(word_list)
word_length = len(word)
guesses = '_' * word_length
guessed_letters = set()
attempts_left = 6

def display():
    """Display the current state of the word and the remaining attempts."""
    print(f"Word: {guesses}")
    print(f"Attempts left: {attempts_left}")
    print(f"Guessed letters: {', '.join(sorted(guessed_letters))}")
    print()

def make_guess():
    """Prompts the player to make a guess."""
    while True:
        guess = input("Guess a letter: ").lower()
        if len(guess) != 1 or not guess.isalpha():
            print("Please enter a single letter.")
        elif guess in guessed_letters:
            print("You've already guessed that letter.")
        else:
            return guess

def update_guesses(guess):
    """Update the current state of the word with the guessed letter."""
    global guesses
    new_guesses = list(guesses)
    for i in range(word_length):
        if word[i] == guess:
            new_guesses[i] = guess
    guesses = ''.join(new_guesses)

def play_game():
    global attempts_left
    print("Welcome to Hangman!")
    
    while attempts_left > 0 and guesses != word:
        display()
        guess = make_guess()
        guessed_letters.add(guess)

        if guess in word:
            print(f"Good guess! '{guess}' is in the word.")
            update_guesses(guess)
        else:
            attempts_left -= 1
            print(f"Oops! '{guess}' is not in the word.")
    
    if guesses == word:
        print(f"Congratulations! You've guessed the word: {word}")
    else:
        print(f"Game Over! The word was: {word}")

if __name__ == "__main__":
    play_game()

