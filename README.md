# Fantasy-number-game
A colourful fantasy style number game
import tkinter as tk
import random

# Setup
root = tk.Tk()
root.title("🔮 Fantasy Guess Game")
root.geometry("360x500")
root.resizable(False, False)

# Animated pastel background
colors = ["#E0BBE4", "#957DAD", "#D291BC", "#FEC8D8", "#FFDFD3"]
color_index = 0

def pulse_background():
    global color_index
    root.configure(bg=colors[color_index])
    title.config(bg=colors[color_index])
    result.config(bg=colors[color_index])
    guess_count_label.config(bg=colors[color_index])
    color_index = (color_index + 1) % len(colors)
    root.after(700, pulse_background)

# Game logic
secret = random.randint(1, 100)
guess_count = 0

def check_guess():
    global guess_count
    user_input = entry.get()
    if not user_input.isdigit():
        result.config(text="❗ Please enter a number!", fg="red")
        return

    guess = int(user_input)
    guess_count += 1
    guess_count_label.config(text=f"✨ Guesses: {guess_count}")

    if guess == secret:
        result.config(text=f"🎉 Correct! It was {secret}!", fg="green")
        guess_btn.config(text="🔁 Play Again", command=restart_game)
    elif guess < secret:
        result.config(text="📉 Too low!", fg="#3333ff")
    else:
        result.config(text="📈 Too high!", fg="#800080")

def restart_game():
    global secret, guess_count
    secret = random.randint(1, 100)
    guess_count = 0
    result.config(text="")
    guess_count_label.config(text="✨ Guesses: 0")
    entry.delete(0, tk.END)
    guess_btn.config(text="Guess!", command=check_guess)

# Fonts
font_title = ("Comic Sans MS", 18, "bold")
font_label = ("Helvetica", 12)
font_btn = ("Arial", 11, "bold")

# UI Widgets
title = tk.Label(root, text="🔮 Guess the Number (1–100)", font=font_title, bg=colors[0])
title.pack(pady=20)

entry = tk.Entry(root, font=font_label, justify="center")
entry.pack(pady=10, ipadx=10, ipady=5)

guess_btn = tk.Button(root, text="Guess!", font=font_btn, bg="#957DAD", fg="white", command=check_guess)
guess_btn.pack(pady=10)

result = tk.Label(root, text="", font=font_label, bg=colors[0])
result.pack(pady=10)

guess_count_label = tk.Label(root, text="✨ Guesses: 0", font=font_label, bg=colors[0])
guess_count_label.pack(pady=5)

# Start background animation
pulse_background()

# Start GUI loop
root.mainloop()
