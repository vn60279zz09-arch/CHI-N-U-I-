<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Chiến Đấu Đi</title>
<style>
body{
    margin:0;
    background:#222;
    color:white;
    font-family:Arial;
    text-align:center;
}
#game{
    width:800px;
    height:500px;
    background:#4aa3ff;
    margin:auto;
    position:relative;
    overflow:hidden;
}
#player{
    width:40px;
    height:40px;
    background:green;
    position:absolute;
    left:100px;
    top:100px;
}
.enemy{
    width:40px;
    height:40px;
    background:red;
    position:absolute;
}
</style>
</head>
<body>

<h1>CHIẾN ĐẤU ĐI</h1>

<div>
Level: <span id="lv">1</span>
|
XP: <span id="xp">0</span>
|
Máu: <span id="hp">100</span>
</div>

<button onclick="secret()">Nhập Mã Bí Mật</button>

<h3 id="mapName">Đảo Quỷ</h3>

<div id="game">
    <div id="player"></div>
</div>

<script>

let player=document.getElementById("player");

let x=100;
let y=100;

let level=1;
let xp=0;
let hp=100;

function updateUI(){
    lv.innerText=level;
    document.getElementById("xp").innerText=xp;
    document.getElementById("hp").innerText=hp;
}

document.addEventListener("keydown",e=>{

    if(e.key=="w") y-=10;
    if(e.key=="s") y+=10;
    if(e.key=="a") x-=10;
    if(e.key=="d") x+=10;

    player.style.left=x+"px";
    player.style.top=y+"px";
});

function spawnEnemy(){

    let e=document.createElement("div");
    e.className="enemy";

    e.style.left=Math.random()*700+"px";
    e.style.top=Math.random()*400+"px";

    document.getElementById("game").appendChild(e);

    e.onclick=function(){

        xp+=10;

        if(xp>=100){
            xp=0;
            level++;

            hp+=20;

            if(level==50)
                mapName.innerText="Đảo Đầu Lâu";

            if(level==100)
                mapName.innerText="Đảo Trời";

            if(level==150)
                mapName.innerText="Đảo Ma";
        }

        updateUI();

        e.remove();
        spawnEnemy();
    };
}

for(let i=0;i<5;i++){
    spawnEnemy();
}

function secret(){

    let code=prompt("Nhập mã:");

    if(code=="000"){

        level=200;
        hp=9999;

        alert("Mở khóa cấp 200 và khả năng bay!");
    }

    updateUI();
}

updateUI();

</script>

</body>
</html>
