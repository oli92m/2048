import random
import copy

board = [[0 for _ in range(4)] for _ in range(4)]
possible_spawn = [2 for _ in range(9)] + [4]

first_rows = [0, 0]
first_cols = [0, 0]

while first_rows[0] == first_rows[1] and first_cols[0] == first_cols[1]:
    first_rows = [random.randrange(0, 4), random.randrange(0, 4)]
    first_cols = [random.randrange(0, 4), random.randrange(0, 4)]

board[first_rows[0]][first_cols[0]] = random.choice(possible_spawn)
board[first_rows[1]][first_cols[1]] = random.choice(possible_spawn)


def setup_movement_keys():
    up_key = input('Wich key to move up? ')
    down_key = input('Wich key to move down? ')
    left_key = input('Wich key to move left? ')
    right_key = input('Wich key to move right? ')
    return [up_key, down_key, left_key, right_key]


keys = setup_movement_keys()


def move_left(board):
    for i in range(4):
        for j in range(3):
            if board[i][j] == 0:
                board[i][j] = board[i][j+1]
                board[i][j + 1] = 0
    return board


def move_right(board):
    for i in range(4):
        for j in range(3):
            if board[i][j+1] == 0:
                board[i][j+1] = board[i][j]
                board[i][j] = 0
    return board


def move_up(board):
    for i in range(3):
        for j in range(4):
            if board[i][j] == 0:
                board[i][j] = board[i+1][j]
                board[i+1][j] = 0
    return board


def move_down(board):
    for i in range(3):
        for j in range(4):
            if board[i+1][j] == 0:
                board[i+1][j] = board[i][j]
                board[i][j] = 0
    return board


def left_sum(board):
    for i in range(4):
        for j in range(3):
            if board[i][j] == board[i][j + 1]:
                board[i][j] = board[i][j] * 2
                board[i][j + 1] = 0
    return board


def right_sum(board):
    for i in range(4):
        for j in range(3, 0, -1):
            if board[i][j] == board[i][j-1]:
                board[i][j] = board[i][j] * 2
                board[i][j-1] = 0
    return board


def up_sum(board):
    for i in range(3):
        for j in range(4):
            if board[i][j] == board[i+1][j]:
                board[i][j] = board[i][j] * 2
                board[i+1][j] = 0
    return board


def down_sum(board):
    for i in range(3, 0, -1):
        for j in range(4):
            if board[i][j] == board[i-1][j]:
                board[i][j] = board[i][j] * 2
                board[i-1][j] = 0
    return board


def update(board, keys):
    move = input()
    previous_board = copy.deepcopy(board)

    if move == keys[0]:
        for k in range(4):
            move_up(board)
        up_sum(board)
        move_up(board)

    elif move == keys[1]:
        for j in range(4):
            if board[1][j] == board[2][j] == board[3][j] and board[1][j] != 0:
                board[1][j] = board[0][j]
                board[0][j] = 0
                board[2][j] = board[2][j]
                board[3][j] = 2*board[3][j]
        for k in range(4):
            move_down(board)
        down_sum(board)
        move_down(board)

    elif move == keys[2]:
        for k in range(4):
            move_left(board)
        left_sum(board)
        move_left(board)

    elif move == keys[3]:
        for i in range(4):
            if board[i][1] == board[i][2] == board[i][3] and board[i][1] != 0:
                board[i] = [0, board[i][0], board[i][1], 2*board[i][2]]
        for k in range(4):
            move_right(board)
        right_sum(board)
        move_right(board)

    if previous_board == board:
        print('invalid move')
        print('')
    else:
        empty_tiles = []
        for i in range(4):
            for j in range(4):
                if board[i][j] == 0:
                    empty_tiles.append([i, j])
        selected_tiles = random.choice(empty_tiles)
        board[selected_tiles[0]][selected_tiles[1]] = random.choice(possible_spawn)

    return board


def show(board):
    show_board = copy.deepcopy(board)
    for i in range(4):
        for j in range(4):
            if show_board[i][j] == 0:
                show_board[i][j] = '.'
    for i in range(4):
        print(''.join(' ' * (4 - len(str(digit))) + str(digit) + ' ' for digit in show_board[i]))
        print('')


def check_defeat(board):
    game_lost = True
    for i in range(4):
        for j in range(4):
            if board[i][j] == 0:
                game_lost = False
            if j < 3:
                if board[i][j] == board[i][j+1]:
                    game_lost = False
            if i < 3:
                if board[i][j] == board[i + 1][j]:
                    game_lost = False
    return game_lost


def check_win(board):
    game_won = False
    for i in range(4):
        for j in range(4):
            if board[i][j] == 2048:
                game_won = True
    return game_won


def main(board, keys):
    win = False
    show(board)

    while not win:
        update(board, keys)
        show(board)
        game_lost = check_defeat(board)
        game_won = check_win(board)
        if game_lost:
            print('Game Over!')
            break
        if game_won:
            print('You won!')
            break


main(board, keys)
