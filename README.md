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

/* ===== LOGO ===== */
.logo{
    position:fixed;
    top:20px;
    left:50%;
    transform:translateX(-50%);
    font-size:60px;
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

.logo.animate{
    animation:logoAnim 2.5s ease-out;
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
    backdrop-filter: blur(8px);
}

/* ===== GRID ===== */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:120px 40px 60px;
}

/* ===== CARD (картина на столе) ===== */
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

/* стол */
.table{
    height:220px;
    background:
    linear-gradient(0deg, rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
    url('https://images.unsplash.com/photo-1519681393784-d120267933ba');
    background-size:cover;
    position:relative;
    overflow:hidden;
}

/* рамка (картина) */
.frame{
    position:absolute;
    width:70%;
    height:70%;
    top:15%;
    left:15%;
    border:4px solid rgba(255,255,255,0.3);
    border-radius:6px;
    overflow:hidden;
    box-shadow:0 10px 30px rgba(0,0,0,0.6);
}

/* фон картины */
.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.5s;
}

/* машинка */
.car{
    position:absolute;
    width:60%;
    left:20%;
    top:55%;
    transform:translateY(-50%) scale(0.8);
    opacity:0;
}

/* тень */
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

/* ===== ANIMATION ===== */
@keyframes carMove{
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
    animation:carMove 0.9s ease-out forwards;
}

.card:hover .shadow{
    opacity:1;
}

.card:hover .art{
    filter:brightness(0.4);
    transform:scale(1.1);
}

.card:not(:hover) .car{
    animation:none;
    opacity:0;
}

/* text */
h3{
    margin:10px;
}
.price{
    margin:10px;
    color:#00ff88;
}
</style>
</head>

<body>

<div class="logo" id="logo">APEX</div>
<button class="back" onclick="scrollToTop()">← Back</button>

<div class="grid">

<!-- 10 ОБЪЯВЛЕНИЙ -->
<script>
const data = [
"BMW M3 Art",
"Nissan GTR Art",
"Mercedes AMG Art",
"Toyota Supra Art",
"Audi RS6 Art",
"Lamborghini Huracan Art",
"Porsche 911 Art",
"Ferrari F8 Art",
"McLaren 720S Art",
"Bugatti Chiron Art"
];

const grid = document.currentScript.parentElement;

data.forEach((name,i)=>{
grid.innerHTML += `
<div class="card">
    <div class="table">
        <div class="frame">
            <img class="art" src="https://picsum.photos/600/400?random=${i}">
            <img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
            <div class="shadow"></div>
        </div>
    </div>
    <h3>${name}</h3>
    <div class="price">$${49+i*5}</div>
</div>
`;
});
</script>

</div>

<script>
/* LOGO ANIMATION */
function playLogo(){
    const logo=document.getElementById("logo");
    logo.classList.remove("animate");
    void logo.offsetWidth;
    logo.classList.add("animate");
}

window.addEventListener("load",playLogo);

/* SCROLL BACK TOP */
function scrollToTop(){
    window.scrollTo({top:0, behavior:"smooth"});
}

/* повтор логотипа при возврате вверх */
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
