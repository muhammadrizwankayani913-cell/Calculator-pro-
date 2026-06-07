PRO calc
html_code = '''<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>Calculator</title>
<style>
* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }
body {
  min-height:100vh; display:flex; justify-content:center; align-items:center;
  font-family:'Segoe UI',system-ui,sans-serif; padding:8px;
  background:radial-gradient(ellipse at 20% 20%,rgba(120,119,198,0.3) 0%,transparent 50%),
             radial-gradient(ellipse at 80% 80%,rgba(255,119,198,0.15) 0%,transparent 50%),
             radial-gradient(ellipse at 50% 50%,rgba(99,102,241,0.1) 0%,transparent 60%),
             linear-gradient(135deg,#0f0c29 0%,#1a1a2e 25%,#16213e 50%,#1a1a2e 75%,#0f0c29 100%);
  background-attachment:fixed; position:relative; overflow:hidden;
}
body::before {
  content:''; position:fixed; top:0; left:0; right:0; bottom:0;
  background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,255,255,0.03) 2px,rgba(0,255,255,0.03) 4px);
  pointer-events:none; z-index:0;
}
body::after {
  content:''; position:fixed; top:-50%; left:-50%; width:200%; height:200%;
  background:conic-gradient(from 0deg,transparent 0deg,rgba(99,102,241,0.03) 60deg,transparent 120deg,rgba(236,72,153,0.03) 180deg,transparent 240deg,rgba(99,102,241,0.03) 300deg,transparent 360deg);
  animation:rotate 30s linear infinite; pointer-events:none; z-index:0;
}
@keyframes rotate { 100% { transform:rotate(360deg); } }
.calc {
  width:100%; max-width:340px; position:relative; z-index:1;
  background:linear-gradient(145deg,rgba(255,255,255,0.1) 0%,rgba(255,255,255,0.05) 100%);
  border-radius:24px; padding:16px;
  backdrop-filter:blur(30px) saturate(180%);
  border:1px solid rgba(255,255,255,0.18);
  box-shadow:0 0 0 1px rgba(255,255,255,0.05) inset,
             0 25px 50px -12px rgba(0,0,0,0.5),
             0 0 100px rgba(99,102,241,0.1);
}
.calc::before {
  content:''; position:absolute; top:0; left:0; right:0; bottom:0;
  border-radius:24px; padding:1.5px;
  background:linear-gradient(135deg,rgba(99,102,241,0.4),rgba(236,72,153,0.2),rgba(99,102,241,0.4));
  -webkit-mask:linear-gradient(#fff 0 0) content-box,linear-gradient(#fff 0 0);
  -webkit-mask-composite:xor; mask-composite:exclude; pointer-events:none;
}
.screen {
  background:linear-gradient(180deg,rgba(0,0,0,0.6) 0%,rgba(0,0,0,0.4) 100%);
  border-radius:16px; padding:16px 14px; margin-bottom:14px;
  text-align:right; min-height:100px;
  display:flex; flex-direction:column; justify-content:flex-end;
  border:1px solid rgba(255,255,255,0.08);
  box-shadow:inset 0 2px 10px rgba(0,0,0,0.3),0 1px 0 rgba(255,255,255,0.05);
  position:relative; overflow:hidden;
}
.screen::after {
  content:''; position:absolute; top:0; left:0; right:0; height:1px;
  background:linear-gradient(90deg,transparent,rgba(255,255,255,0.2),transparent);
}
#expr { color:rgba(255,255,255,0.45); font-size:13px; word-break:break-all; min-height:18px; letter-spacing:0.5px; }
#result { color:#fff; font-size:36px; font-weight:300; word-break:break-all; margin-top:4px; text-shadow:0 0 20px rgba(255,255,255,0.15); }
.modes { display:flex; gap:8px; margin-bottom:12px; justify-content:center; }
.mode-btn {
  flex:1; padding:8px; border:none; border-radius:10px;
  background:rgba(255,255,255,0.06); color:#888; font-size:12px;
  cursor:pointer; transition:0.3s; font-weight:500; letter-spacing:0.5px;
  border:1px solid rgba(255,255,255,0.08); position:relative; overflow:hidden;
}
.mode-btn.active {
  background:linear-gradient(135deg,#6366f1,#ec4899); color:#fff;
  box-shadow:0 4px 20px rgba(99,102,241,0.4),0 0 0 1px rgba(255,255,255,0.1) inset;
  border:none;
}
.btns { display:grid; grid-template-columns:repeat(4,1fr); gap:8px; }
.btn {
  border:none; border-radius:12px; padding:12px 0; font-size:16px;
  cursor:pointer; transition:0.15s; font-weight:500; color:#fff;
  position:relative; overflow:hidden; backdrop-filter:blur(10px);
}
.btn:active { transform:scale(0.88); }
.num {
  background:linear-gradient(145deg,rgba(255,255,255,0.14) 0%,rgba(255,255,255,0.07) 100%);
  border:1px solid rgba(255,255,255,0.1);
  box-shadow:0 4px 15px rgba(0,0,0,0.1),inset 0 1px 0 rgba(255,255,255,0.1);
}
.num:hover { background:linear-gradient(145deg,rgba(255,255,255,0.22) 0%,rgba(255,255,255,0.12) 100%); }
.op {
  background:linear-gradient(145deg,rgba(99,102,241,0.3) 0%,rgba(99,102,241,0.15) 100%);
  border:1px solid rgba(99,102,241,0.25); color:#a5b4fc;
  box-shadow:0 4px 15px rgba(99,102,241,0.15),inset 0 1px 0 rgba(255,255,255,0.1);
}
.op:hover { background:linear-gradient(145deg,rgba(99,102,241,0.45) 0%,rgba(99,102,241,0.25) 100%); }
.fn {
  background:linear-gradient(145deg,rgba(236,72,153,0.2) 0%,rgba(236,72,153,0.1) 100%);
  border:1px solid rgba(236,72,153,0.2); color:#f9a8d4; font-size:13px;
  box-shadow:0 4px 15px rgba(236,72,153,0.1),inset 0 1px 0 rgba(255,255,255,0.1);
}
.fn:hover { background:linear-gradient(145deg,rgba(236,72,153,0.35) 0%,rgba(236,72,153,0.2) 100%); }
.eq {
  background:linear-gradient(145deg,#6366f1 0%,#ec4899 100%);
  box-shadow:0 4px 20px rgba(99,102,241,0.4),0 0 0 1px rgba(255,255,255,0.15) inset;
  font-size:18px; grid-column:span 1;
}
.eq:hover { background:linear-gradient(145deg,#818cf8 0%,#f472b6 100%); }
.ac {
  background:linear-gradient(145deg,rgba(245,158,11,0.25) 0%,rgba(245,158,11,0.12) 100%);
  border:1px solid rgba(245,158,11,0.2); color:#fcd34d;
}
.del {
  background:linear-gradient(145deg,rgba(245,158,11,0.25) 0%,rgba(245,158,11,0.12) 100%);
  border:1px solid rgba(245,158,11,0.2); color:#fcd34d;
}
.zero { grid-column:span 2; }
.hide { display:none !important; }
@media(max-width:360px){ .calc{max-width:100%;padding:12px;} .btn{padding:10px 0;font-size:14px;} .fn{font-size:11px;} #result{font-size:30px;} .screen{min-height:80px;padding:12px 10px;} }
@media(max-width:320px){ .btn{padding:8px 0;font-size:13px;} .fn{font-size:10px;} }
</style>
</head>
<body>
<div class="calc">
  <div class="screen">
    <div id="expr"></div>
    <div id="result">0</div>
  </div>
  <div class="modes">
    <button class="mode-btn active" onclick="setMode('simple')">Simple</button>
    <button class="mode-btn" onclick="setMode('sci')">Scientific</button>
  </div>
  <div class="btns" id="simple">
    <button class="btn ac" onclick="clr()">AC</button>
    <button class="btn del" onclick="back()">⌫</button>
    <button class="btn op" onclick="add('%')">%</button>
    <button class="btn op" onclick="add('/')">÷</button>
    <button class="btn num" onclick="add('7')">7</button>
    <button class="btn num" onclick="add('8')">8</button>
    <button class="btn num" onclick="add('9')">9</button>
    <button class="btn op" onclick="add('*')">×</button>
    <button class="btn num" onclick="add('4')">4</button>
    <button class="btn num" onclick="add('5')">5</button>
    <button class="btn num" onclick="add('6')">6</button>
    <button class="btn op" onclick="add('-')">−</button>
    <button class="btn num" onclick="add('1')">1</button>
    <button class="btn num" onclick="add('2')">2</button>
    <button class="btn num" onclick="add('3')">3</button>
    <button class="btn op" onclick="add('+')">+</button>
    <button class="btn num zero" onclick="add('0')">0</button>
    <button class="btn num" onclick="add('.')">.</button>
    <button class="btn eq" onclick="calc()">=</button>
  </div>
  <div class="btns hide" id="sci">
    <button class="btn ac" onclick="clr()">AC</button>
    <button class="btn del" onclick="back()">⌫</button>
    <button class="btn fn" onclick="add('(')">(</button>
    <button class="btn fn" onclick="add(')')">)</button>
    <button class="btn fn" onclick="ins('Math.sin(')">sin</button>
    <button class="btn fn" onclick="ins('Math.cos(')">cos</button>
    <button class="btn fn" onclick="ins('Math.tan(')">tan</button>
    <button class="btn op" onclick="add('/')">÷</button>
    <button class="btn fn" onclick="ins('Math.log(')">ln</button>
    <button class="btn fn" onclick="ins('Math.log10(')">log</button>
    <button class="btn fn" onclick="add('^')">xʸ</button>
    <button class="btn op" onclick="add('*')">×</button>
    <button class="btn fn" onclick="ins('Math.sqrt(')">√</button>
    <button class="btn fn" onclick="ins('Math.PI')">π</button>
    <button class="btn fn" onclick="ins('Math.E')">e</button>
    <button class="btn op" onclick="add('-')">−</button>
    <button class="btn num" onclick="add('7')">7</button>
    <button class="btn num" onclick="add('8')">8</button>
    <button class="btn num" onclick="add('9')">9</button>
    <button class="btn op" onclick="add('+')">+</button>
    <button class="btn num" onclick="add('4')">4</button>
    <button class="btn num" onclick="add('5')">5</button>
    <button class="btn num" onclick="add('6')">6</button>
    <button class="btn fn" onclick="ins('Math.abs(')">|x|</button>
    <button class="btn num" onclick="add('1')">1</button>
    <button class="btn num" onclick="add('2')">2</button>
    <button class="btn num" onclick="add('3')">3</button>
    <button class="btn op" onclick="add('%')">%</button>
    <button class="btn num zero" onclick="add('0')">0</button>
    <button class="btn num" onclick="add('.')">.</button>
    <button class="btn eq" onclick="calc()">=</button>
  </div>
</div>
<script>
let expr='',res='0';
function show(){ document.getElementById('expr').textContent=expr; document.getElementById('result').textContent=res||'0'; }
function add(c){ expr+=c; show(); }
function ins(c){ expr+=c; show(); }
function clr(){ expr=''; res='0'; show(); }
function back(){ expr=expr.slice(0,-1); show(); }
function calc(){
  try{
    let e=expr.replace(/\\^/g,'**').replace(/×/g,'*').replace(/÷/g,'/').replace(/−/g,'-');
    res=eval(e); if(!isFinite(res)||isNaN(res)) throw 0;
    res=Math.round(res*1e12)/1e12;
    show(); expr=String(res);
  }catch(x){ res='Error'; show(); expr=''; }
}
function setMode(m){
  document.querySelectorAll('.mode-btn').forEach(function(b){ b.classList.remove('active'); });
  event.target.classList.add('active');
  document.getElementById('simple').classList.toggle('hide',m!='simple');
  document.getElementById('sci').classList.toggle('hide',m!='sci');
}
document.addEventListener('keydown',function(e){
  var k=e.key;
  if(/[0-9+\\-*/.()%^]/.test(k)) add(k);
  if(k==='Enter') calc();
  if(k==='Backspace') back();
  if(k==='Escape') clr();
});
</script>
</body>
</html>'''

with open('/mnt/agents/output/calculator.html', 'w', encoding='utf-8') as f:
    f.write(html_code)

print("File saved successfully!")
print(f"Total characters: {len(html_code)}")
