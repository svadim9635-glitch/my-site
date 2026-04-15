<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>APEX STORE</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    
    <style>
        /* Чистка мусора GitHub сверху */
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

        /* --- ОБНОВЛЕННОЕ АНИМИРОВАННОЕ ЛОГО --- */
        .title {
            position: fixed;
            top: 15px;
            left: 50%;
            transform: translateX(-50%);
            height: 80px; 
            width: auto;
            z-index: 9999;
            opacity: 0; /* Изначально невидимое */
            filter: invert(1) contrast(1.5) brightness(1.2);
            mix-blend-mode: screen;
        }

        @keyframes titleAnim {
            0% { 
                opacity: 0; 
                transform: translateX(-50%) translateY(-30px) scale(0.8); 
                filter: invert(1) blur(20px); /* Сильное размытие в начале */
            }
            50% {
                opacity: 0.5;
                filter: invert(1) blur(10px);
            }
            100% { 
                opacity: 1; 
                transform: translateX(-50%) translateY(0) scale(1); 
                filter: invert(1) blur(0); /* Четкое изображение в конце */
            }
        }

        .title.animate {
            /* 2.5 секунды — оптимально для красивого вступления */
            animation: titleAnim 2.5s cubic-bezier(0.215, 0.61, 0.355, 1) forwards;
        }

        /* Сетка товаров */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 30px;
            padding: 150px 40px 60px;
        }

        /* Твои закрепленные карточки */
        .product-card {
            background: #111;
            border-radius: 15px;
            padding: 20px;
            text-align: center;
            cursor: pointer;
            border: 1px solid rgba(255, 255, 255, 0.05);
            transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
        }

        .product-card:hover {
            transform: scale(1.06);
            background: #1a1a1a;
            border: 1px solid rgba(255, 255, 255, 0.2);
            box-shadow: 0 10px 30px rgba(255, 255, 255, 0.1);
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

    <img src="https://i.postimg.cc/sGr0Q65G/APEX-LOGO-FULL.jpg" class="title" id="title" alt="APEX">

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
