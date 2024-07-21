import time
import random


def print_pause(msg_to_print):
    #This function is designed to reduce complexity of code by lessening the lines
    """Print a message and pause for 2 seconds."""
    print(msg_to_print)
    time.sleep(2)


def intro(item, option, score):
    """Introduce the game setting."""
    print_pause(
        "You find yourself standing in an open field, filled "
        "with grass and yellow sunflowers.\n"
    )
    print_pause(
        f"Rumor has it that a "+ option +" is somewhere around "
        "here, and has been terrorizing the city.\n"
    )
    print_pause("In front of you is a house.\n")
    print_pause("To your right is a very mysterious cave.\n")
    print_pause(
        "In your hand you hold your trusty (but not very effective) pocketknife.\n"
    )
    print_pause(f"Your current score is: {score}\n")


def cave(item, option, score):
    """Handle the cave scenario."""
    if "sword" in item:
#this function checks if the player has the sword in their inventory
        print_pause("\nYou look into the mysterious cave.")
        print_pause("\nYou try to find something new in all this rocky mess")
        print_pause("\nYou go back outside")
    else:
        print_pause("\nYou look into the mysterious cave.")
        print_pause("\nYou try to find something useful in all this rocky mess")
        print_pause("\nYou catch a glimpse of a very shiny but faint gold color")
        print_pause("\nYou found the Golden sword of justice!")
        print_pause("\nYou go back outside")
        item.append("sword")
        score += 10  # Increase score for finding the sword
    print_pause(f"Your current score is: {score}\n")
    field(item, option, score)


def house(item, option, score):
    """Handle the house scenario."""
    print_pause("\nYou approach the door of the house.")
    print_pause(
        "\nYou are about to knock when the door opens and out steps a " + option +"."
    )
    print_pause(
        "\nA shiver runs down your spine knowing this is the "+ option +"'s house!"
#+ option + function takes a random word from the list       
    )
    print_pause("\nThe " + option + " attacks you!\n")

    if "sword" not in item:
        print_pause(
            f"You feel a bit overwhelmed by the "+ option + ", "
            "knowing you only have a tiny pocketknife.\n"
        )

    while True:
        choice2 = input("Would you like to (1) fight or (2) run away?\n")
        if choice2 == "1":
            if "sword" in item:
                print_pause(
                    f"\nAs the "  + option + " moves to attack, you unsheath your new sword."
                )
                print_pause(
                    "\nThe Golden sword of justice shines brightly in your hand "
                    "as you brace yourself for the attack."
                )
                print_pause(
                    f"\nBut the"  + option + " takes one look at your Golden sword "
                    "of justice and runs away!"
                )
                print_pause(
                    f"\nYou have rid the city of the {option} "
                    "You are victorious!\n"
                )
                score += 20  # Increase score for defeating the enemy with the sword
            else:
                print_pause("\nYou do your best...")
                print_pause(
                    "but your tiny pocketknife is no match for the " + option + "."

                )
                print_pause("\nYou have been defeated!\n")
                score -= 10  # Decrease score for being defeated
            print_pause(f"Your final score is: {score}\n")
            play_again()
            break
        elif choice2 == "2":
            print_pause(
                "\nYou run back into the field.\n"
                "You see the creature from a distance but it doesn't "
                "seem to be following you.\n"
            )
            print_pause(f"Your current score is: {score}\n")
            field(item, option, score)
            break
#this function ends the game
        else:
            print_pause("Please enter '1' to fight or '2' to run away.")


def field(item, option, score):
    """Present the field choices to the player."""
    print_pause("Enter 1 to open the door.")
    print_pause("Enter 2 to search the mysterious cave.")
    print_pause("What would you like to do?")

    while True:
        choice1 = input("(Please enter 1 or 2.)\n")
#this function is so the player can choose what they want
        if choice1 == "1":
            house(item, option, score)
            break
        elif choice1 == "2":
            cave(item, option, score)
            break
        else:
            print_pause("Please enter '1' to open the door or '2' to search the cave.")


def play_again():
    """Ask the player if they want to play again."""
    again = input("Would you like to play again? (y/n)\n").lower()
    if again == "y":
        print_pause("\n\n\nFantastic! Restarting the game ...\n\n\n")
        play_game()
    elif again == "n":
        print_pause("\n\n\nThanks for playing! See you next time.\n\n\n")
    else:
        play_again()


def play_game():
    """Start the game."""
    item = []
    option = random.choice(
        ["Mutated animal", "Werewolf", "Dragon", "Cerberus", "Troll"]
    )
    score = 0  # Initialize score
    intro(item, option, score)
    field(item, option, score)


if __name__ == "__main__":
    play_game()
