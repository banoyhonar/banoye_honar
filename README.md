<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>بانوی هنر</title>
  <style>
    body {
      font-family: sans-serif;
      margin: 0;
      background: linear-gradient(90deg, #c3f584, #ffd166, #90e0ef, #ff6b6b);
    }
    nav {
      background-color: #333;
      color: white;
      display: flex;
      padding: 10px;
      justify-content: center;
      flex-wrap: wrap;
    }
    nav a {
      color: white;
      margin: 0 10px;
      text-decoration: none;
      font-weight: bold;
    }
    .slider, .section {
      padding: 20px;
      text-align: center;
    }
    .slider {
      background-color: #fff;
      border: 2px dashed #333;
      margin: 20px;
    }
    .slider-container {
      max-width: 100%;
      position: relative;
    }
    .slide {
      width: 100%;
      height: auto;
      border-radius: 10px;
      display: none;
    }
    .section {
      background-color: rgba(255, 255, 255, 0.8);
      margin: 10px;
      border-radius: 10px;
    }
    footer {
      background-color: #111;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .product-img {
      width: 150px;
      border-radius: 10px;
      cursor: pointer;
      border: 2px solid transparent;
      transition: 0.3s;
    }
    .product-img:hover {
      border-color: #ff6b6b;
    }
    #cart ul {
      list-style: none;
      padding: 0;
    }
    .remove-btn {
      background-color: #ff6b6b;
      border: none;
      color: white;
      margin-right: 10px;
      padding: 3px 8px;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <nav>
    <a href="#">همه</a>
    <a href="#">عروسک</a>
    <a href="#">کت</a>
    <a href="#">گیره و سنجاق</a>
    <a href="#">کلاه و شالگردن</a>
    <a href="#">محصولات پارچه‌ای</a>
  </nav>

  <div class="slider">
    <h2>محصولات ویژه بانوی هنر</h2>
    <div class="slider-container">
      <img src="images/product1.jpg" class="slide" style="display:block;">
      <img src="images/product2.jpg" class="slide">
      <img src="images/product3.jpg" class="slide">
    </div>
  </div>

  <div class="section">
    <h3>محصولات</h3>
    <div id="products" style="display: flex; flex-wrap: wrap; gap: 20px; justify-content: center;">
      <img src="images/product1.jpg" alt="محصول ۱" data-name="عروسک خرسی" data-price="50000" class="product-img">
      <img src="images/product2.jpg" alt="کلاه بافتنی" data-name="کلاه بافتنی" data-price="70000" class="product-img">
      <img src="images/product3.jpg" alt="شال‌گردن رنگی" data-name="شال‌گردن رنگی" data-price="65000" class="product-img">
    </div>
  </div>

  <div class="section" id="cart">
    <h3>سبد خرید</h3>
    <ul id="cart-items"></ul>
    <p id="total">جمع کل: ۰ تومان</p>
  </div>

  <footer>
    <p>اینستاگرام: <a href="https://instagram.com/honar_l44" style="color:#ffcc00">@honar_l44</a></p>
    <p>تلفن: 09010836644</p>
    <p>© بانوی هنر</p>
  </footer>

  <script>
    // اسلایدر
    let slideIndex = 0;
    const slides = document.getElementsByClassName("slide");

    function showSlides() {
      for (let i = 0; i < slides.length; i++) {
        slides[i].style.display = "none";
      }
      slideIndex++;
      if (slideIndex > slides.length) { slideIndex = 1; }
      slides[slideIndex - 1].style.display = "block";
      setTimeout(showSlides, 3000);
    }

    showSlides();

    // سبد خرید
    let cartItems = JSON.parse(localStorage.getItem("cart")) || [];
    const cartList = document.getElementById("cart-items");
    const totalEl = document.getElementById("total");

    function updateCart() {
      cartList.innerHTML = "";
      let total = 0;
      cartItems.forEach((item, index) => {
        const li = document.createElement("li");
        li.innerHTML = `
          <button class="remove-btn" onclick="removeItem(${index})">حذف</button>
          ${item.name} - ${item.price.toLocaleString()} تومان
        `;
        cartList.appendChild(li);
        total += item.price;
      });
      totalEl.textContent = `جمع کل: ${total.toLocaleString()} تومان`;
      localStorage.setItem("cart", JSON.stringify(cartItems));
    }

    function removeItem(index) {
      cartItems.splice(index, 1);
      updateCart();
    }

    document.querySelectorAll(".product-img").forEach(img => {
      img.addEventListener("click", () => {
        const name = img.getAttribute("data-name");
        const price = parseInt(img.getAttribute("data-price"));
        cartItems.push({ name, price });
        updateCart();
      });
    });

    updateCart();
  </script>

</body>
</html>
