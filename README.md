import tkinter as tk
import os
from recovery import * 

def show_files():
    path='/home/ramin/Desktop/'
    disk = entry_disk.get()
    folder = entry_folder.get()  # Get the folder name from the input field
    extensions = entry_extensions.get()  # Get the file extensions from the input field
    
    folder_path = path+folder

    isExist = os.path.exists(folder_path)
    if not isExist:
         os.makedirs(folder_path)


    args1 = {
        'disk': disk,
        'outdir': None,
        'pattern': None,
        'cluster_size': None,
        'sector_size': None,
        'mft': None,
        'save_mft': 'mft'
    }
    rec_from_file(**args1)
    args2 = {
        'disk': disk,
        'outdir': folder_path,
        'pattern':'*.'+extensions,
        'cluster_size': None,
        'sector_size': None,
        'mft': 1,
        'save_mft': None
    }
    rec_from_file(**args2)



    file_list = []
    for file in os.listdir(folder_path):
        if file.endswith(tuple(extensions)):
            file_list.append(file)

    # Clear the text widget
    text.delete(1.0, tk.END)

    # Display the files in the text widget
    for file in file_list:
        text.insert(tk.END, file + '\n')

# Create the main window
window = tk.Tk()
window.title("File Viewer")
window.geometry("400x300")  # Set the window size

# Center the window on the screen
window.eval('tk::PlaceWindow . center')

# Set the background color
# Set the background color
window.configure(background="#f0f0f0")


# Create the input field for the disk name
label_disk = tk.Label(window, text="Disk Name:", font=("Arial", 12))
label_disk.pack(pady=5)

entry_disk = tk.Entry(window, font=("Arial", 12), bg="#f8f8f8", fg="#333333", bd=1, relief=tk.SOLID)
entry_disk.pack(pady=5)



# Create the input field for the folder name
label_folder = tk.Label(window, text="Folder Name:", font=("Arial", 12))
label_folder.pack(pady=5)

entry_folder = tk.Entry(window, font=("Arial", 12), bg="#f8f8f8", fg="#333333", bd=1, relief=tk.SOLID)
entry_folder.pack(pady=5)

# Create the input field for the file extensions
label_extensions = tk.Label(window, text="File Extensions (comma-separated):", font=("Arial", 12))
label_extensions.pack(pady=5)

entry_extensions = tk.Entry(window, font=("Arial", 12), bg="#f8f8f8", fg="#333333", bd=1, relief=tk.SOLID)
entry_extensions.pack(pady=5)
# Create a button to show the files
button = tk.Button(window, text="Show Files", command=show_files)
button.pack(pady=10)

# Create a text widget to display the files
text = tk.Text(window)
text.pack()

# Start the main event loop
window.mainloop()
