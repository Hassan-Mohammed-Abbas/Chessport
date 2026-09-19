<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Chessport</title>

<script src="https://cdn.jsdelivr.net/npm/chess.js@1.0.0/dist/chess.min.js"></script>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}

body{
  font-family:Arial,Tahoma,sans-serif;
  background:#080c16;
  color:white;
  min-height:100vh;
}

button{
  font-family:inherit;
  cursor:pointer;
}

.hidden{
  display:none!important;
}

/* ===== HOME ===== */

.screen{
  min-height:100vh;
  padding:25px 15px 40px;
}

.header{
  text-align:center;
  padding:30px 10px;
}

.logo{
  font-size:48px;
  font-weight:900;
  letter-spacing:-2px;
}

.logo span{
  font-size:42px;
}

.subtitle{
  margin-top:10px;
  color:#aeb8ca;
  font-size:19px;
}

.card{
  max-width:650px;
  margin:18px auto;
  background:#11182a;
  border:1px solid #273550;
  border-radius:25px;
  padding:25px;
  box-shadow:0 15px 40px rgba(0,0,0,.25);
}

.big-btn{
  width:100%;
  border:0;
  border-radius:17px;
  padding:18px;
  margin:8px 0;
  background:#2563eb;
  color:white;
  font-size:21px;
  font-weight:bold;
}

.big-btn.secondary{
  background:#1b263d;
}

.big-btn:hover{
  filter:brightness(1.12);
}

/* ===== SETUP ===== */

.title{
  text-align:center;
  font-size:30px;
  margin-bottom:25px;
}

.label{
  display:block;
  color:#aeb8ca;
  margin:18px 0 10px;
  font-size:17px;
  font-weight:bold;
}

.options{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:10px;
}

.option{
  border:2px solid #293750;
  background:#0d1423;
  color:white;
  padding:14px;
  border-radius:14px;
  font-size:16px;
}

.option.selected{
  border-color:#3b82f6;
  background:#172b51;
}

.themes{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:12px;
}

.theme{
  border:3px solid transparent;
  border-radius:14px;
  overflow:hidden;
  background:#0b1120;
  padding:5px;
}

.theme.selected{
  border-color:#3b82f6;
}

.theme-board{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  aspect-ratio:1;
}

.theme-board div{
  min-height:25px;
}

.theme-name{
  text-align:center;
  padding:7px 2px;
  font-size:13px;
}

/* ===== GAME ===== */

.game-wrap{
  max-width:850px;
  margin:auto;
}

.game-top{
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:10px;
  margin-bottom:12px;
}

.player-box{
  background:#11182a;
  border:1px solid #273550;
  border-radius:15px;
  padding:10px 15px;
  flex:1;
  text-align:center;
}

.player-name{
  font-weight:bold;
  margin-bottom:5px;
}

.clock{
  font-size:28px;
  font-weight:900;
  background:#070b14;
  border-radius:10px;
  padding:7px;
}

.clock.active{
  outline:3px solid #2563eb;
}

.board-container{
  width:min(92vw,700px);
  margin:auto;
  border:7px solid #0a0f1b;
  border-radius:18px;
  overflow:hidden;
  box-shadow:0 20px 50px rgba(0,0,0,.35);
}

.board{
  display:grid;
  grid-template-columns:repeat(8,1fr);
  aspect-ratio:1;
}

.square{
  position:relative;
  display:flex;
  align-items:center;
  justify-content:center;
  user-select:none;
  touch-action:manipulation;
  font-size:clamp(31px,9vw,67px);
  line-height:1;
}

.square.light{
  background:#f0d9b5;
}

.square.dark{
  background:#b58863;
}

.square.selected{
  box-shadow:inset 0 0 0 5px #22c55e;
}

.square.last{
  box-shadow:inset 0 0 0 5px rgba(250,204,21,.65);
}

.square.legal::after{
  content:"";
  width:22%;
  height:22%;
  background:rgba(20,30,20,.35);
  border-radius:50%;
  position:absolute;
}

.square.capture::after{
  content:"";
  width:75%;
  height:75%;
  border:5px solid rgba(200,40,40,.55);
  border-radius:50%;
  position:absolute;
}

