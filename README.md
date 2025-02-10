# Farhan
Bin to CC 
import random

# Luhn Algorithm for validation
def luhn_check(card_number):
    digits = [int(d) for d in str(card_number)]
    checksum = 0
    reverse = digits[::-1]
    
    for i, digit in enumerate(reverse):
        if i % 2 == 1:
            digit *= 2
            if digit > 9:
                digit -= 9
        checksum += digit
    
    return checksum % 10 == 0

# Generate a valid CC number from a BIN
def generate_cc(bin_format):
    while True:
        cc_number = ''
        for char in bin_format:
            if char == 'x':
                cc_number += str(random.randint(0, 9))
            else:
                cc_number += char

        if luhn_check(cc_number):
            return cc_number

# Generate random CVV and Expiry Date
def generate_cvv():
    return str(random.randint(100, 999))

def generate_expiry():
    month = str(random.randint(1, 12)).zfill(2)
    year = str(random.randint(25, 30))
    return f"{month}/{year}"

# Main function
def main():
    bin_input = input("Enter BIN (Ex: 414720xxxxxxxxxx): ")
    
    if len(bin_input) < 6 or 'x' not in bin_input:
        print("Invalid BIN format! Use 'x' for random digits.")
        return

    num_cards = int(input("How many cards to generate? "))

    for _ in range(num_cards):
        cc = generate_cc(bin_input)
        cvv = generate_cvv()
        expiry = generate_expiry()
        print(f"CC: {cc} | EXP: {expiry} | CVV: {cvv}")

if __name__ == "__main__":
    main()
