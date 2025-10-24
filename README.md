<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>FurnitureFlow - Shop & Checkout</title>
<style>
  body {
    font-family: "Poppins", sans-serif;
    margin: 0;
    background: #f8f8f8;
    color: #333;
  }
  header {
    background: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 30px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    position: sticky;
    top: 0;
    z-index: 10;
  }
  header img.logo {
    height: 40px;
  }
  header h1 {
    font-size: 22px;
    margin: 0;
  }
  header nav span {
    cursor: pointer;
    background: #ff6347;
    color: #fff;
    padding: 6px 14px;
    border-radius: 20px;
    transition: 0.3s;
  }
  header nav span:hover {
    background: #e5533b;
  }
  main {
    padding: 20px;
  }

  /* 🔍 Search + Filter bar */
  .filter-bar {
    position: sticky;
    top: 70px;
    background: #fff;
    z-index: 9;
    padding: 10px 20px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    border-radius: 10px;
    margin-bottom: 20px;
  }
  #searchBar {
    width: 50%;
    padding: 10px 15px;
    border-radius: 20px;
    border: 1px solid #ccc;
    font-size: 16px;
    outline: none;
  }
  .price-filter {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .price-filter input {
    width: 100px;
    padding: 6px;
    border-radius: 6px;
    border: 1px solid #ccc;
  }
  .price-filter button {
    background: #ff6347;
    color: #fff;
    border: none;
    border-radius: 6px;
    padding: 6px 10px;
    cursor: pointer;
    transition: 0.3s;
  }
  .price-filter button:hover {
    background: #e5533b;
  }

  .vendor-section {
    margin-bottom: 40px;
  }
  .vendor-section h2 {
    border-left: 5px solid #ff6347;
    padding-left: 10px;
  }
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 20px;
  }
  .card {
    background: #fff;
    border-radius: 10px;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
    padding: 15px;
    text-align: center;
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 10px rgba(0,0,0,0.15);
  }
  .card img {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 8px;
  }
  .card h3 {
    margin: 10px 0 5px;
  }
  .card p {
    margin: 0;
    color: #777;
  }
  .btn {
    background: #ff6347;
    border: none;
    color: #fff;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    margin-top: 8px;
  }
  .btn:disabled {
    opacity: 0.6;
  }

  #cartOverlay {
    position: fixed;
    right: 0;
    top: 0;
    background: #fff;
    width: 350px;
    height: 100%;
    box-shadow: -4px 0 10px rgba(0,0,0,0.3);
    transform: translateX(100%);
    transition: 0.3s;
    padding: 20px;
    z-index: 50;
    overflow-y: auto;
  }
  #cartOverlay.active {
    transform: translateX(0);
  }
  #cartOverlay h2 {
    margin-top: 0;
  }
  .cart-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
    border-bottom: 1px solid #eee;
    padding-bottom: 5px;
  }
  .qty-btn {
    padding: 4px 10px;
    border: 1px solid #ccc;
    cursor: pointer;
    border-radius: 4px;
    background: #f0f0f0;
  }
  .back-btn {
    background: #ccc;
    border: none;
    color: #333;
    padding: 8px 14px;
    border-radius: 6px;
    cursor: pointer;
    margin-top: 10px;
    width: 100%;
  }
  .back-btn:hover {
    background: #bdbdbd;
  }

  .checkout-section {
    display: none;
    padding: 30px;
    text-align: center;
  }
  #qrcode {
    margin: 20px auto;
  }
  .action-btns button {
    margin: 10px;
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
  }
  .pay {
    background: #28a745;
    color: #fff;
  }
  .cancel {
    background: #ccc;
  }
</style>
</head>
<body>

<header>
  <div class="logo-box">
    <img src="https://1000logos.net/wp-content/uploads/2016/10/Amazon-Logo.png" alt="FurnitureFlow" class="logo">
  </div>
  <h1>FurnitureFlow</h1>
  <nav><span id="cartBtn">Cart (<span id="cartCount">0</span>)</span></nav>
</header>

<!-- 🔍 Search + Filter Bar -->
<div class="filter-bar">
  <input type="text" id="searchBar" placeholder="Search for furniture or vendor...">
  <div class="price-filter">
    <label>Price:</label>
    <input type="number" id="minPrice" placeholder="Min ₹" min="0">
    <input type="number" id="maxPrice" placeholder="Max ₹" min="0">
    <button onclick="applyPriceFilter()">Filter</button>
  </div>
