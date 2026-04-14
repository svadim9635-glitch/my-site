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
    background:#0a0a0a;
    color:white;
}

/* ===== TOP ===== */
.top{
    position:fixed;
    top:0;
    width:100%;
    padding:15px;
    display:flex;
    justify-content:space-between;
    background:rgba(0,0,0,0.6);
    backdrop-filter:blur(10px);
    z-index:9999;
}

.logo{
    font-weight:900;
    font-size:24px;
}

/* buttons */
.btn{
    background:#111;
    border:1px solid #333;
    color:white;
    padding:8px 12px;
    cursor:pointer;
    margin-left:5px;
    border-radius:8px;
}

/* ===== SECTIONS ===== */
section{
    display:none;
    padding:100px 40px;
}

.active{
    display:block;
}

/* ===== LOGIN ===== */
.loginBox{
    max-width:300px;
    margin:auto;
}

/* ===== PROFILE ===== */
.card{
    background:#111;
    padding:15px;
    border-radius:10px;
    margin:10px 0;
}

/* ===== ADMIN ===== */
.adminBox{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
    gap:15px;
}

.stat{
    background:#111;
    padding:20px;
    border-radius:10px;
    text-align:center;
}

.green{color:#00ff88;}
</style>
</head>

<body>

<!-- TOP -->
<div class="top">
<div class="logo">APEX</div>

<div>
<button class="btn" onclick="show('shop')">Shop</button>
<button class="btn" onclick="show('login')">Login</button>
<button class="btn" onclick="show('profile')">Profile</button>
<button class="btn" onclick="show('admin')">Admin</button>
</div>
</div>

<!-- SHOP -->
<section id="shop" class="active">
<h1>Shop</h1>
<p>Карточки товаров тут</p>
</section>

<!-- LOGIN -->
<section id="login">
<div class="loginBox">
<h2>Login / Register</h2>
<input placeholder="Name" id="name">
<button class="btn" onclick="login()">Enter</button>
</div>
</section>

<!-- PROFILE -->
<section id="profile">
<h2>Profile</h2>

<div class="card">
<p>👤 User: <span id="userName">Guest</span></p>
</div>

<div class="card">
<h3>Saved paintings</h3>
<p>Пока пусто</p>
</div>

<div class="card">
<h3>Orders</h3>
<p>Пока пусто</p>
</div>
</section>

<!-- ADMIN -->
<section id="admin">
<h2>Admin Panel</h2>

<div class="adminBox">

<div class="stat">
<h3 class="green" id="visits">124</h3>
<p>Visits</p>
</div>

<div class="stat">
<h3 class="green" id="users">12</h3>
<p>Users</p>
</div>

<div class="stat">
<h3 class="green" id="orders">3</h3>
<p>Orders</p>
</div>

<div class="stat">
<h3 class="green" id="online">1</h3>
<p>Online</p>
</div>

</div>
</section>

<script>

/* ===== NAV ===== */
function show(id){
document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* ===== LOGIN ===== */
function login(){
let name=document.getElementById("name").value;
if(!name) return;

localStorage.setItem("user",name);
document.getElementById("userName").innerText=name;
show("profile");
}

/* load user */
let user=localStorage.getItem("user");
if(user){
document.getElementById("userName").innerText=user;
}

/* ===== FAKE STATS ===== */
let visits=localStorage.getItem("visits")||0;
visits++;
localStorage.setItem("visits",visits);

document.getElementById("visits").innerText=visits;
document.getElementById("users").innerText=3;
document.getElementById("orders").innerText=1;
document.getElementById("online").innerText=1;

</script>

</body>
</html>
