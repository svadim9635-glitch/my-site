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

/* ===== TOP BAR ===== */
.top{
position:fixed;
top:0;
left:0;
width:100%;
display:flex;
justify-content:space-between;
padding:12px 20px;
background:rgba(0,0,0,0.6);
backdrop-filter:blur(10px);
z-index:9999;
}

.logo{
font-weight:900;
font-size:22px;
letter-spacing:4px;
}

.btn{
background:#111;
border:1px solid #333;
color:white;
padding:8px 12px;
border-radius:8px;
cursor:pointer;
margin-left:5px;
}

/* ===== SECTIONS ===== */
section{
display:none;
padding:90px 30px;
}

.active{display:block;}

/* ===== GRID ===== */
.grid{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(250px,1fr));
gap:20px;
}

/* ===== CARD ===== */
.card{
background:#111;
border-radius:12px;
overflow:hidden;
cursor:pointer;
transition:0.3s;
}

.card:hover{
transform:scale(1.04);
}

.frame{
height:200px;
position:relative;
overflow:hidden;
}

.frame img{
width:100%;
height:100%;
object-fit:cover;
}

/* ===== BUILDER ===== */
.builder{
display:grid;
grid-template-columns:1fr 1fr;
gap:20px;
}

.preview{
height:300px;
background:#111;
display:flex;
align-items:center;
justify-content:center;
border:1px solid #333;
}

.preview img{
width:70%;
}

input,select{
width:100%;
padding:10px;
margin:8px 0;
background:#111;
color:white;
border:1px solid #333;
}

/* ===== ADMIN ===== */
.admin{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
gap:15px;
}

.box{
background:#111;
padding:20px;
border-radius:10px;
text-align:center;
}

.green{color:#00ff88;}
</style>
</head>

<body>

<div class="top">
<div class="logo">APEX</div>

<div>
<button class="btn" onclick="show('shop')">Shop</button>
<button class="btn" onclick="show('workshop')">Workshop</button>
<button class="btn" onclick="show('login')">Login</button>
<button class="btn" onclick="show('profile')">Profile</button>
<button class="btn" onclick="show('admin')">Admin</button>
</div>
</div>

<!-- ================= SHOP ================= -->
<section id="shop" class="active">
<h2>Shop</h2>
<div class="grid" id="shopGrid"></div>
</section>

<!-- ================= WORKSHOP ================= -->
<section id="workshop">
<h2>Workshop</h2>

<div class="builder">

<div>
<select id="car" onchange="update()">
<option value="https://pngimg.com/uploads/car/car_PNG1640.png">Car 1</option>
<option value="https://pngimg.com/uploads/lamborghini/lamborghini_PNG10709.png">Car 2</option>
</select>

<select id="bg" onchange="update()">
<option value="https://images.unsplash.com/photo-1519681393784-d120267933ba">Black table</option>
<option value="https://images.unsplash.com/photo-1500530855697-b586d89ba3ee">Garage</option>
</select>

<input id="frameColor" placeholder="Frame color (white/red/blue)" oninput="update()">

<div class="preview" id="preview">
<img id="prevCar" src="https://pngimg.com/uploads/car/car_PNG1640.png">
</div>

<button class="btn" onclick="saveDesign()">Save design</button>

</div>
</div>
</section>

<!-- ================= LOGIN ================= -->
<section id="login">
<h2>Login</h2>
<input id="name" placeholder="Your name">
<button class="btn" onclick="login()">Enter</button>
</section>

<!-- ================= PROFILE ================= -->
<section id="profile">
<h2>Profile</h2>

<div id="userBox"></div>

<h3>Saved Designs</h3>
<div id="saved"></div>

<h3>Orders</h3>
<div id="orders"></div>
</section>

<!-- ================= ADMIN ================= -->
<section id="admin">
<h2>Admin Panel</h2>

<div class="admin">
<div class="box"><div class="green" id="visits">0</div><p>Visits</p></div>
<div class="box"><div class="green" id="users">0</div><p>Users</p></div>
<div class="box"><div class="green" id="savedC">0</div><p>Saved</p></div>
<div class="box"><div class="green" id="online">1</div><p>Online</p></div>
</div>
</section>

<script>

/* ================= NAV ================= */
function show(id){
document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
document.getElementById(id).classList.add("active");
}

/* ================= DATA ================= */
let user = localStorage.getItem("user") || null;
let users = JSON.parse(localStorage.getItem("users") || "[]");
let saved = JSON.parse(localStorage.getItem("saved") || "[]");
let orders = JSON.parse(localStorage.getItem("orders") || "[]");

/* ================= LOGIN ================= */
function login(){
let name=document.getElementById("name").value;
if(!name) return;

localStorage.setItem("user",name);

if(!users.includes(name)){
users.push(name);
localStorage.setItem("users",JSON.stringify(users));
}

user=name;
renderProfile();
show('profile');
}

/* ================= PROFILE ================= */
function renderProfile(){

document.getElementById("userBox").innerHTML=
user ? `<div class="box">👤 ${user}</div>` : `<div>No user</div>`;

document.getElementById("saved").innerHTML=
saved.map(s=>`<div class="box">${s.car} | ${s.frame}</div>`).join("");

document.getElementById("orders").innerHTML=
orders.map(o=>`<div class="box">${o}</div>`).join("");
}

/* ================= WORKSHOP ================= */
function update(){
document.getElementById("prevCar").src=document.getElementById("car").value;
}

function saveDesign(){
let design={
car:document.getElementById("car").value,
frame:document.getElementById("frameColor").value
};

saved.push(design);
localStorage.setItem("saved",JSON.stringify(saved));
alert("Saved!");
renderProfile();
}

/* ================= SHOP ================= */
let shop=document.getElementById("shopGrid");

for(let i=0;i<10;i++){
shop.innerHTML+=`
<div class="card">
<div class="frame">
<img src="https://picsum.photos/600/400?random=${i}">
</div>
<h3>Art ${i+1}</h3>
</div>`;
}

/* ================= ADMIN ================= */
function adminUpdate(){
document.getElementById("visits").innerText=
localStorage.getItem("visits")||1;

document.getElementById("users").innerText=users.length;
document.getElementById("savedC").innerText=saved.length;
document.getElementById("online").innerText=1;
}

/* ================= INIT ================= */
let visits=localStorage.getItem("visits")||0;
visits++;
localStorage.setItem("visits",visits);

renderProfile();
adminUpdate();

</script>

</body>
</html>
