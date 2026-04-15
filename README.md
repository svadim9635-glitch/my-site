<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>APEX STORE</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background: #0b0b0b;
            color: white;
            overflow-x: hidden;
        }

        /* ===== ЛОГОТИП APEX (АНИМИРОВАННЫЙ) ===== */
        .title-container {
            position: absolute;
            top: 40px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            z-index: 10000;
            opacity: 0;
            pointer-events: none;
        }

        .title-container img {
            width: 80%;
            max-width: 600px;
            height: auto;
            /* Убираем белый фон и инвертируем в белый текст */
            filter: invert(1) contrast(1.5) brightness(1.2);
            mix-blend-mode: screen;
        }

        @keyframes apexAppearance {
            0% {
                opacity: 0;
                transform: scale(1.2) translateY(-20px);
                filter: invert(1) blur(20px) brightness(3);
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

        /* ===== МАЛЕНЬКИЙ ЛОГО СЛЕВА ===== */
        .logo {
            position: fixed;
            top: 15px;
            left: 20px;
            font-size: 24px;
            font-weight: 900;
            letter-spacing: 4px;
            z-index: 9999;
            opacity: 0.7;
        }

        /* ===== ГРИД ТОВАРОВ ===== */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            padding: 250px 40px 60px; /* Отступ сверху, чтобы логотип не перекрывал товары */
        }

        /* ===== КАРТОЧКА И ЭФФЕКТ ОТЫВА ===== */
        .card {
            background: #111;
            border-radius: 15px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.4s cubic-bezier(0.22, 1, 0.36, 1);
        }

        .card:hover {
            transform: translateY(-5px);
        }

        .table {
            height: 250px;
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)), url('https://images.unsplash.com/photo-1519681393784-d120267933ba?auto=format&fit=crop&w=800&q=80');
            background-size: cover;
            position: relative;
        }

        .frame {
            position: absolute;
            width: 75%;
            height: 75%;
            top: 12.5%;
            left: 12.5%;
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: 5px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.8);
        }

        .art {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: 0.6s;
        }

        /* Сама машинка */
        .car {
            position: absolute;
            width: 70%;
            left: 15%;
            top: 50%;
            opacity: 0;
            transform: translateY(-50%) scale(0.8);
            transition: all 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
            filter: drop-shadow(0 0 0 rgba(0,0,0,0));
        }

        /* Эффект при наведении на карточку */
        .card:hover .car {
            opacity: 1;
            /* Машинка отрывается, поднимается и поворачивается */
            transform: translateY(-70%) scale(1.15) rotate(-12deg);
            filter: drop-shadow(15px 25px 15px rgba(0,0,0,0.6));
        }

        .card:hover .art {
            filter: brightness(0.3);
            transform: scale(1.1);
        }

        h3 { padding: 15px 15px 5px; margin: 0; font-size: 18px; }
        .price { padding: 0 15px 20px; color: #00ff88; font-weight: bold; }

        .back {
            position: fixed; top: 20px; left: 20px; z-index: 10001;
            padding: 10px 15px; background: rgba(0,0,0,0.6);
            border: 1px solid rgba(255,255,255,0.2); color: white;
            border-radius: 10px; cursor: pointer; display: none;
        }
    </style>
</head>
<body>

<div class="logo">APEX</div>
<div class="title-container" id="title">
    <img src="https://i.postimg.cc/sGr0Q65G/APEX-LOGO-FULL.jpg" alt="APEX">
</div>

<button class="back" id="backBtn" onclick="goBack()">← Back</button>

<div id="home">
    <div class="grid" id="grid"></div>
</div>

<div id="product" style="display:none; padding: 120px 40px;">
    <h1 id="pTitle"></h1>
    <p id="pPrice"></p>
    <div id="gallery"></div>
</div>

<script>
    const cars = ["Porsche 911 GT3", "BMW M4 Art", "Nissan GTR R35", "Lambo Huracan", "Audi RS6 Avant", "Ferrari F8"];
    const grid = document.getElementById("grid");

    const products = cars.map((name, i) => ({
        title: name,
        price: `$${99 + i * 20}`,
        img: `https://picsum.photos/600/400?random=${i}`
    }));

    products.forEach((p, i) => {
        grid.innerHTML += `
        <div class="card" onclick="openProduct(${i})">
            <div class="table">
                <div class="frame">
                    <img class="art" src="${p.img}">
                    <img class="car" src="https://pngimg.com/uploads/porsche/porsche_PNG10614.png">
                </div>
            </div>
            <h3>${p.title}</h3>
            <div class="price">${p.price}</div>
        </div>`;
    });

    function openProduct(i) {
        document.getElementById("home").style.display = "none";
        document.getElementById("title").style.display = "none";
        document.getElementById("product").style.display = "block";
        document.getElementById("backBtn").style.display = "block";
        document.getElementById("pTitle").innerText = products[i].title;
        document.getElementById("pPrice").innerText = products[i].price;
    }

    function goBack() {
        document.getElementById("home").style.display = "block";
        document.getElementById("title").style.display = "flex";
        document.getElementById("product").style.display = "none";
        document.getElementById("backBtn").style.display = "none";
    }

    window.addEventListener("load", () => {
        const t = document.getElementById("title");
        if (t) t.classList.add("animate");
    });
</script>

</body>
</html>
