import re

common_passwords = [
    '123456', 'password', '12345678', 'qwerty', '123456789', '12345', '1234', 
    '111111', '1234567', 'dragon', '123123', 'baseball', 'abc123', 'football',
    'monkey', 'letmein', 'shadow', 'master', '666666', 'qwertyuiop', '123321',
    'mustang', '1234567890', 'michael', '654321', 'superman', '1qaz2wsx', 
    '7777777', 'qazwsx', 'password1'
]

def password_strength(password):
    length = len(password)
    feedback = []

    if length < 8:
        feedback.append("Password is too short. Should be at least 8 characters.")
    elif length <= 12:
        feedback.append("Password length is decent but consider using more than 12 characters for better security.")
    else:
        feedback.append("Good length.")

    if not re.search(r"[A-Z]", password):
        feedback.append("Password should include at least one uppercase letter.")
    if not re.search(r"[a-z]", password):
        feedback.append("Password should include at least one lowercase letter.")
    if not re.search(r"[0-9]", password):
        feedback.append("Password should include at least one digit.")
    if not re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        feedback.append("Password should include at least one special character.")
    
    if password in common_passwords:
        feedback.append("Password is too common. Choose a more unique password.")

    strength_score = 0
    if length >= 8:
        strength_score += 1
    if length > 12:
        strength_score += 1
    if re.search(r"[A-Z]", password):
        strength_score += 1
    if re.search(r"[a-z]", password):
        strength_score += 1
    if re.search(r"[0-9]", password):
        strength_score += 1
    if re.search(r"[!@#$%^&*(),.?\":{}|<>]", password):
        strength_score += 1
    if password not in common_passwords:
        strength_score += 1

    if strength_score <= 2:
        feedback.append("Overall Password Strength: Weak")
    elif 3 <= strength_score <= 4:
        feedback.append("Overall Password Strength: Moderate")
    else:
        feedback.append("Overall Password Strength: Strong")
    
    return "\n".join(feedback)

password = input("Enter your password: ")
print(password_strength(password))