</div>

<main id="shopPage">
  <!-- 🪑 All Vendor Sections Restored -->
  <div class="vendor-section">
    <h2>Naina Furniture</h2>
    <div class="product-grid">
      <div class="card">
        <img src="https://images.unsplash.com/photo-1586023492125-27b2c045efd7" alt="Chair">
        <h3>Wooden Chair</h3>
        <p>₹2500</p>
        <button class="btn" onclick="addToCart('Wooden Chair',2500)">Add to Cart</button>
      </div>
      <div class="card">
        <img src="https://encrypted-tbn3.gstatic.com/shopping?q=tbn:ANd9GcRa-xw75PyuTBpzzb-iT8xoX7lm45N6Q5V_g9nMD2qmsrLJpaz_lnai6inWSXtM-Gzwiw1-EY638S14y8fIp2Q36O-1_qUC6STtN5l0HKucXOwOgkfabZ_r" alt="Table">
        <h3>Coffee Table</h3>
        <p>₹4500</p>
        <button class="btn" onclick="addToCart('Coffee Table',4500)">Add to Cart</button>
      </div>
    </div>
  </div>

  <div class="vendor-section">
    <h2>Goyal Furniture House (Dhakoli, Zirakpur)</h2>
    <div class="product-grid">
      <div class="card">
        <img src="https://m.media-amazon.com/images/I/81JpcjgMsUL.AC_UF894,1000_QL80.jpg" alt="Sofa">
        <h3>3-Seater Sofa</h3>
        <p>₹12000</p>
        <button class="btn" onclick="addToCart('3-Seater Sofa',12000)">Add to Cart</button>
      </div>
      <div class="card">
        <img src="https://m.media-amazon.com/images/I/715PNlll8lL.AC_UF894,1000_QL80.jpg" alt="Bed">
        <h3>King Size Bed</h3>
        <p>₹22000</p>
        <button class="btn" onclick="addToCart('King Size Bed',22000)">Add to Cart</button>
      </div>
    </div>
  </div>

  <div class="vendor-section">
    <h2>Royal Furniture & Decorators (Baltana)</h2>
    <div class="product-grid">
      <div class="card">
        <img src="https://images.woodenstreet.de/image/cache/data/wardrobes-mdf/zyra-4-door-wardrobe-without-mirror-gothic-grey-classic-oak-finish/new-logo/1-810x702.jpg" alt="Wardrobe">
        <h3>Modern Wardrobe</h3>
        <p>₹18000</p>
        <button class="btn" onclick="addToCart('Modern Wardrobe',18000)">Add to Cart</button>
      </div>
      <div class="card">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSzCUKGnZYtuqcDyt5CfYb1Qix0oWVY3gJn_g&s" alt="Dining Set">
        <h3>Dining Table Set</h3>
        <p>₹25000</p>
        <button class="btn" onclick="addToCart('Dining Table Set',25000)">Add to Cart</button>
      </div>
    </div>
  </div>

  <div class="vendor-section">
    <h2>Kapoor Furniture House</h2>
    <div class="product-grid">
      <div class="card">
        <img src="https://m.media-amazon.com/images/I/71ClGjocCKL.AC_UF894,1000_QL80.jpg" alt="Office Chair">
        <h3>Office Chair</h3>
        <p>₹7500</p>
        <button class="btn" onclick="addToCart('Office Chair',7500)">Add to Cart</button>
      </div>
      <div class="card">
        <img src="https://pritihome.com/wp-content/uploads/2024/03/1-18-1.webp" alt="Bookshelf">
        <h3>Bookshelf</h3>
        <p>₹6800</p>
        <button class="btn" onclick="addToCart('Bookshelf',6800)">Add to Cart</button>
      </div>
    </div>
  </div>
</main>

<div id="cartOverlay">
  <h2>Your Cart</h2>
  <div id="cartItems"></div>
  <h3>Total: ₹<span id="totalPrice">0</span></h3>
  <button class="btn" onclick="goToCheckout()">Proceed to Pay</button>
  <button class="back-btn" onclick="closeCart()">← Back to Shop</button>
</div>

