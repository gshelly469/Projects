from a1_support import *

def display_game(game,grid_size):
    '''this is used to
    display the game'''

    line=('-'*(grid_size*4+4))
    print(' ',end=' ')
    for i in range(grid_size):
        if i<9:
            print('|',i+1,end=" ")
        else:
            print('|',i+1,end='')
    print("|")
    print(line)
    for j in range(grid_size):
        print(ALPHA[j],end=" ")
        for k in range(grid_size):
            print('|',game[j*grid_size+k],end=" ")
        print("|")
        print(line)

def parse_position(action,grid_size):
    '''this is parse
    function'''
    if (len(action)==2 and action[1].isnumeric()):
        if (ord('A')<=ord(action[0]) and ord(action[0])<=ord(ALPHA[grid_size-1]) and int(action[1])<=grid_size):
#            print('inside upper loop')
            a=ALPHA.index(action[0])
#            print('******',a)
            b=(a,int(action[1])-1)
            return b
        else:
            print(INVALID)
#            display_game(game,grid_size)
#            print('')
            return None

    elif (action[0]=='f' and action[1]==' ' and len(action)==4 and action[3].isnumeric()):
#        print('inside 1 loop')
        if (ord('A')<=ord(action[2]) and ord(action[2])<=ord(ALPHA[grid_size-1]) and int(action[3])<=grid_size):
#            print('inside 2 loop')
            c=ALPHA.index(action[2])
            d=(c,int(action[3])-1)
            return d
        else:
#            print(INVALID)
#            display_game(game,grid_size)
#            print('')
            return None

    else:
        print(INVALID)
#        display_game(game,grid_size)
#        print('')
        return None

def position_to_index(position,grid_size):
    '''this is position
    index'''
    return (position[0]*grid_size+position[1])

def replace_character_at_index(game,index,character):
    '''this is replace
    character function'''
    if game[index]=='~':
        g=game[:index]+character+game[index+1:]
        return g
    else:
        return None
#    print('*********',index,game[6])
#    print('game index',game[index],index,character,g)

def flag_cell(game,index):
    '''this is flag
    cell'''
    if (game[index] != FLAG and game[index]=='~'):
        h=game[:index]+FLAG+game[index+1:]
    elif game[index] == FLAG:
        h=game[:index]+'~'+game[index+1:]
    return h

def index_in_direction(index,grid_size,direction):
    '''this is direction
    index'''
#    print('########',index,direction)
    if ((direction=='right' or direction=='up-right' or direction=='down-right') and ((index+1)%grid_size)==0):
#        print(direction,index)
        return None
    if ((direction=='left' or direction=='up-left' or direction=='down-left') and ((index)%grid_size)==0):
#        print(direction,index)
        return None

    if (direction=='up'):
        index-=grid_size
    elif (direction=='down'):
        index+=grid_size
    elif (direction=='left'):
        index-=1
    elif (direction=='right'):
        index+=1
    elif (direction=='up-right'):
        index=index-grid_size+1
    elif (direction=='up-left'):
        index=index-grid_size-1
    elif (direction=='down-right'):
        index=index+grid_size+1
    elif (direction=='down-left'):
        index=index+grid_size-1

    if (index>=0 and index<grid_size*grid_size):
        return index
    else:
        return None

#    print('*******',index)
#    return index

def check_win(game, pokemon_locations):
    '''this is check 
    win'''
    var1=0
    for i in game:
        if (i==FLAG):
#            print('inside 1 loop',i)
            if game.index(i) in pokemon_locations:
                var1+=1
        elif (i==UNEXPOSED):
            return False
        else:
            pass
    if var1==len(pokemon_locations):
        return True
    else:
        return False

def number_at_cell(game,pokemon_locations,grid_size,index):
    '''this is number
    cell'''
    u=0
    p=neighbour_directions(index,grid_size)
    for i in p:
        if i in pokemon_locations:
            u+=1
#    print('This is the number of pokemon in neighbours',u)
    return u
    

    

def neighbour_directions(index,grid_size):
    '''this is neighbour
    function'''
    list1=[]
    for i in DIRECTIONS:
#        if ((i=='right' or i=='up-right' or i=='down-right') and ((index+1)%grid_size)==0):
#            print(i,index)
#            continue
#        if ((i=='left' or i=='up-left' or i=='down-left') and ((index)%grid_size)==0):
#            print(i,index)
#            continue
        x=index_in_direction(index,grid_size,i)
        if x is None:
            continue
        else:
            list1.append(x)
#        else:
#    print(list1)
    return list1


def main():
    '''this is main
    function'''
    print("Please input the size of the grid:",end=' ')
    grid_size=int(input())
