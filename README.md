<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>"Venta de Pasteles Carlos"</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #f8b400;
            padding: 15px;
            text-align: center;
            color: white;
            font-size: 24px;
        }
        .container {
            padding: 20px;
            max-width: 1000px;
            margin: 0 auto;
        }
        .products {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: space-around;
        }
        .product {
            background-color: white;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            width: 30%;
            text-align: center;
            box-sizing: border-box;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .product h3 {
            color: #333;
        }
        .product button {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }
        .product button:hover {
            background-color: #45a049;
        }
        .cart {
            background-color: white;
            padding: 15px;
            margin-top: 20px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        .cart h2 {
            color: #333;
        }
        .cart ul {
            list-style-type: none;
            padding: 0;
        }
        .cart ul li {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }
        .cart button {
            background-color: #f8b400;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin-top: 10px;
        }
        .cart button:hover {
            background-color: #e7a100;
        }
        .promo-code {
            margin-top: 20px;
            text-align: center;
        }
        .promo-code input {
            padding: 8px;
            font-size: 16px;
            width: 200px;
            margin-right: 10px;
            border-radius: 5px;
        }
        .promo-code button {
            background-color: #ff5722;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .promo-code button:hover {
            background-color: #e64a19;
        }
        .checkout {
            margin-top: 30px;
            padding: 15px;
            background-color: #ff9800;
            color: white;
            font-size: 20px;
            text-align: center;
        }
        .checkout button {
            background-color: #4CAF50;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<header>
    Venta de Pasteles Carlos
</header>

<div class="container">
    <!-- Catálogo de productos -->
    <section class="products">
        <div class="product">
            <h3>Pastel de Chocolate</h3>
            <p>Código: PASTEL01</p>
            <p>Precio: S/20</p>
            <img src="https://content-cocina.lecturas.com/medio/2023/03/23/el-mejor-pastel-de-chocolate_24bd9cda_1200x1200.jpg" width="150px" height="150px">
            <button onclick="addToCart('PASTEL01', 'Pastel de Chocolate', 20)">Agregar al carrito</button>
        </div>
        <div class="product">
            <h3>Pastel de Vainilla</h3>
            <p>Código: PASTEL02</p>
            <p>Precio: S/18</p>
            <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcThO97LbMaovL7s02wSL9xUAw-pYAi9zss-Dw&s" width="150px" height="150px">
            <button onclick="addToCart('PASTEL02', 'Pastel de Vainilla', 18)">Agregar al carrito</button>
        </div>
        <div class="product">
            <h3>Pastel Red Velvet</h3>
            <p>Código: PASTEL03</p>
            <p>Precio: S/25</p>
             <img src="https://blog.marianlaquecocina.com/wp-content/uploads/2019/02/20190208_170242-e15498121382011.jpg" width="150px" height="150px">
            <button onclick="addToCart('PASTEL03', 'Pastel Red Velvet', 25)">Agregar al carrito</button>
        </div>
    </section>

    <!-- Carrito de compras -->
    <section class="cart">
        <h2>Tu Carrito</h2>
        <ul id="cart-items"></ul>
        <p id="total">Total: $0</p>
    </section>

    <!-- Código promocional -->
    <section class="promo-code">
        <input type="text" id="promo-code" placeholder="Código promocional">
        <button onclick="applyPromo()">Aplicar Código</button>
    </section>

    <!-- Checkout -->
    <section class="checkout">
        <button onclick="checkout()">Finalizar Compra</button>
    </section>
</div>

<script>
    let cart = [];
    let total = 0;

    // Función para agregar productos al carrito
    function addToCart(code, name, price) {
        cart.push({ code, name, price });
        total += price;
        updateCart();
    }

    // Función para actualizar el carrito
    function updateCart() {
        const cartItems = document.getElementById('cart-items');
        cartItems.innerHTML = '';
        cart.forEach(item => {
            const li = document.createElement('li');
            li.textContent = `${item.name} - $${item.price}`;
            cartItems.appendChild(li);
        });
        document.getElementById('total').textContent = `Total: $${total}`;
    }

    // Función para aplicar el código promocional
    function applyPromo() {
        const promoCode = document.getElementById('promo-code').value;
        if (promoCode === 'DESCUENTO10') {
            total *= 0.9; // Aplica un 10% de descuento
            alert('¡Descuento aplicado!');
            updateCart();
        } else {
            alert('Código promocional inválido');
        }
    }

    // Función para finalizar la compra
    function checkout() {
        if (cart.length > 0) {
            alert(`Pedido realizado con éxito. Total: $${total}`);
            cart = [];
            total = 0;
            updateCart();
        } else {
            alert('Tu carrito está vacío. Agrega productos antes de proceder.');
        }
    }
</script>

</body>
</html>
