import random
import string
import datetime

def get_user_options():
    print("\n------ PASSWORD GENERATOR OPTIONS ------")
    length = int(input("Enter desired password length: "))
    use_letters = input("Include letters (y/n): ").lower() == 'y'
    use_digits = input("Include digits (y/n): ").lower() == 'y'
    use_symbols = input("Include symbols (y/n): ").lower() == 'y'
    count = int(input("How many passwords to generate: "))

    return length, use_letters, use_digits, use_symbols, count

def build_character_pool(letters, digits, symbols):
    pool = ""
    if letters:
        pool += string.ascii_letters
    if digits:
        pool += string.digits
    if symbols:
        pool += string.punctuation
    return pool

def generate_password(length, pool):
    if not pool:
        return "No characters selected!"
    return ''.join(random.choice(pool) for _ in range(length))

def save_passwords(password_list):
    file_name = "saved_passwords.txt"
    with open(file_name, "a") as file:
        file.write("\n--- Generated on " + str(datetime.datetime.now()) + " ---\n")
        for pw in password_list:
            file.write(pw + "\n")
    print(f"✅ {len(password_list)} password(s) saved to '{file_name}'.")

def main():
    try:
        length, use_letters, use_digits, use_symbols, count = get_user_options()
        if length <= 0 or count <= 0:
            print("Length and count must be positive integers.")
            return

        character_pool = build_character_pool(use_letters, use_digits, use_symbols)
        password_list = []

        for i in range(count):
            pw = generate_password(length, character_pool)
            print(f"Password {i+1}: {pw}")
            password_list.append(pw)

        save_choice = input("Do you want to save the passwords? (y/n): ").lower()
        if save_choice == 'y':
            save_passwords(password_list)
        else:
            print("Passwords not saved.")

    except ValueError:
        print("Please enter valid numbers for length and count.")

if __name__ == "__main__":
    main()
