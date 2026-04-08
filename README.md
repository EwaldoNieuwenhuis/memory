# Memory Game

A multiplayer memory game created with PHP, JavaScript, and MySQL. This game supports tracking turns, a leaderboard system, and admin functionalities for managing memory images and games.

## Features
- **Multiplayer Memory Setup:** Select two users to compete against each other in a game of memory.
- **Customizable Board Size:** Choose how many image pairs to play with.
- **Admin Panel:** Administrators can upload new images via file upload or links, disable existing images, and host new games manually.
- **Game History:** Tracks player wins, number of turns taken, and dates played.

## Requirements
- A local web server stack like **XAMPP**, **WAMP**, or **MAMP** (requires Apache/Nginx, MySQL, and PHP).

## Installation & Setup

1. **Clone the Repository**
   Clone or download this repository and place the folder into your web server's document root (e.g., `htdocs` for XAMPP, `www` for WAMP).

2. **Database Setup**
   - Open phpMyAdmin or your preferred MySQL database management tool.
   - Create a new database named `memory`.
   - Locate the file `database/memory.sql` within the project.
   - Import this SQL file into the `memory` database you just created. This sets up the necessary tables and initial data.

3. **Database Configuration**
   The application connects to a MySQL database named `memory` on `localhost` with the username `root` and no password. 
   If your local database setup uses a different username or password, you need to update the PDO connection string in `index.php` and other files:
   ```php
   $db = new PDO("mysql:host=localhost;dbname=memory;", "root", "");
   ```

## How to Use

1. **Start the Web Server**
   Ensure your Apache server and MySQL services are running.

2. **Access the Game**
   Navigate to the project directory in your browser, for instance: `http://localhost/memory/`

3. **Register / Login**
   - Click "Make New Account" to register new users. *Note: You'll need two separate accounts to play a game against each other.*
   - In the login form, enter the credentials for both Player 1 and Player 2 simultaneously and click "Login Players".

4. **Play the Game**
   - After both players are logged in, select the number of images to play with from the dropdown.
   - Click "Choose" to generate the board.
   - Take turns clicking on tiles to find matching pairs! As pairs are found, turns are tracked per player.

5. **Admin Access**
   - Go to `Administration Log In` via the main login page.
   - Once logged in with a valid admin account, you can perform admin tasks such as adding new images to the memory pool, disabling images, or manually hosting a game.

## Tech Stack & Architecture

- **`functions.php`**: This is the core logic file. It houses PHP functions for generating HTML forms, interacting with the database, handling image uploads, validating users, and generating the game board. Start here if you want to understand or extend the backend functionality.
- **`index.php`**: The main entry point. It manages session states (showing the game board if logged in, or the forms if not) and sets up the central structure.
- **`js/functions_js.js`**: Contains the frontend logic for flipping cards, tracking turns, checking matches, and communicating with the backend. 
- **`api/`**: Contains scripts requests via AJAX from the frontend JavaScript to update the database asynchronously as the game progresses (e.g., logging a game completion).
- **`css/styles.css`**: Contains custom styling, alongside the integrated Bootstrap framework.

## Security Note

Passwords are obfuscated using a local custom `md5` hashing process combined with a static salt (`'josthanos'`). To change how passwords are encrypted, review `functions.php` and the registration processes. For deploying this project in a real-world server, switching to native built-in functions like `password_hash()` and `password_verify()` is highly recommended over this legacy method.
