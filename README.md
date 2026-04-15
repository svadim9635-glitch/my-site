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
    overflow-x:hidden;
}

/* ================= LOGO ================= */
.logo{
    position:fixed;
    top:18px;
    left:50%;
    transform:translateX(-50%);
    font-size:70px;
    font-weight:900;
    letter-spacing:14px;
    z-index:9999;
    display:flex;
    gap:5px;
}

/* буквы */
.logo span{
    opacity:0;
    transform:translateY(20px);
}

/* анимация */
.logo.show span{
    animation:letterIn 0.8s ease forwards;
}

.logo.show span:nth-child(1){animation-delay:0s;}
.logo.show span:nth-child(2){animation-delay:0.15s;}
.logo.show span:nth-child(3){animation-delay:0.3s;}
.logo.show span:nth-child(4){animation-delay:0.45s;}

@keyframes letterIn{
    0%{opacity:0; transform:translateY(25px); filter:blur(10px);}
    100%{opacity:1; transform:translateY(0); filter:blur(0);}
}

/* ================= BACK BUTTON ================= */
.back{
    position:fixed;
    top:20px;
    left:20px;
    z-index:9999;
    padding:10px 15px;
    background:rgba(0,0,0,0.6);
    border:1px solid rgba(255,255,255,0.2);
    border-radius:10px;
    cursor:pointer;
    backdrop-filter:blur(8px);
    color:white;
}

/* ================= GRID ================= */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:120px 40px 60px;
}

/* ================= CARD ================= */
.card{
    background:#111;
    border-radius:14px;
    overflow:hidden;
    cursor:pointer;
    transition:0.3s;
}

.card:hover{
    transform:scale(1.04);
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
    width:72%;
    height:72%;
    top:14%;
    left:14%;
    border:3px solid rgba(255,255,255,0.25);
    border-radius:10px;
    overflow:hidden;
    box-shadow:0 10px 30px rgba(0,0,0,0.7);
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
    transform:translateY(-50%) scale(0.75);
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

/* ================= CAR ANIMATION ================= */
@keyframes carAnim{
    0%{
        opacity:0;
        transform:translateY(-50%) scale(0.7) rotate(0deg);
    }
    60%{
        opacity:1;
        transform:translateY(-75%) scale(1) rotate(-10deg);
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

.card:not(:hover) .car{
    opacity:0;
    animation:none;
}

/* ================= PRODUCT ================= */
.product{
    display:none;
    padding:120px 40px;
}

.gallery img{
    width:220px;
    border-radius:10px;
    margin:5px;
}

/* TEXT */
h3{margin:10px;}
.price{margin:10px;color:#00ff88;}
</style>
</head>

<body>

<!-- LOGO -->
<div class="logo" id="logo"></div>

<!-- BACK -->
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

/* ================= LOGO INTRO ================= */
const logoText="APEX";
const logo=document.getElementById("logo");

logoText.split("").forEach(l=>{
    const span=document.createElement("span");
    span.textContent=l;
    logo.appendChild(span);
});

/* запускаем ОДИН РАЗ */
window.addEventListener("load",()=>{
    setTimeout(()=>logo.classList.add("show"),50);
});

/* ================= PRODUCTS ================= */
const products = Array.from({length:10}, (_,i)=>({
    title: [
        "BMW M3 Art","Nissan GTR Art","Mercedes AMG Art",
        "Toyota Supra Art","Audi RS6 Art","Lambo Huracan",
        "Porsche 911","Ferrari F8","McLaren 720S","Bugatti Chiron"
    ][i],
    price:`$${49+i*5}`,
    img:`https://picsum.photos/600/400?random=${i}`
}));

const grid=document.getElementById("grid");

products.forEach((p,i)=>{
grid.innerHTML+=`
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

/* ================= PRODUCT PAGE ================= */
function openProduct(i){
    home.style.display="none";
    product.style.display="block";

    pTitle.innerText=products[i].title;
    pPrice.innerText=products[i].price;

    gallery.innerHTML=`
        <img src="${products[i].img}">
        <img src="https://picsum.photos/600/400?random=${i+20}">
    `;
}

function goBack(){
    home.style.display="block";
    product.style.display="none";
}
</script>

</body>
</html>
