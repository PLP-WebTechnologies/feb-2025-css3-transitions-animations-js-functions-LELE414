<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Interactive Sign-Up Page</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <h1>Sign Up for The Coolest Club!</h1>

  <form id="signupForm">
    <label for="username">Username:</label>
    <input type="text" id="username" required />
    <span class="error" id="usernameError"></span>

    <label for="email">Email:</label>
    <input type="email" id="email" required />
    <span class="error" id="emailError"></span>

    <label for="password">Password:</label>
    <input type="password" id="password" required />
    <button type="button" id="togglePassword">Show</button>
    <span class="error" id="passwordError"></span>

    <button type="submit">Sign Up</button>
  </form>

  <p id="message"></p>

  <h2>Previously Stored Data:</h2>
  <p id="storedData"></p>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
  background-color: #f4f4f4;
}

form {
  display: inline-block;
  text-align: left;
  padding: 20px;
  border: 2px solid #ccc;
  border-radius: 10px;
  background-color: #fff;
  transition: all 0.3s ease-in-out;
  opacity: 1;
}

form:hover {
  transform: scale(1.05);
}

input {
  display: block;
  margin: 10px 0 5px;
  padding: 8px;
  width: 250px;
  transition: background-color 0.3s ease;
}

input:focus {
  background-color: #f0f8ff;
  outline: none;
}
button {
  padding: 8px 15px;
  margin-top: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.3s ease;
}

button:hover {
  background-color: #4CAF50;
  transform: scale(1.1);
}

.error {
  color: red;
  font-size: 0.9em;
}

#message {
  color: green;
  font-weight: bold;
  transition: opacity 0.5s ease-in-out;
}

#storedData {
  font-size: 1.2em;
  margin-top: 20px;
  color: #333;
}

document.addEventListener("DOMContentLoaded", () => {
  const form = document.getElementById("signupForm");
  const username = document.getElementById("username");
  const email = document.getElementById("email");
  const password = document.getElementById("password");
  const message = document.getElementById("message");
  const storedData = document.getElementById("storedData");

  const usernameError = document.getElementById("usernameError");
  const emailError = document.getElementById("emailError");
  const passwordError = document.getElementById("passwordError");

  const togglePasswordBtn = document.getElementById("togglePassword");

  // Load stored data from localStorage
  const savedData = JSON.parse(localStorage.getItem("userData"));
  if (savedData) {
    storedData.textContent = Username: ${savedData.username}, Email: ${savedData.email};
  } else {
    storedData.textContent = "No data stored.";
  }

  // Toggle password visibility
  togglePasswordBtn.addEventListener("click", () => {
    const isHidden = password.type === "password";
    password.type = isHidden ? "text" : "password";
    togglePasswordBtn.textContent = isHidden ? "Hide" : "Show";
  });
 // Form submission handler
  form.addEventListener("submit", (e) => {
    e.preventDefault();

    // Reset previous error messages
    usernameError.textContent = "";
    emailError.textContent = "";
    passwordError.textContent = "";
    message.textContent = "";

    let isValid = true;

    // Simple validation
    if (username.value.trim() === "") {
      usernameError.textContent = "Username is required.";
      isValid = false;
    }

    if (email.value.trim() === "") {
      emailError.textContent = "Email is required.";
      isValid = false;
    }

    if (password.value.trim().length < 6) {
      passwordError.textContent = "Password must be at least 6 characters.";
      isValid = false;
    }

    // If form is valid, store the data in localStorage and show a success message
    if (isValid) {
      const userData = {
        username: username.value,
        email: email.value,
      };

 // Save to localStorage
      localStorage.setItem("userData", JSON.stringify(userData));

      message.textContent = "Sign-up successful! Welcome!";
      message.style.color = "green";
      form.reset();

      // Display stored data immediately after successful sign-up
      storedData.textContent = Username: ${userData.username}, Email: ${userData.email};
    }
  });
});
