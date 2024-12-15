# simon says game


//HTML CODE

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="index.css">
    <title>simon says game</title>
</head>
<body>
    <h1>simon says game</h1>
    <h2>your highest score was 0 now</h2>
    <h3>press any key </h3>
    <div class="div">
        <div class="line_one">
            <div class="box orange" type="button" id="orange">1</div>
            <div class="box yellow" type="button" id="yellow">2</div>
        </div>
      <div class="line_two">
        <div class="box brown" type="button" id="brown">3</div>
        <div class="box green" type="button" id="green">4</div>
      </div>
       
    </div>
    <script src="index.js"></script>
</body>
</html>

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


//JS CODE 

let gameseq = [];
let userseq = [];

let btns = ['orange','yellow','brown','green'];
let start = false;
let level = 0;
let h3 = document.querySelector('h3');
let h2 =document.querySelector('h2');
document.addEventListener('keypress',function(){
    if(start==false){
        console.log('game start');
        start = true;
        level1();
    }
});

function gameflash(btn){
  btn.classList.add('flash');
  setTimeout(function(){
    btn.classList.remove('flash');
  },1000)
};

function userflash(btn){
    btn.classList.add('userflash');
    setTimeout(function(){
      btn.classList.remove('userflash');
    },250)
  };

function level1(){
    userseq=[];
    level++;
    h3.innerText=`level ${level}`;

    let random = Math.floor(Math.random()*3);
    let randinx = btns[random];
    let randcolor = document.querySelector(`.${randinx}`);
   
    gameseq.push(randinx);
    gameflash(randcolor);
};

function check(index){
   if(gameseq[index]==userseq[index]){
     if(gameseq.length==userseq.length){
        setTimeout(level1,200);
     }
   }else{
    h3.innerHTML=`you press the wrong button,your score was <b>${level}</b><br>press any key to start game agin!`;
    let body = document.querySelector('body');
    body.classList.add('reset');
    setTimeout(function(){
        body.classList.remove('reset');
    },250);
    highest();
     reset();
   }
}

function userpress(){
    let btn = this;
    userflash(btn);

     let color = btn.getAttribute('id');
    userseq.push(color);
    console.log(userseq);
     
    check( userseq.length-1);
}

let allbtn =document.querySelectorAll('.box');
for(btn of allbtn){
    btn.addEventListener('click',userpress);
}

function reset(){
    start = false;
    level = 0;
    userseq=[];
    gameseq=[];
}

function highest(){
  let highestscore ='';
  if(level>highestscore){
    highestscore+=level;
    h2.innerText=`your last score was ${highestscore}`;
  }else{
    check();
  }
}


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

//CSS CODE

body{
    text-align: center;
}
.div{
    display: flex;
    justify-content: center;
}
.box{
    height: 5rem;
    width: 5rem;
    border: 4px solid black;
    border-radius: 20%;
    margin: 1rem;
}

.orange{
    background-color: orange;
}
.green{
    background-color: green;
}
.yellow{
    background-color: yellow;
}
.brown{
    background-color: brown;
}
.flash{
    background-color: white;
}

.userflash{
    background-color: black;
}

.reset{
    background-color: red;
}
