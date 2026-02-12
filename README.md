# Swiggy-clone
Swiggy Clone is a food delivery web app that allows users to browse restaurants, view menus, place orders, and track deliveries online. It includes features like user login, cart system, payment options, and real-time order updates for a smooth experience.
#Output
 https://srihema28.github.io/Swiggy-clone/


 <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Swiggy-Style Food Delivery – Pro Version</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;900&display=swap" rel="stylesheet">
  <style>
    :root {
      --primary: #fc8019;
      --dark: #0b0b0b;
      --gray: #555;
      --light: #fafafa;
      --white: #ffffff;
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter,system-ui;background:var(--light);color:var(--dark)}
    img{max-width:100%;display:block;border-radius:16px}
    a{text-decoration:none;color:inherit}

    header{position:sticky;top:0;background:var(--white);z-index:120;box-shadow:0 2px 18px rgba(0,0,0,.05)}
    .nav{max-width:1240px;margin:auto;padding:14px 20px;display:flex;align-items:center;justify-content:space-between}

    /* Logo */
    .brand{display:flex;align-items:center;gap:8px;font-weight:900;font-size:1.45rem;color:var(--primary)}
    .brand-logo{width:34px;height:34px;border-radius:10px;background:linear-gradient(135deg,#ffb77b,#fc8019);display:grid;place-items:center;color:#fff;font-size:1.2rem;font-weight:900}

    .menu{display:flex;gap:26px;align-items:center}
    .menu a{font-weight:500;color:var(--gray)}
    .btn{padding:10px 18px;border-radius:999px;border:none;cursor:pointer;font-weight:600}
    .btn-primary{background:var(--primary);color:#fff}

    .hamburger{display:none;cursor:pointer}
    .bar{width:24px;height:2px;background:var(--dark);margin:4px 0}

    @media(max-width:768px){
      .menu{display:none;position:absolute;right:16px;top:68px;background:#fff;border-radius:18px;padding:16px;flex-direction:column;box-shadow:0 20px 40px rgba(0,0,0,.1)}
      .menu.open{display:flex}
      .hamburger{display:block}
    }

    .hero{max-width:1240px;margin:auto;padding:50px 20px;display:grid;grid-template-columns:1.1fr .9fr;gap:30px;align-items:center}
    .hero h1{font-size:clamp(2.2rem,5vw,3.6rem);margin:0}
    .search-box{display:flex;gap:8px;background:#fff;border-radius:18px;padding:10px;box-shadow:0 12px 30px rgba(0,0,0,.08)}
    .search-box input{flex:1;border:none;outline:none;padding:10px}

    @media(max-width:900px){.hero{grid-template-columns:1fr}}

    .section{max-width:1240px;margin:auto;padding:20px 20px 40px}
    .section h2{margin-bottom:16px}

    .categories{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:14px}
    .category{padding:14px;text-align:center;background:#fff;border-radius:18px;font-weight:600;box-shadow:0 12px 30px rgba(0,0,0,.06)}

    .cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:20px}
    .card{background:#fff;border-radius:22px;overflow:hidden;box-shadow:0 12px 30px rgba(0,0,0,.06)}
    .card-body{padding:14px 16px}

    /* Auth modal */
    .modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,.45);display:none;align-items:center;justify-content:center}
    .modal{background:#fff;border-radius:22px;padding:22px;width:min(420px,92%)}
    .modal h3{margin-top:0}
    .modal input{width:100%;padding:10px;border-radius:10px;border:1px solid #ddd;margin-bottom:10px}

    /* Cart Page */
    .cart{max-width:940px;margin:0 auto 60px;background:#fff;border-radius:24px;padding:20px;box-shadow:0 20px 40px rgba(0,0,0,.08)}
    .cart-item{display:flex;justify-content:space-between;padding:10px 0;border-bottom:1px solid #eee}

    footer{background:#0e0e0e;color:#d9d9d9;padding:40px 20px;margin-top:30px}
  </style>
</head>
<body>
<header>
  <nav class="nav">
    <div class="brand"><div class="brand-logo">TT</div> Tasty Time</div>
    <div id="hamburger" class="hamburger"><div class="bar"></div><div class="bar"></div><div class="bar"></div></div>
    <div id="menu" class="menu">
      <a href="#restaurants">Restaurants</a>
      <a href="#categories">Categories</a>
      <a href="#about">About</a>
      <a href="#offers">Offers</a>
      <button class="btn btn-primary" onclick="openAuth()">Login / Sign up</button>
      <button class="btn" onclick="openCart()">🛒 Cart</button>
    </div>
  </nav>
</header>

<section class="hero">
  <div>
    <h1>Fast. Fresh. Delivered to your door.</h1>
    <p>Explore restaurants, track orders live and enjoy exclusive offers.</p>
    <div class="search-box">
      <input id="search" placeholder="Search for dishes or restaurants...">
      <button class="btn btn-primary" onclick="searchRestaurants()">Search</button>
    </div>
  </div>
  <div>
    <img src="https://images.unsplash.com/photo-1600891964599-f61ba0e24092?w=900&q=80" alt="Food"/>
  </div>
</section>

<section class="section" id="offers">
  <h2>🔥 Best Offers Today</h2>
  <div class="cards">
    <div class="card"><img src="pizza.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Pizzas</strong><p>Use code: PIZZA50</p></div></div>
    <div class="card"><img src="burger.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Burgers</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="dessert.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Desserts</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="biriyani.jpeg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Biriyani</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="noodles.webp" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Noodles</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="download.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on veg meels</strong><p>60% OFF</p></div></div>
    <div class="card"><img src="images.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Chicken 65</strong><p>60% OFF</p></div></div>
    <div class="card"><img src="shar.avif" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Shawarma</strong><p>60% OFF</p></div></div>
  </div> 
</section>

<section class="section" id="categories">
  <h2>Popular Categories</h2>
  <div class="categories">
    
    <div class="card"><img src="pizza.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Pizzas</strong><p>Use code: PIZZA50</p></div></div>
    <div class="card"><img src="burger.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Burgers</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="dessert.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Desserts</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="biriyani.jpeg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Biriyani</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="noodles.webp" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>Buy 1 Get 1 Noodles</strong><p>Weekend special</p></div></div>
    <div class="card"><img src="download.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on veg meels</strong><p>60% OFF</p></div></div>
    <div class="card"><img src="images.jpg" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Chicken 65</strong><p>60% OFF</p></div></div>
    <div class="card"><img src="shar.avif" style="width:350px; height:355px; object-fit:cover;"><div class="card-body"><strong>50% OFF on Shawarma</strong><p>60% OFF</p></div></div>
  </div>
</section>

<section class="section" id="restaurants">
  <h2>Top Restaurants Near You</h2>
  <div class="cards" id="cardContainer"></div>
</section>

<section class="section" id="about">
  <h2>About Us</h2>
  <p>We are a modern food delivery platform focused on speed, quality and customer happiness.</p>
</section>

<!-- Cart page section -->
<section class="section">
  <div id="cartPage" class="cart" style="display:none">
    <h2>Your Cart</h2>
    <div id="cartItems"></div>
    <p id="cartTotal"><strong>Total:</strong> ₹0</p>
    <button class="btn btn-primary">Proceed to Checkout</button>
  </div>
</section>

<!-- Authentication modal -->
<div id="authModal" class="modal-backdrop">
  <div class="modal">
    <h3>Login / Sign up</h3>
    <input placeholder="Email">
    <input type="password" placeholder="Password">
    <button class="btn btn-primary" style="width:100%">Continue</button>
    <p style="text-align:center;margin-top:8px"><a href="#" onclick="closeAuth()">Close</a></p>
  </div>
</div>

<footer>
  <div style="max-width:1240px;margin:auto">
    <h3>Swiggy-Style Pro</h3>
    <p>Complete, professional front-end with pages, cart and authentication UI.</p>
  </div>
</footer>

<script>
  const restaurants=[
    \
    {name:'Burger Hub',type:'American, Fast Food',rating:'4.2',price:199,img:'https://images.unsplash.com/photo-1550547660-d9450f859349?w=900&q=80'},
    
  ];

  const cart=[];

  function renderCards(list){
    document.getElementById('cardContainer').innerHTML=list.map(r=>`
      <div class='card'>
        <img src='${r.img}'>
        <div class='card-body'>
          <strong>${r.name}</strong>
          <p>${r.type}</p>
          <p>⭐ ${r.rating} • ₹${r.price}</p>
          <button class='btn btn-primary' onclick='addToCart("${r.name}",${r.price})'>Add to cart</button>
        </div>
      </div>`).join('');
  }

  function searchRestaurants(){
    const q=document.getElementById('search').value.toLowerCase();
    const f=restaurants.filter(r=>r.name.toLowerCase().includes(q)||r.type.toLowerCase().includes(q));
    renderCards(f.length?f:restaurants);
  }

  function addToCart(name,price){
    cart.push({name,price});
    alert('Added to cart');
  }

  function openCart(){
    const box=document.getElementById('cartItems');
    box.innerHTML=cart.map(c=>`<div class='cart-item'><span>${c.name}</span><span>₹${c.price}</span></div>`).join('');
    const total=cart.reduce((s,c)=>s+c.price,0);
    document.getElementById('cartTotal').innerHTML=`<strong>Total:</strong> ₹${total}`;
    document.getElementById('cartPage').style.display='block';
    window.scrollTo({top:document.getElementById('cartPage').offsetTop,behavior:'smooth'});
  }

  function openAuth(){document.getElementById('authModal').style.display='flex'}
  function closeAuth(){document.getElementById('authModal').style.display='none'}

  const hamburger=document.getElementById('hamburger');
  const menu=document.getElementById('menu');
  hamburger.onclick=()=>menu.classList.toggle('open');

  renderCards(restaurants);
</script>
</body>
</html>