<!-- Checkout Page -->
<div id="checkoutPage" class="checkout-section">
  <h2>Proceed to Payment</h2>
  <p>Total amount: ₹<span id="checkoutTotal"></span></p>
  <canvas id="qrcode"></canvas>
  <div class="action-btns">
    <button class="pay" onclick="openUPILink()">Pay via Google Pay</button>
    <button class="cancel" onclick="cancelCheckout()">Cancel / Go Back</button>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/qrious@4.0.2/dist/qrious.min.js"></script>
<script>
  let cart = JSON.parse(localStorage.getItem('cart') || '[]');
  const cartCount = document.getElementById('cartCount');
  const cartOverlay = document.getElementById('cartOverlay');
  const cartItemsDiv = document.getElementById('cartItems');
  const totalPriceEl = document.getElementById('totalPrice');

  function updateCart() {
    localStorage.setItem('cart', JSON.stringify(cart));
    cartCount.textContent = cart.reduce((a,b)=>a+b.qty,0);
    renderCart();
  }

  function addToCart(name, price) {
    const item = cart.find(i=>i.name===name);
    if(item) item.qty++;
    else cart.push({name,price,qty:1});
    updateCart();
  }

  function renderCart() {
    cartItemsDiv.innerHTML = '';
    let total = 0;
    cart.forEach((item,i)=>{
      total += item.price * item.qty;
      cartItemsDiv.innerHTML += `
        <div class="cart-item">
          <span>${item.name}</span>
          <div>
            <button class="qty-btn" onclick="changeQty(${i},-1)">-</button>
            ${item.qty}
            <button class="qty-btn" onclick="changeQty(${i},1)">+</button>
          </div>
        </div>`;
    });
    totalPriceEl.textContent = total;
  }

  function changeQty(index, delta) {
    cart[index].qty += delta;
    if(cart[index].qty <= 0) cart.splice(index,1);
    updateCart();
  }

  document.getElementById('cartBtn').onclick = () => {
    cartOverlay.classList.add('active');
    renderCart();
  };

  function closeCart() {
    cartOverlay.classList.remove('active');
  }

  function goToCheckout() {
    const shopPage = document.getElementById('shopPage');
    const checkoutPage = document.getElementById('checkoutPage');
    const total = cart.reduce((a,b)=>a+b.price*b.qty,0);
    document.getElementById('checkoutTotal').textContent = total;
    shopPage.style.display = 'none';
    cartOverlay.classList.remove('active');
    checkoutPage.style.display = 'block';
    const upiLink = upi://pay?pa=anu83anand@oksbi&pn=FurnitureFlow&am=${total}&cu=INR;
    new QRious({
      element: document.getElementById('qrcode'),
      value: upiLink,
      size: 200
    });
  }

  function openUPILink() {
    const total = cart.reduce((a,b)=>a+b.price*b.qty,0);
    const link = upi://pay?pa=anu83anand@oksbi&pn=FurnitureFlow&am=${total}&cu=INR;
    window.location.href = link;
  }

  function cancelCheckout() {
    document.getElementById('checkoutPage').style.display = 'none';
    document.getElementById('shopPage').style.display = 'block';
  }

  // 🔍 Search Functionality
  const searchBar = document.getElementById('searchBar');
  searchBar.addEventListener('input', function() {
    const query = this.value.toLowerCase();
    const vendors = document.querySelectorAll('.vendor-section');
    vendors.forEach(vendor => {
      const vendorName = vendor.querySelector('h2').textContent.toLowerCase();
      const products = vendor.querySelectorAll('.card');
      let vendorMatch = vendorName.includes(query);
      let anyProductVisible = false;

      products.forEach(product => {
        const productName = product.querySelector('h3').textContent.toLowerCase();
        if (productName.includes(query) || vendorMatch) {
          product.style.display = 'block';
          anyProductVisible = true;
        } else {
          product.style.display = 'none';
        }
      });

      vendor.style.display = (vendorMatch || anyProductVisible) ? 'block' : 'none';
    });
  });

  // 💰 Price Filter
  function applyPriceFilter() {
    const min = parseInt(document.getElementById('minPrice').value) || 0;
    const max = parseInt(document.getElementById('maxPrice').value) || Infinity;
    const products = document.querySelectorAll('.card');
    products.forEach(product => {
      const price = parseInt(product.querySelector('p').textContent.replace('₹','').trim());
      product.style.display = (price >= min && price <= max) ? 'block' : 'none';
    });
  }

  updateCart();
</script>
</body>
</html>
