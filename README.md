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

/* ЛОГОТИП (Твой новый, из картинки) */
.title{
    position:fixed;
    top:15px;
    left:50%;
    transform:translateX(-50%);
    /* Настройки размера под твою картинку */
    height: 70px;
    width: auto;
    z-index: 9998;
    opacity: 0;
    /* Убираем фон и делаем буквы белыми */
    filter: invert(1) brightness(1.2);
    mix-blend-mode: screen;
}

/* Твоя оригинальная анимация */
@keyframes titleAnim{
    0%{
        opacity:0;
        transform:translateX(-50%) translateY(-20px) scale(0.8);
        filter: invert(1) blur(10px);
    }
    100%{
        opacity:1;
        transform:translateX(-50%) translateY(0) scale(1);
        filter: invert(1) blur(0);
    }
}

.title.animate{
    animation:titleAnim 2.5s ease-out forwards;
}

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
    display: none;
}

.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:120px 40px 60px;
}

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

.table{
    height:220px;
    background:
    linear-gradient(rgba(0,0,0,0.6),rgba(0,0,0,0.6)),
    url('https://images.unsplash.com/photo-1519681393784-d120267933ba');
    background-size:cover;
    position:relative;
}

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

.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.5s;
}

.car{
    position:absolute;
    width:65%;
    left:18%;
    top:55%;
    opacity:0;
    transform:translateY(-50%) scale(0.8);
}

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

.product{
    display:none;
    padding:120px 40px;
}

.gallery img{
    width:200px;
    border-radius:10px;
}

h3{margin:10px;}
.price{margin:10px;color:#00ff88;}
</style>
</head>

<body>

<div class="logo">APEX</div>
<img src="https://i.postimg.cc/sGr0Q65G/APEX-LOGO-FULL.jpg" class="title" id="title">

<button class="back" id="backBtn" onclick="goBack()">← Back</button>

<div id="home">
<div class="grid" id="grid"></div>
</div>

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

const products = cars.map((name,i)=>({
    title:name,
    price:`$${49+i*5}`,
    img:`https://picsum.photos/600/400?random=${i}`
}));

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

function openProduct(i){
    document.getElementById("home").style.display="none";
    document.getElementById("product").style.display="block";
    document.getElementById("backBtn").style.display="block";

    document.getElementById("pTitle").innerText=products[i].title;
    document.getElementById("pPrice").innerText=products[i].price;

    document.getElementById("gallery").innerHTML=`
        <img src="${products[i].img}">
        <img src="https://picsum.photos/600/400?random=${i+10}">
    `;
}

function goBack(){
    document.getElementById("home").style.display="block";
    document.getElementById("product").style.display="none";
    document.getElementById("backBtn").style.display="none";
}

window.addEventListener("load",()=>{
    const t=document.getElementById("title");
    t.classList.add("animate"); 
});
</script>

</body>
</html>
