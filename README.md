import re
COMMON_PATTERNS = [
]

def check_common_patterns(password):
    
    return any(pattern in password.lower() for pattern in COMMON_PATTERNS)

def calculate_password_score(password):
    score = 0
    
    length = len(password)
    if length > 15:
        score += 3
    elif length >= 12:
        score += 2
    else:
        score -= 2

    if re.search(r'[A-Z]', password):
        score += 2

    if re.search(r'[a-z]', password):
        score += 2
        
    if re.search(r'[0-9]', password):
        score += 2

    if re.search(r'[@$!%*?&^#]', password):
        score += 3

    if check_common_patterns(password):
        score -= 5

    return score

def password_strength_feedback(score):
    if score >= 12:
        strength = "Strong"
    elif score >= 8:
        strength = "Moderate"
    else:
        strength = "Weak"
    
    return strength

def generate_improvement_suggestions(password):
    suggestions = []
    
    if len(password) < 12:
        suggestions.append("Password should be at least 12 characters long.")
    
    if not re.search(r'[A-Z]', password):
        suggestions.append("Include at least one uppercase letter.")
    
    if not re.search(r'[a-z]', password):
        suggestions.append("Include at least one lowercase letter.")
    
    if not re.search(r'[0-9]', password):
        suggestions.append("Include at least one number.")
    
    if not re.search(r'[@$!%*?&^#]', password):
        suggestions.append("Include at least one special character (e.g., @$!%*?&^#).")
    
    if check_common_patterns(password):
        suggestions.append("Avoid using common patterns or dictionary words.")
    
    return suggestions

def main():
 
    password = input("Enter your password: ")

    score = calculate_password_score(password)
    
    strength = password_strength_feedback(score)

    suggestions = generate_improvement_suggestions(password)

    print(f"\nPassword Strength: {strength} (Score: {score})")

    if strength == "Weak":
        print("\nSuggestions for improvement:")
        for suggestion in suggestions:
            print(f"- {suggestion}")
    elif strength == "Moderate":
        print("\nSuggestions for improvement:")
        for suggestion in suggestions:
            print(f"- {suggestion}")
    else:
        print("\nYour password is strong!")

if __name__ == "__main__":
    main()
