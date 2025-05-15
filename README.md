# calculadora-descuentos
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Calculadora de Descuentos</title>
  <link rel="stylesheet" href="styles.css" />
  <link rel="manifest" href="manifest.json" />
</head>
<body>
  <main class="container">
    <h1>Calculadora de Ofertas y Descuentos</h1>
    
    <label>Precio unitario:
      <input type="number" id="precio" placeholder="Ej: 100">
    </label>

    <label>Cantidad:
      <input type="number" id="cantidad" placeholder="Ej: 3">
    </label>

    <label>Tipo de oferta:
      <select id="tipoOferta">
        <option value="descuento">Descuento (%)</option>
        <option value="2x1">2x1</option>
        <option value="3x2">3x2</option>
        <option value="porCantidad">Compra más y ahorra</option>
      </select>
    </label>

    <label id="descuentoLabel">Porcentaje de descuento:
      <input type="number" id="descuento" placeholder="Ej: 20">
    </label>

    <button onclick="calcular()">Calcular</button>

    <div class="resultado" id="resultado"></div>
  </main>

  <script src="app.js"></script>
</body>
</html>
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: #f0f8ff;
  color: #333;
}

.container {
  max-width: 500px;
  margin: auto;
  padding: 1em;
  background: #ffffff;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
  margin-top: 2em;
  border-radius: 8px;
}

h1 {
  text-align: center;
  color: #0077cc;
}

label {
  display: block;
  margin: 1em 0 0.5em;
}

input, select {
  width: 100%;
  padding: 0.5em;
  margin-bottom: 0.5em;
  border-radius: 4px;
  border: 1px solid #ccc;
}

button {
  width: 100%;
  background-color: #0077cc;
  color: white;
  padding: 1em;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1.1em;
}

button:hover {
  background-color: #005fa3;
}

.resultado {
  margin-top: 1em;
  padding: 1em;
  background-color: #e0f7fa;
  border-radius: 6px;
  text-align: center;
  font-weight: bold;
}
document.getElementById('tipoOferta').addEventListener('change', () => {
  const tipo = document.getElementById('tipoOferta').value;
  document.getElementById('descuentoLabel').style.display = (tipo === 'descuento') ? 'block' : 'none';
});

function calcular() {
  const precio = parseFloat(document.getElementById('precio').value);
  const cantidad = parseInt(document.getElementById('cantidad').value);
  const tipo = document.getElementById('tipoOferta').value;
  const descuento = parseFloat(document.getElementById('descuento').value) || 0;
  let total = 0;

  if (isNaN(precio) || isNaN(cantidad) || precio <= 0 || cantidad <= 0) {
    return mostrarResultado('Ingresa un precio y cantidad válidos');
  }

  switch (tipo) {
    case 'descuento':
      total = precio * cantidad * (1 - descuento / 100);
      break;
    case '2x1':
      total = precio * Math.ceil(cantidad / 2);
      break;
    case '3x2':
      total = precio * (cantidad - Math.floor(cantidad / 3));
      break;
    case 'porCantidad':
      if (cantidad >= 10) total = precio * cantidad * 0.8;
      else if (cantidad >= 5) total = precio * cantidad * 0.9;
      else total = precio * cantidad;
      break;
  }

  mostrarResultado(`Total: $${total.toFixed(2)}`);
}

function mostrarResultado(mensaje) {
  document.getElementById('resultado').textContent = mensaje;
{
  "name": "Calculadora de Descuentos",
  "short_name": "Descuentos",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#f0f8ff",
  "theme_color": "#0077cc",
  "icons": [
    {
      "src": "shopping-cart-192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "shopping-cart-512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}

self.addEventListener("install", (event) => {
  event.waitUntil(
    caches.open("app-cache-v1").then((cache) => {
      return cache.addAll([
        "/",
        "/index.html",
        "/styles.css",
        "/app.js",
        "/manifest.json",
        "/shopping-cart-192.png",
        "/shopping-cart-512.png"
      ]);
    })
  );
});

self.addEventListener("fetch", (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});


self.addEventListener("fetch", (e) => {
  e.respondWith(
    caches.match(e.request).then((response) => {
      return response || fetch(e.request);
    })
  );
});
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('service-worker.js')
    .then(() => console.log('Service Worker registrado'))
    .catch((error) => console.error('Error al registrar SW', error));
}
