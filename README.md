import random
def del_card():
    cards= [11 , 1 , 2 , 3 , 4 , 5 , 6 , 7, 8 , 9, 10 , 10, 10, 10]
    random_card= random.choice(cards)
    return random_card

def calculate_score(cards):
    if  sum(cards)==21 and len(cards)==2:
        return 0
    if 11 in cards and sum(cards) > 21:
        cards.remove(11)
        cards.append(1)
    return sum(cards)

def compare(user_score, computer_score):
    if user_score == computer_score:
        return "draw"
    elif computer_score== 0:
        return "lose, opponent has blackjack"
    elif user_score== 0:
        return "win with balckjack"
    elif user_score>21:
        return "you lose"
    elif computer_score>21:
        return "you win"
    elif user_score > computer_score:
        return "you win"    
    else:
        return "you lose"

def play_game():
    user_card= []
    computer_card= []
    computer_score= -1
    user_score=-1
    is_fame_over= False

    for _ in range(2):
        user_card.append(del_card())
        computer_card.append(del_card())
    while not is_game_over:   
        user_score= calculate_score(user_card)
        computer_score= calculate_score(computer_card)

        if user_score==0 or computer_score==0 or user_score>21:
            is_game_over=True
        else:
            user_should_deal= input("type 'y' to get another card , 'n' to pass ")
            if user_should_deal=="y":
                user_card.append(del_card())
            else:
                is_game_over = True

    while computer_score != 0 and computer_score< 17:
        computer_card.append(del_card())
        computer_score= calculate_score(computer_card)


    print(f"your final hand is {user_card} and final score is {user_score}")
    print(f"your final hand is {computer_card} and final score is {computer_score}")
    print(compare(user_score,computer_score)) 


while input("do you want to play again? type 'y' or 'n': ") == "y":
    print("\n"*100)
    play_game()
