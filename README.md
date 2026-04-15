<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>APEX STORE</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    
    <style>
        /* Убираем лишнее сверху */
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

        /* КАРТОЧКА ТОВАРА */
        .product-card {
            background: #111;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            position: relative;
            z-index: 1;
            
            /* ЖЕСТКАЯ ПЛАВНОСТЬ ДЛЯ ПРОВЕРКИ */
            transition: all 0.3s ease-in-out !important;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        /* ФИНАЛЬНЫЙ ЭФФЕКТ ПОДСВЕЧИВАНИЯ И УВЕЛИЧЕНИЯ */
        .product-card:hover {
            transform: scale(1.08) !important; /* Увеличение */
            z-index: 10;
            background: #1c1c1c !important; /* Подсветка фона */
            box-shadow: 0 0 30px rgba(255, 255, 255, 0.2) !important; /* Белое свечение */
            border: 1px solid rgba(255, 255, 255, 0.4) !important;
        }

        .product-img {
            width: 100%;
            height: 250px;
            border-radius: 10px;
            margin-bottom: 15px;
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
            const t = document.getElementById("title");
            if (t) t.classList.add("animate");
        });
    </script>
</body>
</html>
