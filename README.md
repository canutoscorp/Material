<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista de Productos</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            text-align: center;
        }
        .container {
            width: 90%;
            max-width: 400px;
            margin: auto;
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
        }
        h3 {
            color: #333;
            font-size: 18px;
        }
        .producto {
            cursor: pointer;
            padding: 10px;
            margin: 5px;
            background: #007bff;
            color: white;
            display: block;
            border-radius: 5px;
            font-weight: bold;
            transition: 0.3s;
            font-size: 16px;
        }
        .producto:hover {
            background: #0056b3;
        }
        .lista {
            background: #fff3cd;
            color: #856404;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ffeeba;
            min-height: 60px;
            text-align: left;
            font-size: 16px;
            overflow-y: auto;
            max-height: 150px;
        }
        .cantidad {
            font-weight: bold;
            color: #d9534f;
        }
        input {
            width: calc(100% - 20px);
            padding: 10px;
            margin-top: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        button {
            background: #28a745;
            color: white;
            border: none;
            padding: 12px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px;
            width: 100%;
            margin-top: 10px;
        }
        button:hover {
            background: #218838;
        }
        .mensaje-adicional {
            font-size: 14px;
            color: #555;
            margin-top: 20px;
            text-align: center;
            font-weight: bold;
        }
    </style>
</head>
<body>

    <div class="container">
        <h3>Selecciona los productos:</h3>
        <div id="productos-container"></div>

        <h3>Otros productos:</h3>
        <input type="text" id="productoPersonalizado" placeholder="Escribe un producto y presiona Enter">
        
        <h3>Lista de selección:</h3>
        <div class="lista" id="listaProductos">Se requiere:</div>
        
        <button onclick="copiarYEnviar()">Copiar y Enviar a WhatsApp</button>

        <p class="mensaje-adicional">Si la persona a cargo no se encuentra disponible, copia el pedido para enviarlo a la persona asignada temporalmente. Gracias.</p>
        <button onclick="copiarPedido()">Copiar pedido</button>
    </div>

    <script>
        // Lista de productos predefinidos
        const productos = ["Potty", "Caulk Rojo", "Caulk Rosa", "Caulk Azul", "Caulk Clear", "Cinta Tape", "Solo", 
                           "Plastico Ventanas", "Plastico Piso", "Musket Brown", "Tricorn Black", "Tuxedo", "Beige", 
                           "Pintura Piso", "Lija 120", "Lija 150", "Lija 180"];

        // Objeto para almacenar cantidades
        let carrito = {};

        // Obtener contenedor de productos
        const contenedor = document.getElementById("productos-container");

        // Generar botones de productos
        productos.forEach(producto => {
            let btn = document.createElement("div");
            btn.className = "producto";
            btn.textContent = producto;
            btn.onclick = () => agregarProducto(producto);
            contenedor.appendChild(btn);
        });

        // Agregar productos al cuadro de texto
        function agregarProducto(nombre) {
            if (carrito[nombre]) {
                carrito[nombre]++;  // Aumenta la cantidad si ya está agregado
            } else {
                carrito[nombre] = 1; // Agrega el producto por primera vez
            }
            actualizarLista();
        }

        // Agregar productos personalizados
        document.getElementById("productoPersonalizado").addEventListener("keypress", function(event) {
            if (event.key === "Enter") {
                let nombre = this.value.trim();
                if (nombre) {
                    agregarProducto(nombre);
                    this.value = ""; // Limpiar input
                }
            }
        });

        // Actualizar cuadro de texto con los productos y cantidades
        function actualizarLista() {
            let lista = "<strong>Se requiere:</strong><br>";
            for (let producto in carrito) {
                lista += `<span class="cantidad">${carrito[producto]}</span> - ${producto}<br>`;
            }
            document.getElementById("listaProductos").innerHTML = lista;
        }

        // Función para copiar solo el pedido sin enviarlo a WhatsApp
        function copiarPedido() {
            let mensaje = "Se requiere:\n";
            for (let producto in carrito) {
                mensaje += `${carrito[producto]} - ${producto}\n`;
            }

            if (mensaje.trim() === "Se requiere:\n") {
                alert("Agrega productos antes de copiar.");
                return;
            }

            // Copiar al portapapeles
            let tempInput = document.createElement("textarea");
            tempInput.value = mensaje;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand("copy");
            document.body.removeChild(tempInput);

            alert("Pedido copiado al portapapeles.");
        }

        // Función para copiar y enviar a WhatsApp
        function copiarYEnviar() {
            let mensaje = "Se requiere:\n";
            for (let producto in carrito) {
                mensaje += `${carrito[producto]} - ${producto}\n`;
            }

            if (mensaje.trim() === "Se requiere:\n") {
                alert("Agrega productos antes de enviar.");
                return;
            }

            // Copiar al portapapeles
            let tempInput = document.createElement("textarea");
            tempInput.value = mensaje;
            document.body.appendChild(tempInput);
            tempInput.select();
            document.execCommand("copy");
            document.body.removeChild(tempInput);

            // Número de WhatsApp
            let numeroWhatsApp = "12512562787"; // Número con código de país sin '+'

            // Enviar a WhatsApp
            let url = `https://wa.me/${numeroWhatsApp}?text=${encodeURIComponent(mensaje)}`;
            window.location.href = url;
        }
    </script>

</body>
</html>
