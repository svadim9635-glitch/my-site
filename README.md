<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX STORE</title>

<style>
<body>

<div class="title-container" id="title">
    <img src="https://i.postimg.cc/sGr0Q65G/APEX-LOGO-FULL.jpg" alt="APEX">
</div>

<div class="logo">APEX</div>

<div id="home">
    <div class="grid" id="grid"></div>
</div>

<style>
/* ... (здесь твой старый CSS для body, grid, card, carAnim, etc.) ... */

/* ————— НОВЫЙ CSS ДЛЯ ПОЛНОГО ЛОГОТИПА ————— */
.title-container {
    /* Чтобы уезжало вверх при скролле */
    position: absolute; 
    top: 50px; /* Отступ от самого верха */
    left: 0;
    width: 100%; /* Занимаем всю ширину */
    display: flex;
    justify-content: center; /* Центрируем */
    z-index: 10000; /* Самый высокий слой */
    opacity: 0;
}

.title-container img {
    /* Крупный размер (можешь менять), но не больше экрана */
    width: 60%; 
    max-width: 600px; 
    height: auto;
    display: block;
    
    /* Магия прозрачности и белого цвета */
    filter: invert(1) contrast(1.5) brightness(1.2);
    mix-blend-mode: screen; 
}

/* Эффектная анимация: появление из тумана и вспышки */
@keyframes apexAppearance {
    0% {
        opacity: 0;
        transform: scale(1.2) translateY(-20px);
        filter: invert(1) blur(20px) brightness(3);
    }
    30% {
        opacity: 1;
        filter: invert(1) blur(5px) brightness(1.5);
    }
    100% {
        opacity: 1;
        transform: scale(1) translateY(0);
        filter: invert(1) blur(0) brightness(1.2);
    }
}

.title-container.animate {
    animation: apexAppearance 2.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>

<script>
/* ... (твой старый скрипт для генерации карточек, openProduct, etc.) ... */

/* ————— ЗАПУСК АНИМАЦИИ НА ВСЮ СТРУКТУРУ ————— */
window.addEventListener("load", () => {
    // Находим новый контейнер целиком
    const t = document.getElementById("title");
    if (t) {
        // Добавляем класс, и анимация запускается
        t.classList.add("animate"); 
    }
});
</script>

</body>
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
