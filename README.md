# hh
hh
import tkinter as tk
import os
from ntfsrecover import *

def show_directory_files():
    directory = entry.get()  # Get the directory path from the entry widget
    files = os.listdir(directory)  # Get the list of files in the directory

    # Clear the text widget
    text.delete(1.0, tk.END)
    result = ramin()
    print(result)

    # Display the files in the text widget
    for file in files:
        text.insert(tk.END, file + '\n')

# Create the main window
window = tk.Tk()
window.title("Directory Files Viewer")

# Create an entry widget to get the directory path
entry = tk.Entry(window)
entry.pack()

# Create a button to trigger the file display
button = tk.Button(window, text="Show Directory Files", command=show_directory_files)
button.pack()

# Create a text widget to display the files
text = tk.Text(window)
text.pack()

# Start the main event loop
window.mainloop()

