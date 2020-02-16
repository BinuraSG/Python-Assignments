#### Binura Gunasekera
#### ITI 1120 [D]
#### 300021973
#### Assignment 3

import random
       
def shuffle_deck(deck):
    '''(list of str)->None
       Shuffles the given list of strings representing the playing deck    
    '''
    
    # YOUR CODE GOES HERE
    random.shuffle(deck)
    

def create_board(size):
    '''int->list of str
       Precondition: size is even positive integer between 2 and 52
       Returns a rigorous deck (i.e. board) of a given size.
    '''
    board = [None]*size 

    letter='A'
    for i in range(len(board)//2):
          board[i]=letter
          board[i+len(board)//2 ]=board[i]
          letter=chr(ord(letter)+1)
    shuffle_deck(board)
    return (board)
    



def print_board(a):
    '''(list of str)->None
       Prints the current board in a nicely formated way
    '''
    for i in range(len(a)):
        print('{0:4}'.format(a[i]), end=' ')
    print()
    for i in range(len(a)):
        print('{0:4}'.format(str(i+1)), end=' ')


def wait_for_player():
    '''()->None
    Pauses the program/game until the player presses enter
    '''
    input("\nPress enter to continue. ")
    print()

def print_revealed(discovered, p1, p2, original_board):
    '''(list of str, int, int, list of str)->None
    Prints the current board with the two new positions (p1 & p2) revealed from the original board
    Preconditions: p1 & p2 must be integers ranging from 1 to the length of the board 
    '''
    # YOUR CODE GOES HERE
    
    optimal=(len(original_board)//2)
    count=0
    while "*" in discovered:
        print_board(discovered)
        #NOTE: It wasn't required to put a while loop that promped the user to 're-input' values of p1 and p2, if they were out of range, and an error is normal
        print("\nPick two positions: i.e in the range of: [1:"+str(len(discovered))+"]")
        p1 = int(input("\nWhat is the first position you would like revealed? : "))-1
        p2 = int(input("What is the second position you would like revealed: "))-1
        print("\n")
        count+=1
        if p1!=p2 and discovered[p1]=='*' and discovered[p2]=='*':
            if original_board[p1] == original_board[p2]:
                    discovered[p1]=original_board[p2]
                    discovered[p2]=original_board[p2]
                    (print_board(discovered))
                    if original_board == discovered:
                        print ("\nYou took", count, "guesses which is", count-optimal, "guesses from the optimal amount.")
                    else:
                        wait_for_player()
                        print("\n"*25)
            elif original_board[p1]!=original_board[p2]:
                    discovered[p1]=original_board[p1]
                    discovered[p2]=original_board[p2]
                    (print_board(discovered))
                    discovered[p1]='*'
                    discovered[p2]='*'
                    wait_for_player()
                    print("\n"*25)
        #Condition for each possibility to give a unique message. Tells the user whether they put the same positions, or if the position they put was paired already (or both)           
        elif (p1 == p2) and (discovered[p1]=='*' and discovered[p2]=='*'):
            print ("You chose the same positions, please choose again. \n")
            count-=1
        elif (p1 == p2) and (discovered[p1]=='*' and discovered[p2]!='*'):
            print("You chose the same positions, and the position(s) you've chosen have been paired already. Please choose again\n :")
            count-=1
        elif (p1 == p2) and (discovered[p1]!='*' and discovered[p2]=='*'):
            print("You chose the same positions, and the position(s) you've chosen have been paired already. Please choose again\n :")
            count-=1
        elif (p1 == p2) and (discovered[p1]!='*' and discovered[p2]!='*'):
            print("You chose the same positions, and the position(s) you've chosen have been paired already. Please choose again\n :")
            count-=1
        else:
            print("The position(s) you have chosen have already been paired, this guess doesn't count!)")
            count-=1
    

#############################################################################
#   FUNCTIONS FOR OPTION 1 (with the board being read from a given file)    #
#############################################################################

def read_raw_board(file):
    '''str->list of str
    Returns a list of strings represeniting a deck of cards that was stored in a file. 
    The deck may not necessarifly be playable
    '''
    raw_board = open(file).read().splitlines()
    for i in range(len(raw_board)):
        raw_board[i]=raw_board[i].strip()
    return raw_board


def clean_up_board(l):
    '''list of str->list of str

    The functions takes as input a list of strings representing a deck of cards. 
    It returns a new list containing the same cards as l except that
    one of each cards that appears odd number of times in l is removed
    and all the cards with a * on their face sides are removed
    '''
    print("\nRemoving one of each cards that appears odd number of times and removing all stars ...\n")
    playable_board=[]

    # YOUR CODE GOES HERE
    
    while '*' in l:
        l.remove('*')
    for i in l:
        counter = l.count(i)
        if (counter%2 != 0):
            l[l.index(i)] = None
    while None in l:
        l.remove(None)
    return l
    
    
    return playable_board


def is_rigorous(l):
    '''list of str->True or None
    Returns True if every element in the list appears exactlly 2 times or the list is empty.
    Otherwise, it returns False.

    Precondition: Every element in the list appears even number of times
    '''

    # YOUR CODE GOES HERE
    if l ==[]:
        return True
    else:
        for i in l:
            counter = l.count(i)
            if counter != 2 :
                return False
    return True
 
                
        

####################################################################3

def play_game(board):
    '''(list of str)->None
    Plays a concentration game using the given board
    Precondition: board a list representing a playable deck
    '''
    print("\n"*25)
    print("Ready to play ...\n")
    
    st = star_board(board)

    # this is the funciton that plays the game
    # YOUR CODE GOES HERE
    while st!=board:
        p1 = 2 #non-global variables for p1 and p2 so that they aren't undefined in the function call below
        p2 = 3 #These are dummy variables with no real meaning, they are changed in print_revealed
        
        print_revealed(st,p1,p2,board)



#main
#Prints the border(s)
def ascii_name_plaque(name):
    j = len(name)
    border = '*' * (j+8)
    print(border)
    print("*" + " " *(j+6) + "*")
    print("*" + "___" +name + "___" +"*")
    print("*" + " " * (j+6) + "*")
    print(border)


    
# YOUR CODE TO GET A CHOICE 1 or CHOCE 2 from a player GOES HERE
"""
List of str --> List of str
Converts generated list into star list (*******)
"""
def star_board(star):
    board = [None] * len(star)
    for i in range(len(board)):
        board[i]='*'
    return board
"""
No parameters
Takes input from user and chooses whether to generate a rigorous deck, or read from a file
"""
#Uses while loops to make sure user inputs 1 or 2 (valid inputs)
def choice():
#Code for option 1
    n=int(input("Would you like (enter 1 or 2 to indicate your choice): \n (1) me to generate a rigorous deck of cards for you \n (2) or, would you like me to read a deck from a file? \n"))
    while n!=(1) and n!=(2):
        n=int(input("Sorry, that is not an acceptable input. Please pick between '1' or '2': \n"))
    if n==1:
        print("You chose to have a rigorous deck generated for you")
        print("\n")
        size=int(input("How many cards would you like to play with? Please choose an EVEN number (between 0 and 52) "))
        while (size %2 !=0) or (size<=0 or 52<size):
            size=int(input("How many cards would you like to play with? Please choose an EVEN number (between 0 and 52) "))
        if 0<size<=52:
            print("\nShuffling the deck ... ")
            wait_for_player()
            board=create_board(size)
            play_game(board)
            
#Code for option 2      
    elif n==2:
        print("You chose to read a deck from a file")
        print("\n")
        
        file=input('Enter the name of the file: ')
        file=file.strip()
        board = read_raw_board(file)
        board = clean_up_board(board)
        if is_rigorous(board)==False:
            ascii_name_plaque("The deck is now playable, is not rigorous, and contains: " + str(len(board))+ " cards")
        elif (is_rigorous(board)==True) and (len(board)==0):
            ascii_name_plaque("The deck is now playable, is rigorous, and contains: " +str(len(board))+ " cards")
            wait_for_player()
            print("\n"*25)
            print("\nShuffling the deck ... ")
            wait_for_player()
            print("\n"*25)
            print("The resulting board is empty. \nPlaying the Concentration game with an empty board is impossible.\nGood Bye!")
            return
            
        elif is_rigorous(board)==True:
            ascii_name_plaque("The deck is now playable, is rigorous, and contains: " + str(len(board)) + " cards")
        wait_for_player()
        play_game(board)
        
#Functions that are executed on IDLE start 
ascii_name_plaque("Welcome to the Concentration Game")
print("\n"*2)
choice()
# YOUR CODE FOR OPTION 1 GOES HERE

    

# In option 1 somewhere you need to and MUST have a call like this:
# board=create_board(size)

# YOUR CODE FOR OPTION 2 GOES HERE
# In option 2 somewhere you need to and MUST have the following 4 lines of code one after another
#
#print("You chose to load a deck of cards from a file")
#file=input("Enter the name of the file: ")
#file=file.strip()
#board=read_raw_board(file)
#board=clean_up_board(board)

