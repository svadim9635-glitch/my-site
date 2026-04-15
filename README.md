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

/* ===== LOGO ===== */
.logo{
    position:fixed;
    top:20px;
    left:50%;
    transform:translateX(-50%);
    font-size:70px;
    font-weight:900;
    letter-spacing:14px;
    display:flex;
    z-index:9999;
}

.logo span{
    opacity:0;
    transform:translateY(20px);
    animation:logoAnim 0.8s ease forwards;
}

.logo span:nth-child(1){animation-delay:0s;}
.logo span:nth-child(2){animation-delay:0.1s;}
.logo span:nth-child(3){animation-delay:0.2s;}
.logo span:nth-child(4){animation-delay:0.3s;}

@keyframes logoAnim{
    to{
        opacity:1;
        transform:translateY(0);
    }
}

/* ===== BACK ===== */
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
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:120px 40px;
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
    transform:scale(1.05);
}

/* TABLE */
.table{
    height:200px;
    background:url('https://images.unsplash.com/photo-1519681393784-d120267933ba');
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
    border:2px solid white;
    overflow:hidden;
}

/* IMAGE */
.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.4s;
}

/* CAR */
.car{
    position:absolute;
    width:65%;
    left:18%;
    top:55%;
    opacity:0;
}

/* SHADOW */
.shadow{
    position:absolute;
    width:60%;
    height:10px;
    left:20%;
    bottom:10px;
    background:black;
    filter:blur(10px);
    opacity:0;
}

/* ANIMATION */
@keyframes carAnim{
    0%{opacity:0; transform:translateY(0) scale(0.7);}
    100%{opacity:1; transform:translateY(-30px) scale(1);}
}

.card:hover .car{
    animation:carAnim 0.6s forwards;
}

.card:hover .shadow{
    opacity:1;
}

.card:hover .art{
    filter:brightness(0.4);
}

/* ===== PRODUCT ===== */
.product{
    display:none;
    padding:120px 40px;
}

.gallery img{
    width:200px;
    margin:5px;
}
</style>
</head>

<body>

<div class="logo" id="logo"></div>
<button class="back" onclick="goBack()">← Back</button>

<div id="home">
<div class="grid" id="grid"></div>
</div>

<div id="product" class="product">
<h1 id="pTitle"></h1>
<p id="pPrice"></p>
<div id="gallery" class="gallery"></div>
</div>

<script>

/* LOGO */
const logoText="APEX";
const logo=document.getElementById("logo");

logoText.split("").forEach(l=>{
    const span=document.createElement("span");
    span.textContent=l;
    logo.appendChild(span);
});

/* PRODUCTS (РОВНО 10) */
const products=[
"BMW M3","GTR","AMG","SUPRA","RS6",
"HURACAN","911","F8","720S","CHIRON"
].map((name,i)=>({
    title:name,
    price:`$${50+i*5}`,
    img:`https://picsum.photos/600/400?${i}`
}));

const grid=document.getElementById("grid");

/* ВАЖНО: чистим */
grid.innerHTML="";

/* РЕНДЕР 10 КАРТОЧЕК */
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

/* PRODUCT PAGE */
function openProduct(i){
    home.style.display="none";
    product.style.display="block";

    pTitle.innerText=products[i].title;
    pPrice.innerText=products[i].price;

    gallery.innerHTML=`
    <img src="${products[i].img}">
    <img src="https://picsum.photos/600/400?${i+20}">
    `;
}

function goBack(){
    home.style.display="block";
    product.style.display="none";
}

</script>

</body>
</html>
