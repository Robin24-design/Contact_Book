# Contact Book

A simple interactive Contact Book script (stored in `Index.html`) that demonstrates basic contact management operations: add, search, delete, and view all contacts.

> Note: The repository stores the script inside `Index.html` (the file contains Python code). The script is an interactive command-line program and requires Python 3 to run.

## Features

- Add a new contact (name, phone number, email)
- Search for a contact by name (case-insensitive)
- Delete a contact by name
- View all contacts in a formatted list
- Simple text-menu driven CLI loop

## Files

- `Index.html` — The main script file containing the contact book implementation (Python code placed in this file).
- `README.md` — This documentation (updated to explain the code and how to use it).

## How to run

1. Ensure you have Python 3 installed. Check with `python3 --version`.
2. Rename `Index.html` to `contact_book.py` (optional, but recommended) or run it directly with Python:

   python3 Index.html

3. Follow the interactive menu prompts:
   - 1: Add Contact
   - 2: Search Contact
   - 3: Delete Contact
   - 4: View All Contacts
   - 5: Exit

The script runs in a loop until you choose `5` to exit.

## Code walkthrough

The script stores contacts in an in-memory list called `contacts`. Each contact is represented as a dictionary with keys for name, phone, and email. The main components are:

- `contacts = []`
  - An in-memory list that holds contact dictionaries for the running session.

- `add_contact()`
  - Prompts the user for `name`, `phone`, and `email`.
  - Creates a dictionary for the contact and appends it to `contacts`.
  - Prints a success message.

- `search_contact(name)`
  - Iterates through `contacts` and returns the first dictionary where the contact's name matches `name` (comparison is case-insensitive).
  - Returns `None` if no match is found.

- `delete_contact(name)`
  - Uses `search_contact` to find a contact by name and removes it from the `contacts` list if found.
  - Prints whether the deletion succeeded or that the contact wasn't found.

- `view_all()`
  - Prints all contacts in a formatted layout with an index and separators. If there are no contacts, prints a message to indicate that.

- Main menu loop
  - A `while True` loop presents a text menu and calls the appropriate function based on user input (1–5). Input is read using `input()` and the corresponding action is executed.

## Example session

1. Run the script:

   python3 Index.html

2. Add a contact (choose `1`):

   Enter name: Alice
   enter Phone number: 123-456-7890
   enter EmailAddress: alice@example.com

   Contact 'Alice' added successfully!

3. Search for a contact (choose `2`):

   Enter name to search: alice

   Contact Found:
   Name : Alice
   Phone: 123-456-7890
   Email: alice@example.com

4. View all contacts (choose `4`) — shows a numbered list of contacts.

5. Exit (choose `5`).

## Known issues and suggested fixes

While reviewing the code in `Index.html`, I found a few bugs and inconsistencies that will affect the script's behavior. Here are the issues and recommended fixes:

1. Key name mismatches
   - Problem: `add_contact()` creates a contact dictionary with keys `{"name": name, "Phone number": phone, "EmailAddress": email}` but other parts of the code (e.g., `view_all()` and the search/display blocks) access `contact['phone']` and `contact['email']`.
   - Result: This causes KeyError or missing data when viewing, searching, or printing contacts.
   - Fix: Use consistent keys across the code. Recommended keys: `"name"`, `"phone"`, `"email"`.

   Example replacement in add_contact():
   ```py
   contact = {"name": name, "phone": phone, "email": email}
   ```

2. Typos and text
   - Problem: Small user-facing typos like `Search Conatct` in the menu do not affect functionality but reduce polish.
   - Fix: Correct the spelling and unify menu text.

3. File naming and location
   - Problem: The Python code is saved in a file named `Index.html`, which is misleading.
   - Fix: Rename to `contact_book.py` or `main.py`.

4. No persistence
   - Problem: All contacts are stored only in memory and lost when the program exits.
   - Fix: Add optional save/load functionality using JSON or CSV so contacts persist between runs. Example: save contacts to `contacts.json` when exiting and load at startup.

5. No duplicate handling
   - Problem: Multiple contacts with the same name can be added without warning.
   - Fix: Warn or ask for confirmation when adding a contact with an existing name, or allow multiple entries and provide IDs for deletion.

6. No input validation
   - Problem: Phone and email fields are not validated.
   - Fix: Add simple validation (e.g., regex for email, check numeric or formatted phone number) and re-prompt on invalid input.

7. Partial and fuzzy search
   - Improvement: Allow partial name matches, search by phone or email, or use case-insensitive substring matching.

8. Update/edit contact
   - Improvement: Add an option to edit an existing contact's details.

## Suggested improvements / next steps

- Persist contacts to disk (JSON/CSV) and load them at startup.
- Move the code into a proper Python file and add a `if __name__ == '__main__':` guard.
- Add unit tests for `add_contact`, `search_contact`, `delete_contact`, and `view_all`.
- Implement an `update_contact` function to edit existing entries.
- Replace raw dictionaries with a small `Contact` dataclass for clearer structure.
- Improve the UI (e.g., table output using `tabulate` or a simple TUI library) or add an optional web UI.

## Contributing

Contributions are welcome! Suggested workflow:

1. Fork the repo
2. Create a branch for your change
3. Make changes and add tests where appropriate
4. Open a pull request with a clear description of what you changed and why

## License

This repository does not currently include a license file. If you want to add a license, consider adding an Open Source license such as MIT, Apache-2.0, or GPL-3.0.

---

If you'd like, I can also:
- Rename `Index.html` to `contact_book.py` and fix the key-name bugs and typos, or
- Implement persistence to `contacts.json`, or
- Add unit tests demonstrating the behavior.

Tell me which follow-up you'd like me to do next.