<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Formulario Dinámico</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f1f5f9;
      padding: 30px;
    }
    .container {
      background: white;
      padding: 30px;
      border-radius: 10px;
      max-width: 600px;
      margin: auto;
      box-shadow: 0 5px 15px rgba(0,0,0,0.1);
    }
    .form-group {
      margin-bottom: 20px;
    }
    label {
      font-weight: bold;
      display: block;
      margin-bottom: 8px;
    }
    input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    .result {
      background: #eef2ff;
      padding: 15px;
      border-left: 5px solid #6366f1;
      border-radius: 5px;
      margin-top: 20px;
    }
    .error {
      background: #fee2e2;
      color: #b91c1c;
      border-left: 5px solid #dc2626;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Formulario Dinámico</h2>

    <!-- Nombre propio -->
    <div class="form-group">
      <label for="nombrePropio">Nombre Propio (solo corrige mayúsculas):</label>
      <input type="text" id="nombrePropio" oninput="capitalizarNombre()">
    </div>

    <!-- Mayúsculas -->
    <div class="form-group">
      <label for="mayusculas">Texto en MAYÚSCULAS:</label>
      <input type="text" id="mayusculas" oninput="convertirMayusculas()">
    </div>

    <!-- Minúsculas -->
    <div class="form-group">
      <label for="minusculas">Texto en minúsculas:</label>
      <input type="text" id="minusculas" oninput="convertirMinusculas()">
    </div>

    <!-- Campo valor COP -->
    <div class="form-group">
      <label for="valorCop">Valor en $COP:</label>
      <input type="text" id="valorCop" placeholder="$1.500.000" oninput="validarValor()">
    </div>

    <!-- Resultados -->
    <div id="resultados" class="result" style="display: none;"></div>
  </div>

  <script>
    function capitalizarNombre() {
      const input = document.getElementById("nombrePropio");
      const palabras = input.value.split(" ");
      const resultado = palabras.map(p =>
        p.charAt(0).toUpperCase() + p.slice(1).toLowerCase()
      ).join(" ");
      input.value = resultado;
    }

    function convertirMayusculas() {
      const input = document.getElementById("mayusculas");
      input.value = input.value.toUpperCase();
    }

    function convertirMinusculas() {
      const input = document.getElementById("minusculas");
      input.value = input.value.toLowerCase();
    }

    function limpiarNumero(valor) {
      return parseFloat(valor.replace(/[^0-9]/g, ""));
    }

    function formatearCOP(valor) {
      return "$" + valor.toLocaleString("es-CO");
    }

    function validarValor() {
      const input = document.getElementById("valorCop");
      const output = document.getElementById("resultados");

      const valor = limpiarNumero(input.value);
      if (isNaN(valor)) {
        output.style.display = "none";
        return;
      }

      input.value = formatearCOP(valor);

      const LIMITE = 1207762;
      const MIN_CUOTA = 241542;

      if (valor <= LIMITE) {
        output.innerHTML = `<p><strong>❌ No es posible hacer acuerdo de pago.</strong></p>`;
        output.className = "result error";
        output.style.display = "block";
      } else {
        const cuotaInicial = Math.round(valor * 0.4);
        const saldoPendiente = Math.round(valor * 0.6);
        const cuotas = Math.floor(saldoPendiente / MIN_CUOTA);
        const cuotaMensual = Math.floor(saldoPendiente / cuotas);

        output.innerHTML = `
          <p><strong>✅ Cuota inicial (40%):</strong> ${formatearCOP(cuotaInicial)}</p>
          <p><strong>Saldo pendiente a diferir (60%):</strong> ${formatearCOP(saldoPendiente)}</p>
          <p><strong>Cantidad de cuotas (mínimo ${formatearCOP(MIN_CUOTA)} por cuota):</strong> ${cuotas}</p>
          <p><strong>Valor por cuota:</strong> ${formatearCOP(cuotaMensual)}</p>
        `;
        output.className = "result";
        output.style.display = "block";
      }
    }
  </script>
</body>
</html>
