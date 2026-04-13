[index.html.txt](https://github.com/user-attachments/files/26690253/index.html.txt)
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hot Wheels Art</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin:0;
      background:#0f0f0f;
      color:#fff;
    }
    header {
      padding:20px;
      text-align:center;
      background:#111;
      font-size:24px;
    }
    .container {
      padding:20px;
      max-width:1200px;
      margin:auto;
    }
    .grid {
      display:grid;
      grid-template-columns:repeat(auto-fit, minmax(250px,1fr));
      gap:20px;
    }
    .card {
      background:#1a1a1a;
      border-radius:16px;
      overflow:hidden;
      box-shadow:0 5px 20px rgba(0,0,0,0.5);
    }
    .card img {
      width:100%;
      height:200px;
      object-fit:cover;
    }
    .card-content {
      padding:15px;
    }
    .price {
      font-size:18px;
      margin:10px 0;
    }
    .btn {
      display:inline-block;
      padding:10px 15px;
      background:#ff3c3c;
      color:#fff;
      text-decoration:none;
      border-radius:10px;
    }
    footer {
      text-align:center;
      padding:20px;
      color:#888;
    }
  </style>
</head>
<body>

<header>
  Картины с Hot Wheels
</header>

<div class="container">
  <h2>Готовые работы</h2>
  <div class="grid">

    <div class="card">
      <img src="https://via.placeholder.com/400x300" alt="">
      <div class="card-content">
        <h3>BMW M3</h3>
        <div class="price">1200 грн</div>
        <a href="https://t.me/yourusername" class="btn">Заказать</a>
      </div>
    </div>

    <div class="card">
      <img src="https://via.placeholder.com/400x300" alt="">
      <div class="card-content">
        <h3>Nissan Skyline</h3>
        <div class="price">1400 грн</div>
        <a href="https://t.me/yourusername" class="btn">Заказать</a>
      </div>
    </div>

  </div>
</div>

<footer>
  Напиши в Telegram для заказа
</footer>

</body>
</html>
