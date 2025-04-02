<!DOCTYPE html><html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Магазин кофе</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .product { display: inline-block; margin: 20px; padding: 10px; border: 1px solid #ddd; }
        .cart { margin-top: 20px; }
        .admin { margin-top: 20px; }
    </style>
</head>
<body>
    <h1>Интернет-магазин кофе</h1>
    <div id="products">
        <div class="product" data-name="Эспрессо" data-price="5">
            <h3>Эспрессо</h3>
            <p>Цена: <span class="price">$5</span></p>
            <button onclick="addToCart(this)">Добавить в корзину</button>
        </div>
        <div class="product" data-name="Латте" data-price="6">
            <h3>Латте</h3>
            <p>Цена: <span class="price">$6</span></p>
            <button onclick="addToCart(this)">Добавить в корзину</button>
        </div>
    </div><h2>Корзина</h2>
<div id="cart" class="cart"></div>
<h2>Оформление заказа</h2>
<form id="orderForm">
    <input type="text" id="phone" placeholder="Введите ваш номер телефона" required>
    <button type="submit">Заказать</button>
</form>

<h2>Админ-панель</h2>
<div class="admin">
    <input type="text" id="productName" placeholder="Название кофе">
    <input type="number" id="productPrice" placeholder="Цена">
    <button onclick="addProduct()">Добавить товар</button>
</div>

<script>
    let cart = [];

    function addToCart(button) {
        let product = button.parentElement;
        let name = product.getAttribute('data-name');
        let price = product.getAttribute('data-price');
        cart.push({ name, price });
        updateCart();
    }

    function updateCart() {
        let cartDiv = document.getElementById('cart');
        cartDiv.innerHTML = cart.map(item => <p>${item.name} - $${item.price}</p>).join('');
    }

    document.getElementById('orderForm').addEventListener('submit', function(event) {
        event.preventDefault();
        let phone = document.getElementById('phone').value;
        alert(Заказ оформлен! Телефон: ${phone});
    });

    function addProduct() {
        let name = document.getElementById('productName').value;
        let price = document.getElementById('productPrice').value;
        if (name && price) {
            let productDiv = document.createElement('div');
            productDiv.classList.add('product');
            productDiv.setAttribute('data-name', name);
            productDiv.setAttribute('data-price', price);
            productDiv.innerHTML = <h3>${name}</h3><p>Цена: <span class='price'>$${price}</span></p><button onclick='addToCart(this)'>Добавить в корзину</button>;
            document.getElementById('products').appendChild(productDiv);
        }
    }
</script>

</body>
</html>
