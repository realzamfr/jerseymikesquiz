<!--
	Project: JerseyMikesQuiz
	Author: zamhvh
	© 2026 All Rights Reserved
	
	Unauthorized copying, modification, or distribution without the expressed written consent of Samuel Jenkins is prohibitied.
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
.dropzone.over{border-color:var(--blue);background:var(--blue-bg)}
.hint{font-size:13px;color:var(--faint);align-self:center;padding:4px 8px;pointer-events:none}
.pool-area{margin-top:16px}
.pool{display:flex;flex-wrap:wrap;gap:6px}
.chip{
  display:inline-flex;align-items:center;gap:6px;
  padding:6px 12px;
  background:var(--surface2);
  border:1px solid var(--border);
  border-radius:var(--radius-sm);
  cursor:grab;
  user-select:none;
  font-size:13px;
  color:var(--text);
  transition:background .15s,border-color .15s,opacity .15s;
  -webkit-user-drag:element;
}
.chip:hover{background:var(--faint);border-color:var(--border2)}
.chip.in-drop{cursor:default;background:var(--surface2)}
.chip.dragging{opacity:.35}
.rm{
  background:none;border:none;cursor:pointer;
  color:var(--muted);font-size:14px;line-height:1;
  padding:0;display:inline-flex;align-items:center;justify-content:center;
  width:14px;height:14px;
}
.rm:hover{color:var(--red)}
.nav{display:flex;align-items:center;justify-content:space-between;margin-top:12px}
.step{font-size:13px;color:var(--muted);font-family:'DM Mono',monospace}
.btn{
  padding:9px 20px;
  border:1px solid var(--border2);
  border-radius:var(--radius-sm);
  background:transparent;
  color:var(--text);
  font-size:14px;font-weight:500;
  cursor:pointer;
  font-family:'DM Sans',sans-serif;
  transition:background .15s,border-color .15s;
}
.btn:hover{background:var(--surface2);border-color:var(--border2)}
.btn.primary{background:var(--blue);border-color:var(--blue);color:#fff}
.btn.primary:hover{background:#3178d4;border-color:#3178d4}
.mw-option{
  display:flex;align-items:flex-start;gap:10px;
  padding:12px 14px;
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
</style>
</head>
<body>
<div class="wrap">
  <div class="header">
    <h1>Jersey Mike's Quiz</h1>
    <p>Drag the correct ingredients into each sub</p>
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

let idx=0,subsAns=[],mwAns=-1,dragged=null;

function setPct(v){document.getElementById("pf").style.width=v+"%";}
function pct(){setPct(idx/SUBS.length*100);}

function chip(name,inDrop){
  const c=document.createElement("span");
  c.className="chip"+(inDrop?" in-drop":"");
  c.dataset.v=name;
  c.draggable=!inDrop;
  if(!inDrop){
    c.ondragstart=e=>{dragged=name;c.classList.add("dragging");e.dataTransfer.effectAllowed="move";};
    c.ondragend=()=>c.classList.remove("dragging");
  }
  if(inDrop){
    c.innerHTML=`${name} <button class="rm" title="Remove" onclick="returnChip('${name.replace(/'/g,"\\'")}')">&#x2715;</button>`;
  } else {
    c.textContent=name;
  }
  return c;
}

function renderSub(){
  pct();
  const s=SUBS[idx];
  const ss=document.getElementById("subScreen");
  ss.innerHTML=`
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
      <button class="btn primary" onclick="nextQ()">Next &rarr;</button>
    </div>
  `;
  const dz=document.getElementById("dz");
  dz.appendChild(hint());
  dz.ondragover=e=>{e.preventDefault();dz.classList.add("over");};
  dz.ondragleave=()=>dz.classList.remove("over");
  dz.ondrop=onDrop;
  POOL.forEach(p=>document.getElementById("pool").appendChild(chip(p,false)));
}

function hint(){
  const h=document.createElement("span");
  h.className="hint";h.id="hint";h.textContent="Drag items here";return h;
}

function onDrop(e){
  e.preventDefault();
  const dz=document.getElementById("dz");
  dz.classList.remove("over");
  if(!dragged) return;
  const exists=[...dz.querySelectorAll(".chip")].map(x=>x.dataset.v);
  if(exists.includes(dragged)){dragged=null;return;}
  const fromPool=[...document.getElementById("pool").querySelectorAll(".chip")].find(x=>x.dataset.v===dragged);
  if(fromPool) fromPool.remove();
  const h=document.getElementById("hint");
  if(h) h.remove();
  dz.appendChild(chip(dragged,true));
  dragged=null;
}

function returnChip(name){
  const dz=document.getElementById("dz");
  const c=[...dz.querySelectorAll(".chip")].find(x=>x.dataset.v===name);
  if(c) c.remove();
  if(!dz.querySelector(".chip")) dz.appendChild(hint());
  document.getElementById("pool").appendChild(chip(name,false));
}

function saveAns(){
  const dz=document.getElementById("dz");
  subsAns[idx]=[...dz.querySelectorAll(".chip")].map(x=>x.dataset.v);
}

function nextQ(){
  saveAns();idx++;
  if(idx>=SUBS.length){startMW();return;}
  renderSub();
}

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
        <div class="mw-option" id="opt${i}" onclick="selMW(${i})">
          <input type="radio" name="mw" id="mwr${i}" value="${i}">
          <label for="mwr${i}">${o}</label>
        </div>`).join("")}
    </div>
    <div class="nav">
      <span class="step">${SUBS.length+1} / ${SUBS.length+1}</span>
      <button class="btn primary" onclick="finish()">See results &rarr;</button>
    </div>
  `;
}

function selMW(i){
  document.querySelectorAll(".mw-option").forEach(x=>x.classList.remove("selected"));
  document.getElementById("opt"+i).classList.add("selected");
  document.getElementById("mwr"+i).checked=true;
  mwAns=i;
}

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
renderSub();
</script>
</body>
</html>
