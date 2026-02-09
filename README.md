<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>

body{
margin:0;
background:#000;
color:white;
font-family:Arial;
overflow:hidden;
}

#select{
width:100%;
padding:5px;
}

#top{
display:flex;
justify-content:space-between;
align-items:center;
padding:5px 10px;
}

.logo{height:40px;}

#score{font-size:26px;}

#players{
padding:5px 10px;
font-size:16px;
}

#overs{
height:6px;
background:#333;
margin:5px 10px;
}
#bar{height:100%;width:0;background:#0f0;}

#run{
position:absolute;
top:35%;
width:100%;
text-align:center;
font-size:120px;
display:none;
}

.green{color:#00ff00;}
.red{color:#ff0000;}

#lower{
position:absolute;
bottom:25px;
width:100%;
background:#111;
padding:5px;
font-size:16px;
}

#ticker{
position:absolute;
bottom:0;
background:#900;
width:100%;
color:white;
white-space:nowrap;
overflow:hidden;
}

.move{
display:inline-block;
padding-left:100%;
animation:scroll 15s linear infinite;
}

@keyframes scroll{
from{transform:translateX(0);}
to{transform:translateX(-100%);}
}

</style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu&display=swap');

body{
font-family:'Noto Nastaliq Urdu', Arial;
}
</head>

<body>

<select id="select"></select>

<div id="top">
<img id="l1" class="logo">
<div id="score"></div>
<img id="l2" class="logo">
</div>

<div id="players">بلے باز: — | بولر: —</div>

<div id="overs"><div id="bar"></div></div>

<div id="run"></div>

<div id="lower">🏏 LIVE CRICKET | Mughal AJK</div>

<div id="ticker">
<span class="move">LIVE SCORE | Subscribe Mughal AJK | Cricket Updates 24/7</span>
</div>

<script>

let all=[];
let last="";

fetch("https://api.cricapi.com/v1/currentMatches?apikey=4c5a5909-17e8-4f42-8048-c1a26e368c18&offset=0")
.then(r=>r.json())
.then(d=>{
all=d.data;
let o="";
d.data.forEach((m,i)=>o+=`<option value="${i}">${m.name}</option>`);
select.innerHTML=o;
show(0);
});

function show(i){
if(d==4) four.play();
if(d==6) six.play();
let m=all[i];
if(!m)return;

l1.src=m.teamInfo[0].img;
l2.src=m.teamInfo[1].img;

let s=m.score[0];

score.innerHTML=`${m.teams[0]} ${s.r}/${s.w} (${s.o})`;

let pct=(parseFloat(s.o)%50)/50*100;
bar.style.width=pct+"%";

if(last!="" && s.r!=last){

let d=s.r-last;
run.style.display="block";
run.innerHTML=d;

run.className=(d==4)?"green":(d==6)?"red":"";

setTimeout(()=>run.style.display="none",2000);
}

last=s.r;
}

select.onchange=()=>show(select.value);

setInterval(()=>show(select.value),7000);

</script>

</body>
@import url('https://fonts.googleapis.com/css2?family=Noto+Nastaliq+Urdu&display=swap');

body{
</html>
