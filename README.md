<!DOCTYPE html>
<html>
<head>
  <title>Material</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #3498db; /* Azul claro */
      margin: 0;
      padding: 0;
    }
    #lista-productos {
      width: 100%;
      height: 200px;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
      background-color: #fff; /* Blanco */
    }
    .producto {
      font-weight: bold;
      font-size: 18px;
      margin-bottom: 10px;
      color: #f1c40f; /* Amarillo claro */
    }
    .producto:hover {
      cursor: pointer;
      color: #ff9800; /* Naranja claro */
    }
    #copiar {
      position: absolute;
      top: 10px;
      right: 10px;
      background-color: #337ab7; /* Azul oscuro */
      color: #fff; /* Blanco */
      border: none;
      padding: 10px;
      font-size: 16px;
      cursor: pointer;
    }
    #copiar:hover {
      background-color: #23527c; /* Azul oscuro */
    }
    .container {
      width: 100%;
      padding: 20px;
      box-sizing: border-box;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1 style="text-align: center; margin-top: 20px; color: #fff;">Lista Materiales</h1>
<br>
Toca el producto tantas veces como desees agregar y si requieres algo que no este en la lista solo escribelo antes de copiar.
<br><br>
      <ul style="list-style: none; padding: 0; margin: 0;">
      <li class="producto" onclick="agregarProducto('Cinta Tape')">Cinta Tape</li>
      <li class="producto" onclick="agregarProducto('Solo')">Solo</li>
      <li class="producto" onclick="agregarProducto('Plastico Ventanas')">Plastico Ventanas</li>
      <li class="producto" onclick="agregarProducto('Plastico Piso')">Plastico Piso</li>
      <li class="producto" onclick="agregarProducto('Caulk Rosa')">Caulk Rosa</li>
      <li class="producto" onclick="agregarProducto('Caulk Rojo')">Caulk Rojo</li>
      <li class="producto" onclick="agregarProducto('Caulk Claro')">Caulk Claro</li>
      <li class="producto" onclick="agregarProducto('Potty')">Potty</li>
      <li class="producto" onclick="agregarProducto('Lija 120')">Lija 120</li>
      <li class="producto" onclick="agregarProducto('Lija 150')">Lija 150</li>
      <li class="producto" onclick="agregarProducto('Lija 180')">Lija 180</li>
    </ul>
    <div style="position: relative;">
      <textarea id="lista-productos">SE REQUIERE:</textarea>
      <button id="copiar" onclick="copiarContenido()">Copiar</button>
    </div>
  </div>

  <script>
    let productos = {};

    function agregarProducto(nombreProducto) {
      if (productos[nombreProducto]) {
        productos[nombreProducto]++;
      } else {
        productos[nombreProducto] = 1;
      }

      let lista = "SE REQUIERE:\n";
      for (let producto in productos) {
        lista += `${productos[producto]} ${producto}\n`;
      }

      document.getElementById('lista-productos').value = lista;
    }

    function copiarContenido() {
      let textarea = document.getElementById('lista-productos');
      textarea.select();
      document.execCommand('copy');
      alert('Contenido copiado al portapapeles');
    }
  </script>
</body>
</html>

