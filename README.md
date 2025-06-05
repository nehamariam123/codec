<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Unique Registration Form</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    background: linear-gradient(135deg, #4b6cb7 0%, #182848 100%);
    font-family: 'Poppins', sans-serif;
    margin: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
  }

  .container {
    background: rgba(255, 255, 255, 0.1);
    padding: 40px 50px;
    border-radius: 15px;
    box-shadow: 0 15px 40px rgba(0,0,0,0.4);
    width: 350px;
    backdrop-filter: blur(10px);
    position: relative;
  }

  h2 {
    margin: 0 0 30px;
    font-weight: 600;
    font-size: 28px;
    text-align: center;
    letter-spacing: 1.5px;
  }

  .input-group {
    margin-bottom: 25px;
    position: relative;
  }

  label {
    display: block;
    font-size: 14px;
    margin-bottom: 8px;
    letter-spacing: 0.8px;
  }

  input {
    width: 100%;
    padding: 12px 15px;
    border-radius: 50px;
    border: 2px solid rgba(255, 255, 255, 0.5);
    background: transparent;
    color: #fff;
    font-size: 16px;
    outline: none;
    transition: 0.3s;
  }

  input:focus {
    border-color: #00ffcc;
    box-shadow: 0 0 10px #00ffcc;
  }

  input.valid {
    border-color: #39e600;
    box-shadow: 0 0 10px #39e600;
  }

  input.invalid {
    border-color: #ff4d4d;
    box-shadow: 0 0 10px #ff4d4d;
  }

  .error-msg {
    color: #ff4d4d;
    font-size: 12px;
    margin-top: 5px;
    height: 14px;
    letter-spacing: 0.5px;
  }

  button {
    width: 100%;
    padding: 14px;
    background: #00ffcc;
    border: none;
    border-radius: 50px;
    color: #182848;
    font-weight: 600;
    font-size: 18px;
    cursor: pointer;
    transition: background 0.3s;
    letter-spacing: 1.5px;
  }

  button:hover {
    background: #00cca8;
  }

  /* Animated floating labels optional */
  input:focus + label,
  input:not(:placeholder-shown) + label {
    transform: translateY(-28px);
    font-size: 12px;
    color: #00ffcc;
  }

  label {
    position: absolute;
    left: 20px;
    bottom: 12px;
    color: rgba(255, 255, 255, 0.7);
    pointer-events: none;
    transition: 0.3s ease all;
  }

  .input-group {
    position: relative;
  }
</style>
</head>
<body>
  <div class="container">
    <h2>Create Account</h2>
    <form id="registrationForm" novalidate>
      <div class="input-group">
        <input type="text" id="name" name="name" required placeholder=" " />
        <label for="name">Full Name</label>
        <div class="error-msg" id="nameError"></div>
      </div>
      <div class="input-group">
        <input type="email" id="email" name="email" required placeholder=" " />
        <label for="email">Email Address</label>
        <div class="error-msg" id="emailError"></div>
      </div>
      <div class="input-group">
        <input type="password" id="password" name="password" required placeholder=" " />
        <label for="password">Password</label>
        <div class="error-msg" id="passwordError"></div>
      </div>
      <div class="input-group">
        <input type="password" id="confirmPassword" name="confirmPassword" required placeholder=" " />
        <label for="confirmPassword">Confirm Password</label>
        <div class="error-msg" id="confirmPasswordError"></div>
      </div>
      <div class="input-group">
        <input type="tel" id="phone" name="phone" required placeholder=" " pattern="\\d{10}" />
        <label for="phone">Phone Number (10 digits)</label>
        <div class="error-msg" id="phoneError"></div>
      </div>
      <button type="submit">Register</button>
    </form>
  </div>

<script>
  const form = document.getElementById('registrationForm');

  const validators = {
    name: value => value.trim().length >= 3,
    email: value => /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(value),
    password: value => value.length >= 6,
    confirmPassword: (value, password) => value === password,
    phone: value => /^\d{10}$/.test(value),
  };

  const errorMessages = {
    name: 'Name must be at least 3 characters.',
    email: 'Invalid email address.',
    password: 'Password must be at least 6 characters.',
    confirmPassword: 'Passwords do not match.',
    phone: 'Phone must be 10 digits.',
  };

  form.addEventListener('input', (e) => {
    const field = e.target.name;
    if (!field) return;
    validateField(field);
  });

  function validateField(field) {
    const input = form.elements[field];
    const value = input.value;
    let valid = false;
    if(field === 'confirmPassword') {
      const password = form.elements['password'].value;
      valid = validators[field](value, password);
    } else {
      valid = validators[field](value);
    }
    const errorDiv = document.getElementById(field + 'Error');
    if (valid) {
      input.classList.add('valid');
      input.classList.remove('invalid');
      errorDiv.textContent = '';
    } else {
      input.classList.add('invalid');
      input.classList.remove('valid');
      errorDiv.textContent = errorMessages[field];
    }
    return valid;
  }

  form.addEventListener('submit', (e) => {
    e.preventDefault();
    let allValid = true;
    ['name', 'email', 'password', 'confirmPassword', 'phone'].forEach(field => {
      if(!validateField(field)) {
        allValid = false;
      }
    });
    if (allValid) {
      alert('Registration Successful!');
      form.reset();
      [...form.elements].forEach(el => el.classList.remove('valid'));
    } else {
      alert('Please fix errors before submitting.');
    }
  });
</script>
</body>
</html>

```
