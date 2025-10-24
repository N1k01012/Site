<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Print Studio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif;
            background: #0a0a0a;
            color: #e0e0e0;
            line-height: 1.6;
        }

        header {
            background: #000;
            padding: 1.5rem 2rem;
            border-bottom: 1px solid #222;
            position: sticky;
            top: 0;
            z-index: 100;
        }

        .header-content {
            max-width: 1400px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        h1 {
            font-size: 1.5rem;
            font-weight: 600;
            letter-spacing: -0.5px;
        }

        .cart-btn {
            background: #fff;
            color: #000;
            border: none;
            padding: 0.6rem 1.2rem;
            cursor: pointer;
            font-size: 0.95rem;
            font-weight: 500;
            transition: background 0.2s;
        }

        .cart-btn:hover {
            background: #ddd;
        }

        .cart-count {
            background: #000;
            color: #fff;
            padding: 0.15rem 0.5rem;
            margin-left: 0.5rem;
            font-size: 0.85rem;
        }

        main {
            max-width: 1400px;
            margin: 0 auto;
            padding: 3rem 2rem;
        }

        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
            gap: 2rem;
            margin-top: 2rem;
        }

        .product-card {
            background: #111;
            border: 1px solid #222;
            overflow: hidden;
            transition: border-color 0.2s;
        }

        .product-card:hover {
            border-color: #444;
        }

        .product-image {
            width: 100%;
            height: 280px;
            background: #1a1a1a;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 3rem;
            color: #333;
        }

        .product-info {
            padding: 1.5rem;
        }

        .product-name {
            font-size: 1.1rem;
            font-weight: 500;
            margin-bottom: 0.5rem;
        }

        .product-description {
            color: #999;
            font-size: 0.9rem;
            margin-bottom: 1rem;
            line-height: 1.5;
        }

        .product-price {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 1rem;
        }

        .add-to-cart {
            width: 100%;
            background: #fff;
            color: #000;
            border: none;
            padding: 0.8rem;
            cursor: pointer;
            font-size: 0.95rem;
            font-weight: 500;
            transition: background 0.2s;
        }

        .add-to-cart:hover {
            background: #ddd;
        }

        .cart-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.9);
            z-index: 200;
            align-items: center;
            justify-content: center;
            padding: 2rem;
        }

        .cart-modal.active {
            display: flex;
        }

        .cart-content {
            background: #111;
            border: 1px solid #222;
            max-width: 700px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .cart-header {
            padding: 1.5rem;
            border-bottom: 1px solid #222;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .close-cart {
            background: none;
            border: none;
            color: #fff;
            font-size: 1.5rem;
            cursor: pointer;
            padding: 0;
            line-height: 1;
        }

        .cart-items {
            padding: 1.5rem;
        }

        .cart-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
            border-bottom: 1px solid #222;
        }

        .cart-item:last-child {
            border-bottom: none;
        }

        .item-info h3 {
            font-size: 1rem;
            font-weight: 500;
            margin-bottom: 0.3rem;
        }

        .item-info p {
            color: #999;
            font-size: 0.9rem;
        }

        .item-controls {
            display: flex;
            align-items: center;
            gap: 1rem;
        }

        .quantity-controls {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .qty-btn {
            background: #222;
            color: #fff;
            border: none;
            width: 28px;
            height: 28px;
            cursor: pointer;
            font-size: 1rem;
        }

        .qty-btn:hover {
            background: #333;
        }

        .quantity {
            min-width: 30px;
            text-align: center;
        }

        .remove-btn {
            background: none;
            border: none;
            color: #999;
            cursor: pointer;
            font-size: 0.9rem;
            text-decoration: underline;
        }

        .remove-btn:hover {
            color: #fff;
        }

        .cart-footer {
            padding: 1.5rem;
            border-top: 1px solid #222;
        }

        .cart-total {
            display: flex;
            justify-content: space-between;
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 1.5rem;
        }

        .checkout-btn {
            width: 100%;
            background: #fff;
            color: #000;
            border: none;
            padding: 1rem;
            cursor: pointer;
            font-size: 1rem;
            font-weight: 600;
            transition: background 0.2s;
        }

        .checkout-btn:hover {
            background: #ddd;
        }

        .checkout-btn:disabled {
            background: #333;
            color: #666;
            cursor: not-allowed;
        }

        .empty-cart {
            text-align: center;
            padding: 3rem 1.5rem;
            color: #666;
        }

        .order-form {
            display: none;
        }

        .order-form.active {
            display: block;
            padding: 1.5rem;
        }

        .form-group {
            margin-bottom: 1.2rem;
        }

        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-size: 0.9rem;
            color: #999;
        }

        .form-group input,
        .form-group textarea {
            width: 100%;
            background: #0a0a0a;
            border: 1px solid #222;
            color: #fff;
            padding: 0.8rem;
            font-size: 0.95rem;
            font-family: inherit;
        }

        .form-group input:focus,
        .form-group textarea:focus {
            outline: none;
            border-color: #444;
        }

        .form-group textarea {
            resize: vertical;
            min-height: 80px;
        }

        .form-actions {
            display: flex;
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .btn-secondary {
            flex: 1;
            background: #222;
            color: #fff;
            border: none;
            padding: 1rem;
            cursor: pointer;
            font-size: 0.95rem;
            font-weight: 500;
        }

        .btn-secondary:hover {
            background: #333;
        }

        .order-success {
            display: none;
            padding: 3rem 1.5rem;
            text-align: center;
        }

        .order-success.active {
            display: block;
        }

        .order-success h2 {
            margin-bottom: 1rem;
        }

        .order-success p {
            color: #999;
            margin-bottom: 1.5rem;
        }

        .order-number {
            background: #0a0a0a;
            padding: 1rem;
            margin: 1.5rem 0;
            font-family: monospace;
            font-size: 1.1rem;
        }

        footer {
            background: #000;
            padding: 1.5rem 2rem;
            text-align: center;
            border-top: 1px solid #222;
            margin-top: 4rem;
        }

        .credit {
            color: #666;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <header>
        <div class="header-content">
            <h1>3D Print Studio</h1>
            <button class="cart-btn" onclick="toggleCart()">
                Cart <span class="cart-count">0</span>
            </button>
        </div>
    </header>

    <main>
        <div class="products-grid" id="productsGrid"></div>
    </main>

    <div class="cart-modal" id="cartModal">
        <div class="cart-content">
            <div class="cart-header">
                <h2>Your Order</h2>
                <button class="close-cart" onclick="toggleCart()">×</button>
            </div>
            
            <div id="cartView">
                <div class="cart-items" id="cartItems"></div>
                <div class="cart-footer">
                    <div class="cart-total">
                        <span>Total</span>
                        <span id="cartTotal">$0.00</span>
                    </div>
                    <button class="checkout-btn" id="checkoutBtn" onclick="showOrderForm()">Place Order</button>
                </div>
            </div>

            <div class="order-form" id="orderForm">
                <form id="customerForm" onsubmit="submitOrder(event)">
                    <div class="form-group">
                        <label>Full Name</label>
                        <input type="text" name="name" required>
                    </div>
                    <div class="form-group">
                        <label>Phone Number</label>
                        <input type="tel" name="phone" required>
                    </div>
                    <div class="form-group">
                        <label>Email</label>
                        <input type="email" name="email" required>
                    </div>
                    <div class="form-group">
                        <label>Additional Notes</label>
                        <textarea name="notes" placeholder="Pickup time preferences, special requests, etc."></textarea>
                    </div>
                    <div class="form-actions">
                        <button type="button" class="btn-secondary" onclick="hideOrderForm()">Back</button>
                        <button type="submit" class="checkout-btn">Confirm Order</button>
                    </div>
                </form>
            </div>

            <div class="order-success" id="orderSuccess">
                <h2>Order Confirmed</h2>
                <p>Your order has been received. Please bring the following order number when picking up.</p>
                <div class="order-number" id="orderNumber"></div>
                <p>Payment due at pickup: <strong id="orderAmount"></strong> (Cash only)</p>
                <button class="checkout-btn" onclick="closeOrderSuccess()">Done</button>
            </div>
        </div>
    </div>

    <footer>
        <p class="credit">Visit us at <strong>3dprintcrhs.gt.tc</strong> | Payment due at pickup (Cash only)</p>
        <p class="credit" style="margin-top: 0.5rem;">Made by N1k0</p>
    </footer>

    <script>
        // EDIT YOUR PRODUCTS HERE
        const products = [
            {
                id: 1,
                name: "Custom 3D Print",
                price: 45.00,
                description: "High quality PLA print up to 15cm. Bring your own STL file or choose from our designs."
            },
            {
                id: 2,
                name: "Miniature Figures Set",
                price: 28.00,
                description: "Pack of 5 detailed miniature figures. Perfect for tabletop games and collections."
            },
            {
                id: 3,
                name: "Phone Stand",
                price: 12.00,
                description: "Minimalist phone stand with adjustable angle. Available in multiple colors."
            },
            {
                id: 4,
                name: "Keychain Collection",
                price: 8.00,
                description: "Set of 3 custom keychains. Choose your designs or create your own."
            },
            {
                id: 5,
                name: "Desk Organizer",
                price: 35.00,
                description: "Modular desk organizer with compartments for pens, cables, and office supplies."
            },
            {
                id: 6,
                name: "Plant Pot",
                price: 18.00,
                description: "Geometric plant pot with drainage. Modern design for small to medium plants."
            }
        ];

        let cart = [];

        function renderProducts() {
            const grid = document.getElementById('productsGrid');
            grid.innerHTML = products.map(product => `
                <div class="product-card">
                    <div class="product-image">${product.id}</div>
                    <div class="product-info">
                        <h3 class="product-name">${product.name}</h3>
                        <p class="product-description">${product.description}</p>
                        <div class="product-price">$${product.price.toFixed(2)}</div>
                        <button class="add-to-cart" onclick="addToCart(${product.id})">Add to Cart</button>
                    </div>
                </div>
            `).join('');
        }

        function addToCart(productId) {
            const product = products.find(p => p.id === productId);
            const existing = cart.find(item => item.id === productId);
            
            if (existing) {
                existing.quantity++;
            } else {
                cart.push({ ...product, quantity: 1 });
            }
            
            updateCart();
        }

        function updateQuantity(productId, change) {
            const item = cart.find(i => i.id === productId);
            if (item) {
                item.quantity += change;
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    updateCart();
                }
            }
        }

        function removeFromCart(productId) {
            cart = cart.filter(item => item.id !== productId);
            updateCart();
        }

        function updateCart() {
            const cartCount = document.querySelector('.cart-count');
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.textContent = totalItems;
            
            renderCart();
        }

        function renderCart() {
            const cartItems = document.getElementById('cartItems');
            const cartTotal = document.getElementById('cartTotal');
            const checkoutBtn = document.getElementById('checkoutBtn');
            
            if (cart.length === 0) {
                cartItems.innerHTML = '<div class="empty-cart">Your cart is empty</div>';
                cartTotal.textContent = '$0.00';
                checkoutBtn.disabled = true;
                return;
            }
            
            checkoutBtn.disabled = false;
            
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            
            cartItems.innerHTML = cart.map(item => `
                <div class="cart-item">
                    <div class="item-info">
                        <h3>${item.name}</h3>
                        <p>$${item.price.toFixed(2)} each</p>
                    </div>
                    <div class="item-controls">
                        <div class="quantity-controls">
                            <button class="qty-btn" onclick="updateQuantity(${item.id}, -1)">-</button>
                            <span class="quantity">${item.quantity}</span>
                            <button class="qty-btn" onclick="updateQuantity(${item.id}, 1)">+</button>
                        </div>
                        <button class="remove-btn" onclick="removeFromCart(${item.id})">Remove</button>
                    </div>
                </div>
            `).join('');
            
            cartTotal.textContent = `$${total.toFixed(2)}`;
        }

        function toggleCart() {
            const modal = document.getElementById('cartModal');
            modal.classList.toggle('active');
            if (!modal.classList.contains('active')) {
                hideOrderForm();
                document.getElementById('orderSuccess').classList.remove('active');
                document.getElementById('cartView').style.display = 'block';
            }
        }

        function showOrderForm() {
            document.getElementById('cartView').style.display = 'none';
            document.getElementById('orderForm').classList.add('active');
        }

        function hideOrderForm() {
            document.getElementById('orderForm').classList.remove('active');
            document.getElementById('cartView').style.display = 'block';
        }

        function submitOrder(e) {
            e.preventDefault();
            
            const formData = new FormData(e.target);
            const orderNumber = 'ORD' + Date.now().toString().slice(-8);
            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            
            // Here you would typically send this data to a server
            // For now, we'll just show the success message
            
            document.getElementById('orderForm').classList.remove('active');
            document.getElementById('orderNumber').textContent = orderNumber;
            document.getElementById('orderAmount').textContent = `$${total.toFixed(2)}`;
            document.getElementById('orderSuccess').classList.add('active');
            
            console.log('Order placed:', {
                orderNumber,
                customer: Object.fromEntries(formData),
                items: cart,
                total
            });
        }

        function closeOrderSuccess() {
            cart = [];
            updateCart();
            toggleCart();
            document.getElementById('customerForm').reset();
        }

        // Initialize the page
        renderProducts();
    </script>
</body>
</html>
