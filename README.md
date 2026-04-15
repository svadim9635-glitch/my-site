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
    background:#0b0b0b;
    color:white;
}

/* ===== LOGO (статичное после анимации) ===== */
.logo{
    position:fixed;
    top:15px;
    left:20px;
    font-size:28px;
    font-weight:900;
    letter-spacing:6px;
    z-index:9999;
    opacity:0.9;
}

/* ===== BIG TITLE ===== */
.title{
 position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0.8);
    width: 600px; /* Размер логотипа */
    max-width: 90%;
    z-index: 9999;
    opacity: 0;
    pointer-events: none;
}

/* анимация ТОЛЬКО при входе */
@keyframes titleAnim{
  0% {
        opacity: 0;
        transform: translate(-50%, -55%) scale(0.7);
        filter: blur(20px) brightness(1.5);
    }
    30% {
        opacity: 1;
        transform: translate(-50%, -50%) scale(0.8);
        filter: blur(0px) brightness(1);
    }
    70% {
        opacity: 1;
        transform: translate(-50%, -50%) scale(0.85);
        filter: blur(0px);
    }
    100% {
        opacity: 0;
        transform: translate(-50%, -45%) scale(1);
        filter: blur(10px);
        visibility: hidden;
    }
}

.title.animate{
animation: titleAnim 3.5s cubic-bezier(0.22, 1, 0.36, 1) forwards;
}

/* ===== BACK BUTTON ===== */
.back{
    position:fixed;
    top:20px;
    left:20px;
    z-index:9999;
    padding:10px 15px;
    background:rgba(0,0,0,0.6);
    border:1px solid rgba(255,255,255,0.2);
    color:white;
    border-radius:10px;
    cursor:pointer;
    backdrop-filter:blur(8px);
}

/* ===== GRID ===== */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:120px 40px 60px;
}

/* ===== CARD ===== */
.card{
    background:#111;
    border-radius:12px;
    overflow:hidden;
    cursor:pointer;
    transition:0.3s;
}

.card:hover{
    transform:scale(1.03);
    outline:2px solid rgba(255,255,255,0.15);
}

/* ===== TABLE ===== */
.table{
    height:220px;
    background:
    linear-gradient(rgba(0,0,0,0.6),rgba(0,0,0,0.6)),
    url('https://images.unsplash.com/photo-1519681393784-d120267933ba');
    background-size:cover;
    position:relative;
}

/* FRAME */
.frame{
    position:absolute;
    width:70%;
    height:70%;
    top:15%;
    left:15%;
    border:3px solid rgba(255,255,255,0.25);
    border-radius:8px;
    overflow:hidden;
    box-shadow:0 10px 30px rgba(0,0,0,0.6);
}

/* ART */
.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.5s;
}

/* CAR */
.car{
    position:absolute;
    width:65%;
    left:18%;
    top:55%;
    opacity:0;
    transform:translateY(-50%) scale(0.8);
}

/* SHADOW */
.shadow{
    position:absolute;
    width:60%;
    height:15px;
    left:20%;
    bottom:10px;
    background:black;
    filter:blur(10px);
    opacity:0;
}

/* ANIMATION */
@keyframes carAnim{
    0%{
        opacity:0;
        transform:translateY(-50%) scale(0.7) rotate(0deg);
    }
    50%{
        opacity:1;
        transform:translateY(-70%) scale(1) rotate(-10deg);
    }
    100%{
        opacity:1;
        transform:translateY(-65%) scale(1) rotate(-12deg);
    }
}

.card:hover .car{
    animation:carAnim 0.9s ease forwards;
}

.card:hover .shadow{
    opacity:1;
}

.card:hover .art{
    filter:brightness(0.35);
    transform:scale(1.1);
}

/* ===== PRODUCT PAGE ===== */
.product{
    display:none;
    padding:120px 40px;
}

.gallery img{
    width:200px;
    border-radius:10px;
}

/* TEXT */
h3{margin:10px;}
.price{margin:10px;color:#00ff88;}
</style>
</head>

<body>

<div class="logo">APEX</div>
<img src="https://i.ibb.co/DP6gCNSy/image.jpg" class="title" id="title">

<button class="back" onclick="goBack()">← Back</button>

<!-- HOME -->
<div id="home">
<div class="grid" id="grid"></div>
</div>

<!-- PRODUCT -->
<div id="product" class="product">
<h1 id="pTitle"></h1>
<p id="pPrice"></p>
<div class="gallery" id="gallery"></div>
</div>

<script>

const cars = [
"BMW M3 Art","Nissan GTR Art","Mercedes AMG Art",
"Toyota Supra Art","Audi RS6 Art","Lambo Huracan",
"Porsche 911","Ferrari F8","McLaren 720S","Bugatti Chiron"
];

const grid = document.getElementById("grid");

/* ===== DATA ===== */
const products = cars.map((name,i)=>({
    title:name,
    price:`$${49+i*5}`,
    img:`https://picsum.photos/600/400?random=${i}`
}));

/* ===== CREATE CARDS ===== */
products.forEach((p,i)=>{
grid.innerHTML += `
<div class="card" onclick="openProduct(${i})">
    <div class="table">
        <div class="frame">
            <img class="art" src="${p.img}">
            <img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
            <div class="shadow"></div>
        </div>
    </div>
    <h3>${p.title}</h3>
    <div class="price">${p.price}</div>
</div>`;
});

/* ===== OPEN PRODUCT ===== */
function openProduct(i){
    home.style.display="none";
    product.style.display="block";

    pTitle.innerText=products[i].title;
    pPrice.innerText=products[i].price;

    gallery.innerHTML=`
        <img src="${products[i].img}">
        <img src="https://picsum.photos/600/400?random=${i+10}">
    `;
}

/* ===== BACK ===== */
function goBack(){
    home.style.display="block";
    product.style.display="none";
}

/* ===== TITLE ANIMATION (ONCE ONLY) ===== */
window.addEventListener("load",()=>{
    const t=document.getElementById("title");
    t.classList.add("animate"); // один раз при входе
});

</script>

</body>
</html>
