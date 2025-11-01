# games
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>10 Offline Mini Games — All-in-One</title>
<style>
  :root{
    --bg:#0f1724; --card:#0b1220; --muted:#cbd5e1; --accent:#60a5fa; --accent-2:#7c3aed;
    --glass: rgba(255,255,255,0.03);
  }
  *{box-sizing:border-box}
  html,body{height:100%; margin:0; font-family:Inter,system-ui,Segoe UI,Roboto,Arial; background:linear-gradient(180deg,#071026 0%, #0f1724 100%); color:var(--muted); -webkit-font-smoothing:antialiased;}
  .wrap{max-width:1100px;margin:20px auto;padding:20px}
  header{display:flex;align-items:center;justify-content:space-between;gap:12px;margin-bottom:18px}
  .brand{display:flex;align-items:center;gap:12px}
  .logo{width:56px;height:56px;border-radius:12px;background:linear-gradient(135deg,var(--accent),var(--accent-2));display:flex;align-items:center;justify-content:center;font-weight:800;color:white;font-size:18px;box-shadow:0 8px 30px rgba(92,99,148,0.25)}
  h1{margin:0;font-size:20px}
  .subtitle{color:rgba(203,213,225,0.7);font-size:13px}
  nav{display:flex;gap:8px;flex-wrap:wrap}
  .game-btn{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 12px;border-radius:10px;color:var(--muted);cursor:pointer;font-weight:700}
  .game-btn.active{background:linear-gradient(90deg,var(--accent),var(--accent-2));color:white;box-shadow:0 8px 30px rgba(124,58,237,0.18)}
  main{display:grid;grid-template-columns:320px 1fr;gap:18px}
  .panel{background:var(--card);border-radius:14px;padding:16px;box-shadow:0 10px 30px rgba(2,6,23,0.6)}
  .menu-list{display:flex;flex-direction:column;gap:8px}
  .small{font-size:13px;color:rgba(203,213,225,0.7)}
  /* game area */
  .game-stage{min-height:420px;padding:18px;border-radius:12px;display:flex;flex-direction:column;gap:12px;align-items:center;justify-content:flex-start}
  .top-row{display:flex;gap:12px;align-items:center;width:100%;justify-content:space-between}
  .score{background:rgba(255,255,255,0.03);padding:8px 12px;border-radius:9px;font-weight:700}
  .board{display:grid;gap:10px;justify-content:center}
  /* memory match */
  .mem-card{width:80px;height:80px;border-radius:10px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);display:flex;align-items:center;justify-content:center;font-size:28px;cursor:pointer;user-select:none}
  .mem-card.flipped{background:linear-gradient(180deg,var(--accent),var(--accent-2));color:white}
  /* whack */
  .hole{width:80px;height:60px;border-radius:10px;background:#071126;border:2px solid rgba(255,255,255,0.03);display:flex;align-items:flex-end;justify-content:center;padding-bottom:6px;position:relative;}
  .mole{width:56px;height:56px;border-radius:50%;background:linear-gradient(180deg,#ffb86b,#ff7a59);display:flex;align-items:center;justify-content:center;font-size:20px;transform:translateY(180%);transition:transform .18s cubic-bezier(.2,.9,.3,1);box-shadow:0 6px 18px rgba(0,0,0,0.4)}
  .mole.up{transform:translateY(0)}
  /* Simon */
  .simon-grid{display:grid;grid-template-columns:repeat(2,160px);grid-template-rows:repeat(2,160px);gap:10px}
  .simon-pad{border-radius:14px;cursor:pointer;display:flex;align-items:center;justify-content:center;font-weight:900;color:#071126;font-size:20px}
  .pad-0{background:#2ee6a3}
  .pad-1{background:#ffd86b}
  .pad-2{background:#ff7aa6}
  .pad-3{background:#7aa8ff}
  .pad-active{filter:brightness(1.25);transform:scale(1.03);box-shadow:0 10px 30px rgba(0,0,0,0.4)}
  /* tic */
  .ttt{display:grid;grid-template-columns:repeat(3,110px);gap:6px}
  .cell{width:110px;height:110px;border-radius:10px;background:rgba(255,255,255,0.02);display:flex;align-items:center;justify-content:center;font-size:36px;cursor:pointer}
  /* rps */
  .rps-row{display:flex;gap:12px}
  .rps-btn{padding:12px 16px;border-radius:10px;background:linear-gradient(90deg,var(--accent),var(--accent-2));border:none;color:white;cursor:pointer;font-weight:800}
  /* reaction */
  .react-box{width:300px;height:160px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:26px;cursor:pointer}
  /* snake canvas */
  canvas{background:#071126;border-radius:12px}
  /* slider puzzle */
  .slider-grid{display:grid;gap:4px;background:transparent}
  .sli-tile{width:96px;height:96px;border-radius:8px;background:linear-gradient(180deg,#2b6ef6,#6e3cf9);display:flex;align-items:center;justify-content:center;font-weight:800;color:white;cursor:pointer}
  /* common footer */
  .hint{color:rgba(203,213,225,0.6);font-size:13px}
  @media (max-width:880px){
    main{grid-template-columns:1fr;align-items:start}
    .simon-grid{grid-template-columns:repeat(2,calc(40vw));grid-template-rows:repeat(2,calc(40vw))}
    .ttt{grid-template-columns:repeat(3,calc((100vw - 80px)/3))}
  }
</style>
</head>
<body>
<div class="wrap">
  <header>
    <div class="brand">
      <div class="logo">G10</div>
      <div>
        <h1>10 Mini Games — Offline</h1>
        <div class="subtitle">Play 10 small games with polished visuals — no internet required</div>
      </div>
    </div>

    <nav id="menu" aria-label="Games menu"></nav>
  </header>

  <main>
    <aside class="panel">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
        <strong>Games</strong>
        <div class="hint">Tap or click to open</div>
      </div>
      <div class="menu-list" id="menuList"></div>

      <hr style="margin:14px 0;border:none;border-top:1px solid rgba(255,255,255,0.04)" />
      <div class="small">Controls: touch / mouse / keyboard (where supported)</div>
      <div style="margin-top:12px" class="small">Switch games without leaving the page. Scores reset per run.</div>
    </aside>

    <section class="panel game-stage" id="stage">
      <div class="top-row">
        <div>
          <div id="gTitle" style="font-weight:800;font-size:18px">Select a game</div>
          <div id="gSub" class="small">Choose from the left — 10 games included</div>
        </div>
        <div style="display:flex;gap:8px;align-items:center">
          <div id="scoreBox" class="score" style="display:none">Score: <span id="scoreVal">0</span></div>
          <button id="backBtn" class="game-btn" style="display:none">Back to Menu</button>
        </div>
      </div>

      <div id="gameArea" style="width:100%"></div>
      <div id="gameFooter" class="small hint" style="margin-top:6px"></div>
    </section>
  </main>
</div>

<script>
/* --- Games list (10) --- 
  1 Memory Match
  2 Whack-a-Mole
  3 Simon Says
  4 Tic-Tac-Toe
  5 Rock-Paper-Scissors
  6 Reaction Time
  7 Math Sprint
  8 Slider Puzzle (3x3)
  9 Color Match
 10 Snake
*/

const games = [
  {id:1, name:'Memory Match', fn:gameMemory},
  {id:2, name:'Whack-a-Mole', fn:gameWhack},
  {id:3, name:'Simon Says', fn:gameSimon},
  {id:4, name:'Tic-Tac-Toe', fn:gameTicTacToe},
  {id:5, name:'Rock-Paper-Scissors', fn:gameRPS},
  {id:6, name:'Reaction Time', fn:gameReaction},
  {id:7, name:'Math Sprint', fn:gameMath},
  {id:8, name:'Slider Puzzle', fn:gameSlider},
  {id:9, name:'Color Match', fn:gameColorMatch},
  {id:10,name:'Snake', fn:gameSnake}
];

const menuList = document.getElementById('menuList');
const gTitle = document.getElementById('gTitle');
const gSub = document.getElementById('gSub');
const gameArea = document.getElementById('gameArea');
const scoreBox = document.getElementById('scoreBox');
const scoreVal = document.getElementById('scoreVal');
const backBtn = document.getElementById('backBtn');
const gameFooter = document.getElementById('gameFooter');

let activeCancel = null;
let currentScore = 0;

function makeMenu(){
  games.forEach(g=>{
    const btn = document.createElement('button');
    btn.className = 'game-btn';
    btn.textContent = `${g.id}. ${g.name}`;
    btn.addEventListener('click', ()=>{
      document.querySelectorAll('.game-btn').forEach(b=>b.classList.remove('active'));
      btn.classList.add('active');
      openGame(g);
    });
    menuList.appendChild(btn);
  });
}
makeMenu();

backBtn.addEventListener('click', ()=>showMenu());

function showMenu(){
  cleanup();
  document.querySelectorAll('.game-btn').forEach(b=>b.classList.remove('active'));
  gTitle.textContent = 'Select a game';
  gSub.textContent = 'Choose from the left — 10 games included';
  gameArea.innerHTML = `<div class="hint" style="padding:26px;text-align:center">Pick a game to start. Each game is designed to be quick and fun.</div>`;
  scoreBox.style.display='none';
  backBtn.style.display='none';
  gameFooter.textContent='';
}

/* cleanup active game (stop timers, events, etc.) */
function cleanup(){
  if(activeCancel) {
    try { activeCancel(); } catch(e){/* ignore */ }
    activeCancel = null;
  }
  gameArea.innerHTML = '';
  currentScore = 0;
  scoreVal.textContent = '0';
  scoreBox.style.display='none';
}

/* Utility: shuffle */
function shuffle(a){ for(let i=a.length-1;i>0;i--){ const j=Math.floor(Math.random()*(i+1)); [a[i],a[j]]=[a[j],a[i]] } return a; }

/* ---------- Game 1: Memory Match ---------- */
function gameMemory(){
  cleanup();
  gTitle.textContent='Memory Match';
  gSub.textContent='Flip tiles and match pairs. Good visual feedback and emoji tiles.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';

  const symbols = ['🍎','🍌','🍇','🍓','🍒','🍋','🥝','🍑'];
  let cards = shuffle([...symbols, ...symbols]);
  let flipped = [];
  let matched = 0;
  currentScore = 0; scoreVal.textContent = currentScore;

  const board = document.createElement('div');
  board.className = 'board';
  board.style.gridTemplateColumns = 'repeat(4, 1fr)';
  cards.forEach((s, i)=>{
    const c = document.createElement('div');
    c.className='mem-card';
    c.dataset.symbol = s;
    c.addEventListener('click', ()=> {
      if(c.classList.contains('flipped') || c.classList.contains('matched') || flipped.length===2) return;
      c.classList.add('flipped'); c.textContent = s; flipped.push(c);
      if(flipped.length===2){
        const [a,b] = flipped;
        if(a.dataset.symbol === b.dataset.symbol){
          a.classList.add('matched'); b.classList.add('matched'); matched += 2; currentScore += 10;
          scoreVal.textContent = currentScore;
          flipped = [];
          if(matched === cards.length) {
            gameFooter.textContent = 'You won! Score: ' + currentScore;
          }
        } else {
          setTimeout(()=>{ a.textContent=''; b.textContent=''; a.classList.remove('flipped'); b.classList.remove('flipped'); flipped=[]; }, 700);
        }
      }
    });
    board.appendChild(c);
  });

  gameArea.appendChild(board);

  activeCancel = ()=>{ /* nothing to stop for this game */ };
}

/* ---------- Game 2: Whack-a-Mole ---------- */
function gameWhack(){
  cleanup();
  gTitle.textContent='Whack-a-Mole';
  gSub.textContent='Tap the moles as they pop up. Fast reflexes needed!';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  const grid = document.createElement('div');
  grid.style.display='grid';
  grid.style.gridTemplateColumns = 'repeat(3, 1fr)';
  grid.style.gridGap = '10px';
  grid.style.width = '100%';

  const holes = [];
  for(let i=0;i<9;i++){
    const hole = document.createElement('div'); hole.className='hole';
    const mole = document.createElement('div'); mole.className='mole'; mole.textContent='🐹';
    hole.appendChild(mole);
    grid.appendChild(hole);
    holes.push({hole,mole});
    mole.addEventListener('click', ()=>{ if(mole.classList.contains('up')){ mole.classList.remove('up'); currentScore += 5; scoreVal.textContent = currentScore; }});
  }

  gameArea.appendChild(grid);

  let running = true;
  function popRandom(){
    if(!running) return;
    const idx = Math.floor(Math.random()*holes.length);
    const m = holes[idx].mole;
    m.classList.add('up');
    setTimeout(()=>{ m.classList.remove('up'); }, 700 + Math.random()*900);
    const next = 400 + Math.random()*700;
    setTimeout(popRandom, next);
  }
  popRandom();

  activeCancel = ()=>{ running=false; holes.forEach(h=>h.mole.classList.remove('up')); };

  // stop button auto after 60s
  setTimeout(()=>{ if(running){ running=false; gameFooter.textContent='Time up! Final score: ' + currentScore; } }, 60000);
}

/* ---------- Game 3: Simon Says ---------- */
function gameSimon(){
  cleanup();
  gTitle.textContent='Simon Says';
  gSub.textContent='Repeat the color sequence. Level up as you succeed!';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  const seq = [];
  let playing = false;
  let idx = 0;

  const grid = document.createElement('div');
  grid.className='simon-grid';

  const colors = ['pad-0','pad-1','pad-2','pad-3'];
  for(let i=0;i<4;i++){
    const p = document.createElement('div'); p.className = 'simon-pad ' + colors[i]; p.dataset.index = i; p.textContent = '';
    p.addEventListener('click', ()=>{ if(!playing) return; handleInput(Number(p.dataset.index), p); });
    grid.appendChild(p);
  }

  const startBtn = document.createElement('button'); startBtn.className='game-btn'; startBtn.textContent='Start';
  startBtn.addEventListener('click', ()=>{
    seq.length=0; currentScore=0; scoreVal.textContent=currentScore; nextRound();
  });

  gameArea.appendChild(startBtn);
  gameArea.appendChild(grid);

  function flashPad(i, el, t=400){
    el.classList.add('pad-active');
    setTimeout(()=>el.classList.remove('pad-active'), t);
  }

  function nextRound(){
    playing = false;
    const r = Math.floor(Math.random()*4); seq.push(r);
    gSub.textContent = 'Watch the sequence';
    let delay = 400;
    seq.forEach((x,k)=>{
      setTimeout(()=>{ const pad = grid.children[x]; flashPad(x,pad); }, delay); delay += 600;
    });
    setTimeout(()=>{ playing=true; idx=0; gSub.textContent='Your turn — repeat the sequence'; }, delay);
  }

  function handleInput(i, el){
    if(!playing) return;
    flashPad(i, el, 200);
    if(seq[idx] === i){
      idx++;
      currentScore += 5; scoreVal.textContent = currentScore;
      if(idx === seq.length){
        playing=false;
        setTimeout(()=>{ nextRound(); }, 700);
      }
    } else {
      playing=false;
      gameFooter.textContent = 'Wrong move! Final score: ' + currentScore;
    }
  }

  activeCancel = ()=>{ /* nothing special */ };
}

/* ---------- Game 4: Tic-Tac-Toe ---------- */
function gameTicTacToe(){
  cleanup();
  gTitle.textContent='Tic-Tac-Toe';
  gSub.textContent='Classic 3x3 — play vs another local player.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  const board = Array(9).fill('');
  let turn = 'X';
  const b = document.createElement('div'); b.className='ttt';
  function draw(){
    b.innerHTML='';
    board.forEach((v,i)=>{
      const c = document.createElement('div'); c.className='cell'; c.textContent = v;
      c.addEventListener('click', ()=>{
        if(board[i] || checkWin(board)) return;
        board[i]=turn; c.textContent=turn;
        const w = checkWin(board);
        if(w){ gameFooter.textContent = w === 'Draw' ? 'Draw!' : (w+' wins!'); if(w!=='Draw') currentScore+=10; scoreVal.textContent=currentScore; return; }
        turn = turn === 'X' ? 'O' : 'X';
        gSub.textContent = 'Turn: ' + turn;
      });
      b.appendChild(c);
    });
  }
  function checkWin(bd){
    const lines = [[0,1,2],[3,4,5],[6,7,8],[0,3,6],[1,4,7],[2,5,8],[0,4,8],[2,4,6]];
    for(const [a,c,d] of lines){
      if(bd[a] && bd[a]===bd[c] && bd[a]===bd[d]) return bd[a];
    }
    if(bd.every(Boolean)) return 'Draw';
    return null;
  }

  const reset = document.createElement('button'); reset.className='game-btn'; reset.textContent='Reset';
  reset.addEventListener('click', ()=>{ board.fill(''); turn='X'; gSub.textContent='Turn: X'; gameFooter.textContent=''; draw(); });

  gameArea.appendChild(reset);
  gameArea.appendChild(b);
  gSub.textContent = 'Turn: X';
  draw();

  activeCancel = ()=>{/* nothing to cancel */};
}

/* ---------- Game 5: Rock-Paper-Scissors ---------- */
function gameRPS(){
  cleanup();
  gTitle.textContent='Rock — Paper — Scissors';
  gSub.textContent='Best of quick rounds. Tap your choice.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  const row = document.createElement('div'); row.className='rps-row';
  const choices = ['✊','✋','✌️'];
  choices.forEach((ch,i)=>{
    const btn = document.createElement('button'); btn.className='rps-btn'; btn.textContent = ch;
    btn.addEventListener('click', ()=>{
      const pc = Math.floor(Math.random()*3);
      const outcome = (i - pc + 3) % 3;
      // 0 draw, 1 win, 2 lose (from player's perspective)
      if(outcome === 1){ currentScore += 5; gameFooter.textContent = 'You win! Opponent: ' + choices[pc]; }
      else if(outcome === 2){ gameFooter.textContent = 'You lose! Opponent: ' + choices[pc]; }
      else { gameFooter.textContent = 'Draw — Opponent: ' + choices[pc]; }
      scoreVal.textContent = currentScore;
    });
    row.appendChild(btn);
  });

  gameArea.appendChild(row);
  activeCancel = ()=>{};
}

/* ---------- Game 6: Reaction Time ---------- */
function gameReaction(){
  cleanup();
  gTitle.textContent='Reaction Time';
  gSub.textContent='Wait for green, then tap/click as fast as you can.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  const box = document.createElement('div'); box.className='react-box'; box.style.background='#1f2937'; box.textContent='Click to start';
  let startAt = 0, waiting = false, running = false;
  box.addEventListener('click', ()=>{
    if(!running){
      box.textContent = 'Get ready...'; box.style.background = '#5b21b6'; running = true; waiting = true; gameFooter.textContent='';
      const delay = 1200 + Math.random()*2600;
      setTimeout(()=>{ if(!running) return; box.textContent='CLICK!'; box.style.background='#16a34a'; startAt = performance.now(); waiting = false; }, delay);
    } else {
      if(waiting){ // clicked too early
        running = false; gameFooter.textContent='Too soon! Click to try again.'; box.style.background='#991b1b'; box.textContent='Too soon'; setTimeout(()=>{ box.style.background='#1f2937'; box.textContent='Click to start'; },700);
        return;
      }
      const t = performance.now() - startAt; running=false;
      currentScore = Math.max(0, Math.round(1000 - t)); // higher is better
      scoreVal.textContent = currentScore; gameFooter.textContent = 'Reaction: ' + Math.round(t) + ' ms';
      box.style.background='#1f2937'; box.textContent='Click to try again';
    }
  });

  gameArea.appendChild(box);
  activeCancel = ()=>{ running=false; };
}

/* ---------- Game 7: Math Sprint ---------- */
function gameMath(){
  cleanup();
  gTitle.textContent='Math Sprint';
  gSub.textContent='Solve quick arithmetic under time pressure.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent = currentScore; gameFooter.textContent='';

  let timeLeft = 30; let interval;
  const qBox = document.createElement('div'); qBox.style.display='flex'; qBox.style.flexDirection='column'; qBox.style.alignItems='center'; qBox.style.gap='10px';
  const question = document.createElement('div'); question.style.fontSize='20px';
  const input = document.createElement('input'); input.style.padding='10px'; input.style.borderRadius='8px'; input.style.width='140px';
  input.type='number';
  const btn = document.createElement('button'); btn.className='game-btn'; btn.textContent='Start';

  let answer = null;
  function newQ(){
    const a = Math.floor(1+Math.random()*12);
    const b = Math.floor(1+Math.random()*12);
    answer = a*b;
    question.textContent = `${a} × ${b} = ?`;
    input.value = '';
    input.focus();
  }

  btn.addEventListener('click', ()=>{
    currentScore=0; scoreVal.textContent=currentScore; timeLeft=30; gameFooter.textContent='Time: 30s';
    newQ();
    interval = setInterval(()=>{ timeLeft--; gameFooter.textContent='Time: '+timeLeft+'s'; if(timeLeft<=0){ clearInterval(interval); gameFooter.textContent='Time up! Score: '+currentScore; } },1000);
  });

  input.addEventListener('keydown', (e)=>{
    if(e.key==='Enter'){ if(Number(input.value) === answer){ currentScore += 5; scoreVal.textContent = currentScore; newQ(); } else { /* wrong */ input.value=''; } }
  });

  qBox.appendChild(question); qBox.appendChild(input); qBox.appendChild(btn);
  gameArea.appendChild(qBox);

  activeCancel = ()=>{ clearInterval(interval); };
}

/* ---------- Game 8: Slider Puzzle (3x3) ---------- */
function gameSlider(){
  cleanup();
  gTitle.textContent='Slider Puzzle (3×3)';
  gSub.textContent='Arrange numbers to order. Click tiles adjacent to empty space.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent=currentScore; gameFooter.textContent='';

  const size = 3;
  let grid = [];
  for(let i=1;i<size*size;i++) grid.push(i);
  grid.push(null); // empty
  function shuffleGrid(){
    let arr = grid.slice();
    do{
      arr = shuffle(arr);
    }while(!isSolvable(arr));
    grid = arr;
  }
  function isSolvable(arr){
    const flat = arr.filter(Boolean);
    let inv = 0;
    for(let i=0;i<flat.length;i++) for(let j=i+1;j<flat.length;j++) if(flat[i] > flat[j]) inv++;
    return inv % 2 === 0;
  }

  const wrap = document.createElement('div'); wrap.style.display='inline-block';
  const board = document.createElement('div'); board.className='slider-grid'; board.style.gridTemplateColumns = `repeat(${size}, 1fr)`;
  board.style.width = (size*100 + (size-1)*4) + 'px';
  board.style.gridTemplateRows = `repeat(${size}, 1fr)`;

  function draw(){
    board.innerHTML='';
    grid.forEach((v, idx)=>{
      if(v === null){
        const blank = document.createElement('div'); blank.style.width='96px'; blank.style.height='96px';
        board.appendChild(blank);
      } else {
        const t = document.createElement('div'); t.className='sli-tile'; t.textContent = v;
        t.addEventListener('click', ()=>{ const emptyIdx = grid.indexOf(null); const x = idx%size, y=Math.floor(idx/size); const ex=emptyIdx%size, ey=Math.floor(emptyIdx/size);
          const dist = Math.abs(x-ex)+Math.abs(y-ey);
          if(dist===1){ grid[emptyIdx]=grid[idx]; grid[idx]=null; draw(); checkWin(); currentScore += 1; scoreVal.textContent=currentScore; }
        });
        board.appendChild(t);
      }
    });
  }

  function checkWin(){
    for(let i=0;i<grid.length-1;i++) if(grid[i] !== i+1) return;
    gameFooter.textContent = 'Solved! Moves: ' + currentScore;
  }

  const shuffleBtn = document.createElement('button'); shuffleBtn.className='game-btn'; shuffleBtn.textContent='Shuffle';
  shuffleBtn.addEventListener('click', ()=>{ shuffleGrid(); currentScore=0; scoreVal.textContent=currentScore; gameFooter.textContent='Shuffled — solve it!'; draw(); });

  wrap.appendChild(shuffleBtn); wrap.appendChild(board);
  gameArea.appendChild(wrap);

  shuffleGrid(); draw();

  activeCancel = ()=>{};
}

/* ---------- Game 9: Color Match ---------- */
function gameColorMatch(){
  cleanup();
  gTitle.textContent='Color Match';
  gSub.textContent='Pick the square that matches the color name/text.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent=currentScore; gameFooter.textContent='';

  const colors = [
    {name:'Crimson', value:'#dc2626'},
    {name:'Emerald', value:'#10b981'},
    {name:'Amber', value:'#f59e0b'},
    {name:'Indigo', value:'#6366f1'},
    {name:'Teal', value:'#14b8a6'},
    {name:'Pink', value:'#f472b6'}
  ];

  const target = document.createElement('div'); target.style.fontSize='18px'; target.style.fontWeight='800'; target.style.marginBottom='10px';
  const grid = document.createElement('div'); grid.style.display='grid'; grid.style.gridTemplateColumns='repeat(3, 1fr)'; grid.style.gap='10px'; grid.style.width='300px';

  function newRound(){
    const idx = Math.floor(Math.random()*colors.length);
    const correct = colors[idx];
    target.textContent = correct.name;
    const pool = shuffle(colors.slice()).slice(0,6);
    if(!pool.find(c=>c.name === correct.name)) pool[Math.floor(Math.random()*pool.length)] = correct;
    grid.innerHTML='';
    pool.forEach(c=>{
      const tile = document.createElement('div');
      tile.style.height='80px'; tile.style.borderRadius='8px'; tile.style.cursor='pointer';
      tile.style.background = c.value;
      tile.addEventListener('click', ()=>{
        if(c.name === correct.name){ currentScore += 10; scoreVal.textContent=currentScore; gameFooter.textContent='Correct!'; setTimeout(newRound,600); }
        else { gameFooter.textContent='Wrong — try again'; currentScore = Math.max(0,currentScore-2); scoreVal.textContent=currentScore; }
      });
      grid.appendChild(tile);
    });
  }

  gameArea.appendChild(target); gameArea.appendChild(grid);
  newRound();

  activeCancel = ()=>{};
}

/* ---------- Game 10: Snake (canvas) ---------- */
function gameSnake(){
  cleanup();
  gTitle.textContent='Snake';
  gSub.textContent='Classic snake on a canvas — arrow keys / swipes to control.';
  backBtn.style.display='inline-block';
  scoreBox.style.display='inline-block';
  currentScore = 0; scoreVal.textContent=currentScore; gameFooter.textContent='';

  const canvas = document.createElement('canvas'); canvas.width = 480; canvas.height = 360; canvas.style.width='100%';
  gameArea.appendChild(canvas);
  const ctx = canvas.getContext('2d');

  const gridSize = 20;
  let snake = [{x:5,y:5}];
  let dir = {x:1,y:0};
  let food = null;
  let running = true;
  let tick;

  function placeFood(){
    let tries=0;
    do{
      food = {x: Math.floor(Math.random()*(canvas.width/gridSize)), y: Math.floor(Math.random()*(canvas.height/gridSize))};
      tries++;
    }while(snake.find(s=>s.x===food.x && s.y===food.y) && tries<20);
  }

  function draw(){
    ctx.fillStyle = '#071026'; ctx.fillRect(0,0,canvas.width,canvas.height);
    // snake
    for(let i=0;i<snake.length;i++){
      const s = snake[i];
      ctx.fillStyle = i===0 ? '#60a5fa' : '#7c3aed';
      ctx.shadowColor = 'rgba(124,58,237,0.6)';
      ctx.shadowBlur = 12;
      ctx.fillRect(s.x*gridSize, s.y*gridSize, gridSize-2, gridSize-2);
      ctx.shadowBlur = 0;
    }
    // food
    if(food){
      ctx.fillStyle = '#fb923c';
      ctx.beginPath();
      ctx.arc(food.x*gridSize + gridSize/2 -1, food.y*gridSize + gridSize/2 -1, gridSize/2 -3, 0, Math.PI*2);
      ctx.fill();
    }
  }

  function step(){
    const head = {x: snake[0].x + dir.x, y: snake[0].y + dir.y};
    // wrap
    head.x = (head.x + canvas.width/gridSize) % (canvas.width/gridSize);
    head.y = (head.y + canvas.height/gridSize) % (canvas.height/gridSize);
    // check collision
    if(snake.find(s=>s.x===head.x && s.y===head.y)){ gameOver(); return; }
    snake.unshift(head);
    if(food && head.x===food.x && head.y===food.y){
      currentScore += 10; scoreVal.textContent = currentScore;
      placeFood();
    } else {
      snake.pop();
    }
    draw();
  }

  function gameOver(){
    running=false; clearInterval(tick); gameFooter.textContent='Game Over — Score: '+currentScore;
  }

  function start(){
    snake = [{x:5,y:5},{x:4,y:5},{x:3,y:5}]; dir={x:1,y:0}; placeFood(); currentScore=0; scoreVal.textContent = 0; running=true;
    draw();
    tick = setInterval(step, 140);
  }

  start();

  // controls
  window.addEventListener('keydown', onKey);
  let lastDir = {...dir};
  function onKey(e){
    if(e.key.includes('Arrow')){
      if(e.key==='ArrowUp' && lastDir.y===0){ dir={x:0,y:-1}; lastDir=dir; }
      else if(e.key==='ArrowDown' && lastDir.y===0){ dir={x:0,y:1}; lastDir=dir; }
      else if(e.key==='ArrowLeft' && lastDir.x===0){ dir={x:-1,y:0}; lastDir=dir; }
      else if(e.key==='ArrowRight' && lastDir.x===0){ dir={x:1,y:0}; lastDir=dir; }
    }
    if(e.key === ' ') { // pause/resume
      if(running){ clearInterval(tick); running=false; gameFooter.textContent='Paused'; }
      else { tick = setInterval(step,140); running=true; gameFooter.textContent=''; }
    }
  }

  // simple touch swipe
  let startTouch = null;
  canvas.addEventListener('touchstart', e=>{ const t = e.touches[0]; startTouch = {x:t.clientX, y:t.clientY}; });
  canvas.addEventListener('touchend', e=>{ if(!startTouch) return; const t = e.changedTouches[0]; const dx = t.clientX - startTouch.x, dy = t.clientY - startTouch.y;
    if(Math.abs(dx) > Math.abs(dy)){
      if(dx > 10 && lastDir.x===0){ dir={x:1,y:0}; lastDir=dir; }
      else if(dx < -10 && lastDir.x===0){ dir={x:-1,y:0}; lastDir=dir; }
    } else {
      if(dy > 10 && lastDir.y===0){ dir={x:0,y:1}; lastDir=dir; }
      else if(dy < -10 && lastDir.y===0){ dir={x:0,y:-1}; lastDir=dir; }
    }
    startTouch = null;
  });

  activeCancel = ()=>{ clearInterval(tick); window.removeEventListener('keydown', onKey); };
}

/* Start with menu view */
showMenu();

/* open game helper */
function openGame(g){
  cleanup();
  gTitle.textContent = g.name;
  gSub.textContent = 'Loading...';
  setTimeout(()=>{ // small delay for UX
    try { g.fn(); gSub.textContent = 'Playing: ' + g.name; } catch(e){ gameArea.innerHTML = '<div class="hint">Error loading game.</div>'; }
  }, 120);
}

/* expose showMenu in window for debugging (optional) */
window.showMenu = showMenu;

</script>
<p>
  <h1>hello everyone</h1>
</p>
</body>
</html>
