<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX SHOP</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    color: white;
    background: url('https://images.unsplash.com/photo-1489824904134-891ab64532f1') center/cover fixed;
}

.overlay {
    background: rgba(0,0,0,0.78);
    min-height: 100vh;
}

/* ===== LOGO ===== */
.apex-logo {
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 70px;
    font-weight: 900;
    letter-spacing: 12px;
    z-index: 9999;
    opacity: 0;
}

@keyframes reveal {
    0% {
        opacity: 0;
        transform: translateX(-50%) translateY(-20px) scale(0.8);
        filter: blur(10px);
    }
    50% {
        opacity: 1;
        filter: blur(0);
    }
    100% {
        opacity: 1;
        transform: translateX(-50%) translateY(0) scale(1);
    }
}

.apex-logo.animate {
    animation: reveal 2.5s ease-out;
}

/* HERO */
.hero {
    text-align: center;
    padding: 120px 20px 40px;
}

.hero h1 {
    font-size: 42px;
    margin: 0;
    opacity: 0.8;
}

.hero p {
    color: #aaa;
}

/* GRID */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 40px;
}

.card {
    background: rgba(20,20,20,0.9);
    border-radius: 12px;
    overflow: hidden;
    cursor: pointer;
    transition: 0.3s;
}

.card:hover {
    transform: scale(1.04);
}

.card img {
    width: 100%;
    height: 180px;
    object-fit: cover;
}

.card h3 {
    margin: 10px;
}

.price {
    margin: 10px;
    color: #00ff88;
    font-weight: bold;
}

/* PRODUCT PAGE */
.product {
    display: none;
    padding: 40px;
}

.back {
    padding: 10px 15px;
    background: red;
    border: none;
    color: white;
    border-radius: 8px;
    cursor: pointer;
}

.gallery {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-top: 20px;
}

.gallery img {
    width: 200px;
    border-radius: 10px;
}

.section {
    margin-top: 20px;
    padding: 20px;
    background: rgba(0,0,0,0.5);
    border-radius: 10px;
}

/* SOCIAL */
.social {
    position: fixed;
    bottom: 15px;
    right: 15px;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.social a {
    text-decoration: none;
    padding: 10px;
    border-radius: 10px;
    color: white;
    font-size: 13px;
}

.tg { background:#229ED9; }
.ig { background:linear-gradient(45deg,#f9ce34,#ee2a7b,#6228d7); }
.tt { background:#000; border:1px solid #333; }
</style>
</head>

<body>

<div class="apex-logo" id="logo">APEX</div>

<div class="overlay">

<!-- HOME -->
<div id="home">

    <div class="hero">
        <h1>Premium Car Art Shop</h1>
        <p>Hot Wheels / Automotive / Cinema Style</p>
    </div>

    <div class="grid">

        <div class="card" onclick="openProduct(0)">
            <img src="https://images.unsplash.com/photo-1610832958506-aa56368176cf">
            <h3>BMW M3 Art</h3>
            <div class="price">$49</div>
        </div>

        <div class="card" onclick="openProduct(1)">
            <img src="https://images.unsplash.com/photo-1616788494707-ec28f08d05d5">
            <h3>Nissan GTR Art</h3>
            <div class="price">$59</div>
        </div>

        <div class="card" onclick="openProduct(2)">
            <img src="https://images.unsplash.com/photo-1503376780353-7e6692767b70">
            <h3>Mercedes AMG Art</h3>
            <div class="price">$65</div>
        </div>

    </div>
</div>

<!-- PRODUCT -->
<div id="product" class="product">

    <button class="back" onclick="back()">← Back</button>

    <h1 id="title"></h1>
    <p id="price"></p>

    <div class="gallery" id="gallery"></div>

    <div class="section">
        <h3>Specs</h3>
        <ul id="specs"></ul>
    </div>

    <div class="section">
        <h3>Reviews</h3>
        <p>⭐ 5.0 — Looks insane in real life</p>
        <p>⭐ 4.9 — Fast delivery</p>
        <p>⭐ 5.0 — Premium quality print</p>
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
const products = [
{
    title:"BMW M3 Art",
    price:"$49",
    images:[
        "https://images.unsplash.com/photo-1610832958506-aa56368176cf",
        "https://images.unsplash.com/photo-1503376780353-7e6692767b70"
    ],
    specs:["A4 / A3 Print","Matte finish","Garage cinematic style"]
},
{
    title:"Nissan GTR Art",
    price:"$59",
    images:[
        "https://images.unsplash.com/photo-1616788494707-ec28f08d05d5",
        "https://images.unsplash.com/photo-1525609004556-c46c7d6cf023"
    ],
    specs:["A3 Print","Neon garage style","Premium paper"]
},
{
    title:"Mercedes AMG Art",
    price:"$65",
    images:[
        "https://images.unsplash.com/photo-1503376780353-7e6692767b70",
        "https://images.unsplash.com/photo-1502877338535-766e1452684a"
    ],
    specs:["A3 Print","Gloss finish","Dark aesthetic"]
}
];

function openProduct(i){
    document.getElementById("home").style.display="none";
    document.getElementById("product").style.display="block";

    document.getElementById("title").innerText=products[i].title;
    document.getElementById("price").innerText=products[i].price;

    let g=document.getElementById("gallery");
    g.innerHTML="";
    products[i].images.forEach(img=>{
        g.innerHTML+=`<img src="${img}">`;
    });

    let s=document.getElementById("specs");
    s.innerHTML="";
    products[i].specs.forEach(x=>{
        s.innerHTML+=`<li>${x}</li>`;
    });
}

function back(){
    document.getElementById("home").style.display="block";
    document.getElementById("product").style.display="none";
}

/* ===== LOGO ANIMATION ===== */
function playLogo(){
    const logo=document.getElementById("logo");
    logo.classList.remove("animate");
    void logo.offsetWidth;
    logo.classList.add("animate");
}

window.addEventListener("load", playLogo);

let lastScroll=0;
window.addEventListener("scroll",()=>{
    let y=window.scrollY;

    if(y<80 && lastScroll>200){
        playLogo();
    }

    lastScroll=y;
});
</script>

</body>
</html>
