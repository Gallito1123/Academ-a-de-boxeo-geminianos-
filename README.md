<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Academia de Boxeo Geminianos</title>
  <style>
    body {
      font-family: 'Arial Black', Arial, sans-serif;
      background-color: #1a237e;
      color: white;
    }
    .container {
      max-width: 400px;
      margin: 0 auto;
      padding: 20px;
      background-color: #fff;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
      text-align: center;
    }
    header {
      text-align: center;
      margin-bottom: 20px;
    }
    header h1 {
      font-size: 24px;
    }
    .form-group {
      margin-bottom: 20px;
      text-align: center;
    }
    .form-group label {
      display: block;
      margin-bottom: 5px;
      color: black;
    }
    .form-group input, .form-group select {
      width: 100%;
      padding: 8px;
      font-size: 16px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
    .btn-container {
      display: flex;
      justify-content: center;
      gap: 10px;
      margin-top: 20px;
    }
    .btn {
      padding: 10px 20px;
      font-size: 16px;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      text-decoration: none;
    }
    .facebook-btn {
      background-color: #007bff;
    }
    .whatsapp-btn {
      background-color: #25d366;
    }
    .location-btn {
      background-color: #ff5722;
    }
    .facebook-btn:focus,
    .whatsapp-btn:focus,
    .location-btn:focus {
      outline: none;
    }
    .register-btn {
      background-color: #007bff;
      border-radius: 10px;
    }
    #mensaje-emergente {
      display: none;
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      padding: 20px;
      border-radius: 5px;
      text-align: center;
    }
  </style>
  <script>
    function validarEmail(email) {
      const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return re.test(String(email).toLowerCase());
    }

    function guardarDatos() {
      const email = document.getElementById('email').value;
      const peso = document.getElementById('peso').value;
      const edad = document.getElementById('edad').value;
      const sexo = document.getElementById('sexo').value;
      const gimnasio = document.getElementById('gimnasio').value;

      if (!validarEmail(email)) {
        alert('Por favor, ingresa un correo electrónico válido.');
        return;
      }

      const datos = `Correo Electrónico: ${email}\nPeso: ${peso}\nEdad: ${edad}\nSexo: ${sexo}\nGimnasio: ${gimnasio}`;
      const whatsappUrl = `https://api.whatsapp.com/send?phone=3317549376&text=${encodeURIComponent(datos)}`;

      mostrarMensajeEmergente(whatsappUrl);

      const button = document.getElementById('submit-btn');
      button.textContent = 'Registrar otro peleador';
      button.classList.remove('register-btn');
      button.classList.add('register-another-btn');
      
      document.getElementById('registro-form').reset();
    }

    function mostrarMensajeEmergente(url) {
      const mensajeEmergente = document.getElementById('mensaje-emergente');
      mensajeEmergente.style.display = 'block';
      let contador = 5;
      const intervalo = setInterval(() => {
        if (contador > 0) {
          mensajeEmergente.textContent = `Para terminar envía el mensaje por WhatsApp en ${contador}...`;
          contador--;
        } else {
          clearInterval(intervalo);
          mensajeEmergente.style.display = 'none';
          window.location.href = url;
        }
      }, 1000);
    }

    document.addEventListener('DOMContentLoaded', () => {
      document.getElementById('registro-form').addEventListener('submit', function(event) {
        event.preventDefault();
        guardarDatos();
      });
    });
  </script>
</head>
<body>
  <header>
    <h1>Academia de Boxeo Geminianos</h1>
  </header>
  <div class="container">
    <form id="registro-form">
      <div class="form-group">
        <label for="email">Correo Electrónico:</label>
        <input type="email" id="email" name="email" required>
      </div>
      <div class="form-group">
        <label for="peso">Peso:</label>
        <input type="number" id="peso" name="peso" required>
      </div>
      <div class="form-group">
        <label for="edad">Edad:</label>
        <input type="number" id="edad" name="edad" required>
      </div>
      <div class="form-group">
        <label for="sexo">Sexo:</label>
        <select id="sexo" name="sexo" required>
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
        </select>
      </div>
      <div class="form-group">
        <label for="gimnasio">Gimnasio:</label>
        <input type="text" id="gimnasio" name="gimnasio" required>
      </div>
      <button type="submit" id="submit-btn" class="register-btn btn">Registrarse</button>
    </form>
    <div class="btn-container">
      <a href="https://www.facebook.com/profile.php?id=61558502042220&mibextid=JRoKGi" target="_blank" class="facebook-btn btn">Facebook</a>
      <a href="https://maps.app.goo.gl/mAuRGwhNNV6vgkfp8?g_st=ac" target="_blank" class="location-btn btn">Ubícanos</a>
      <a href="https://api.whatsapp.com/send?phone=3317549376" target="_blank" class="whatsapp-btn btn">WhatsApp</a>
    </div>
  </div>
  <div id="mensaje-emergente">Para terminar envía el mensaje por WhatsApp en 5...</div>
</
