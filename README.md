<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX SHOP</title>

<style>
body{
    margin:0;
    font-family:Arial;
    color:white;
    background:url('https://images.unsplash.com/photo-1489824904134-891ab64532f1') center/cover fixed;
}

.overlay{
    background:rgba(0,0,0,0.8);
    min-height:100vh;
}

/* ===== LOGO ===== */
.apex-logo{
    position:fixed;
    top:20px;
    left:50%;
    transform:translateX(-50%);
    font-size:70px;
    font-weight:900;
    letter-spacing:12px;
    z-index:9999;
    opacity:0;
}

@keyframes logoAnim{
    0%{opacity:0; transform:translateX(-50%) translateY(-20px) scale(0.8); filter:blur(10px);}
    50%{opacity:1; filter:blur(0);}
    100%{opacity:1; transform:translateX(-50%) translateY(0) scale(1);}
}

.apex-logo.animate{
    animation:logoAnim 2.5s ease-out;
}

/* HERO */
.hero{
    text-align:center;
    padding:120px 20px 40px;
}

/* GRID */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:40px;
}

/* CARD */
.card{
    background:rgba(20,20,20,0.9);
    border-radius:12px;
    overflow:hidden;
    cursor:pointer;
    transition:0.3s;
}

.card:hover{
    transform:scale(1.03);
    outline:2px solid rgba(255,255,255,0.15);
}

/* АНИМАЦИЯ */
.card-anim{
    position:relative;
    height:200px;
    overflow:hidden;
}

.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.5s;
}

.car{
    position:absolute;
    width:75%;
    left:12%;
    top:50%;
    transform:translateY(-50%) scale(0.8) rotate(0deg);
    opacity:0;
    transition:0.8s cubic-bezier(0.2,0.8,0.2,1);
}

.shadow{
    position:absolute;
    width:60%;
    height:20px;
    left:20%;
    bottom:30px;
    background:rgba(0,0,0,0.6);
    filter:blur(10px);
    opacity:0;
    transition:0.6s;
}

.card:hover .art{
    transform:scale(1.1);
    filter:brightness(0.35) blur(1px);
}

.card:hover .car{
    opacity:1;
    transform:translateY(-60%) scale(1) rotate(-12deg);
}

.card:hover .shadow{
    opacity:1;
    transform:scale(1.1);
}

/* PRODUCT PAGE */
.product{
    display:none;
    padding:40px;
}

.gallery{
    display:flex;
    gap:10px;
    flex-wrap:wrap;
}

.gallery img{
    width:200px;
    border-radius:10px;
}

.section{
    margin-top:20px;
    padding:20px;
    background:rgba(0,0,0,0.5);
    border-radius:10px;
}

/* SOCIAL */
.social{
    position:fixed;
    bottom:15px;
    right:15px;
    display:flex;
    flex-direction:column;
    gap:10px;
}

.social a{
    padding:10px;
    border-radius:10px;
    color:white;
    text-decoration:none;
}

.tt{background:#000;border:1px solid #333;}
.ig{background:linear-gradient(45deg,#f9ce34,#ee2a7b,#6228d7);}
.tg{background:#229ED9;}
</style>
</head>

<body>

<div class="apex-logo" id="logo">APEX</div>

<div class="overlay">

<!-- HOME -->
<div id="home">

<div class="hero">
<h1>Premium Car Art</h1>
<p>Hot Wheels / Automotive Style</p>
</div>

<div class="grid">

<!-- ТОВАР 1 -->
<div class="card" onclick="openProduct(0)">
<div class="card-anim">
<img class="art" src="https://images.unsplash.com/photo-1511919884226-fd3cad34687c">
<img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
<div class="shadow"></div>
</div>
<h3>BMW M3 Art</h3>
<div class="price">$49</div>
</div>

<!-- ТОВАР 2 -->
<div class="card" onclick="openProduct(1)">
<div class="card-anim">
<img class="art" src="https://images.unsplash.com/photo-1511919884226-fd3cad34687c">
<img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
<div class="shadow"></div>
</div>
<h3>Nissan GTR Art</h3>
<div class="price">$59</div>
</div>

</div>
</div>

<!-- PRODUCT PAGE -->
<div id="product" class="product">

<button onclick="back()">← Назад</button>

<h1 id="title"></h1>
<p id="price"></p>

<div class="gallery" id="gallery"></div>

<div class="section">
<h3>Характеристики</h3>
<ul id="specs"></ul>
</div>

<div class="section">
<h3>Отзывы</h3>
<p>⭐ 5885.0 — Очень крутая работа</p>
<p>⭐ 4.9 — Быстро пришло</p>
</div>

</div>

</div>

<!-- SOCIAL -->
<div class="social">
<a class="tt" href="https://www.tiktok.com/@apex_store_ua" target="_blank">TikTok</a>
<a class="ig" href="https://www.instagram.com/apex_shop_ua/" target="_blank">Instagram</a>
<a class="tg" href="https://t.me/bera_999" target="_blank">Telegram</a>
</div>

<script>
const products=[
{
title:"BMW M3 Art",
price:"$49",
images:["https://images.unsplash.com/photo-1511919884226-fd3cad34687c"],
specs:["A3","Premium print","Garage style"]
},
{
title:"Nissan GTR Art",
price:"$59",
images:["https://images.unsplash.com/photo-1511919884226-fd3cad34687c"],
specs:["A3","Matte","Neon style"]
}
];

function openProduct(i){
home.style.display="none";
product.style.display="block";
title.innerText=products[i].title;
price.innerText=products[i].price;

gallery.innerHTML="";
products[i].images.forEach(img=>{
gallery.innerHTML+=`<img src="${img}">`;
});

specs.innerHTML="";
products[i].specs.forEach(s=>{
specs.innerHTML+=`<li>${s}</li>`;
});
}

function back(){
home.style.display="block";
product.style.display="none";
}

/* LOGO */
function playLogo(){
logo.classList.remove("animate");
void logo.offsetWidth;
logo.classList.add("animate");
}

window.addEventListener("load",playLogo);

let last=0;
window.addEventListener("scroll",()=>{
if(window.scrollY<80 && last>200){
playLogo();
}
last=window.scrollY;
});
</script>

</body>
</html>
