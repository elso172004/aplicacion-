<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>AhorroMax - Inicio de Sesión</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
    }
    .container {
      max-width: 400px;
      margin: 60px auto;
      background: #fff;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    h2 {
      text-align: center;
      color: #333;
    }
    input[type="text"], input[type="password"], input[type="email"] {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      margin-bottom: 20px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      width: 100%;
      padding: 10px;
      background-color: #f0c419;
      border: none;
      border-radius: 5px;
      font-weight: bold;
      cursor: pointer;
    }
    button:hover {
      background-color: #e0b410;
    }
    .switch {
      text-align: center;
      margin-top: 15px;
    }
  </style>
</head>
<body>
  <div class="container" id="login-container">
    <h2>Iniciar Sesión</h2>
    <input type="email" id="loginEmail" placeholder="Correo electrónico" />
    <input type="password" id="loginPassword" placeholder="Contraseña" />
    <button onclick="login()">Ingresar</button>
    <div class="switch">
      ¿No tienes cuenta? <a href="#" onclick="showRegister()">Regístrate</a>
    </div>
  </div>

  <div class="container" id="register-container" style="display: none;">
    <h2>Registro</h2>
    <input type="text" id="registerNombre" placeholder="Nombre completo" />
    <input type="email" id="registerEmail" placeholder="Correo electrónico" />
    <input type="password" id="registerPassword" placeholder="Contraseña" />
    <button onclick="register()">Registrarse</button>
    <div class="switch">
      ¿Ya tienes cuenta? <a href="#" onclick="showLogin()">Inicia sesión</a>
    </div>
  </div>

  <script>
    const API_URL = "http://localhost:3000";

    function showRegister() {
      document.getElementById("login-container").style.display = "none";
      document.getElementById("register-container").style.display = "block";
    }

    function showLogin() {
      document.getElementById("register-container").style.display = "none";
      document.getElementById("login-container").style.display = "block";
    }

    async function login() {
      const email = document.getElementById("loginEmail").value;
      const password = document.getElementById("loginPassword").value;

      const res = await fetch(`${API_URL}/login`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ email, password })
      });

      const data = await res.json();

      if (res.ok) {
        alert("Inicio de sesión exitoso");
        localStorage.setItem("token", data.token);
        // Aquí puedes redirigir al dashboard o mostrar otra vista
      } else {
        alert(data.error);
      }
    }

    async function register() {
      const nombre = document.getElementById("registerNombre").value;
      const email = document.getElementById("registerEmail").value;
      const password = document.getElementById("registerPassword").value;

      const res = await fetch(`${API_URL}/registro`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ nombre, email, password })
      });

      const data = await res.json();

      if (res.ok) {
        alert("Registro exitoso");
        showLogin();
      } else {
        alert(data.error);
      }
    }
  </script>
</body>
</html>
