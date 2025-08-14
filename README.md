<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Notificación ❤️</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #ff7eb3, #ff758c);
      color: white;
      margin: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      text-align: center;
    }
    h1 {
      font-size: 2rem;
      margin-bottom: .5rem;
    }
    p {
      margin: 0 1rem 1.5rem;
      font-size: 1.1rem;
    }
    .btn {
      background: white;
      color: #ff4f81;
      border: none;
      border-radius: 1.5rem;
      padding: 1rem 2rem;
      font-size: 1.1rem;
      font-weight: bold;
      margin: .5rem;
      cursor: pointer;
      width: 80%;
      max-width: 300px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.2);
      transition: transform .2s;
    }
    .btn:active {
      transform: scale(0.95);
    }
    input {
      padding: .7rem;
      border-radius: 1rem;
      border: none;
      font-size: 1rem;
      margin-bottom: 1rem;
      width: 60px;
      text-align: center;
    }
  </style>
</head>
<body>

  <h1>Notificación con ❤️</h1>
  <p>Activa permisos y recibe un recordatorio con amor.</p>

  <button class="btn" onclick="pedirPermiso()">🔓 Dar permiso</button>
  <button class="btn" onclick="mostrarAhora()">💌 Mostrar ahora</button>

  <div>
    <input type="number" id="segundos" min="1" value="5"> seg
  </div>
  <button class="btn" onclick="programar()">⏰ Programar notificación</button>

  <script>
    const soportaNotificaciones = 'Notification' in window;

    async function pedirPermiso() {
      if (!soportaNotificaciones) {
        alert('Tu navegador no soporta notificaciones.');
        return;
      }
      const estado = await Notification.requestPermission();
      if (estado === 'granted') {
        mostrarNoti('Permiso concedido 💖');
      } else {
        alert('Permiso denegado.');
      }
    }

    function mostrarNoti(mensaje) {
      if (Notification.permission === 'granted') {
        new Notification('💖 Corazón para ti', {
          body: mensaje,
          icon: 'https://cdn-icons-png.flaticon.com/512/833/833472.png'
        });
      }
    }

    function mostrarAhora() {
      mostrarNoti('Aquí está tu corazón ❤️');
    }

    function programar() {
      const segundos = parseInt(document.getElementById('segundos').value, 10);
      if (isNaN(segundos) || segundos <= 0) {
        alert('Introduce un número válido.');
        return;
      }
      alert(`Notificación programada para ${segundos} segundos...`);
      setTimeout(() => {
        mostrarNoti(`¡Aquí tienes tu ❤️ después de ${segundos} seg!`);
      }, segundos * 1000);
    }
  </script>

</body>
</html>
