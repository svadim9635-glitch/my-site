<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>APEX STORE</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    
    <style>
        /* Убираем лишнее сверху (линии и надписи GitHub) */
        header, hr, .header-top {
            display: none !important;
        }

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

        /* Заголовок APEX */
        .title {
            position: fixed;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 24px;
            font-weight: 900;
            letter-spacing: 5px;
            z-index: 9999;
            opacity: 0;
        }

        @keyframes titleAnim {
            0% { opacity: 0; transform: translateX(-50%) translateY(-20px); }
            100% { opacity: 1; transform: translateX(-50%) translateY(0); }
        }

        .title.animate {
            animation: titleAnim 2s ease-out forwards;
        }

        /* Сетка товаров */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            padding: 120px 40px 60px;
        }

        /* КАРТОЧКА ТОВАРА С АНИМАЦИЕЙ ПРИ НАВЕДЕНИИ */
        .product-card {
            background: #111;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            /* Плавность всех изменений (0.3 секунды) */
            transition: transform 0.3s cubic-bezier(0.25, 1, 0.5, 1), box-shadow 0.3s ease, background 0.3s ease;
            cursor: pointer;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* Эффект при наведении курсора */
        .product-card:hover {
            transform: translateY(-10px); /* Карточка приподнимается */
            background: #1a1a1a; /* Цвет становится чуть светлее */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5); /* Добавляем мягкую тень */
            border: 1px solid rgba(255, 255, 255, 0.1); /* Проявляется тонкая рамка */
        }

        .product-img {
            width: 100%;
            height: 250px;
            border-radius: 10px;
            margin-bottom: 15px;
            transition: transform 0.5s ease; /* Для плавности картинки */
        }

        /* Небольшое увеличение картинки внутри при наведении */
        .product-card:hover .product-img {
            transform: scale(1.02);
        }

        h3 { margin-bottom: 10px; }
        .price { display: block; color: #00ff88; font-weight: bold; margin-bottom: 15px; }

        .btn-buy {
            padding: 10px 25px;
            background: white;
            color: black;
            border: none;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }

        .btn-buy:hover {
            background: #00ff88;
            transform: scale(1.05);
        }
    </style>
</head>
<body>

    <div class="title" id="title">APEX</div>

    <div class="grid">
        <div class="product-card" data-aos="fade-up" data-aos-delay="200">
            <div class="product-img" style="background: url('https://i.ibb.co/b7aa829e/photo_2026-03-22_02-51-40.jpg') center/cover;"></div>
            <h3>Porsche 911 GT3 RS</h3>
            <span class="price">2500 ₴</span>
            <button class="btn-buy">В корзину</button>
        </div>

        <div class="product-card" data-aos="fade-up" data-aos-delay="400">
            <div class="product-img" style="background: url('https://i.postimg.cc/vH8kX2Yq/branded-box.jpg') center/cover;"></div>
            <h3>Branded Box v1</h3>
            <span class="price">500 ₴</span>
            <button class="btn-buy">В корзину</button>
        </div>
    </div>

    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
        AOS.init();
        window.addEventListener("load", () => {
            document.getElementById("title").classList.add("animate");
        });
    </script>
</body>
</html>