.piece{
  position:relative;
  z-index:2;
  font-family:"Times New Roman",serif;
}

.white-piece{
  color:#fff;
  text-shadow:0 2px 2px #555;
}

.black-piece{
  color:#171717;
  text-shadow:0 1px 1px #aaa;
}

.game-info{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:15px;
  margin-top:18px;
}

.history{
  background:#11182a;
  border:1px solid #273550;
  border-radius:18px;
  padding:17px;
  min-height:120px;
}

.history h3{
  margin-bottom:12px;
}

.moves{
  display:flex;
  flex-wrap:wrap;
  gap:7px;
  color:#dce5f5;
}

.move{
  background:#1a2539;
  padding:6px 9px;
  border-radius:8px;
  font-size:14px;
}

.controls{
  background:#11182a;
  border:1px solid #273550;
  border-radius:18px;
  padding:17px;
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:9px;
}

.control{
  border:0;
  background:#1b263d;
  color:white;
  padding:12px 8px;
  border-radius:11px;
  font-weight:bold;
}

.control.primary{
  background:#2563eb;
}

.status{
  text-align:center;
  margin:15px 0;
  font-size:19px;
  font-weight:bold;
  min-height:25px;
}

.back{
  display:block;
  width:100%;
  max-width:650px;
  margin:15px auto 0;
  border:0;
  background:#27344d;
  color:white;
  padding:14px;
  border-radius:14px;
  font-size:17px;
}

/* ===== THEMES ===== */

