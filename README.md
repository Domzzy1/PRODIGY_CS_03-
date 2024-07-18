Password Complexity Analyzer
Overview

Welcome to the Password Complexity Analyzer, a tool designed to help users understand the strength of their passwords and how long it would take to crack them. This application is part of my cybersecurity internship project at Prodigy Info Tech.
Features

    Real-time Password Analysis: The application evaluates password strength based on length, complexity, and character diversity.
    Time to Crack Estimate: It calculates the approximate time required to crack the password using different attack scenarios.
    User-Friendly Interface: Developed with tkinter and enhanced with ttkthemes for an intuitive and visually appealing user experience.

Installation

To get started with the Password Complexity Analyzer, follow these steps:

    Clone the Repository:

    bash

git clone https://github.com/<your-github-username>/PasswordComplexityAnalyzer.git
cd PasswordComplexityAnalyzer

Install the Required Packages:
Make sure you have pip installed. Then, run:

bash

pip install pillow ttkthemes

Run the Application:

bash

    python password_analyzer.py

Code Explanation

The main script, password_analyzer.py, is structured as follows:
Importing Libraries

python

import tkinter as tk
from tkinter import ttk
from ttkthemes import ThemedStyle
from PIL import Image, ImageTk

Password Analysis Function

python

def analyze_password(password):
    length = len(password)
    complexity = 0
    if any(char.isdigit() for char in password):
        complexity += 1
    if any(char.islower() for char in password):
        complexity += 1
    if any(char.isupper() for char in password):
        complexity += 1
    if any(char in "!@#$%^&*()_+" for char in password):
        complexity += 1

    if complexity == 1:
        time_to_crack = "Seconds"
    elif complexity == 2:
        time_to_crack = "Minutes"
    elif complexity == 3:
        time_to_crack = "Hours"
    elif complexity == 4:
        time_to_crack = "Years"
    else:
        time_to_crack = "Instantly"

    return complexity, time_to_crack

Setting Up the GUI

python

root = tk.Tk()
root.title("Password Complexity Analyzer")

style = ThemedStyle(root)
style.set_theme("arc")

mainframe = ttk.Frame(root, padding="10 10 10 10")
mainframe.grid(column=0, row=0, sticky=(tk.W, tk.E, tk.N, tk.S))

password_label = ttk.Label(mainframe, text="Enter Password:")
password_label.grid(column=1, row=1, sticky=tk.W)
password = tk.StringVar()
password_entry = ttk.Entry(mainframe, width=25, textvariable=password, show="*")
password_entry.grid(column=2, row=1, sticky=(tk.W, tk.E))

Function to Update Analysis

python

def update_analysis(*args):
    password_str = password.get()
    complexity, time_to_crack = analyze_password(password_str)
    complexity_label.config(text=f"Complexity: {complexity}/4")
    time_label.config(text=f"Time to Crack: {time_to_crack}")

analyze_button = ttk.Button(mainframe, text="Analyze", command=update_analysis)
analyze_button.grid(column=2, row=2, sticky=tk.W)

Displaying the Analysis Results

python

complexity_label = ttk.Label(mainframe, text="Complexity: ")
complexity_label.grid(column=1, row=3, sticky=tk.W)
time_label = ttk.Label(mainframe, text="Time to Crack: ")
time_label.grid(column=2, row=3, sticky=tk.W)

Running the Application

python

root.mainloop()

Future Enhancements

    Enhanced Password Metrics: Adding more detailed metrics and suggestions for improving password strength.
    Database Integration: Storing analyzed passwords and their metrics in a database for future reference.
    Security Features: Implementing additional security features to safeguard the application and user data.

Contribution

Contributions are welcome! If you have suggestions for improving the tool or want to report a bug, please open an issue or submit a pull request.
License

This project is licensed under the MIT License - see the LICENSE file for details.
