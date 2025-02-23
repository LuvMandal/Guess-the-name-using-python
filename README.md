# Guess-the-name-using-python
import tkinter as tk
import random

# Function to start a new game
def new_game():
    global secret_number, attempts
    secret_number = random.randint(1, 10)
    attempts = 0
    result_label.config(text="Guess a number!", fg="black")
    guess_button.config(state="normal")
    entry.delete(0, tk.END)

# Function to check the guess
def check_guess():
    global attempts
    attempts += 1
    try:
        guess = int(entry.get())
        if guess < secret_number:
            result_label.config(text="Too low! Try again.", fg="red")
        elif guess > secret_number:
            result_label.config(text="Too high! Try again.", fg="red")
        else:
            result_label.config(text=f"Correct! You guessed it in {attempts} tries!", fg="green")
            guess_button.config(state="disabled")  
    except ValueError:
        result_label.config(text="Enter a valid number!", fg="red")

# Initialize game
root = tk.Tk()
root.title(" Guess the Number Game ")
root.geometry("400x300")
root.configure(bg="#2E4053")  

# UI Elements
title_label = tk.Label(root, text="Guess a number (1-10)", font=("Arial", 16, "bold"), bg="#2E4053", fg="white")
title_label.pack(pady=15)

entry = tk.Entry(root, font=("Arial", 14), width=5, justify="center")
entry.pack(pady=5)

guess_button = tk.Button(root, text="Guess", command=check_guess, font=("Arial", 12, "bold"), bg="#3498DB", fg="white", padx=10, pady=5)
guess_button.pack(pady=10)

result_label = tk.Label(root, text="Start guessing!", font=("Arial", 12, "italic"), bg="#2E4053", fg="white")
result_label.pack()

reset_button = tk.Button(root, text="Play Again", command=new_game, font=("Arial", 12, "bold"), bg="#E74C3C", fg="white", padx=10, pady=5)
reset_button.pack(pady=10)

# Start the first game
new_game()
root.mainloop()


