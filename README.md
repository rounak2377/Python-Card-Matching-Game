# Python-Card-Matching-Game
Created by Rounak Kumar Gupta, Mechanical Engineering student at Veer Surendra Sai University of Technology (VSSUT), Burla
[card_matching_game.py](https://github.com/user-attachments/files/23577932/card_matching_game.py)
import tkinter as tk
import random
from tkinter import messagebox

# Create main window
root = tk.Tk()
root.title("Card Matching Game")

# Prepare cards
symbols = list('AABBCCDDEEFFGGHH') # For 4x4 grid
random.shuffle(symbols)
buttons = []
flipped = []
matched = []

def on_click(i):
    if i in matched or i in flipped:
        return
    buttons[i]['text'] = symbols[i]
    flipped.append(i)
    if len(flipped) == 2:
        root.after(500, check_match)

def check_match():
    i, j = flipped
    if symbols[i] == symbols[j]:
        matched.extend([i, j])
        if len(matched) == len(symbols):
            messagebox.showinfo("Congratulations!", "You matched all pairs!")
    else:
        buttons[i]['text'] = ""
        buttons[j]['text'] = ""
    flipped.clear()

# Create grid of buttons
for i in range(len(symbols)):
    btn = tk.Button(root, text="", width=8, height=4,
                    command=lambda i=i: on_click(i))
    btn.grid(row=i // 4, column=i % 4)
    buttons.append(btn)

root.mainloop()
