# PRODIGY-_ANDROIDDEVELOPMENT_04
from tkinter import *
from tkinter import messagebox
root = Tk()
root.title("Tic Tac Toe")
current_player = "X"
board = [""] * 9
buttons = []
def check_winner():
 winning_positions = [
 (0,1,2), (3,4,5), (6,7,8),
 (0,3,6), (1,4,7), (2,5,8),
 (0,4,8), (2,4,6)
 ]
 for a, b, c in winning_positions:
 if board[a] == board[b] == board[c] != "":
 return board[a]
 if "" not in board:
 return "Tie"
 return None
def button_click(index):
 global current_player
 if board[index] == "":
 board[index] = current_player
 buttons[index]["text"] = current_player
 winner = check_winner()
 if winner:
 if winner == "Tie":
 messagebox.showinfo("Game Over", "It's a Tie!")
 else:
 messagebox.showinfo("Game Over", f"Player {winner} wins!")
 reset_game()
 else:
 current_player = "O" if current_player == "X" else "X"
def reset_game():
 global current_player, board
 current_player = "X"
 board = [""] * 9
 for button in buttons:
 button["text"] = ""
for i in range(9):
 button = Button(root, text="", width=10, height=4,
 font=("Arial", 20),
 command=lambda i=i: button_click(i))
 button.grid(row=i//3, column=i%3)
 buttons.append(button)
reset_button = Button(root, text="Reset Game",
 font=("Arial", 14),
 command=reset_game)
reset_button.grid(row=3, column=0, columnspan=3, sticky="we")
root.mainloop()
