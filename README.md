<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dark Premium Store</title>
    <link href="https://unpkg.com/aos@2.3.1/dist/aos.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;700&display=swap" rel="stylesheet">
    
    <style>
        /* 1. БАЗОВЫЕ НАСТРОЙКИ (Темная тема) */
        body {
            background-color: #0a0a0a; /* Глубокий черный */
            color: #ffffff;
            font-family: 'Inter', sans-serif;
            margin: 0;
            padding: 0;
            overflow-x: hidden;
        }

        /* 2. ГЛАВНЫЙ ЭКРАН (Без воды) */
        header {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: radial-gradient(circle at center, #1a1a1a 0%, #0a0a0a 100%);
        }

        header h1 {
            font-size: 4rem;
            margin-bottom: 10px;
            letter-spacing: -2px;
        }

        header p {
            color: #888;
            font-size: 1.2rem;
            margin-bottom: 30px;
        }

        .btn-main {
            padding: 15px 40px;
            background: #ffffff;
            color: #000;
            text-decoration: none;
            border-radius: 30px;
            font-weight: bold;
            transition: 0.4s ease; /* Плавность кнопки */
        }

        .btn-main:hover {
            transform: scale(1.05);
            box-shadow: 0 0 20px rgba(255,255,255,0.4);
        }

        /* 3. СЕТКА ТОВАРОВ */
        .container {
            max-width: 1100px;
            margin: 100px auto;
            padding: 0 20px;
        }

        .shop-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 40px;
        }

        /* 4. КАРТОЧКА ТОВАРА (Плавная анимация при наведении) */
        .product-card {
            background: #151515;
            padding: 20px;
            border-radius: 20px;
            border: 1px solid #222;
            transition: 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94); /* Плавность как у Apple */
            text-align: center;
        }

        .product-card:hover {
            border-color: #444;
            transform: translateY(-10px); /* Мягкий подъем вверх */
        }

        .product-img {
            width: 100%;
            height: 250px;
            background: #222; /* Заглушка для фото */
            border-radius: 15px;
            margin-bottom: 20px;
            object-fit: cover;
            transition: 0.5s ease;
        }

        .product-card:hover .product-img {
            transform: scale(1.03); /* Небольшая анимация фото */
        }

        .price {
            font-size: 1.5rem;
            color: #fff;
            margin: 15px 0;
            display: block;
        }

        .btn-buy {
            background: transparent;
            border: 1px solid #444;
            color: #fff;
            padding: 10px 25px;
            border-radius: 10px;
            cursor: pointer;
            transition: 0.3s;
        }

        .btn-buy:hover {
            background: #fff;
            color: #000;
        }

        /* Плавный скролл всей страницы */
        html {
            scroll-behavior: smooth;
        }
    </style>
</head>
<body>

    <header>
        <h1 data-aos="fade-up" data-aos-duration="1500">APEX SHOP</h1>
        <p data-aos="fade-up" data-aos-duration="2000">Лимитированные модели и премиум упаковка</p>
        <a href="#shop" class="btn-main" data-aos="zoom-in" data-aos-delay="500">Смотреть каталог</a>
    </header>

    <div class="container" id="shop">
        <div class="shop-grid">
            
            <div class="product-card" data-aos="fade-up">
                <div class="product-img" style="background: url('ТВОЯ_ССЫЛКА_НА_ФОТО_1') center/cover;"></div>
                <h3>Red Bull RB21-H</h3>
                <span class="price">15 000 ₴</span>
                <button class="btn-buy">В корзину</button>
            </div>

            <div class="product-card" data-aos="fade-up" data-aos-delay="200">
                <div class="product-img" style="background: url('ТВОЯ_ССЫЛКА_НА_ФОТО_2') center/cover;"></div>
                <h3>Branded Box v1</h3>
                <span class="price">500 ₴</span>
                <button class="btn-buy">В корзину</button>
            </div>

            <div class="product-card" data-aos="fade-up" data-aos-delay="400">
                <div class="product-img" style="background: url('ТВОЯ_ССЫЛКА_НА_ФОТО_3') center/cover;"></div>
                <h3>Custom Stencil</h3>
                <span class="price">1 200 ₴</span>
                <button class="btn-buy">В корзину</button>
            </div>

        </div>
    </div>

    <script src="https://unpkg.com/aos@2.3.1/dist/aos.js"></script>
    <script>
        AOS.init({
            once: true /* Анимация проигрывается один раз при появлении */
        });
    </script>

</body>
</html>