.theme-classic .light,
.classic .light{background:#f0d9b5}
.theme-classic .dark,
.classic .dark{background:#b58863}

.theme-green .light,
.green .light{background:#eeeed2}
.theme-green .dark,
.green .dark{background:#769656}

.theme-blue .light,
.blue .light{background:#d9e8f5}
.theme-blue .dark,
.blue .dark{background:#4f81a8}

.theme-wood .light,
.wood .light{background:#e8cfa7}
.theme-wood .dark,
.wood .dark{background:#9a633d}

.theme-gray .light,
.gray .light{background:#dedede}
.theme-gray .dark,
.gray .dark{background:#777}

.theme-purple .light,
.purple .light{background:#eadcf2}
.theme-purple .dark,
.purple .dark{background:#80649a}

@media(max-width:600px){
  .screen{
    padding:12px 10px 30px;
  }

  .logo{
    font-size:38px;
  }

  .subtitle{
    font-size:16px;
  }

  .card{
    padding:17px;
  }

  .themes{
    grid-template-columns:repeat(2,1fr);
  }

  .game-info{
    grid-template-columns:1fr;
  }

  .game-top{
    gap:6px;
  }

  .player-box{
    padding:8px;
  }

  .clock{
    font-size:22px;
  }
}
</style>
</head>

<body>

<!-- ================= HOME ================= -->

<section id="homeScreen" class="screen">

  <div class="header">
    <div class="logo">Chessport ☾</div>
    <div class="subtitle">منصة شطرنج عربية — تعمل على الهاتف والكمبيوتر</div>
  </div>

  <div class="card">

    <button class="big-btn" onclick="showSetup()">
      ♟️ لعب مباراة جديدة
    </button>

    <button class="big-btn secondary" onclick="alert('قسم البطولات سيتم تطويره قريبًا 🏆')">
      🏆 البطولات
    </button>

    <button class="big-btn secondary" onclick="alert('قسم تعلم الشطرنج سيتم تطويره قريبًا 📚')">
      📚 تعلم الشطرنج
    </button>

  </div>

</section>


<!-- ================= SETUP ================= -->

<section id="setupScreen" class="screen hidden">

  <div class="card">

    <h1 class="title">⚙️ إعداد المباراة</h1>

    <div class="label">اختر لونك</div>

    <div class="options">
      <button id="whiteBtn" class="option selected" onclick="chooseColor('w')">
        ⚪ الأبيض
      </button>

      <button id="blackBtn" class="option" onclick="chooseColor('b')">
        ⚫ الأسود
      </button>
    </div>


    <div class="label">وقت المباراة</div>

    <div class="options">

      <button class="option selected timeOption" data-time="10" onclick="chooseTime(10,this)">
        10 دقائق
      </button>

      <button class="option timeOption" data-time="5" onclick="chooseTime(5,this)">
        5 دقائق
      </button>

      <button class="option timeOption" data-time="3" onclick="chooseTime(3,this)">
        3 دقائق
      </button>

      <button class="option timeOption" data-time="15" onclick="chooseTime(15,this)">
        15 دقيقة
      </button>

    </div>


    <div class="label">🎨 اختر رقعة من 6</div>

    <div class="themes">

      <button class="theme selected" onclick="chooseTheme('classic',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">كلاسيك</div>
      </button>


      <button class="theme" onclick="chooseTheme('green',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">أخضر</div>
      </button>


      <button class="theme" onclick="chooseTheme('blue',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">أزرق</div>
      </button>


      <button class="theme" onclick="chooseTheme('wood',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">خشبي</div>
      </button>


      <button class="theme" onclick="chooseTheme('gray',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">رمادي</div>
      </button>


      <button class="theme" onclick="chooseTheme('purple',this)">
        <div class="theme-board">
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
          <div class="light"></div><div class="dark"></div><div class="light"></div><div class="dark"></div>
          <div class="dark"></div><div class="light"></div><div class="dark"></div><div class="light"></div>
        </div>
        <div class="theme-name">بنفسجي</div>
      </button>

    </div>


    <button class="big-btn" onclick="startGame()">
      🚀 ابدأ المباراة
    </button>

    <button class="back" onclick="showHome()">
      ← العودة للرئيسية
    </button>

  </div>

</section>


<!-- ================= GAME ================= -->

<section id="gameScreen" class="screen hidden">

  <div class="game-wrap">

    <div class="game-top">

      <div class="player-box">
        <div class="player-name">⚫ الأسود</div>
        <div id="blackClock" class="clock">10:00</div>
      </div>

      <div class="player-box">
        <div class="player-name">⚪ الأبيض</div>
        <div id="whiteClock" class="clock">10:00</div>
      </div>

    </div>


    <div id="status" class="status">
      دور الأبيض
    </div>


    <div id="board" class="board-container"></div>


    <div class="game-info">

      <div class="history">
        <h3>📜 سجل النقلات</h3>
        <div id="moves" class="moves">
          لا توجد نقلات بعد
        </div>
      </div>


      <div class="controls">

        <button class="control" onclick="undoMove()">
          ↩️ تراجع
        </button>

        <button class="control" onclick="flipBoard()">
          🔄 قلب الرقعة
        </button>

        <button class="control primary" onclick="copyMoves()">
          📋 نسخ النقلات
        </button>

        <button class="control" onclick="newGameConfirm()">
          🆕 مباراة جديدة
        </button>

      </div>

    </div>


    <button class="back" onclick="leaveGame()">
      ← الخروج للموقع
    </button>

  </div>

</section>


<script>

/* ================= VARIABLES ================= */

let game = new Chess();

let selectedSquare = null;

let boardFlipped = false;

let selectedColor = "w";

let selectedTime = 10;

let selectedTheme = "classic";

let timerInterval = null;

let whiteSeconds = selectedTime * 60;

let blackSeconds = selectedTime * 60;

let gameStarted = false;


/* ================= PIECES ================= */

/*
  الملك تم تغييره إلى هلال ☾ حسب طلبك.
*/

const pieces = {
  w:{
    p:"♙",
    r:"♖",
    n:"♘",
    b:"♗",
    q:"♕",
    k:"☾"
  },

  b:{
    p:"♟",
    r:"♜",
    n:"♞",
    b:"♝",
    q:"♛",
    k:"☾"
  }
};


/* ================= SCREENS ================= */

function showHome(){

  stopTimer();

  document.getElementById("homeScreen").classList.remove("hidden");
  document.getElementById("setupScreen").classList.add("hidden");
  document.getElementById("gameScreen").classList.add("hidden");

}


function showSetup(){

  document.getElementById("homeScreen").classList.add("hidden");
  document.getElementById("setupScreen").classList.remove("hidden");
  document.getElementById("gameScreen").classList.add("hidden");

}


function showGame(){

  document.getElementById("homeScreen").classList.add("hidden");
  document.getElementById("setupScreen").classList.add("hidden");
  document.getElementById("gameScreen").classList.remove("hidden");

}


/* ================= SETUP ================= */

function chooseColor(color){

  selectedColor = color;

  document.getElementById("whiteBtn").classList.remove("selected");
  document.getElementById("blackBtn").classList.remove("selected");

  if(color==="w"){
    document.getElementById("whiteBtn").classList.add("selected");
  }else{
    document.getElementById("blackBtn").classList.add("selected");
  }

}


function chooseTime(minutes,button){

  selectedTime = minutes;

  document.querySelectorAll(".timeOption").forEach(x=>{
    x.classList.remove("selected");
  });

  button.classList.add("selected");

}


function chooseTheme(theme,button){

  selectedTheme = theme;

  document.querySelectorAll(".theme").forEach(x=>{
    x.classList.remove("selected");
  });

  button.classList.add("selected");

}


/* ================= START GAME ================= */

function startGame(){

  game = new Chess();

  selectedSquare = null;

  boardFlipped = selectedColor === "b";

  whiteSeconds = selectedTime * 60;
  blackSeconds = selectedTime * 60;

  gameStarted = true;

  showGame();

  updateClocks();

  renderBoard();

  renderMoves();

  updateStatus();

  startTimer();

}


/* ================= BOARD ================= */

function renderBoard(){

  const container = document.getElementById("board");

  container.innerHTML = "";

  const board = document.createElement("div");

  board.className = "board " + selectedTheme;


  let files = ["a","b","c","d","e","f","g","h"];

  let ranks = [8,7,6,5,4,3,2,1];


  if(boardFlipped){

    files.reverse();

    ranks.reverse();

  }


  for(let r of ranks){

    for(let f of files){

      const squareName = f+r;

      const square = document.createElement("div");

      square.className = "square";


      const fileIndex = files.indexOf(f);

      const rankIndex = ranks.indexOf(r);

      square.classList.add(
        (fileIndex + rankIndex) % 2 === 0
        ? "light"
        : "dark"
      );


      if(selectedSquare === squareName){

        square.classList.add("selected");

      }


      const history = game.history({verbose:true});

      const lastMove = history[history.length-1];

      if(lastMove &&
        (lastMove.from===squareName || lastMove.to===squareName)){

        square.classList.add("last");

      }


      if(selectedSquare){

        const legalMoves = game.moves({
          square:selectedSquare,
          verbose:true
        });

        const possible = legalMoves.find(
          m=>m.to===squareName
        );

        if(possible){

          if(game.get(squareName)){

            square.classList.add("capture");

          }else{

            square.classList.add("legal");

          }

        }

      }


      const piece = game.get(squareName);

      if(piece){

        const pieceElement = document.createElement("div");

        pieceElement.className =
          "piece " +
          (piece.color==="w" ? "white-piece" : "black-piece");

        pieceElement.textContent =
          pieces[piece.color][piece.type];

        square.appendChild(pieceElement);

      }


      square.onclick = ()=>handleSquare(squareName);

      board.appendChild(square);

    }

  }


  container.appendChild(board);

}


/* ================= MOVE ================= */

function handleSquare(square){

  if(!gameStarted) return;

  const piece = game.get(square);


  if(selectedSquare){

    const legalMoves = game.moves({
      square:selectedSquare,
      verbose:true
    });

    const move = legalMoves.find(
      m=>m.to===square
    );


    if(move){

      try{

        game.move({
          from:selectedSquare,
          to:square,
          promotion:"q"
        });

        selectedSquare = null;

        renderBoard();

        renderMoves();

        updateStatus();

        return;

      }catch(e){

        console.log(e);

      }

    }


    if(piece && piece.color===game.turn()){

      selectedSquare = square;

      renderBoard();

      return;

    }


    selectedSquare = null;

    renderBoard();

    return;

  }


  if(piece && piece.color===game.turn()){

    selectedSquare = square;

    renderBoard();

  }

}


/* ================= MOVES ================= */

function renderMoves(){

  const box = document.getElementById("moves");

  const history = game.history();

  box.innerHTML = "";


  if(history.length===0){

    box.textContent = "لا توجد نقلات بعد";

    return;

  }


  history.forEach((move,index)=>{

    const span = document.createElement("span");

    span.className = "move";

    const number = Math.floor(index/2)+1;

    if(index%2===0){

      span.textContent = number + ". " + move;

    }else{

      span.textContent = move;

    }

    box.appendChild(span);

  });

}


/* ================= STATUS ================= */

function updateStatus(){

  const status = document.getElementById("status");

  if(game.isCheckmate()){

    const winner =
      game.turn()==="w"
      ? "الأسود"
      : "الأبيض";

    status.textContent =
      "🏆 كش مات — الفائز: " + winner;

    gameStarted=false;

    stopTimer();

    return;

  }


  if(game.isDraw()){

    status.textContent = "🤝 تعادل";

    gameStarted=false;

    stopTimer();

    return;

  }


  if(game.isCheck()){

    status.textContent =
      "⚠️ كش — دور " +
      (game.turn()==="w" ? "الأبيض" : "الأسود");

  }else{

    status.textContent =
      "دور " +
      (game.turn()==="w" ? "الأبيض ⚪" : "الأسود ⚫");

  }


  document.getElementById("whiteClock")
    .classList.toggle("active",game.turn()==="w");

  document.getElementById("blackClock")
    .classList.toggle("active",game.turn()==="b");

}


/* ================= CLOCK ================= */

function startTimer(){

  stopTimer();

  timerInterval = setInterval(()=>{

    if(!gameStarted) return;

    if(game.turn()==="w"){

      whiteSeconds--;

    }else{

      blackSeconds--;

    }


    updateClocks();


    if(whiteSeconds<=0){

      whiteSeconds=0;

      gameStarted=false;

      stopTimer();

      document.getElementById("status").textContent =
        "🏆 انتهى الوقت — الفائز: الأسود";

    }


    if(blackSeconds<=0){

      blackSeconds=0;

      gameStarted=false;

      stopTimer();

      document.getElementById("status").textContent =
        "🏆 انتهى الوقت — الفائز: الأبيض";

    }

  },1000);

}


function stopTimer(){

  if(timerInterval){

    clearInterval(timerInterval);

    timerInterval=null;

  }

}


function formatTime(seconds){

  const min=Math.floor(seconds/60);

  const sec=seconds%60;

  return String(min).padStart(2,"0")+
    ":"+
    String(sec).padStart(2,"0");

}


function updateClocks(){

  document.getElementById("whiteClock").textContent =
    formatTime(whiteSeconds);

  document.getElementById("blackClock").textContent =
    formatTime(blackSeconds);

}


/* ================= UNDO ================= */

function undoMove(){

  if(game.history().length===0) return;

  game.undo();

  selectedSquare=null;

  renderBoard();

  renderMoves();

  updateStatus();

}


/* ================= FLIP ================= */

function flipBoard(){

  boardFlipped=!boardFlipped;

  renderBoard();

}


/* ================= COPY ================= */

function copyMoves(){

  const history=game.history();

  if(history.length===0){

    alert("لا توجد نقلات لنسخها.");

    return;

  }


  let text="Chessport\n\n";

  history.forEach((move,index)=>{

    const number=Math.floor(index/2)+1;

    if(index%2===0){

      text+=number+". "+move+" ";

    }else{

      text+=move+"\n";

    }

  });


  navigator.clipboard.writeText(text)
    .then(()=>{

      alert("✅ تم نسخ سجل النقلات");

    })
    .catch(()=>{

      alert("لم يتمكن المتصفح من النسخ.");

    });

}


/* ================= NEW GAME ================= */

function newGameConfirm(){

  if(confirm("بدء مباراة جديدة؟")){

    startGame();

  }

}


/* ================= LEAVE ================= */

function leaveGame(){

  if(confirm("هل تريد الخروج من المباراة؟")){

    stopTimer();

    gameStarted=false;

    showHome();

  }

}


/* ================= INIT ================= */

showHome();

</script>

</body>
</html>
