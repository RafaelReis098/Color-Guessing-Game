legal_colors = ['R', 'G', 'B', 'Y', 'W', 'O', 'M', 'V']


def generate_color_sequence():
    import random
    random.seed()

    sequence = random.sample(range(len(legal_colors)), 4)
    return [legal_colors[i] for i in sequence]

colors = generate_color_sequence()

attempts = 5

def provide_hint(secret, guess):
    return ['R' if g == s else 'W' if g in secret else '_' for g, s in zip(guess, secret)]

print("Possible colors are R, G, B, Y, W, O, M, V")
print("Please enter your guess with no spaces between colors. Colors cannot be repeated\n")

guess_count = 0

for guess_count in range(1, attempts + 1):
    for _ in range(3):  # Allow 3 attempts to enter a valid guess
        user_guess = input(f"Enter your guess (e.g., RGBY): ").upper()
        user_guess = list(user_guess)

        if all(color in legal_colors for color in user_guess) and len(user_guess) == 4:
            break
        else:
            print("Invalid input. Please enter a valid guess.")
    else:
        print("You've exceeded the maximum number of invalid attempts.")
        break

    if user_guess == colors:
        print(f"Guess {guess_count}")
        print("You win.")
        break

    else:
        hint = provide_hint(colors, user_guess)
        delimiter = ''
        hint = delimiter.join(hint)
        print(f"Guess {guess_count}")
        print(hint)

if user_guess != colors:
    print("You lose! The correct sequence was:", ''.join(colors))
      
