# CS50 Final Project - Password Manager
#### Video Demo: https://youtu.be/ShoVyN_sQMY

## Description
Password Manager is a web application that allows the user to manage passwords by adding custom passwords or generating them randomly, being able to select the desired number of characters and which ones (letters, digits, special characters). These, along with the chosen username/email and link of the site, are stored in a table in the home page, where the user can access all this data.

The project was built in Python using Flask and Bootstrap. It also incorporates CSS, JavaScript (to show and hide the passwords in the homepage table) and SQLite for database management.

## The Database
I used two tables for my database: users and passwords.

1. **users**: Stores user credentials for authentication. It includes the username and a hashed password (hash), ensuring passwords are not stored in plain text for security.

2. **passwords**: Stores saved passwords for different websites while keeping them securely linked to a specific user (user_id). It includes the user_id, the site, username, and encrypted_password (instead of the normal password for security reasons).

## Source files
*layout.html* - Base template for all the other pages.

*login.html* - Allows users to log in to their account.

*register.html* - Page where the user can create a new account.

*logout.html* - Logs users out of their session.

*index.html* - Homepage of the site that contains the passwords table.

*add.html* - Lets users add a custom password (linked to a site and a username).

*generate.html* - Provides a password generator with customizable options.

*generate_key.py* - Generates a one-time encryption key

*encryption_key.key* - Stores the key generated in generate_key.py.

*app.py* - Handles user authentication (/register, /login, /logout), password management (/, /add, /delete) and password generation (/generate).

## Encryption and Decryption using Fernet
For this project I used Fernet encryption from the cryptography python library, to be able to encrypt passwords before storing them in the database and decrypt them when displaying them on the homepage.

Fernet is a symmetric encryption method, meaning the same key is used for both encryption and decryption, ensuring that only someone with the correct key can access the original data. This is ideal for securely managing passwords.

### How Fernet is Used:
1. **Generating and storing the encryption key:** To use Fernet encryption, I first needed to generate a secure encryption key. A separate file (*generate_key.py*), which runs only once is responsible for generating and storing this key in a file called *encryption_key.key*. The key is created using Fernet.generate_key() and then saved to the file. This key is then used for both ecnryption and decryption processes.

2. **Encryption during password storage (Add and Generate pages):** When a user adds a password, it is first encrypted before being saved to the database. The encryption key stored in *encryption_key.key* is loaded and use to perform the encryption.

3. **Decryption for display (Index page):** When displaying the stored passwords, each one is decrypted using the same encryption key. The password is decrypted also using Fernet and displayed to the user in plain text.

## Implementing password visibility toggle using JavaScript
I used JavaScript to allow users to show or hide their passwords in the homepage. By clicking the "Show" or "Hide" button next to a password, the script switches the input field's type between "password" (hidden) and "text" (shown), improving usability while mantaining security.

### How the script works
1. **Event listener for button clicks:** The script listens for click events on each button linked to the password.

2. **Toggle password visibility:** When a user clicks the button, the scripts switches the password field's type between "text" and "password" and the button text updates between "Show" and "Hide" to provide clear feedback to the user.

## Possible improvements
Just like any web application, my project can also be improved. A few ideias:

1. Allow the user to change their password by adding a feature in the account settings where they can securely update their existing password. This would include verifying the old password before allowing the change and then updating the new password in the database to ensure security.

2. Implement a password strength checker, so that when the user adds or generates a new passwords, feedback is given on how secure that password is. This could be a bar that starts empty and fills up changing colors depending on the password the user is adding, utilizing factors like length and character variety.

3. Implement password categories, so that the user can organize their saved passwords into different fields for example, Social Media, Work and Email. This would help with organization.

4. Password expiration alerts, to notify the user when a password hasn't been changed in a long time, encouraging better password management. For example, if a password is not updated for a certain amount of time, the user receives a warning suggesting that they should update it.

5. Copy to clipboard function, allowing the user to quickly copy their passwords without manually selecting them. This could be made with a copy button next to each password and with the help of JavaScript it would be copied to the clipboard.

## References
**Fernet encryption and decryption:** https://medium.com/@rahulgosavi.94/fernet-encryption-and-decryption-2101f0e3097a

**Generating a random password using the python random module:** https://docs.python.org/3/library/secrets.html#module-secrets

## Source Code Access
To comply with CS50's Academic Honesty Policy, the source code is hosted in a private repository to prevent plagiarism.
