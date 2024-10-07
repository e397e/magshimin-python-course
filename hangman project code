# Hangman ASCII art with the word "Hangman"
HANGMAN_ASCII_ART = """ 
    _    _
   | |  | |
   | |__| | __ _ _ __   __ _ _ __ ___   __ _ _ __
   |  __  |/ _` | '_ \\ / _` | '_ ` _ \\ / _` | '_ \\
   | |  | | (_| | | | | (_| | | | | | | (_| | | | |
   |_|  |_|\\__,_|_| |_|\\__, |_| |_| |_|\\__,_|_| |_|
                        __/ |
                       |___/
"""
# Maximum number of tries before losing the game
MAX_TRIES = 6

# Dictionary containing ASCII art for each stage of the hangman
HANGMAN_PHOTOS = {
    0: """x-------x""",
    1: """    x-------x
    |
    |
    |
    |
    |""",
    2: """    x-------x
    |       |
    |       0
    |
    |
    |""",
    3: """    x-------x
    |       |
    |       0
    |       |
    |
    |""",
    4: """x-------x
    |       |
    |       0
    |      /|\\
    |
    |
    """,
    5: """    x-------x
    |       |
    |       0
    |      /|\\
    |      / 
    |""",
    6: """x-------x
    |       |
    |       0
    |      /|\\
    |      / \\
    |"""}


def check_win(secret_word, old_letters_guessed):
    """
    This function check if there a win
    :param secret_word: the secret word
    :param old_letters_guessed: the letters that guessed 
    :type secret_word: str
    :type old_letters_guessed: str
    :return: if there is a win
    :rtype: bool
    """
    #Create an empty list to store the guessed letters
    guessed_letters = []
    # Iterate over each character in the secret word
    for char in secret_word:
        # Check if the character has been guessed before
        if old_letters_guessed.count(char) >= 1:
            # If the character has been guessed, append it to the list of guessed letters
            guessed_letters.append(char)

    if len(guessed_letters) == len(secret_word):# Check if the number of guessed letters is equal to the length of the secret word and return True or False accordingly
        return True
    else:
        return False


def show_hidden_word(secret_word, old_letters_guessed):
    """
    This function print the hidden word with the letters that guessed
    :param secret_word: the secret word
    :param old_letters_guessed: the letters that guessed 
    :type secret_word: str
    :type old_letters_guessed: str
    :return: the hidden word
    :rtype: str
    """
    # Create an empty list to store the hidden word
    hidden_word = []
    # Iterate over each character in the secret word
    for char in secret_word:
        # Check if the character has been guessed before
        if old_letters_guessed.count(char) >= 1:
            # If the character has been guessed, append it to the hidden word
            hidden_word.append(char)
        else:
            # If the character has not been guessed, append an underscore to the hidden word
            hidden_word.append("_")
    # Join the characters in the hidden word list with spaces and return the result        
    return " ".join(hidden_word)


def check_valid_input(letter_guessed, old_letters_guessed):
    """
    This function get letter and list of guessed letters and return true if this valid and false either
    :param letter_guessed:
    :param old_letters_guessed:
    :type letter_guessed: str
    :type old_letters_guessed: list of str
    :return: True/False
    :rtype: bool
    """
    # Check if the guessed letter is a single alphabetic character and has not been guessed before
    if not letter_guessed.isalpha() or len(letter_guessed) > 1:
        return False
    # Check if the guessed letter has been guessed before by the user    
    elif letter_guessed in old_letters_guessed:
        return False
    else:
        return True


def try_update_letter_guessed(letter_guessed, old_letters_guessed):
    """
    :param letter_guessed:
    :param old_letters_guessed:
    :type letter_guessed: str
    :type old_letters_guessed: list of str
    :return: True/False
    :rtype: bool
    """
    # Check if the guessed letter is a valid input
    if not check_valid_input(letter_guessed, old_letters_guessed):
        # If not valid, print 'X' and the sorted list of guessed letters
        print("X")
        print(" -> ".join(sorted(old_letters_guessed)))
        return False
    else:
        # If valid, append the guessed letter to the list of guessed letters
        old_letters_guessed.append(letter_guessed)
        return True


