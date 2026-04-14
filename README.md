<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>APEX SHOP</title>

<style>
body{
    margin:0;
    font-family:Arial;
    background:#0f0f0f;
    color:white;
}

/* ===== BACK BUTTON (фиксированный угол) ===== */
.back-btn{
    position:fixed;
    top:20px;
    left:20px;
    z-index:9999;
    background:rgba(0,0,0,0.6);
    border:1px solid rgba(255,255,255,0.2);
    color:white;
    padding:10px 15px;
    border-radius:10px;
    cursor:pointer;
    backdrop-filter: blur(8px);
}

/* ===== GRID ===== */
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
    gap:20px;
    padding:60px;
}

/* ===== CARD ===== */
.card{
    background:#1b1b1b;
    border-radius:12px;
    overflow:hidden;
    cursor:pointer;
    transition:0.25s;
}

.card:hover{
    transform:scale(1.03);
    outline:2px solid rgba(255,255,255,0.15);
}

/* ===== ANIMATION AREA ===== */
.card-anim{
    position:relative;
    height:200px;
    overflow:hidden;
}

/* фон (картина) */
.art{
    width:100%;
    height:100%;
    object-fit:cover;
    transition:0.5s;
}

/* машинка */
.car{
    position:absolute;
    width:75%;
    left:12%;
    top:50%;
    transform:translateY(-50%) scale(0.7) rotate(0deg);
    opacity:0;
}

/* тень */
.shadow{
    position:absolute;
    width:60%;
    height:20px;
    left:20%;
    bottom:25px;
    background:black;
    filter:blur(12px);
    opacity:0;
}

/* ===== KEYFRAMES (ВАЖНО ДЛЯ ПЕРЕЗАПУСКА) ===== */
@keyframes carAnim {
    0%{
        opacity:0;
        transform:translateY(-50%) scale(0.6) rotate(0deg);
    }
    50%{
        opacity:1;
        transform:translateY(-65%) scale(1) rotate(-10deg);
    }
    100%{
        opacity:1;
        transform:translateY(-60%) scale(1) rotate(-12deg);
    }
}

/* запуск анимации */
.card:hover .car{
    animation:carAnim 0.9s ease-out forwards;
}

.card:hover .shadow{
    opacity:1;
}

.card:hover .art{
    filter:brightness(0.35);
    transform:scale(1.1);
}

/* reset (ВАЖНО) */
.card:not(:hover) .car{
    animation:none;
    opacity:0;
    transform:translateY(-50%) scale(0.7);
}

.card:not(:hover) .shadow{
    opacity:0;
}

/* текст */
h3{
    margin:10px;
}
.price{
    margin:10px;
    color:#00ff88;
}

/* ===== PRODUCT PAGE ===== */
.product{
    display:none;
    padding:40px;
}

.gallery img{
    width:200px;
    border-radius:10px;
    margin:5px;
}
</style>
</head>

<body>

<!-- КНОПКА НАЗАД (всегда сверху слева) -->
<button class="back-btn" onclick="goBack()">← Back</button>

<!-- HOME -->
<div id="home">

<div class="grid">

    <div class="card">
        <div class="card-anim">
            <img class="art" src="https://images.unsplash.com/photo-1511919884226-fd3cad34687c">
            <img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
            <div class="shadow"></div>
        </div>
        <h3>BMW M3 Art</h3>
        <div class="price">$49</div>
    </div>

    <div class="card">
        <div class="card-anim">
            <img class="art" src="https://images.unsplash.com/photo-1503376780353-7e6692767b70">
            <img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
            <div class="shadow"></div>
        </div>
        <h3>Nissan GTR Art</h3>
        <div class="price">$59</div>
    </div>

</div>

</div>

<script>
function goBack(){
    window.scrollTo({top:0, behavior:'smooth'});
}
</script>

</body>
</html>
