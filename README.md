import tkinter as tk
import random
import string

def generate_password():
    length = int(length_entry.get())
    characters = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(random.choice(characters) for _ in range(length))
    result_label.config(text=f"Password: {password}")

# GUI Design
root = tk.Tk()
root.title("Password Generator")
root.geometry("300x200")
root.config(bg="lightblue")

tk.Label(root, text="Enter Length:", bg="lightblue", font=("Arial", 12)).pack(pady=5)
length_entry = tk.Entry(root)
length_entry.pack()

tk.Button(root, text="Generate", command=generate_password).pack(pady=10)
result_label = tk.Label(root, text="", bg="lightblue", font=("Arial", 12, "bold"))
result_label.pack()

root.mainloop()
