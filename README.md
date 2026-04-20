<!--
	Project: Jersey Mikes Quiz
	Author: zamhvh
	© 2026 All Rights Reserved
	
	Any form of unauthorized copying, modification, or distribution of this code and all its contents without the expressed written consent of Samuel Jenkins is prohibited and could lead to legal action.
-->

<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Jersey Mike's Quiz</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#0c0c0e;
  --surface:#141417;
  --surface2:#1c1c21;
  --border:#2a2a32;
  --border2:#38383f;
  --text:#f0f0f2;
  --muted:#6b6b78;
  --faint:#3a3a44;
  --blue:#4a8fff;
  --blue-bg:#0f1e36;
  --green:#3fcf6e;
  --green-bg:#0b2a1a;
  --amber:#f5a623;
  --amber-bg:#2a1d06;
  --red:#f55353;
  --red-bg:#2a0d0d;
  --radius:10px;
  --radius-sm:6px;
}
body{
  font-family:'DM Sans',system-ui,sans-serif;
  background:var(--bg);
  color:var(--text);
  min-height:100vh;
  padding:32px 16px 64px;
  /* Prevent text selection during drag */
  -webkit-user-select:none;
  user-select:none;
}
.wrap{max-width:680px;margin:auto}
.header{margin-bottom:28px}
.header h1{
  font-size:24px;font-weight:500;
  letter-spacing:-0.3px;
  margin-bottom:4px;
}
.header p{font-size:14px;color:var(--muted)}
.progress-track{
  height:3px;
  background:var(--surface2);
  border-radius:4px;
  overflow:hidden;
  margin-bottom:28px;
}
.progress-fill{
  height:100%;
  background:var(--blue);
  border-radius:4px;
  transition:width .5s cubic-bezier(.4,0,.2,1);
}
.card{
  background:var(--surface);
  border:1px solid var(--border);
  border-radius:var(--radius);
  padding:20px 24px;
  margin-bottom:12px;
}
.sub-num{
  font-family:'DM Mono',monospace;
  font-size:11px;
  color:var(--blue);
  letter-spacing:.5px;
  margin-bottom:4px;
}
.sub-name{font-size:20px;font-weight:500;margin-bottom:18px;letter-spacing:-0.2px}
.sect-label{
  font-size:11px;
  font-weight:500;
  color:var(--muted);
  letter-spacing:.7px;
  text-transform:uppercase;
  margin-bottom:8px;
}
.dropzone{
  min-height:68px;
  background:var(--bg);
  border:1px dashed var(--border2);
  border-radius:var(--radius-sm);
  padding:10px;
  display:flex;
  flex-wrap:wrap;
  gap:6px;
  align-items:flex-start;
  transition:border-color .2s,background .2s;
}
/* Desktop drag-over state */
.dropzone.over{border-color:var(--blue);background:var(--blue-bg)}
/* Mobile tap-to-add visual cue: dropzone is always a valid target */
.dropzone.tap-target{border-color:var(--blue);border-style:dashed}
.hint{font-size:13px;color:var(--faint);align-self:center;padding:4px 8px;pointer-events:none}
.pool-area{margin-top:16px}
.pool{display:flex;flex-wrap:wrap;gap:6px}

/* Base chip */
.chip{
  display:inline-flex;align-items:center;gap:6px;
  padding:8px 14px;
  background:var(--surface2);
  border:1px solid var(--border);
  border-radius:var(--radius-sm);
  user-select:none;
  font-size:13px;
  color:var(--text);
  transition:background .15s,border-color .15s,opacity .15s,transform .1s;
  touch-action:none; /* allow our custom touch handling */
  min-height:36px; /* bigger touch target on mobile */
}

/* Pool chip (can be added) */
.chip.pool-chip{
  cursor:grab;
}
.chip.pool-chip:hover{background:var(--faint);border-color:var(--border2)}

/* Tap-mode: highlight selected chip in pool */
.chip.pool-chip.tapped{
  background:var(--blue-bg);
  border-color:var(--blue);
  color:var(--blue);
}

