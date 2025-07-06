import csv

file_name = "expenses.csv"

def initialize_file():
    try:
        with open(file_name, "x", newline = "") as f:
            writer = csv.writer(f)
            writer.writerow(["DATE", " AMOUNT", " CATEGORY", " NOTE"])
            print("✔️ File created: 'expenses.csv' with headers.")
    except FileExistsError:
        with open(file_name, "r+"
                  , newline = "") as f:
            first_line= f.readline()
            if not first_line:
                writer= csv.writer(f)
                f.seek(0)
                writer.writerow(["DATE", " AMOUNT", " CATEGORY", " NOTE"])
                print("❕File existed but was empty - headers added.")
            else:
                print("📁 File already exists. No creation required again.")

from datetime import datetime   # if not added already

def add_expense():

    # Ask for date
    date= input("Enter date (as DD-MM-YYYY) or press Enter for using today's date: ")
    if date.strip() == "":
        date = datetime.now().strftime("%d-%m-%Y")  # Using today's date

    # Ask for amount
    try:
        amount = float(input("Enter amount spent: ₹"))
    except ValueError:
        print("❌ Invalid input, Please enter a number.")
        return
    
    # Ask for category of expense
    category = input("Enter category (eg. Food, Travel, etc.): ")

    # Ask for an optional note
    note = input("Enter a note(optional): ")

    # Add the data to our csv file
    with open(file_name, "a", newline = '') as f:
        writer = csv.writer(f)
        writer.writerow([date, amount, category, note])

    print("✔️ Expense saved!")

def show_total_expense():
    total=0.0
    try:
        with open(file_name, "r") as f:
            reader= csv.reader(f)
            next(reader) # skipping headers row

            for row in reader:
                try:
                    amount=float(row[1])
                    total=total+amount
                except (ValueError, IndexError):
                    print("❗Skipped a bad row: ", row)

        print(f"💰Total spent: ₹{total:.2f}")

    except FileNotFoundError:
        print("❌ Expense file not found.")

def show_expenses_by_date():
    try:
        with open(file_name, "r") as f:
            reader= csv.reader(f)
            next(reader)

            print("\n📅 Expenses by Date:")
            for row in reader:
                try:
                    print(f"{row[0]} | ₹{row[1]} | {row[2]} | {row[3]}")
                except IndexError:
                    print("❗Skipped incomplete row:", row)
    except FileNotFoundError:
        print("❌ Expense file not found.")

def show_expense_table():
    # shows the values in a clean and neat tabular form.
    try:
        with open(file_name, "r") as f:
            reader = list(csv.reader(f))
            print("\n📋 Expense Table:\n")
            for row in reader:
                print(" | ".join(row))
    except FileNotFoundError:
        print("❌ File not found.")

def export_expenses():
    # for saving your csv file for backup or for sending it to someone.
    new_file = input("Enter name of export file (e.g. export.csv): ")
    try:
        with open(file_name, "r") as original, open(new_file, "w", newline="") as new:
            new.write(original.read())
        print(f"✅ Expenses exported to {new_file}")
    except:
        print("❌ Could not export file.")

initialize_file()
add_expense()
show_total_expense()
show_expense_table()
export_expenses()