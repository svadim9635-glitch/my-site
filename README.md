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

/* ===== LOGO ===== */

.logo{
    position:relative;
    margin-top:40px;
    text-align:center;

    opacity:0;
    transform:scale(0.8);
    filter:blur(20px);

    transition:0.8s ease;
}

.logo.show{
    opacity:1;
    transform:scale(1);
    filter:blur(0);
}

.logo svg{
    width:520px;
    max-width:90%;
}

/* ===== BACK BUTTON ===== */

.back{
    position:fixed;
    top:20px;
    left:20px;

    padding:10px 15px;

    background:#111;

    border:1px solid #333;

    color:white;

    border-radius:8px;

    cursor:pointer;

    z-index:9999;
}

/* ===== GRID ===== */

.grid{
    display:grid;

    grid-template-columns:
    repeat(auto-fit,minmax(260px,1fr));

    gap:20px;

    padding:40px;
}

/* ===== CARD ===== */

.card{
    background:#111;

    border-radius:14px;

    overflow:hidden;

    cursor:pointer;

    transition:0.3s;

    display:flex;

    flex-direction:column;
}

.card:hover{
    transform:scale(1.04);
}

/* ===== VERTICAL CARD ===== */

.table{

    width:100%;

    aspect-ratio:3/4;

    background:
    linear-gradient(
    rgba(0,0,0,0.35),
    rgba(0,0,0,0.35)
    ),

    url('https://images.unsplash.com/photo-1519681393784-d120267933ba');

    background-size:cover;

    background-position:center;

    position:relative;
}

/* ===== FRAME ===== */

.frame{

    position:absolute;

    width:75%;

    height:75%;

    top:12%;

    left:12%;

    border:2px solid rgba(255,255,255,0.8);

    overflow:hidden;

    border-radius:8px;
}

/* ===== IMAGE ===== */

.art{

    width:100%;

    height:100%;

    object-fit:cover;

    transition:0.4s;
}

/* ===== CAR ===== */

.car{

    position:absolute;

    width:60%;

    left:20%;

    top:55%;

    opacity:0;

    pointer-events:none;
}

/* ===== SHADOW ===== */

.shadow{

    position:absolute;

    width:60%;

    height:12px;

    left:20%;

    bottom:10px;

    background:black;

    filter:blur(10px);

    opacity:0;

    transition:0.3s;
}

/* ===== ANIMATION ===== */

@keyframes carAnim{

    0%{
        opacity:0;
        transform:
        translateY(0)
        scale(0.7)
        rotate(0deg);
    }

    100%{
        opacity:1;
        transform:
        translateY(-25px)
        scale(1)
        rotate(-10deg);
    }

}

.card:hover .car{
    animation:carAnim 0.6s forwards;
}

.card:hover .shadow{
    opacity:1;
}

.card:hover .art{
    filter:brightness(0.35);
}

/* ===== PRODUCT PAGE ===== */

.product{

    display:none;

    padding:120px 40px;
}

.gallery img{

    width:220px;

    margin:5px;

    border-radius:10px;
}

/* ===== TEXT ===== */

h3{
    margin:10px;
}

.price{
    margin:10px;
    color:#00ff88;
}

.info-block{
    margin-top:20px;
    background:#111;
    padding:25px;
    border-radius:14px;
    line-height:1.8;
}

</style>
</head>

<body>

<!-- ===== BACK ===== -->

<button class="back" onclick="goBack()">
← Back
</button>

<!-- ===== HOME ===== -->

<div id="home">

<!-- ===== LOGO ===== -->

<div class="logo" id="logo">

<svg viewBox="0 0 900 220"
xmlns="http://www.w3.org/2000/svg">

<text
x="50%"
y="58%"
text-anchor="middle"

fill="white"

font-size="150"

font-weight="900"

letter-spacing="12"

font-family="Arial Black, Arial"

transform="skewX(-14)"

>

APEX

</text>

</svg>

</div>

<!-- ===== PRODUCTS ===== -->

<div class="grid" id="grid"></div>

</div>

<!-- ===== PRODUCT PAGE ===== -->

<div id="product" class="product">

<h1 id="pTitle"></h1>

<p id="pPrice"></p>

<div id="gallery" class="gallery"></div>

</div>

<script>

/* ===== LOGO ANIMATION ===== */

window.onload=()=>{

    setTimeout(()=>{

        document
        .getElementById("logo")
        .classList
        .add("show");

    },200);

};

/* ===== PRODUCTS ===== */

const products=[

"BMW M3",

"Nissan GTR",

"Mercedes AMG",

"Toyota Supra",

"Audi RS6",

"Lamborghini Huracan",

"Porsche 911",

"Ferrari F8",

"McLaren 720S",

"Bugatti Chiron"

].map((name,i)=>({

    title:name,

    price:`$${50+i*5}`,

    img:
`https://picsum.photos/600/400?random=${i}`

}));

const grid=document.getElementById("grid");

/* ===== CREATE CARDS ===== */

products.forEach((p,i)=>{

grid.innerHTML += `

<div class="card"
onclick="openProduct(${i})">

    <div class="table">

        <div class="frame">

            <img
            class="art"
            src="${p.img}">

            <img
            class="car"
            src="https://pngimg.com/uploads/car/car_PNG1640.png">

            <div class="shadow"></div>

        </div>

    </div>

    <h3>${p.title}</h3>

    <div class="price">
    ${p.price}
    </div>

</div>

`;

});

/* ===== OPEN PRODUCT ===== */

function openProduct(i){

    home.style.display="none";

    product.style.display="block";

    pTitle.innerText=
    products[i].title;

    pPrice.innerText=
    products[i].price;

    gallery.innerHTML=`

        <img src="${products[i].img}">

        <img
        src="https://picsum.photos/600/400?random=${i+20}">

        <img
        src="https://picsum.photos/600/400?random=${i+40}">

        <div class="info-block">

        <h2>Характеристики</h2>

        <p>• Размер: 40x60 см</p>

        <p>• Материал рамки: дерево</p>

        <p>• Покрытие: матовое</p>

        <p>• Машинка: Hot Wheels</p>

        <p>• Подсветка: LED</p>

        <p>• Тип крепления: настенное</p>

        <p>• Ручная сборка</p>

        </div>

        <div class="info-block">

        <h2>Описание</h2>

        <p style="opacity:0.8;">

        Уникальная кастомная картина
        с моделью автомобиля.

        Каждая работа собирается вручную.

        Возможно создание индивидуального дизайна,
        выбор цвета рамки, фона и автомобиля.

        </p>

        </div>

        <div class="info-block">

        <h2>Отзывы</h2>

        <p>★★★★★ — Очень круто выглядит вживую</p>

        <p>★★★★★ — Качество лучше чем ожидал</p>

        <p>★★★★★ — Идеальный подарок</p>

        </div>

    `;
}

/* ===== BACK ===== */

function goBack(){

    home.style.display="block";

    product.style.display="none";

}

</script>

</body>
</html>
