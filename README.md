# BankAppWindow
Assignment
from tkinter import *

# Define the GUI window
root = Tk()
root.geometry("500x500")
root.title("Bank App")

# Define the bank accounts
savings_balance = 0
current_balance = 0

# Define the functions to handle deposit, withdrawal and check balance
def deposit(account, amount):
    global savings_balance, current_balance
    if account == "savings":
        savings_balance += amount
        print(f"Deposited {amount} into savings account. New balance: {savings_balance}")
    elif account == "current":
        current_balance += amount
        print(f"Deposited {amount} into current account. New balance: {current_balance}")
    else:
        print("Invalid account type.")

def withdraw(account, amount):
    global savings_balance, current_balance
    if account == "savings":
        if amount > savings_balance:
            print("Insufficient funds in savings account.")
        else:
            savings_balance -= amount
            print(f"Withdrew {amount} from savings account. New balance: {savings_balance}")
    elif account == "current":
        if amount > current_balance:
            print("Insufficient funds in current account.")
        else:
            current_balance -= amount
            print(f"Withdrew {amount} from current account. New balance: {current_balance}")
    else:
        print("Invalid account type.")

def check_balance(account):
    global savings_balance, current_balance
    if account == "savings":
        print(f"Savings account balance: {savings_balance}")
    elif account == "current":
        print(f"Current account balance: {current_balance}")
    else:
        print("Invalid account type.")

# Define the GUI elements
var_account_type = StringVar()
var_account_type.set("savings")
var_deposit_amount = StringVar()
var_withdraw_amount = StringVar()

# Define the GUI functions
def deposit_button_click():
    deposit(var_account_type.get(), int(var_deposit_amount.get()))

def withdraw_button_click():
    withdraw(var_account_type.get(), int(var_withdraw_amount.get()))

def check_balance_button_click():
    check_balance(var_account_type.get())

# Define the GUI layout
label_title = Label(root, text="Bank App", font=("Arial", 23, "bold"))
label_title.pack(pady=20)

label_account_type = Label(root, text="Account Type")
label_account_type.pack()

radio_savings = Radiobutton(root, text="Savings", variable=var_account_type, value="savings")
radio_savings.pack()

radio_current = Radiobutton(root, text="Current", variable=var_account_type, value="current")
radio_current.pack()

label_deposit_amount = Label(root, text="Deposit Amount")
label_deposit_amount.pack()

entry_deposit_amount = Entry(root, textvariable=var_deposit_amount)
entry_deposit_amount.pack()

button_deposit = Button(root, text="Deposit", command=deposit_button_click)
button_deposit.pack(pady=10)

label_withdraw_amount = Label(root, text="Withdraw Amount")
label_withdraw_amount.pack()

entry_withdraw_amount = Entry(root, textvariable=var_withdraw_amount)
entry_withdraw_amount.pack()

button_withdraw = Button(root, text="Withdraw", command=withdraw_button_click)
button_withdraw.pack(pady=10)

button_check_balance = Button(root, text="Check Balance", command=check_balance_button_click)
button_check_balance.pack(pady=10)

root.mainloop()