/* Drop chip (inside dropzone) */
.chip.in-drop{cursor:default;}
.chip.in-drop:hover{background:var(--surface2)}

/* Dragging ghost */
.chip.dragging{opacity:.3;transform:scale(0.96)}

/* Floating drag ghost (cloned element) */
#dragGhost{
  position:fixed;
  pointer-events:none;
  z-index:9999;
  opacity:.85;
  transform:scale(1.05);
  transition:none;
  border-color:var(--blue);
  background:var(--blue-bg);
  color:var(--text);
}

.rm{
  background:none;border:none;cursor:pointer;
  color:var(--muted);font-size:14px;line-height:1;
  padding:0;display:inline-flex;align-items:center;justify-content:center;
  width:18px;height:18px;
  flex-shrink:0;
}
.rm:hover{color:var(--red)}
.nav{display:flex;align-items:center;justify-content:space-between;margin-top:12px}
.step{font-size:13px;color:var(--muted);font-family:'DM Mono',monospace}
.btn{
  padding:10px 20px;
  border:1px solid var(--border2);
  border-radius:var(--radius-sm);
  background:transparent;
  color:var(--text);
  font-size:14px;font-weight:500;
  cursor:pointer;
  font-family:'DM Sans',sans-serif;
  transition:background .15s,border-color .15s;
  min-height:40px;
}
.btn:hover{background:var(--surface2);border-color:var(--border2)}
.btn.primary{background:var(--blue);border-color:var(--blue);color:#fff}
.btn.primary:hover{background:#3178d4;border-color:#3178d4}
.mw-option{
  display:flex;align-items:flex-start;gap:10px;
  padding:14px;
  border:1px solid var(--border);
  border-radius:var(--radius-sm);
  margin-bottom:8px;
  cursor:pointer;
  transition:background .15s,border-color .15s;
}
.mw-option:hover{background:var(--surface2);border-color:var(--border2)}
.mw-option.selected{border-color:var(--blue);background:var(--blue-bg)}
.mw-option input{accent-color:var(--blue);margin-top:3px;flex-shrink:0}
.mw-option label{font-size:14px;cursor:pointer;line-height:1.5;color:var(--text)}
.result-score{text-align:center;padding:28px 0 20px}
.score-val{font-size:72px;font-weight:500;letter-spacing:-3px;line-height:1}
.score-sub{font-size:13px;color:var(--muted);margin-top:6px}
.score-grade{font-size:16px;font-weight:500;margin-top:8px}
.breakdown-item{
  display:flex;justify-content:space-between;align-items:flex-start;
  padding:12px 0;
  border-bottom:1px solid var(--border);
}
.breakdown-item:last-child{border-bottom:none}
.bi-name{font-size:14px;color:var(--text)}
.bi-num{font-size:11px;color:var(--muted);font-family:'DM Mono',monospace;margin-bottom:2px}
.bi-right{display:flex;align-items:center;gap:8px;flex-shrink:0;margin-left:12px}
.badge{
  padding:3px 8px;border-radius:4px;
  font-size:11px;font-weight:500;
  font-family:'DM Mono',monospace;
  white-space:nowrap;
}
.badge.full{background:var(--green-bg);color:var(--green)}
.badge.partial{background:var(--amber-bg);color:var(--amber)}
.badge.miss{background:var(--red-bg);color:var(--red)}
.expand{
  background:none;border:none;font-size:11px;color:var(--blue);
  cursor:pointer;font-family:'DM Sans',sans-serif;
  padding:0;white-space:nowrap;
}
.detail{font-size:12px;color:var(--muted);margin-top:6px;display:none;line-height:1.8}
.detail.open{display:block}
.tag{display:inline-block;padding:2px 7px;border-radius:3px;margin:2px;font-size:11px}
.tag.ok{background:var(--green-bg);color:var(--green)}
.tag.miss{background:var(--amber-bg);color:var(--amber)}
.tag.extra{background:var(--red-bg);color:var(--red)}
.actions{display:flex;gap:8px;margin-top:12px}
.hidden{display:none}

/* Mobile hint bar */
.mobile-hint{
  font-size:12px;color:var(--muted);
  text-align:center;
  margin-bottom:10px;
  display:none;
}
@media(hover:none){
  .mobile-hint{display:block}
}
</style>
</head>
<body>
<div class="wrap">
  <div class="header">
    <h1>Jersey Mike's Quiz</h1>
    <p>Add the correct ingredients to each sub</p>
  </div>
  <div class="progress-track"><div class="progress-fill" id="pf"></div></div>
  <div id="subScreen"></div>
  <div id="mwScreen" class="hidden"></div>
  <div id="resultScreen" class="hidden"></div>
</div>

<script>
const SUBS=[
  {name:"Jersey Shore",num:"#2",ingredients:["ham","provolone","cappacuolo"]},
  {name:"Ham & Provolone",num:"#3",ingredients:["ham","provolone"]},
  {name:"Super Sub",num:"#5",ingredients:["ham","provolone","prosciuttini","cappacuolo"]},
  {name:"Roast Beef & Provolone",num:"#6",ingredients:["roast beef","provolone"]},
  {name:"Turkey & Provolone",num:"#7",ingredients:["turkey","provolone"]},
  {name:"Club Sub",num:"#8",ingredients:["turkey","ham","provolone","bacon","mayo"]},
  {name:"Club Supreme",num:"#9",ingredients:["roast beef","turkey","swiss","bacon","mayo"]},
  {name:"Tuna Fish",num:"#10",ingredients:["tuna"]},
  {name:"Original Italian",num:"#13",ingredients:["ham","provolone","cappacuolo","prosciuttini","salami","pepperoni"]},
  {name:"Veggie",num:"#14",ingredients:["swiss","provolone","bell peppers"]}
];
const POOL=[...new Set(SUBS.flatMap(s=>s.ingredients))].sort();
const MW={
  q:"What is the correct Mike's Way order?",
  opts:[
    "onions, lettuce, tomato, vinegar, oil, oregano, salt",
    "lettuce, tomato, onions, oil, vinegar, salt, oregano",
    "onions, tomato, lettuce, oil, vinegar, oregano, salt",
    "lettuce, onions, tomato, vinegar, oil, salt, oregano"
  ],
  ans:0
};

let idx=0, subsAns=[], mwAns=-1;

// ─── Drag state (desktop HTML5 + touch) ───────────────────────────────────────
let dragged=null;       // name string being dragged
let ghost=null;         // floating DOM clone for touch drag
let touchSrc=null;      // source chip element for touch drag
let touchOffX=0, touchOffY=0;

// ─── Tap state (mobile tap-to-add) ────────────────────────────────────────────
let tappedChip=null;    // currently selected pool chip name (tap mode)

// Detect if the device primarily uses touch (no fine pointer)
const isTouchDevice=()=>window.matchMedia('(hover:none)').matches;

// ─── Helpers ──────────────────────────────────────────────────────────────────
function setPct(v){document.getElementById("pf").style.width=v+"%";}
function pct(){setPct(idx/SUBS.length*100);}

function getDropzone(){return document.getElementById("dz");}
function getPool(){return document.getElementById("pool");}

function getDropzoneItems(){
  return [...getDropzone().querySelectorAll(".chip")].map(x=>x.dataset.v);
}

function hint(){
  const h=document.createElement("span");
  h.className="hint";h.id="hint";
  h.textContent=isTouchDevice()?"Tap an ingredient below to add":"Drag items here";
  return h;
}

function refreshHint(){
  const dz=getDropzone();
  const h=document.getElementById("hint");
  if(dz.querySelectorAll(".chip").length===0){
    if(!h) dz.appendChild(hint());
  } else {
    if(h) h.remove();
  }
}

// ─── Chip factory ─────────────────────────────────────────────────────────────
function makeDropChip(name){
  const c=document.createElement("span");
  c.className="chip in-drop";
  c.dataset.v=name;
  c.innerHTML=`${name}<button class="rm" title="Remove">&#x2715;</button>`;
  c.querySelector(".rm").addEventListener("click",e=>{
    e.stopPropagation();
    returnChip(name);
  });
  return c;
}

function makePoolChip(name){
  const c=document.createElement("span");
  c.className="chip pool-chip";
  c.dataset.v=name;
  c.draggable=true;
  c.textContent=name;

  // ── Desktop drag events ──
  c.addEventListener("dragstart",e=>{
    dragged=name;
    c.classList.add("dragging");
    e.dataTransfer.effectAllowed="move";
  });
  c.addEventListener("dragend",()=>{
    c.classList.remove("dragging");
    dragged=null;
  });

  // ── Touch drag events ──
  c.addEventListener("touchstart",onTouchStart,{passive:false});

  // ── Tap-to-add (touch) ──
  c.addEventListener("click",()=>{
    if(!isTouchDevice()) return; // desktop handles via drag
    handleTapOnPoolChip(name, c);
  });

  return c;
}

// ─── Desktop drop handling ─────────────────────────────────────────────────────
function bindDropzone(dz){
  dz.addEventListener("dragover",e=>{e.preventDefault();dz.classList.add("over");});
  dz.addEventListener("dragleave",()=>dz.classList.remove("over"));
  dz.addEventListener("drop",e=>{
    e.preventDefault();
    dz.classList.remove("over");
    if(!dragged) return;
    addToDropzone(dragged);
    dragged=null;
  });
}

// ─── Touch drag handling ──────────────────────────────────────────────────────
function onTouchStart(e){
  if(isTouchDevice()) return; // let tap handler deal with it on touch-primary devices
  const touch=e.touches[0];
  const chip=e.currentTarget;
  const name=chip.dataset.v;
  const rect=chip.getBoundingClientRect();
  touchOffX=touch.clientX-rect.left;
  touchOffY=touch.clientY-rect.top;
  touchSrc=chip;

  // Create ghost
  ghost=chip.cloneNode(true);
  ghost.id="dragGhost";
  ghost.classList.add("chip");
  ghost.style.width=rect.width+"px";
  ghost.style.left=(touch.clientX-touchOffX)+"px";
  ghost.style.top=(touch.clientY-touchOffY)+"px";
  document.body.appendChild(ghost);

  chip.classList.add("dragging");
  e.preventDefault();

  document.addEventListener("touchmove",onTouchMove,{passive:false});
  document.addEventListener("touchend",onTouchEnd);
}

function onTouchMove(e){
  if(!ghost) return;
  const touch=e.touches[0];
  ghost.style.left=(touch.clientX-touchOffX)+"px";
  ghost.style.top=(touch.clientY-touchOffY)+"px";
  e.preventDefault();
}

function onTouchEnd(e){
  document.removeEventListener("touchmove",onTouchMove);
  document.removeEventListener("touchend",onTouchEnd);
  if(!ghost||!touchSrc) return;

  const touch=e.changedTouches[0];
  ghost.remove(); ghost=null;
  touchSrc.classList.remove("dragging");

  const name=touchSrc.dataset.v;
  touchSrc=null;

  // Hit test: is the finger over the dropzone?
  const dz=getDropzone();
  if(!dz) return;
  const r=dz.getBoundingClientRect();
  if(touch.clientX>=r.left&&touch.clientX<=r.right&&
     touch.clientY>=r.top&&touch.clientY<=r.bottom){
    addToDropzone(name);
  }
}

// ─── Tap-to-add (touch primary devices) ──────────────────────────────────────
function handleTapOnPoolChip(name, chipEl){
  // If already tapped, deselect
  if(tappedChip===name){
    chipEl.classList.remove("tapped");
    tappedChip=null;
    getDropzone().classList.remove("tap-target");
    return;
  }
  // Deselect previous
  if(tappedChip){
    const prev=getPool().querySelector(`[data-v="${CSS.escape(tappedChip)}"]`);
    if(prev) prev.classList.remove("tapped");
  }
  tappedChip=name;
  chipEl.classList.add("tapped");
  // Highlight dropzone as target
  getDropzone().classList.add("tap-target");
}

// Tapping the dropzone when a chip is selected adds it
function bindDropzoneTap(dz){
  dz.addEventListener("click",()=>{
    if(!tappedChip) return;
    addToDropzone(tappedChip);
    tappedChip=null;
    dz.classList.remove("tap-target");
  });
}

// ─── Core add/remove ─────────────────────────────────────────────────────────
function addToDropzone(name){
  const dz=getDropzone();
  const pool=getPool();
  if(getDropzoneItems().includes(name)) return; // already there
  const fromPool=pool.querySelector(`[data-v="${CSS.escape(name)}"]`);
  if(fromPool) fromPool.remove();
  dz.appendChild(makeDropChip(name));
  refreshHint();
}

function returnChip(name){
  const dz=getDropzone();
  const c=[...dz.querySelectorAll(".chip")].find(x=>x.dataset.v===name);
  if(c) c.remove();
  refreshHint();
  const pool=getPool();
  if(!pool.querySelector(`[data-v="${CSS.escape(name)}"]`)){
    pool.appendChild(makePoolChip(name));
  }
  // Deselect tap if returning the tapped chip
  if(tappedChip===name){
    tappedChip=null;
    dz.classList.remove("tap-target");
  }
}

// ─── Render ──────────────────────────────────────────────────────────────────
function renderSub(){
  pct();
  tappedChip=null;
  const s=SUBS[idx];
  const ss=document.getElementById("subScreen");
  ss.classList.remove("hidden");
  ss.innerHTML=`
    <div class="mobile-hint">Tap an ingredient to select it, then tap the box above to add it</div>
    <div class="card">
      <div class="sub-num">${s.num}</div>
      <div class="sub-name">${s.name}</div>
      <div class="sect-label">Drop ingredients</div>
      <div class="dropzone" id="dz"></div>
      <div class="pool-area">
        <div class="sect-label">Ingredients</div>
        <div class="pool" id="pool"></div>
      </div>
    </div>
    <div class="nav">
      <span class="step">${idx+1} / ${SUBS.length+1}</span>
      <button class="btn primary" id="nextBtn">Next &rarr;</button>
    </div>
  `;

  const dz=document.getElementById("dz");
  dz.appendChild(hint());
  bindDropzone(dz);
  bindDropzoneTap(dz);

  document.getElementById("nextBtn").addEventListener("click",nextQ);

  const pool=document.getElementById("pool");
  POOL.forEach(p=>pool.appendChild(makePoolChip(p)));
}

function saveAns(){
  subsAns[idx]=getDropzoneItems();
}

function nextQ(){
  saveAns();
  idx++;
  tappedChip=null;
  if(idx>=SUBS.length){startMW();return;}
  renderSub();
}

// ─── Mike's Way ──────────────────────────────────────────────────────────────
function startMW(){
  document.getElementById("subScreen").classList.add("hidden");
  const ms=document.getElementById("mwScreen");
  ms.classList.remove("hidden");
  setPct(SUBS.length/(SUBS.length+1)*100);
  ms.innerHTML=`
    <div class="card">
      <div class="sub-num">Mike's Way</div>
      <div class="sub-name" style="margin-bottom:16px">${MW.q}</div>
      ${MW.opts.map((o,i)=>`
        <div class="mw-option" id="opt${i}">
          <input type="radio" name="mw" id="mwr${i}" value="${i}">
          <label for="mwr${i}">${o}</label>
        </div>`).join("")}
    </div>
    <div class="nav">
      <span class="step">${SUBS.length+1} / ${SUBS.length+1}</span>
      <button class="btn primary" id="finBtn">See results &rarr;</button>
    </div>
  `;
  MW.opts.forEach((_,i)=>{
    document.getElementById("opt"+i).addEventListener("click",()=>selMW(i));
  });
  document.getElementById("finBtn").addEventListener("click",finish);
}

function selMW(i){
  document.querySelectorAll(".mw-option").forEach(x=>x.classList.remove("selected"));
  document.getElementById("opt"+i).classList.add("selected");
  document.getElementById("mwr"+i).checked=true;
  mwAns=i;
}

// ─── Results ─────────────────────────────────────────────────────────────────
function finish(){
  document.getElementById("mwScreen").classList.add("hidden");
  const rs=document.getElementById("resultScreen");
  rs.classList.remove("hidden");
  setPct(100);

  let total=0;
  const items=SUBS.map((s,i)=>{
    const u=(subsAns[i]||[]).map(x=>x.toLowerCase());
    const c=s.ingredients.map(x=>x.toLowerCase());
    const hits=u.filter(x=>c.includes(x));
    const extras=u.filter(x=>!c.includes(x));
    const missed=c.filter(x=>!u.includes(x));
    const r=hits.length/c.length;
    total+=r;
    return{s,u,c,hits,extras,missed,r};
  });
  const mwOk=mwAns===MW.ans;
  if(mwOk) total+=1;
  const p=Math.round(total/(SUBS.length+1)*100);
  const grade=p>=90?"Excellent":p>=75?"Good":p>=50?"Needs work":"Keep practicing";
  const gc=p>=90?"var(--green)":p>=75?"var(--blue)":p>=50?"var(--amber)":"var(--red)";

  rs.innerHTML=`
    <div class="card result-score">
      <div class="score-val">${p}%</div>
      <div class="score-sub">overall score</div>
      <div class="score-grade" style="color:${gc}">${grade}</div>
    </div>
    <div class="card breakdown">
      ${items.map((it,i)=>{
        const bc=it.r===1?"full":it.r>0?"partial":"miss";
        const bl=it.r===1?"Perfect":it.r>0?`${it.hits.length}/${it.c.length}`:"0 / "+it.c.length;
        return `<div class="breakdown-item">
          <div style="flex:1;min-width:0">
            <div class="bi-num">${SUBS[i].num}</div>
            <div class="bi-name">${SUBS[i].name}</div>
            <div class="detail" id="d${i}">
              ${it.hits.map(x=>`<span class="tag ok">&#10003; ${x}</span>`).join("")}
              ${it.missed.map(x=>`<span class="tag miss">&#8722; ${x}</span>`).join("")}
              ${it.extras.map(x=>`<span class="tag extra">&#43; ${x} (extra)</span>`).join("")}
            </div>
          </div>
          <div class="bi-right">
            <span class="badge ${bc}">${bl}</span>
            <button class="expand" onclick="toggle('d${i}')">details</button>
          </div>
        </div>`;
      }).join("")}
      <div class="breakdown-item">
        <div style="flex:1">
          <div class="bi-num">Mike's Way</div>
          <div class="bi-name">Correct order</div>
          <div class="detail" id="dmw">
            <div style="margin-top:4px;color:var(--muted)">
              <span style="color:var(--text)">Correct:</span> ${MW.opts[MW.ans]}<br>
              ${mwAns!==-1&&!mwOk?`<span style="color:var(--text)">You chose:</span> ${MW.opts[mwAns]}`:""}
            </div>
          </div>
        </div>
        <div class="bi-right">
          <span class="badge ${mwOk?"full":"miss"}">${mwOk?"Correct":"Wrong"}</span>
          <button class="expand" onclick="toggle('dmw')">details</button>
        </div>
      </div>
    </div>
    <div class="actions">
      <button class="btn primary" onclick="location.reload()">Try again</button>
    </div>
  `;
}

function toggle(id){document.getElementById(id).classList.toggle("open");}

// ─── Init ─────────────────────────────────────────────────────────────────────
renderSub();
</script>
</body>
</html>
