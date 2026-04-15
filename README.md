<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>APEX STORE</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    
    <style>
        /* ОБНУЛЕНИЕ И ЧИСТКА (Убираем белую линию и отступы) */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #0b0b0b;
            color: white;
            font-family: Arial, sans-serif;
            overflow-x: hidden;
        }

        /* ЛОГОТИП APEX (Твоя полная картинка) */
        .title-container {
            position: absolute; /* Привязан к странице, уезжает при скролле */
            top: 40px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            z-index: 10000;
            opacity: 0;
        }

        .title-container img {
            width: 80%;
            max-width: 500px;
            height: auto;
            /* Делаем буквы белыми, убираем фон */
            filter: invert(1) contrast(1.5) brightness(1.2);
            mix-blend-mode: screen;
        }

        @keyframes apexAppearance {
            0% { opacity: 0; transform: scale(1.1); filter: invert(1) blur(15px); }
            100% { opacity: 1; transform: scale(1); filter: invert(1) blur(0); }
        }

        .title-container.animate {
            animation: apexAppearance 2s ease-out forwards;
        }

        /* ГРИД И КАРТОЧКИ */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            padding: 200px 40px 60px; /* Отступ сверху под логотип */
        }

        .product-card {
            background: #111;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            transition: 0.3s;
        }

        .product-card:hover {
            transform: translateY(-10px);
            background: #161616;
        }

        .product-img {
            width: 100%;
            height: 250px;
            border-radius: 10px;
            margin-bottom: 15px;
            /* Твоя розовая Porsche подставлена сюда */
        }

        h3 { margin-bottom: 10px; font-size: 20px; }
        .price { display: block; color: #00ff88; font-size: 18px; margin-bottom: 15px; font-weight: bold; }

        .btn-buy {
            padding: 10px 25px;
            background: white;
            color: black;
            border: none;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn-buy:hover {
            background: #00ff88;
        }
    </style>
</head>
<body>

    <div class="title-container" id="title">
        <img src="https://i.postimg.cc/sGr0Q65G/APEX-LOGO-FULL.jpg" alt="APEX">
    </div>

    <div class="grid">
        
        <div class="product-card" data-aos="fade-up" data-aos-delay="200">
            <div class="product-img" style="background: url('https://i.ibb.co/b7aa829e/photo-2026-03-22_02-51-40.jpg') center/cover;"></div>
            <h3>Porsche 911 GT3 RS</h3>
            <span class="price">2500 ₴</span>
            <button class="btn-buy">В корзину</button>
        </div>

        <div class="product-card" data-aos="fade-up" data-aos-delay="400">
            <div class="product-img" style="background: url('https://picsum.photos/600/400?random=2') center/cover;"></div>
            <h3>Branded Box v1</h3>
            <span class="price">500 ₴</span>
            <button class="btn-buy">В корзину</button>
        </div>

    </div>

    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
        // Инициализация AOS анимаций
        AOS.init();

        // Запуск анимации логотипа
        window.addEventListener("load", () => {
            const t = document.getElementById("title");
            if (t) t.classList.add("animate");
        });
    </script>
</body>
</html>
