import os

FILE_NAME = "contacts.txt"

def load_contacts():
    if not os.path.exists(FILE_NAME):
        return []
    with open(FILE_NAME, "r") as file:
        lines = file.readlines()
        contacts = [line.strip().split(",") for line in lines]
    return contacts

def save_contacts(contacts):
    with open(FILE_NAME, "w") as file:
        for contact in contacts:
            file.write(",".join(contact) + "\n")

def display_contacts(contacts):
    if not contacts:
        print("📭 No contacts found!")
        return
    print("\n📒 Contact List:")
    for i, (name, phone, email) in enumerate(contacts, 1):
        print(f"{i}. Name: {name}, Phone: {phone}, Email: {email}")
    print()

def add_contact(contacts):
    name = input("Enter name: ")
    phone = input("Enter phone: ")
    email = input("Enter email: ")
    contacts.append([name, phone, email])
    print("✅ Contact added.")

def search_contact(contacts):
    keyword = input("Enter name or phone to search: ").lower()
    found = [c for c in contacts if keyword in c[0].lower() or keyword in c[1]]
    if found:
        print("\n🔍 Search Results:")
        for contact in found:
            print(f"Name: {contact[0]}, Phone: {contact[1]}, Email: {contact[2]}")
    else:
        print("❌ No matching contact found.")

def update_contact(contacts):
    display_contacts(contacts)
    try:
        index = int(input("Enter contact number to update: ")) - 1
        if 0 <= index < len(contacts):
            name = input("Enter new name: ")
            phone = input("Enter new phone: ")
            email = input("Enter new email: ")
            contacts[index] = [name, phone, email]
            print("🔁 Contact updated.")
        else:
            print("⚠️ Invalid contact number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def delete_contact(contacts):
    display_contacts(contacts)
    try:
        index = int(input("Enter contact number to delete: ")) - 1
        if 0 <= index < len(contacts):
            removed = contacts.pop(index)
            print(f"🗑️ Deleted contact: {removed[0]}")
        else:
            print("⚠️ Invalid contact number.")
    except ValueError:
        print("⚠️ Please enter a valid number.")

def main():
    contacts = load_contacts()

    while True:
        print("\n===== CONTACT BOOK MENU =====")
        print("1. Show All Contacts")
        print("2. Add New Contact")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")
        choice = input("Enter your choice (1-6): ")

        if choice == "1":
            display_contacts(contacts)
        elif choice == "2":
            add_contact(contacts)
        elif choice == "3":
            search_contact(contacts)
        elif choice == "4":
            update_contact(contacts)
        elif choice == "5":
            delete_contact(contacts)
        elif choice == "6":
            save_contacts(contacts)
            print("📁 Contacts saved. Goodbye!")
            break
        else:
            print("⚠️ Invalid choice. Please enter 1–6.")

if __name__ == "__main__":
    main()
