# LIBRERIA-AKY
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Librería AKY</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background: #f9f9f9; }
    header { text-align: center; padding: 20px; background: #4CAF50; color: white; }
    .product { background: white; padding: 20px; margin: 20px auto; max-width: 400px; border-radius: 12px; box-shadow: 0 2px 6px rgba(0,0,0,0.2); }
    .product img { max-width: 100%; border-radius: 12px; }
    button { background: #4CAF50; color: white; border: none; padding: 10px 15px; border-radius: 8px; cursor: pointer; }
    button:hover { background: #45a049; }
    #cart { background: white; padding: 20px; margin: 20px auto; max-width: 400px; border-radius: 12px; box-shadow: 0 2px 6px rgba(0,0,0,0.2); }
    select, input { width: 100%; padding: 8px; margin-top: 8px; border: 1px solid #ccc; border-radius: 8px; }
    .checkout { margin-top: 15px; display: flex; flex-direction: column; gap: 10px; }
    .checkout button { width: 100%; }
  </style>
</head>
<body>

<header>
  <h1>LIBRERÍA AKY</h1>
  <p>Los mejores precios más cerca de ti</p>
</header>

<section class="product">
  <img src="https://via.placeholder.com/400x300.png?text=Pañitos+Húmedos" alt="Pañitos Húmedos">
  <h2>Pañitos Húmedos</h2>
  <p><del>S/ 4.00</del> <strong>Oferta: S/ 2.00</strong></p>
  <button onclick="addToCart()">Agregar al carrito</button>
</section>

<section id="cart">
  <h2>🛒 Carrito</h2>
  <div id="cart-items"></div>
  <p><strong>Subtotal:</strong> S/ <span id="subtotal">0.00</span></p>

  <label for="distrito">Distrito de entrega</label>
  <select id="distrito" onchange="updateDelivery()">
    <option value="">-- Selecciona --</option>
    <option value="Nuevo Chimbote">Nuevo Chimbote (S/ 4.00)</option>
    <option value="Chimbote Centro">Chimbote Centro (S/ 6.00)</option>
    <option value="Otros distritos">Otros distritos (S/ 10.00)</option>
  </select>

  <label for="direccion">Dirección de entrega</label>
  <input type="text" id="direccion" placeholder="Ej. Av. Perú 123">

  <label for="referencia">Referencia</label>
  <input type="text" id="referencia" placeholder="Ej. Frente al parque">

  <p><strong>Costo delivery:</strong> S/ <span id="delivery">0.00</span></p>
  <p><strong>Total:</strong> S/ <span id="total">0.00</span></p>

  <div class="checkout">
    <button onclick="checkoutWhatsApp()">📲 Consultar por WhatsApp</button>
    <button onclick="checkoutMercadoPago()">💳 Pagar en línea (Mercado Pago)</button>
  </div>
</section>

<script>
  let cart = [];
  let deliveryCost = 0;

  function addToCart() {
    cart.push({ name: "Pañitos Húmedos", price: 2.00 });
    renderCart();
  }

  function renderCart() {
    let itemsHtml = "";
    let subtotal = 0;
    cart.forEach((item, i) => {
      itemsHtml += `<p>${item.name} - S/ ${item.price.toFixed(2)}</p>`;
      subtotal += item.price;
    });
    document.getElementById("cart-items").innerHTML = itemsHtml || "<p>Tu carrito está vacío</p>";
    document.getElementById("subtotal").innerText = subtotal.toFixed(2);
    updateDelivery();
  }

  function updateDelivery() {
    const distrito = document.getElementById("distrito").value;
    if (distrito === "Nuevo Chimbote") deliveryCost = 4;
    else if (distrito === "Chimbote Centro") deliveryCost = 6;
    else if (distrito === "Otros distritos") deliveryCost = 10;
    else deliveryCost = 0;

    const subtotal = parseFloat(document.getElementById("subtotal").innerText);
    document.getElementById("delivery").innerText = deliveryCost.toFixed(2);
    document.getElementById("total").innerText = (subtotal + deliveryCost).toFixed(2);
  }

  function checkoutWhatsApp() {
    const subtotal = document.getElementById("subtotal").innerText;
    const delivery = document.getElementById("delivery").innerText;
    const total = document.getElementById("total").innerText;
    const direccion = document.getElementById("direccion").value;
    const referencia = document.getElementById("referencia").value;
    const distrito = document.getElementById("distrito").value;

    let mensaje = `Hola, quiero hacer un pedido:%0A`;
    cart.forEach(item => {
      mensaje += `- ${item.name} S/ ${item.price.toFixed(2)}%0A`;
    });
    mensaje += `Subtotal: S/ ${subtotal}%0A`;
    mensaje += `Delivery (${distrito}): S/ ${delivery}%0A`;
    mensaje += `Total: S/ ${total}%0A`;
    mensaje += `Dirección: ${direccion}%0AReferencia: ${referencia}`;

    window.open(`https://wa.me/51918413584?text=${mensaje}`, "_blank");
  }

  function checkoutMercadoPago() {
    alert("Aquí iría la integración con Mercado Pago (requiere backend).");
  }
</script>

</body>
</html>
