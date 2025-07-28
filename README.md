# Password-Checker
A simple Python password strength checker
# Simple Password Strength Checker using SHA-512
# Author: [Your Name]
# This script reads usernames and passwords from a file,
# hashes the passwords, and checks how strong they are.

import hashlib  # Used for hashing passwords

# Function to check the strength of a given password
def check_strength(p):
    # Add 1 point for each condition the password meets
    score = sum([
        len(p) >= 8,                      # Is at least 8 characters long
        any(c.isupper() for c in p),     # Contains uppercase letters
        any(c.islower() for c in p),     # Contains lowercase letters
        any(c.isdigit() for c in p),     # Contains numbers
        any(not c.isalnum() for c in p)  # Contains special characters
    ])
    
    # Return strength rating based on the total score
    # score 0–1 = Weak, 2–3 = Moderate, 4–5 = Very Strong
    return ["Weak", "Moderate", "Very Strong"][score // 2]

# Open the file containing usernames and passwords
with open("users.txt") as f:
    for line in f:
        # Split each line into username and password
        u, p = line.strip().split(":")

        # Print the username
        print(f"User: {u}")

        # Print the SHA-512 hashed version of the password
        print(f"Hash: {hashlib.sha512(p.encode()).hexdigest()}")

        # Print the password strength rating
        print(f"Strength: {check_strength(p)}\n")
