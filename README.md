Project Idea: File Integrity Checker

Objective: This tool will allow you to upload a file and check its integrity by computing and comparing its hash value (e.g., SHA-256). It can help detect unauthorized changes or corruption in files.

Key Features:
Calculate and store file hash: The program will compute the hash of a file (using SHA-256) when it’s first uploaded.
Verify integrity: The program will compute the hash of a file and compare it to the stored hash to check if the file has been modified.
Simple command-line interface (CLI): The user will provide a file and select whether they want to compute the hash or verify the file’s integrity.

**Step 1: Create the Script**
Python Code for File Integrity Checker

import hashlib
import os

def calculate_hash(file_path):
    """Calculate the SHA-256 hash of a file."""
    hash_sha256 = hashlib.sha256()
    with open(file_path, 'rb') as file:
        while chunk := file.read(4096):
            hash_sha256.update(chunk)
    return hash_sha256.hexdigest()

def check_integrity(original_hash, file_path):
    """Check if the file's hash matches the original hash."""
    new_hash = calculate_hash(file_path)
    if new_hash == original_hash:
        print("File integrity is intact.")
    else:
        print("File has been modified or corrupted.")

def main():
    print("File Integrity Checker")
    print("1. Calculate Hash of a file")
    print("2. Verify Integrity of a file")
    choice = input("Choose an option (1/2): ")

    if choice == '1':
        file_path = input("Enter the path of the file to calculate hash: ")
        if os.path.exists(file_path):
            hash_value = calculate_hash(file_path)
            print(f"SHA-256 hash of the file: {hash_value}")
            with open('file_hash.txt', 'w') as f:
                f.write(hash_value)
            print("Hash saved to 'file_hash.txt'.")
        else:
            print("File not found.")
    
    elif choice == '2':
        file_path = input("Enter the path of the file to verify: ")
        if os.path.exists(file_path):
            if os.path.exists('file_hash.txt'):
                with open('file_hash.txt', 'r') as f:
                    original_hash = f.read().strip()
                check_integrity(original_hash, file_path)
            else:
                print("No stored hash found. Please calculate the hash first.")
        else:
            print("File not found.")
    else:
        print("Invalid choice. Exiting.")

if __name__ == '__main__':
    main()

**Explanation:**
1. calculate_hash(file_path): This function calculates the SHA-256 hash of the file.
2. check_integrity(original_hash, file_path): This function compares the hash of the current file with the stored hash to check if the file has been altered.

3. Main CLI Interface:
Users can choose to either calculate the hash of a file or verify its integrity.
If they calculate the hash, it is saved to a text file (file_hash.txt).
If they verify integrity, it compares the file’s current hash with the one saved in file_hash.txt.

**Step 2: Save the Script and Create GitHub Repository**
1. Save the Python script as file_integrity_checker.py (or any name you prefer).

2. Initialize Git and create a new repository on GitHub:
git init
git add file_integrity_checker.py
git commit -m "Initial commit of File Integrity Checker"

3. Push to GitHub:
Create a new repository on GitHub.
Follow the instructions GitHub provides to push your local repository to
GitHub:
git remote add origin <your-repository-URL>
git push -u origin master

**Step 3: How to Run the Script**
Once the script is uploaded to GitHub, you can run it via the command line by following these steps:

1. Download the script or clone the repository:
git clone <repository-URL>
cd <repository-folder>

2. Run the script:
python file_integrity_checker.py

3. Follow the on-screen prompts to either calculate the hash of a file or verify its integrity.

**Example Usage**
Option 1: Calculate File Hash
Choose an option (1/2): 1
Enter the path of the file to calculate hash: example.txt
SHA-256 hash of the file: <hash_value>
Hash saved to 'file_hash.txt'.

Option 2: Verify File Integrity
Choose an option (1/2): 2
Enter the path of the file to verify: example.txt
File integrity is intact.

Step 4: Upload and Document on GitHub
Add a README.md file with:
A description of the project.
How to install and run the script.

**Example usage.**
Upload the file_integrity_checker.py and README.md to GitHub.
