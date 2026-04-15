<script>

/* ================= LOGO INTRO ================= */
const logoText="APEX";
const logo=document.getElementById("logo");

logoText.split("").forEach(l=>{
    const span=document.createElement("span");
    span.textContent=l;
    logo.appendChild(span);
});

window.addEventListener("load",()=>{
    setTimeout(()=>logo.classList.add("show"),50);
});

/* ================= PRODUCTS (ЖЁСТКО 10) ================= */
const products = [
{title:"BMW M3 Art", price:"$49", img:"https://picsum.photos/600/400?1"},
{title:"Nissan GTR Art", price:"$54", img:"https://picsum.photos/600/400?2"},
{title:"Mercedes AMG Art", price:"$59", img:"https://picsum.photos/600/400?3"},
{title:"Toyota Supra Art", price:"$64", img:"https://picsum.photos/600/400?4"},
{title:"Audi RS6 Art", price:"$69", img:"https://picsum.photos/600/400?5"},
{title:"Lambo Huracan", price:"$74", img:"https://picsum.photos/600/400?6"},
{title:"Porsche 911", price:"$79", img:"https://picsum.photos/600/400?7"},
{title:"Ferrari F8", price:"$84", img:"https://picsum.photos/600/400?8"},
{title:"McLaren 720S", price:"$89", img:"https://picsum.photos/600/400?9"},
{title:"Bugatti Chiron", price:"$99", img:"https://picsum.photos/600/400?10"}
];

const grid=document.getElementById("grid");

/* очищаем на всякий */
grid.innerHTML = "";

/* ГАРАНТИРОВАННО 10 карточек */
for(let i=0;i<products.length;i++){
    const p = products[i];

    grid.innerHTML += `
    <div class="card" onclick="openProduct(${i})">
        <div class="table">
            <div class="frame">
                <img class="art" src="${p.img}">
                <img class="car" src="https://pngimg.com/uploads/car/car_PNG1640.png">
                <div class="shadow"></div>
            </div>
        </div>
        <h3>${p.title}</h3>
        <div class="price">${p.price}</div>
    </div>`;
}

/* ================= PRODUCT PAGE ================= */
function openProduct(i){
    home.style.display="none";
    product.style.display="block";

    pTitle.innerText=products[i].title;
    pPrice.innerText=products[i].price;

    gallery.innerHTML=`
        <img src="${products[i].img}">
        <img src="https://picsum.photos/600/400?random=${i+20}">
    `;
}

function goBack(){
    home.style.display="block";
    product.style.display="none";
}

</script>
