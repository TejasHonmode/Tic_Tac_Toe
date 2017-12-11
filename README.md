# Tic_Tac_Toe
tic tac toe using python

from IPython.display import clear_output
from __future__ import print_function

def displayboard(board):
    
    clear_output()
    print('    |    |    ')
    print('  '+board[7]+' | '+board[8]+'  | '+board[9]+'')
    print('--------------')
    print('    |    |    ')
    print('  '+board[4]+' | '+board[5]+'  | '+board[6]+'')
    print('--------------')
    print('    |    |    ')
    print('  '+board[1]+' | '+board[2]+'  | '+board[3]+'')
    
    
def playerinput():
    
    marker=''
    while not(marker=='O' or marker=='X'):
        marker=raw_input('Do you want x or o?').upper()
        
    if marker=='X':
        return('X','O')
    else:
        return('O','X')
        
    
def placemarker(board,marker,position):
    
    board[position]=marker
    
    
def wincheck(board,mark):
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or # across the top
    (board[4] == mark and board[5] == mark and board[6] == mark) or # across the middle
    (board[1] == mark and board[2] == mark and board[3] == mark) or # across the bottom
    (board[7] == mark and board[4] == mark and board[1] == mark) or # down the middle
    (board[8] == mark and board[5] == mark and board[2] == mark) or # down the middle
    (board[9] == mark and board[6] == mark and board[3] == mark) or # down the right side
    (board[7] == mark and board[5] == mark and board[3] == mark) or # diagonal
    (board[9] == mark and board[5] == mark and board[1] == mark)) # diagonal
    
    
import random
def choosefirst():
    if random.randint(0,1)==0:
        return 'Player 1'
    else:
        return 'Player 2'
    
    
def spacecheck(board,position):
    
    return board[position]==' '
    
    
def full_board_check(board):
    
    for i in range(1,10):
        if space_check(board,i):
            return False
    return True
    
    
def playerchoice(board):
    
    position=' '
    while position not in '1 2 3 4 5 6 7 8 9'.split() or not spacecheck(board,int(position)):
        position= raw_input('Choose your next position:(1-9) ')
        
    return int(position)
    
    
def replay():
    
    return raw_input('Do you want to play again?Enter yes or no').lower().startswith('y')
    
    
print('Welcome to Tic Tac Toe!')

while True:
    
    theboard=[' ']*10
    player1_marker,player2_marker=playerinput()
    turn=choosefirst()
    print(turn+ 'will go first')
    
    game_on=True
    
    while game_on:
        if turn=='Player 1':
            
            displayboard(theboard)
            position=playerchoice(theboard)
            placemarker(theboard,player1_marker,position)
            
            if wincheck(theboard,player1_marker):
                displayboard(theboard)
                print('Congratulations, Player 1, has won the game!')
                game_on=False
            else:
                if full_board_check(theboard):
                    display_board(theboard)
                    print('The game is draw')
                    break
                else:
                    turn='Player 2'
                    
        else:
            #Player 2
            displayboard(theboard)
            position=playerchoice(theboard)
            placemarker(theboard,player2_marker,position)
            
            
            if wincheck(theboard,player2_marker):
                displayboard(theboard)
                print('Congratulations, Player 2, has won the game!')
                game_on=False
            else:
                if full_board_check(theboard):
                    display_board(theboard)
                    print('The game is draw')
                    break
                else:
                    turn='Player 1'
            
    if not replay():
        break
