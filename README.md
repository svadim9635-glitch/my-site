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

/* 1. ИСПРАВЛЕННОЕ ЛОГО (Твое фото вместо текста) */
.title{
    position:fixed;
    top:15px;
    left:50%;
    transform:translateX(-50%);
    /* Ставим высоту как у старого текста, чтобы не резало */
    height: 60px; 
    width: auto;
    z-index: 9998;
    opacity: 0;
    /* Убираем фон и инвертируем буквы в белый */
    filter: invert(1) brightness(1.2);
    mix-blend-mode: screen;
}

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

.card:hover .art
