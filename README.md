<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX STORE</title>

<style>
body{
margin:0;
font-family:Arial;
background:#0a0a0a;
color:white;
}

.top{
position:fixed;
top:0;
left:0;
width:100%;
display:flex;
justify-content:space-between;
padding:12px 20px;
background:rgba(0,0,0,0.7);
backdrop-filter:blur(10px);
z-index:9999;
}

.logo{font-weight:900;font-size:22px;}

.menu button{
background:#111;
border:1px solid #333;
color:white;
padding:8px 10px;
margin-left:5px;
border-radius:8px;
cursor:pointer;
}

section{display:none;padding:100px 30px;}
.active{display:block;}

.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(240px,1fr));
gap:20px;
}

.card{
background:#111;
border-radius:12px;
overflow:hidden;
cursor:pointer;
transition:0.3s;
}
.card:hover{transform:scale(1.03);}

.card img{
width:100%;
height:180px;
object-fit:cover;
}

.product img{
width:300px;
border-radius:10px;
}

.box{
background:#111;
padding:15px;
border-radius:10px;
margin:10px 0;
}

a{color:#00ff88;}
</style>
</head>

<body>

<div class="top">
<div class="logo">APEX</div>

<div class="menu">
<button onclick="show('shop')">Shop</button>
<button onclick="show('product')">Product</button>
<button onclick="show('workshop')">Workshop</button>
<button onclick="show('profile')">Profile</button>
<button onclick="show('admin')">Admin</button>
</div>
</div>

<!-- ================= SHOP ================= -->
<section id="shop" class="active">
<h1>Объявления</h1>
<div class="grid" id="shop"></div>
</section>

<!-- ================= PRODUCT ================= -->
<section id="product">
<h1 id="pTitle"></h1>
<img id="pImg">
<p id="pDesc"></p>

<div class="box">
<h3>Характеристики</h3>
<p id="pSpec"></p>
</div>

<div class="box">
<h3>Связь</h3>
<p>
<a href="https://t.me/bera_999">Telegram</a> |
<a href="https://www.instagram.com/apex_shop_ua/">Instagram</a> |
<a href="https://www.tiktok.com/@apex_store_ua">TikTok</a>
</p>
</div>
</section>

<!-- ================= WORKSHOP ================= -->
<section id="workshop">
<h1>Мастерская</h1>

<select id="car">
<option>BMW</option>
<option>GTR</option>
<option>Supra</option>
</select>

<select id="bg">
<option>Garage</option>
<option>Black table</option>
</select>

<input id="frame" placeholder="Цвет рамки">

<div class="box">
<h3>Превью</h3>
<p id="preview">Выбери параметры</p>
</div>
</section>

<!-- ================= PROFILE ================= -->
<section id="profile">
<h1>Профиль</h1>

<div class="box">
<p>Пользователь: <span id="user">Guest</span></p>
</div>

<div class="box">
<h3>Сохранённые картины</h3>
<div id="saved"></div>
</div>
</section>

<!-- ================= ADMIN ================= -->
<section id="admin">
<h1>Admin Panel</h1>

<div class="box">Посещения: <span id="visits"></span></div>
<div class="box">Пользователи: <span id="users"></span></div>
<div class="box">Сохранённые: <span id="savedCount"></span></div>
<div class="box">Онлайн: 1</div>
</section>

<script>

/* ================= DATA ================= */
let products=[
{
title:"BMW M3 Art",
img:"https://picsum.photos/500/300?1",
desc:"Премиум картина с BMW M3",
spec:"Размер: 40x60 | Материал: холст | Стиль: dark garage"
},
{
title:"Nissan GTR Art",
img:"https://picsum.photos/500/300?2",
desc:"GT-R в стиле кибер гаража",
spec:"Размер: 50x70 | Материал: холст"
},
{
title:"Supra Art",
img:"https://picsum.photos/500/300?3",
desc:"Toyota Supra premium art",
spec:"Размер: 40x60 | Цвет: neon"
}
];

/* ================= SHOP ================= */
let shop=document.getElementById("shop");

products.forEach((p,i)=>{
shop.innerHTML+=`
<div class="card" onclick="openProduct(${i})">
<img src="${p.img}">
<h3>${p.title}</h3>
</div>`;
});

/* ================= OPEN PRODUCT ================= */
function openProduct(i){
show('product');

document.getElementById("pTitle").innerText=products[i].title;
document.getElementById("pImg").src=products[i].img;
document.getElementById("pDesc").innerText=products[i].desc;
document.getElementById("pSpec").innerText=products[i].spec;
}

/* ================= NAV ================= */
function show(id){
document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* ================= PROFILE ================= */
let user=localStorage.getItem("user")||"Guest";
document.getElementById("user").innerText=user;

/* ================= ADMIN ================= */
let visits=localStorage.getItem("visits")||0;
visits++;
localStorage.setItem("visits",visits);

document.getElementById("visits").innerText=visits;
document.getElementById("users").innerText=3;
document.getElementById("savedCount").innerText=0;

</script>

</body>
</html>
