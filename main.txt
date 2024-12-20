# main.py

import re

def analyze_password_strength(password):
    score = 0
    feedback = []

    # Check password length
    if len(password) >= 12:
        score += 2
    elif len(password) >= 8:
        score += 1
    else:
        feedback.append("Increase password length to at least 8 characters.")

    # Check for uppercase letters
    if re.search(r'[A-Z]', password):
        score += 1
    else:
        feedback.append("Add at least one uppercase letter.")

    # Check for lowercase letters
    if re.search(r'[a-z]', password):
        score += 1
    else:
        feedback.append("Add at least one lowercase letter.")

    # Check for digits
    if re.search(r'[0-9]', password):
        score += 1
    else:
        feedback.append("Include at least one numeric digit.")

    # Check for special characters
    if re.search(r'[\W_]', password):
        score += 1
    else:
        feedback.append("Use special characters like @, #, $, etc.")

    # Avoid common passwords
    common_passwords = ["password", "123456", "qwerty", "12345678"]
    if password.lower() in common_passwords:
        feedback.append("Avoid using common passwords like 'password' or '123456'.")

    # Strength rating
    if score >= 6:
        strength = "Very Strong"
    elif score >= 4:
        strength = "Strong"
    elif score >= 2:
        strength = "Fair"
    else:
        strength = "Weak"

    return strength, feedback

# Example usage
if __name__ == "__main__":
    user_password = input("Enter a password to check its strength: ")
    strength, suggestions = analyze_password_strength(user_password)
    print(f"Password Strength: {strength}")
    if suggestions:
        print("Suggestions to improve your password:")
        for suggestion in suggestions:
            print(f"- {suggestion}")
