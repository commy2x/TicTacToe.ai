def play(board):
    """
    A simple rule-based Tic-Tac-Toe AI that plays 'o'.
    Input: board (list of 9 strings) — each is 'x', 'o', or ''.
    Output: integer index (0–8) where 'x' is first player and 'o' should play next.
    """

    # All possible winning lines
    wins = [
        [0,1,2], [3,4,5], [6,7,8],  # rows
        [0,3,6], [1,4,7], [2,5,8],  # columns
        [0,4,8], [2,4,6]            # diagonals
    ]

    # Helper function to find a move that completes or blocks a win
    def find_move(player):
        for line in wins:
            values = [board[i] for i in line]
            if values.count(player) == 2 and values.count('') == 1:
                return line[values.index('')]
        return None

    # 1. Win if possible
    move = find_move('x')
    if move is not None:
        return move

    # 2. Block opponent’s win
    move = find_move('o')
    if move is not None:
        return move

    # 3. Take center if free
    if board[4] == '':
        return 4

    # 4. Take a corner if free
    for i in [0, 2, 6, 8]:
        if board[i] == '':
            return i

    # 5. Take any free space
    for i in range(9):
        if board[i] == '':
            return i

    # No move possible (board full)
    return None