def choose_word(file_path, index):
    """
    This function get 2 params the first file path where the file is and the second is the index num
    it's return a tuple the has:
    1. the num of word (non duplicates)
    2. guessed word by the provided index
    :param file_path: the file path
    :param index: the number of the word to be guessed
    :type file_path: str
    :type index: int
    :return: a tuple with the num of word (non duplicates) and the guessed word
    :rtype: tuple
    """
    # Open the file at the provided path
    file = open(file_path, "r")
    # Initialize an empty tuple to store results
    results_tuple = ()
    # Iterate over each line in the file
    for line in file:
        # Calculate the number of unique words in the line
        num_of_words = len(list(dict.fromkeys(line.split())))
        # Initialize index
        index = 0
        # Ensure index is within the range of words in the line
        while index > len(line.split()):
            # Adjust index if it's greater than the number of words
            index = index - len(line.split())
        # Update the results tuple with the number of words and the word at the specified index
        results_tuple = (num_of_words, line.split()[index - 1])
    # Returning the results
    return results_tuple


def print_hangman(num_of_tries):
    """
    This function gets number of tries and print the hangman according to the level
    :param num_of_tries: The number of tries (means num of fails)
    :type num_of_tries: int
    :return: none
    """
    # Print the hangman figure based on the number of tries
    print(HANGMAN_PHOTOS[num_of_tries])


def is_letter_in_secret(letter_guessed, secret_word):
    """
    This function get letter and check if the letter in the secret word
    :param letter_guessed: the letter that guessed
    :param secret_word: the secret word
    :type letter_guessed: str
    :type secret_word: str
    :return: letter in or not
    :rtype: bool
    """
    # Check if the guessed letter is not in the secret word
    if letter_guessed not in secret_word:
        # Print sad face if the letter is not in the word and return False
        print(":(")
        return False
    else:
        # Return True
        return True


def main():
    """
    Hangman game
    """
    
    # Print the Hangman ASCII art
    print(HANGMAN_ASCII_ART)
    # Prompt the user to enter the file path containing words
    file_path = input("Enter file path: ")
    # Prompt the user to enter the index of the word to be guessed
    word_index = int(input("Enter index: "))
    # Choose a word from the file based on the provided index
    secret_word = choose_word(file_path, word_index)[1]
    # Initialize an empty list to store the guessed letters
    old_letters_guessed = []
    # Initialize the number of tries to 0
    num_of_tries = 0

    print("Let's Start!")
    # Calling the function to rint the initial hangman figure
    print_hangman(0)
    # Print the hidden version of the secret word
    print(show_hidden_word(secret_word, old_letters_guessed))

    # Continue the game loop until the maximum number of tries is reached or the player wins
    while not num_of_tries == MAX_TRIES and not check_win(secret_word, old_letters_guessed):
        # Prompt the user to guess a letter and convert it to lowercase
        letter_guessed = input("Guess a letter: ").lower()
        # Update the guessed letters list with the new guessed letter
        if try_update_letter_guessed(letter_guessed, old_letters_guessed):
            # If the guessed letter is not in the secret word, increment the number of tries and print the updated hangman figure
            if not is_letter_in_secret(letter_guessed, secret_word):
                num_of_tries += 1
                print_hangman(num_of_tries)
                # Print the current state of the word with guessed letters revealed
                print(show_hidden_word(secret_word, old_letters_guessed))
            else:
                # Print the secret word and all the letter guessed
                print(show_hidden_word(secret_word, old_letters_guessed))
    # Check if the player wins or loses and print the corresponding message
    if check_win(secret_word, old_letters_guessed):
        print("WIN")
    else:
        print("LOSE")


if __name__ == "__main__":
    main()
