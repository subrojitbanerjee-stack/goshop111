# goshop111
<!DOCTYPE html><html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>goshop</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
<style>
body{margin:0;font-family:Poppins;background:#fafafa}
header{background:#111;color:white;padding:15px;text-align:center}
.hero{height:100vh;background:url('https://i.ibb.co/HfyQ1LYr/20260227-232513.jpg') center/cover no-repeat;display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;color:white}
.hero h1{font-size:3rem}
.hero button{padding:12px 25px;background:#ff6600;border:none;color:white;cursor:pointer;margin-top:15px}
.products{padding:30px}
.carousel{display:flex;gap:20px;overflow-x:auto}
.card{background:white;border-radius:12px;padding:15px;min-width:220px;text-align:center;box-shadow:0 4px 10px rgba(0,0,0,0.1)}
.card img{width:100%;height:150px;object-fit:cover;border-radius:10px}
.cart-btn{background:#ff6600;color:white;border:none;padding:8px 15px;margin-top:10px;cursor:pointer}
.cart-icon{position:fixed;top:20px;right:20px;background:#ff6600;color:white;padding:15px;border-radius:50%;cursor:pointer;font-size:18px}
.whatsapp{position:fixed;bottom:20px;right:20px;background:#25D366;color:white;padding:15px;border-radius:50%;text-decoration:none;font-size:20px}
.modal{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,0.5);display:none;justify-content:center;align-items:center}
.modal-content{background:white;padding:20px;width:90%;max-width:400px;border-radius:10px}
input{width:100%;padding:10px;margin:5px 0}
.send{background:#ff6600;color:white;border:none;padding:10px;width:100%;cursor:pointer}
</style>
</head>
<body>
<header>
<h2>goshop</h2>
<p>Fresh Finds, Best Prices</p>
</header>
<section class="hero">
<h1>Welcome to goshop</h1>
<button onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">Shop Now</button>
</section>
<div class="cart-icon" onclick="toggleCart()">🛒 <span id="count">0</span></div>
<section id="products" class="products">
<h2>Our Products</h2>
<div class="carousel" id="productList"></div>
</section>
<div class="modal" id="cartModal">
<div class="modal-content">
<h3>Your Cart</h3>
<ul id="cartItems"></ul>
<input type="text" id="name" placeholder="Customer Name">
<input type="text" id="phone" placeholder="Phone Number">
<button class="send" onclick="sendOrder()">Send Order</button>
<button onclick="toggleCart()">Close</button>
</div>
</div>
<a class="whatsapp" href="https://wa.me/99999999">💬</a>
<script src="https://cdn.jsdelivr.net/npm/emailjs-com@2/dist/email.min.js"></script>
<script>
emailjs.init("YOUR_PUBLIC_KEY");
const products=[
{img:"https://i.ibb.co/yFr0P33p/image.jpg",name:"Watch",price:499},
{img:"https://i.ibb.co/chKzpf73/image.jpg",name:"Shoes",price:799},
{img:"https://i.ibb.co/PG9tSjFw/image.jpg",name:"Jeans",price:999},
{img:"https://i.ibb.co/8ngXmC92/515-R4-CLGOHL-AC-UF894-1000-QL80-FMwebp.webp",name:"Bag",price:599},
{img:"https://i.ibb.co/gMF8wMMH/d9a73e0a7d79e654af7353c1e33744b2.jpg",name:"Clock",price:299},
{img:"https://i.ibb.co/MxXNQjxX/35cae80761902d61b4d240ccda344bd3.jpg",name:"T-shirt",price:399},
{img:"https://i.ibb.co/chBWCL68/a9a01cfc497ab4b4d53514e92eeeaf63.jpg",name:"Cap",price:199},
{img:"https://i.ibb.co/bj4cz2T6/eb53bd23a5d545353735c29e12e2923c.jpg",name:"Accessories",price:149}
];
let cart=[];
const list=document.getElementById("productList");
products.forEach((p,i)=>{
list.innerHTML+=`<div class='card'>
<img src='${p.img}'>
<h4>${p.name}</h4>
<p>₹${p.price}</p>
<button class='cart-btn' onclick='addToCart(${i})'>Add to Cart</button>
</div>`});
function addToCart(i){cart.push(products[i]);document.getElementById("count").innerText=cart.length}
function toggleCart(){let modal=document.getElementById("cartModal");modal.style.display=modal.style.display==="flex"?"none":"flex";renderCart()}
function renderCart(){let html="";cart.forEach(p=>html+=`<li>${p.name} - ₹${p.price}</li>`);document.getElementById("cartItems").innerHTML=html}
function sendOrder(){
let items=cart.map(p=>p.name).join(", ");
emailjs.send("YOUR_SERVICE_ID","YOUR_TEMPLATE_ID",{
name:document.getElementById("name").value,
phone:document.getElementById("phone").value,
items:items,
to_email:"subrojitbanerjee@gmail.com"
}).then(()=>alert("Order Sent Successfully"))
}
</script>
</body>
</html>