#    if ( grid_size.isnumeric() and grid_size>=0 ):

    print("Please input the number of pokemons:",end=' ')
    number_of_pokemons=int(input())
    game=(UNEXPOSED*grid_size*grid_size)
    display_game(game,grid_size)
    print('')
    pokemon_locations=generate_pokemons(grid_size,number_of_pokemons)
    game_copy=game

    while(True):
        print('Please input action: ',end='')
        action=input()
        if (action=='q'):
            print('You sure about that buddy? (y/n):',end=' ')
            confirm_action=input()
            if confirm_action=='n':
                print("Let's keep going.")
                display_game(game,grid_size)
                print('')
            elif confirm_action=='y':
                print('Catch you on the flip side.')
                break
            else:
                print(INVALID)
                display_game(game,grid_size)
                print('')

        elif (action=='h'):
            print(HELP_TEXT)
            display_game(game,grid_size)
            print('')


        elif (action==':)'):
            print("It's rewind time.")
            game=game_copy
            pokemon_locations=generate_pokemons(grid_size,number_of_pokemons)
            display_game(game,grid_size)
            print('')


        else:
            if (len(action)==2 or len(action)==3):
                position=parse_position(action,grid_size)
                if position is None:
                    display_game(game,grid_size)
                    print('')
                    continue
                else:
                    index=position_to_index(position,grid_size)
                    if index in pokemon_locations:
                        for i in pokemon_locations:
                            game=replace_character_at_index(game, i, POKEMON)
    #                        print('showss',game)
                        display_game(game,grid_size)
                        print('You have scared away all the pokemons.')
                        break

                    exposed_cell_index=big_fun_search(game,grid_size,pokemon_locations,index)
                    exposed_cell_index.append(index)

                    for i in exposed_cell_index:
                        m=number_at_cell(game, pokemon_locations, grid_size, i)
                        temp=replace_character_at_index(game,i,str(m))
                        if temp is None:
#                            print('')
                            continue
                        else:
                            game=temp
#                print('this is game string',game)
            elif (len(action)==4 or len(action)==5):
                position=parse_position(action,grid_size)
                if position is None:
                    display_game(game,grid_size)
                    print('')
                    continue
                else:
                    index=position_to_index(position,grid_size)
                    game=flag_cell(game,index)

            else:
#                if action is None:
#                    continue
                print(INVALID)
                display_game(game,grid_size)
                print('')
                continue

            display_game(game,grid_size)

        
            bool1=check_win(game,pokemon_locations)
    #        print("this is bool",bool1)
            if bool1:
                print('You win.')
                break

            print('')




#########################UNCOMMENT THIS FUNCTION WHEN READY#######################
"""Searching adjacent cells to see if there are any Pokemon"s present.

 	Using some sick algorithms.

 	Find all cells which should be revealed when a cell is selected.

 	For cells which have a zero value (i.e. no neighbouring pokemons) all the cell"s
 	neighbours are revealed. If one of the neighbouring cells is also zero then
 	all of that cell"s neighbours are also revealed. This repeats until no
 	zero value neighbours exist.

 	For cells which have a non-zero value (i.e. cells with neightbour pokemons), only
 	the cell itself is revealed.

 	Parameters:
 		game (str): Game string.
 		grid_size (int): Size of game.
 		pokemon_locations (tuple<int, ...>): Tuple of all Pokemon's locations.
 		index (int): Index of the currently selected cell

 	Returns:
 		(list<int>): List of cells to turn visible.
"""
def big_fun_search(game, grid_size, pokemon_locations, index):
        '''this is big fun
        search'''
        queue = [index]
        discovered = [index]
        visible = []
        
#        print('*****',queue,discovered,visible)

        
        if game[index] == FLAG:
            return queue
        
        number = number_at_cell(game, pokemon_locations, grid_size, index)
        if number != 0:
#            print('+++++++',queue,index)
            return queue
        
        while queue:
            node = queue.pop()
#            print(node)
            
            for neighbour in neighbour_directions(node, grid_size):
                if neighbour in discovered or neighbour is None:
                    continue
                
                discovered.append(neighbour)
#                print('this is discovered neighbour 1::',discovered,neighbour)
                if game[neighbour] != FLAG:
                    number = number_at_cell(game, pokemon_locations, grid_size, neighbour)
#                    print('This is number at given index 2::',number,neighbour)
                    if number == 0:
                        queue.append(neighbour)
#                        print('This is updated queue 3::',queue)
                visible.append(neighbour)
#                print('This is updated visible 4::',visible)
        return visible
# #########################UNCOMMENT THIS FUNCTION WHEN READY#######################

if __name__ == "__main__":
    main()
