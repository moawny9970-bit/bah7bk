<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>❤️ لينا</title>

<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;700;900&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

<style>
*{margin:0;padding:0;box-sizing:border-box}
body{
font-family:'Cairo',sans-serif;
background:#000;color:#fff;
overflow:hidden;height:100vh
}

/* خلفية */
.bg-gradient{
position:fixed;width:100%;height:100%;
background:radial-gradient(circle at 20% 50%,#2a0a1a 0%,#000 50%),
radial-gradient(circle at 80% 20%,#1a0a2a 0%,#000 50%);
animation:bgMove 15s ease infinite;
}
@keyframes bgMove{50%{opacity:.8}}

/* loading */
#loading{
position:fixed;width:100%;height:100%;
display:flex;justify-content:center;align-items:center;
flex-direction:column;background:#000;z-index:9999;
transition:.8s;
}
.loading-dot{
width:12px;height:12px;background:#ff4d6d;border-radius:50%;
box-shadow:0 0 40px #ff4d6d;
animation:growDot 2.5s forwards;
}
@keyframes growDot{to{transform:scale(60);opacity:0}}
#loadingText{margin-top:20px;font-weight:900}

/* sections */
.section{
position:fixed;width:100%;height:100%;
display:none;justify-content:center;align-items:center;
flex-direction:column;
opacity:0;transform:scale(1.1);
transition:.6s;
}
.section.active{opacity:1;transform:scale(1)}

/* lock */
.dots{display:flex;gap:10px;margin:20px}
.dot{
width:12px;height:12px;border-radius:50%;
border:2px solid #fff3;
}
.dot.filled{background:#fff}

.keypad{display:grid;grid-template-columns:repeat(3,70px);gap:15px}
.key{
width:70px;height:70px;border-radius:50%;
display:flex;justify-content:center;align-items:center;
background:#fff1;font-size:24px;cursor:pointer;
}
.key:active{background:#ff4d6d}

/* message */
#message p{
font-size:20px;margin:10px 0;
opacity:0;animation:fade .8s forwards;
}
@keyframes fade{to{opacity:1}}

/* buttons */
.glass-btn{
padding:12px 25px;border-radius:25px;
border:none;background:#ff4d6d;
color:#fff;font-size:16px;cursor:pointer;
}

/* hearts */
.heart{
position:fixed;color:#ff4d6d;
animation:float 3s linear forwards;
}
@keyframes float{
to{transform:translateY(-100vh);opacity:0}
}
</style>
</head>

<body>

<div class="bg-gradient"></div>

<!-- loading -->
<div id="loading">
<div class="loading-dot"></div>
<p id="loadingText">في حكاية بدأت…</p>
</div>

<!-- lock -->
<div id="lock" class="section">
<p>ادخل الباسورد 🤍</p>

<div class="dots">
<div class="dot"></div><div class="dot"></div><div class="dot"></div>
<div class="dot"></div><div class="dot"></div><div class="dot"></div>
<div class="dot"></div>
</div>

<div class="keypad">
<div class="key" data-n="1">1</div>
<div class="key" data-n="2">2</div>
<div class="key" data-n="3">3</div>
<div class="key" data-n="4">4</div>
<div class="key" data-n="5">5</div>
<div class="key" data-n="6">6</div>
<div class="key" data-n="7">7</div>
<div class="key" data-n="8">8</div>
<div class="key" data-n="9">9</div>
<div></div>
<div class="key" data-n="0">0</div>
</div>

<p id="error"></p>
</div>

<!-- message -->
<div id="message" class="section"></div>

<script>

// ===== FIX مهم =====
let currentSection=null;
let intervals=[];

function showSection(id){
if(currentSection){
let prev=currentSection;
prev.classList.remove('active');
setTimeout(()=>{prev.style.display='none'},600);
}

let el=document.getElementById(id);
el.style.display='flex';
setTimeout(()=>el.classList.add('active'),10);

currentSection=el;
}

// clear intervals
function clearAllIntervals(){
intervals.forEach(i=>clearInterval(i));
intervals=[];
}

// loading
setTimeout(()=>{
document.getElementById('loading').style.opacity='0';
setTimeout(()=>{
document.getElementById('loading').style.display='none';
showSection('lock');
},800);
},2000);

// ===== LOCK =====
const PASS="2024326";
let input="";

let dots=document.querySelectorAll('.dot');

document.querySelectorAll('.key').forEach(k=>{
k.onclick=()=>{
if(!k.dataset.n) return;

input+=k.dataset.n;
updateDots();

if(input.length==7){
setTimeout(checkPass,200);
}
}
});

function updateDots(){
dots.forEach((d,i)=>{
d.classList.toggle('filled',i<input.length);
});
}

function checkPass(){
if(input===PASS){
showSection('message');
setTimeout(startMessage,500);
}else{
document.getElementById('error').innerText='غلط 😏';
input='';
updateDots();
}
}

// ===== MESSAGE =====
const messages=[
"فاكرة أول مرة؟",
"انتي بقيتي كل حاجة",
"مش بعرف أقول كلام كبير… بس بحبك",
"كملي ❤️"
];

function startMessage(){
clearAllIntervals();

let el=document.getElementById('message');
el.innerHTML="";
let i=0;

let int=setInterval(()=>{
if(i<messages.length){
let p=document.createElement('p');
p.innerText=messages[i];
el.appendChild(p);
i++;
}else{
clearInterval(int);
}
},1500);

intervals.push(int);
}

// حماية من أي error
window.onerror=function(){
showSection('lock');
};

// hearts
function createHearts(){
for(let i=0;i<10;i++){
let h=document.createElement('div');
h.className='heart';
h.innerHTML='❤️';
h.style.left=Math.random()*100+'%';
document.body.appendChild(h);
setTimeout(()=>h.remove(),3000);
}
}

</script>

</body>
</html>
