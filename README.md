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

/* ===== STATIC LOGO ===== */
.logo{
    position:fixed;
    top:18px;
    left:20px;
    font-size:28px;
    font-weight:900;
    letter-spacing:6px;
    z-index:9999;
    opacity:0.9;
}

/* ===== ANIMATED TITLE (APEX) ===== */
.title{
    position:fixed;
    top:18px;
    left:50%;
    transform:translateX(-50%);
    font-size:60px;
    font-weight:900;
    letter-spacing:12px;
    z-index:9998;
    opacity:0;
}

@keyframes titleAnim{
    0%{
        opacity:0;
        transform:translateX(-50%) translateY(-20px) scale(0.85);
        filter:blur(10px);
    }
    50%{
        opacity:1;
        filter:blur(0);
    }
    100%{
        opacity:1;
        transform:translateX(-50%) translateY(0) scale(1);
    }
}

.title.animate{
    animation:titleAnim 2.5s ease-out;
}

/* ===== BACK BUTTON ===== */
.back{
    position:fixed;
    top:20px;
    left:20px;
    z-index:9999;
    margin-top:40px;
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

/* ===== TABLE (черный стол) ===== */
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

/* ===== ANIMATION ===== */
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

/* reset */
.card:not(:hover) .car{
    opacity:0;
    animation:none;
}

/* TEXT */
h3{margin:10px;}
.price{margin:10px;color:#00ff88;}
</style>
</head>

<body>

<div class="logo">APEX</div>
<div class="title" id="title">APEX</div>

<button class="back" onclick="scrollToTop()">← Back</button>

<div class="grid" id="grid"></div>

<script>
const cars = [
"BMW M3 Art","Nissan GTR Art","Mercedes AMG Art",
"Toyota Supra Art","Audi RS6 Art","Lambo Huracan",
"Porsche 911","Ferrari F8","McLaren 720S","Bugatti Chiron"
];

const grid = document.getElementById("grid");

/* create 10 cards */
cars.forEach((name,i)=>{
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
    </div>`;
});

/* ===== TITLE ANIMATION ===== */
function playTitle(){
    const t=document.getElementById("title");
    t.classList.remove("animate");
    void t.offsetWidth;
    t.classList.add("animate");
}

window.addEventListener("load",playTitle);

/* scroll back top */
function scrollToTop(){
    window.scrollTo({top:0,behavior:"smooth"});
}

/* repeat animation when back to top */
let last=0;
window.addEventListener("scroll",()=>{
    if(window.scrollY<80 && last>200){
        playTitle();
    }
    last=window.scrollY;
});
</script>

</body>
</html>
