<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Apex Shop</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    color: white;
    background: url('https://images.unsplash.com/photo-1489824904134-891ab64532f1') center/cover fixed;
}

/* затемнение фона */
.overlay {
    background: rgba(0,0,0,0.75);
    min-height: 100vh;
}

/* HERO */
.hero {
    text-align: center;
    padding: 80px 20px 40px;
}

.hero h1 {
    font-size: 48px;
    margin: 0;
}

.hero p {
    color: #bbb;
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
    transform: scale(1.03);
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
.product-page {
    display: none;
    padding: 40px;
}

.back {
    background: red;
    padding: 10px 15px;
    border: none;
    color: white;
    cursor: pointer;
    border-radius: 8px;
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
    margin-top: 30px;
    background: rgba(0,0,0,0.5);
    padding: 20px;
    border-radius: 12px;
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
    font-size: 14px;
    text-align: center;
    color: white;
}

.tg { background:#229ED9; }
.ig { background:linear-gradient(45deg,#f9ce34,#ee2a7b,#6228d7); }
.tt { background:#000; border:1px solid #333; }
</style>

</head>

<body>

<div class="overlay">

<!-- ГЛАВНАЯ -->
<div id="home">

    <div class="hero">
        <h1>Apex Hot Wheels Shop</h1>
        <p>Картины и коллекционные модели машин</p>
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

<!-- СТРАНИЦА ТОВАРА -->
<div id="product" class="product-page">

    <button class="back" onclick="goBack()">← Назад</button>

    <h1 id="title"></h1>
    <p id="price"></p>

    <div class="gallery" id="gallery"></div>

    <div class="section">
        <h3>Характеристики</h3>
        <ul id="specs"></ul>
    </div>

    <div class="section">
        <h3>Отзывы</h3>
        <p>⭐ 5/5 — Очень крутая работа!</p>
        <p>⭐ 5/5 — Быстрая доставка и качество топ</p>
        <p>⭐ 4.8/5 — Выглядит ещё лучше чем на фото</p>
    </div>

</div>

</div>

<!-- СОЦСЕТИ -->
<div class="social">
    <a class="tt" href="https://www.tiktok.com/@apex_store_ua" target="_blank">TikTok</a>
    <a class="ig" href="https://www.instagram.com/apex_shop_ua/" target="_blank">Instagram</a>
    <a class="tg" href="https://t.me/bera_999" target="_blank">Telegram</a>
</div>

<script>
const products = [
{
    title: "BMW M3 Art",
    price: "$49",
    images: [
        "https://images.unsplash.com/photo-1610832958506-aa56368176cf",
        "https://images.unsplash.com/photo-1503376780353-7e6692767b70"
    ],
    specs: [
        "Размер: A4/A3",
        "Материал: premium print",
        "Стиль: cinematic garage"
    ]
},
{
    title: "Nissan GTR Art",
    price: "$59",
    images: [
        "https://images.unsplash.com/photo-1616788494707-ec28f08d05d5",
        "https://images.unsplash.com/photo-1525609004556-c46c7d6cf023"
    ],
    specs: [
        "Размер: A3",
        "Материал: matte print",
        "Стиль: neon garage"
    ]
},
{
    title: "Mercedes AMG Art",
    price: "$65",
    images: [
        "https://images.unsplash.com/photo-1503376780353-7e6692767b70",
        "https://images.unsplash.com/photo-1502877338535-766e1452684a"
    ],
    specs: [
        "Размер: A3",
        "Материал: premium glossy",
        "Стиль: dark garage aesthetic"
    ]
}
];

function openProduct(i){
    document.getElementById("home").style.display = "none";
    document.getElementById("product").style.display = "block";

    document.getElementById("title").innerText = products[i].title;
    document.getElementById("price").innerText = products[i].price;

    let gallery = document.getElementById("gallery");
    gallery.innerHTML = "";
    products[i].images.forEach(img=>{
        gallery.innerHTML += `<img src="${img}">`;
    });

    let specs = document.getElementById("specs");
    specs.innerHTML = "";
    products[i].specs.forEach(s=>{
        specs.innerHTML += `<li>${s}</li>`;
    });
}

function goBack(){
    document.getElementById("home").style.display = "block";
    document.getElementById("product").style.display = "none";
}
</script>

</body>
</html>
