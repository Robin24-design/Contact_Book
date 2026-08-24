# Contact Book — Code Description

This README describes the Contact Book script exactly as it appears in the repository (file: `Index.html`). No changes were made to the code — this is a detailed explanation of what the existing code does, how it behaves at runtime, and what to expect when you run it.

---

## Where the code lives

- File: `Index.html` (contains a Python script — the file is a plain-text file with Python code inside it).

## Purpose

The script implements a simple, interactive command-line Contact Book that stores contacts in memory and provides a small menu-driven interface to add, search, delete, and view contacts.

## High-level flow

1. Initialize an in-memory list named `contacts`.
2. Define four functions that operate on this list:
   - `add_contact()` — gather user input and append a new contact dictionary to the list.
   - `search_contact(name)` — iterate over the list and return the first matching contact dictionary by name (case-insensitive comparison).
   - `delete_contact(name)` — use `search_contact` to find and remove a contact.
   - `view_all()` — print all contacts in a formatted layout.
3. Enter an infinite `while True` main menu loop that prompts the user for an action (Add, Search, Delete, View All, Exit) and calls the corresponding function. The loop breaks when the user selects Exit.

## Data model used by the script

- contacts: A list object in module scope used as the in-memory storage for all contact entries in the current program run.
- Each contact is represented as a Python dictionary. The code *intends* to keep three fields per contact: name, phone, and email. (See the exact key names used by the script in the code explanation below.)

## Functions and behavior (line-by-line explanation)

- contacts = []
  - Creates an empty list to hold contact dictionaries.

- def add_contact():
  - Prompts the user sequentially for three inputs:
    - name = input("enter name: ")
    - phone = input("enter Phone number: ")
    - email = input("enter EmailAddress: ")
  - Constructs a dictionary named `contact` with the following keys and assigned values from user input:
    - "name" → value of `name` variable
    - "Phone number" → value of `phone` variable
    - "EmailAddress" → value of `email` variable
  - Appends the `contact` dictionary to the `contacts` list.
  - Prints a confirmation: Contact '<name>' added successfully!

- def search_contact(name):
  - Iterates over each `contact` dictionary in `contacts`.
  - Compares `contact["name"].lower()` to `name.lower()` to perform a case-insensitive equality check.
  - If matched returns the contact dictionary immediately.
  - If no match is found after scanning the list returns `None`.

- def delete_contact(name):
  - Calls `search_contact(name)` to look up an existing contact by exact name match (case-insensitive).
  - If a contact is found, removes it from `contacts` using `contacts.remove(contact)` and prints a success message.
  - If not found, prints a "not found" message.

- def view_all():
  - If `contacts` is empty (`if not contacts:`) prints "No contacts to display." and returns early.
  - Otherwise prints a header and iterates through `contacts` with an `enumerate` (1-based index). For each contact it prints three lines showing:
    - Name (from contact['name'])
    - Phone Number (attempts to print contact['phone'])
    - EmailAddress (attempts to print contact['email'])
    - and a separator line of dashes after each contact

- Main menu loop (while True):
  - Prints a menu with five choices:
    1. Add Contact
    2. Search Conatct
    3. Delete Contact
    4. View All Contacts
    5. Exit
  - Accepts a single-line input (choice = input("Enter your choice (1-5): ")).
  - Handles choices:
    - "1": calls `add_contact()`
    - "2": prompts for `search_name`, calls `search_contact(search_name)`, and if result is not None prints the contact details (Name, Phone, Email) otherwise prints "Contact not found". The code prints a small header "Contact Found:" before the details.
    - "3": prompts for `del_name` and calls `delete_contact(del_name)`.
    - "4": calls `view_all()`.
    - "5": prints an exit message and executes `break` to end the loop and stop the program.
    - Any other input: prints "Invalid choice. Please enter 1-5." and continues the loop.

## Note on exact key names and printed fields

- When a contact is created in `add_contact()`, keys are: "name", "Phone number", and "EmailAddress".
- When the script prints details in `view_all()` and in the menu search result it references `contact['phone']` and `contact['email']`.
- Because the key names used for storage and the key names used for printing are not the same (capitalization and spacing differ), the printed phone/email may not display as intended when the program is run. The script still uses `contact['name']` consistently for lookups and printing the name.

This README records these exact behaviors to describe what the provided code does at runtime.

## Example run (reflecting current behavior)

1. Start the program e.g. `python3 Index.html` (the file contains Python code).
2. Choose option 1 and add a contact:
   - enter name: Alice
   - enter Phone number: 123-456-7890
   - enter EmailAddress: alice@example.com
   - Program prints: Contact 'Alice' added successfully!
3. Choose option 2 to search for "alice":
   - Enter name to search: alice
   - Program prints: "Contact Found:" and then attempts to print the contact details. It will correctly print the Name because `contact['name']` exists. The phone and email lines attempt to read keys `contact['phone']` and `contact['email']` which were not created by `add_contact()` (the stored keys are different), so depending on the Python interpreter run this may raise a KeyError when trying to access missing keys, or show incorrect behavior.
4. Choose option 4 to view all contacts: the view loop attempts to read `contact['phone']` and `contact['email']` for each entry; the mismatch between stored key names and accessed key names is an observable behavior at runtime.
5. Choose option 5 to exit.

## User-facing text and formatting

- Menu text contains a small spelling inconsistency: "Search Conatct" (typo) — the program logic still routes option 2 to the search flow.
- Messages and prompts are plain and minimal, using simple print/input statements.

## Runtime characteristics

- The script is synchronous and blocking — it waits for user input at each prompt.
- All data is stored only in memory for the current session; there is no file persistence in the provided code.
- The program will finish only when the user chooses the Exit option (5) or interrupts the process (Ctrl-C).

## Summary

This README documents the Contact Book code exactly as provided in `Index.html` and explains how it behaves, including the exact keys the code writes to and the keys it expects when printing. I made no changes to the code itself — this is purely documentation that describes the current implementation and its runtime behavior.

If you want, I can now:
- Add a separate file that documents the observed mismatches and potential runtime errors in more detail (still without changing the code), or
- Add an example transcript captured from a real run of the script as a demonstration (again, without modifying the code).

Tell me which of those (if any) you want next, or confirm that this README is what you needed.