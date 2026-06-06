pro calc : 


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Pro Scientific Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
        }
        
        :root {
            --bg: #0a0a0f;
            --bg-card: #12121a;
            --bg-btn: #1a1a2e;
            --bg-btn-num: #1e1e2e;
            --text: #ffffff;
            --text-dim: #8888a0;
            --cyan: #00d4ff;
            --purple: #a855f7;
            --red: #ef4444;
            --green: #22c55e;
            --orange: #f97316;
        }
        
        body {
            background: var(--bg);
            color: var(--text);
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            height: 100vh;
            width: 100vw;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .calc-wrap {
            width: 100%;
            height: 100%;
            max-width: 400px;
            display: flex;
            flex-direction: column;
            background: var(--bg-card);
            position: relative;
        }
        
        @media (min-width: 401px) {
            .calc-wrap {
                height: 95vh;
                border-radius: 16px;
                border: 1px solid rgba(255,255,255,0.05);
                box-shadow: 0 0 40px rgba(0,212,255,0.1);
            }
        }
        
        /* Header - Compact */
        .header {
            padding: 8px 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255,255,255,0.03);
            flex-shrink: 0;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 6px;
        }
        
        .logo-icon {
            width: 28px;
            height: 28px;
            background: linear-gradient(135deg, var(--cyan), var(--purple));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            font-weight: bold;
        }
        
        .logo-text {
            font-size: 14px;
            font-weight: 700;
            letter-spacing: 1px;
            background: linear-gradient(90deg, var(--cyan), var(--purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .header-btn {
            background: none;
            border: none;
            color: var(--text-dim);
            font-size: 16px;
            cursor: pointer;
            padding: 4px;
        }
        
        /* Mode Tabs */
        .tabs {
            display: flex;
            padding: 4px 8px;
            gap: 6px;
            flex-shrink: 0;
        }
        
        .tab {
            flex: 1;
            padding: 6px;
            border: none;
            border-radius: 8px;
            background: var(--bg-btn);
            color: var(--text-dim);
            font-size: 11px;
            font-weight: 700;
            letter-spacing: 0.5px;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        .tab.active {
            background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(168,85,247,0.1));
            color: var(--cyan);
            border: 1px solid rgba(0,212,255,0.2);
        }
        
        /* Memory Bar */
        .mem-bar {
            display: flex;
            padding: 2px 8px;
            gap: 4px;
            flex-shrink: 0;
        }
        
        .mem-btn {
            flex: 1;
            padding: 4px 2px;
            border: none;
            border-radius: 6px;
            background: var(--bg-btn);
            color: var(--text-dim);
            font-size: 10px;
            font-weight: 700;
            cursor: pointer;
        }
        
        .mem-btn.active {
            color: var(--cyan);
            background: rgba(0,212,255,0.1);
        }
        
        /* Display - Compact */
        .display {
            padding: 6px 12px;
            text-align: right;
            flex-shrink: 0;
            min-height: 60px;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
        }
        
        .history-line {
            font-size: 12px;
            color: var(--text-dim);
            min-height: 16px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        
        .main-line {
            font-size: 32px;
            font-weight: 300;
            color: var(--text);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            line-height: 1.2;
        }
        
        .main-line.small {
            font-size: 24px;
        }
        
        .main-line.tiny {
            font-size: 18px;
        }
        
        /* Keypad - Fills remaining space */
        .keypad {
            flex: 1;
            display: grid;
            gap: 4px;
            padding: 4px 8px 8px;
            min-height: 0;
        }
        
        .keypad.basic {
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: repeat(5, 1fr);
        }
        
        .keypad.scientific {
            grid-template-columns: repeat(5, 1fr);
            grid-template-rows: repeat(6, 1fr);
        }
        
        .btn {
            border: none;
            border-radius: 12px;
            font-size: 20px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.1s;
            display: flex;
            align-items: center;
            justify-content: center;
            user-select: none;
            -webkit-user-select: none;
            min-height: 0;
        }
        
        .btn:active {
            transform: scale(0.92);
            opacity: 0.8;
        }
        
        .btn-num {
            background: var(--bg-btn-num);
            color: var(--text);
            font-size: 22px;
        }
        
        .btn-op {
            background: linear-gradient(135deg, rgba(0,212,255,0.15), rgba(0,212,255,0.05));
            color: var(--cyan);
            font-size: 22px;
        }
        
        .btn-op.active {
            background: linear-gradient(135deg, var(--cyan), var(--purple));
            color: white;
        }
        
        .btn-fn {
            background: rgba(239,68,68,0.1);
            color: var(--red);
            font-size: 14px;
        }
        
        .btn-sci {
            background: rgba(168,85,247,0.1);
            color: var(--purple);
            font-size: 12px;
            font-weight: 600;
        }
        
        .btn-eq {
            background: linear-gradient(135deg, var(--cyan), var(--purple));
            color: white;
            font-size: 24px;
            box-shadow: 0 0 15px rgba(0,212,255,0.3);
        }
        
        .btn-zero {
            grid-column: span 2;
        }
        
        /* History Panel */
        .history-panel {
            position: absolute;
            top: 0;
            right: -100%;
            width: 100%;
            height: 100%;
            background: var(--bg-card);
            z-index: 100;
            transition: right 0.25s ease;
            display: flex;
            flex-direction: column;
        }
        
        .history-panel.open {
            right: 0;
        }
        
        .hist-header {
            padding: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255,255,255,0.05);
            flex-shrink: 0;
        }
        
        .hist-title {
            font-size: 14px;
            color: var(--cyan);
            font-weight: 600;
        }
        
        .hist-close {
            background: none;
            border: none;
            color: var(--text-dim);
            font-size: 20px;
            cursor: pointer;
        }
        
        .hist-list {
            flex: 1;
            overflow-y: auto;
            padding: 8px;
        }
        
        .hist-item {
            padding: 10px;
            border-bottom: 1px solid rgba(255,255,255,0.02);
            cursor: pointer;
            border-radius: 8px;
            margin-bottom: 4px;
        }
        
        .hist-item:active {
            background: rgba(0,212,255,0.05);
        }
        
        .hist-expr {
            font-size: 12px;
            color: var(--text-dim);
        }
        
        .hist-res {
            font-size: 16px;
            color: var(--cyan);
            font-weight: 600;
        }
        
        .hist-empty {
            text-align: center;
            padding: 40px;
            color: var(--text-dim);
            font-size: 14px;
        }
        
        .hist-clear {
            padding: 8px;
            border-top: 1px solid rgba(255,255,255,0.05);
            flex-shrink: 0;
        }
        
        .hist-clear-btn {
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 10px;
            background: rgba(239,68,68,0.1);
            color: var(--red);
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
        }
        
        ::-webkit-scrollbar {
            width: 3px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--cyan);
            border-radius: 2px;
        }
    </style>
</head>
<body>
    <div class="calc-wrap">
        <div class="header">
            <div class="logo">
                <div class="logo-icon">Σ</div>
                <div class="logo-text">CALC PRO</div>
            </div>
            <button class="header-btn" onclick="toggleHistory()">📋</button>
        </div>
        
        <div class="tabs">
            <button class="tab active" onclick="setMode('basic')" id="tab-basic">BASIC</button>
            <button class="tab" onclick="setMode('scientific')" id="tab-sci">SCIENTIFIC</button>
        </div>
        
        <div class="mem-bar">
            <button class="mem-btn" onclick="memClear()">MC</button>
            <button class="mem-btn" onclick="memRecall()">MR</button>
            <button class="mem-btn" onclick="memAdd()">M+</button>
            <button class="mem-btn" onclick="memSub()">M−</button>
        </div>
        
        <div class="display">
            <div class="history-line" id="hist-line"></div>
            <div class="main-line" id="main-line">0</div>
        </div>
        
        <!-- Basic Keypad -->
        <div class="keypad basic" id="kp-basic">
            <button class="btn btn-fn" onclick="clearAll()">AC</button>
            <button class="btn btn-fn" onclick="clearEntry()">CE</button>
            <button class="btn btn-sci" onclick="op('%')">%</button>
            <button class="btn btn-op" onclick="op('/')">÷</button>
            
            <button class="btn btn-num" onclick="num('7')">7</button>
            <button class="btn btn-num" onclick="num('8')">8</button>
            <button class="btn btn-num" onclick="num('9')">9</button>
            <button class="btn btn-op" onclick="op('*')">×</button>
            
            <button class="btn btn-num" onclick="num('4')">4</button>
            <button class="btn btn-num" onclick="num('5')">5</button>
            <button class="btn btn-num" onclick="num('6')">6</button>
            <button class="btn btn-op" onclick="op('-')">−</button>
            
            <button class="btn btn-num" onclick="num('1')">1</button>
            <button class="btn btn-num" onclick="num('2')">2</button>
            <button class="btn btn-num" onclick="num('3')">3</button>
            <button class="btn btn-op" onclick="op('+')">+</button>
            
            <button class="btn btn-num btn-zero" onclick="num('0')">0</button>
            <button class="btn btn-num" onclick="num('.')">.</button>
            <button class="btn btn-eq" onclick="calc()">=</button>
        </div>
        
        <!-- Scientific Keypad -->
        <div class="keypad scientific" id="kp-sci" style="display:none">
            <button class="btn btn-sci" onclick="sci('sin')">sin</button>
            <button class="btn btn-sci" onclick="sci('cos')">cos</button>
            <button class="btn btn-sci" onclick="sci('tan')">tan</button>
            <button class="btn btn-sci" onclick="sci('log')">log</button>
            <button class="btn btn-sci" onclick="sci('ln')">ln</button>
            
            <button class="btn btn-sci" onclick="sci('asin')">sin⁻¹</button>
            <button class="btn btn-sci" onclick="sci('acos')">cos⁻¹</button>
            <button class="btn btn-sci" onclick="sci('atan')">tan⁻¹</button>
            <button class="btn btn-sci" onclick="sci('sqrt')">√</button>
            <button class="btn btn-sci" onclick="sci('cbrt')">∛</button>
            
            <button class="btn btn-sci" onclick="op('^')">xʸ</button>
            <button class="btn btn-sci" onclick="sci('sq')">x²</button>
            <button class="btn btn-sci" onclick="sci('cb')">x³</button>
            <button class="btn btn-sci" onclick="sci('fact')">n!</button>
            <button class="btn btn-sci" onclick="num('(')">(</button>
            
            <button class="btn btn-sci" onclick="num(')')">)</button>
            <button class="btn btn-sci" onclick="num('3.14159')">π</button>
            <button class="btn btn-sci" onclick="num('2.71828')">e</button>
            <button class="btn btn-fn" onclick="clearAll()">AC</button>
            <button class="btn btn-fn" onclick="clearEntry()">CE</button>
            
            <button class="btn btn-num" onclick="num('7')">7</button>
            <button class="btn btn-num" onclick="num('8')">8</button>
            <button class="btn btn-num" onclick="num('9')">9</button>
            <button class="btn btn-sci" onclick="op('%')">%</button>
            <button class="btn btn-op" onclick="op('/')">÷</button>
            
            <button class="btn btn-num" onclick="num('4')">4</button>
            <button class="btn btn-num" onclick="num('5')">5</button>
            <button class="btn btn-num" onclick="num('6')">6</button>
            <button class="btn btn-sci" onclick="sci('abs')">|x|</button>
            <button class="btn btn-op" onclick="op('*')">×</button>
            
            <button class="btn btn-num" onclick="num('1')">1</button>
            <button class="btn btn-num" onclick="num('2')">2</button>
            <button class="btn btn-num" onclick="num('3')">3</button>
            <button class="btn btn-sci" onclick="sci('rec')">¹/x</button>
            <button class="btn btn-op" onclick="op('-')">−</button>
            
            <button class="btn btn-num" onclick="num('0')">0</button>
            <button class="btn btn-num" onclick="num('.')">.</button>
            <button class="btn btn-sci" onclick="toggleSign()">+/-</button>
            <button class="btn btn-sci" onclick="toggleDeg()" id="deg-btn">DEG</button>
            <button class="btn btn-eq" onclick="calc()">=</button>
        </div>
        
        <!-- History -->
        <div class="history-panel" id="hist-panel">
            <div class="hist-header">
                <div class="hist-title">📋 History</div>
                <button class="hist-close" onclick="toggleHistory()">✕</button>
            </div>
            <div class="hist-list" id="hist-list">
                <div class="hist-empty">No calculations</div>
            </div>
            <div class="hist-clear">
                <button class="hist-clear-btn" onclick="clearHist()">Clear All</button>
            </div>
        </div>
    </div>
    
    <script>
        let cur = '0', prev = '', op = null, reset = false;
        let mem = 0, hist = [], deg = true, mode = 'basic';
        
        const main = document.getElementById('main-line');
        const histLine = document.getElementById('hist-line');
        const histList = document.getElementById('hist-list');
        const histPanel = document.getElementById('hist-panel');
        
        function upd() {
            main.textContent = cur;
            main.classList.remove('small','tiny');
            if(cur.length>10) main.classList.add('small');
            if(cur.length>15) main.classList.add('tiny');
        }
        
        function num(n) {
            if(reset) { cur=''; reset=false; }
            if(cur==='0' && n!=='.') cur=n;
            else if(n==='.' && cur.includes('.')) return;
            else cur+=n;
            upd();
        }
        
        function opFn(o) {
            if(op!==null && !reset) calc();
            prev=cur; op=o; reset=true;
            histLine.textContent = prev+' '+sym(o);
        }
        
        function sym(o) {
            return {'+':'+','-':'−','*':'×','/':'÷','^':'^','%':'%'}[o]||o;
        }
        
        function calc() {
            if(op===null || reset) return;
            let r, p=parseFloat(prev), c=parseFloat(cur);
            try {
                switch(op) {
                    case '+': r=p+c; break;
                    case '-': r=p-c; break;
                    case '*': r=p*c; break;
                    case '/': if(c===0) throw new Error('Div0'); r=p/c; break;
                    case '^': r=Math.pow(p,c); break;
                    case '%': r=p%c; break;
                    default: return;
                }
                r=fmt(r);
                addHist(prev+' '+sym(op)+' '+cur, r);
                cur=String(r); op=null; reset=true; histLine.textContent='';
                upd();
            } catch(e) {
                cur='Error'; upd();
                setTimeout(()=>{cur='0';upd();},1500);
            }
        }
        
        function fmt(n) {
            if(!isFinite(n)) return 'Error';
            if(Math.abs(n)<1e-10) return 0;
            let r=Math.round(n*1e10)/1e10;
            let s=String(r);
            if(s.length>12) s=r.toExponential(8);
            return parseFloat(s);
        }
        
        function sci(f) {
            let n=parseFloat(cur), r, ex=f+'('+cur+')';
            try {
                switch(f) {
                    case 'sin': r=deg?Math.sin(n*Math.PI/180):Math.sin(n); break;
                    case 'cos': r=deg?Math.cos(n*Math.PI/180):Math.cos(n); break;
                    case 'tan': r=deg?Math.tan(n*Math.PI/180):Math.tan(n); break;
                    case 'asin': r=deg?Math.asin(n)*180/Math.PI:Math.asin(n); break;
                    case 'acos': r=deg?Math.acos(n)*180/Math.PI:Math.acos(n); break;
                    case 'atan': r=deg?Math.atan(n)*180/Math.PI:Math.atan(n); break;
                    case 'log': if(n<=0) throw new Error(); r=Math.log10(n); break;
                    case 'ln': if(n<=0) throw new Error(); r=Math.log(n); break;
                    case 'sqrt': if(n<0) throw new Error(); r=Math.sqrt(n); break;
                    case 'cbrt': r=Math.cbrt(n); break;
                    case 'sq': r=n*n; ex=cur+'²'; break;
                    case 'cb': r=n*n*n; ex=cur+'³'; break;
                    case 'fact': if(n<0||!Number.isInteger(n)) throw new Error(); r=1; for(let i=2;i<=n;i++)r*=i; ex=cur+'!'; break;
                    case 'abs': r=Math.abs(n); ex='|'+cur+'|'; break;
                    case 'rec': if(n===0) throw new Error(); r=1/n; ex='1/'+cur; break;
                    case 'deg': deg=!deg; cur=deg?'DEG':'RAD'; upd(); setTimeout(()=>{cur=String(n);upd();},800); return;
                }
                r=fmt(r); addHist(ex,r); cur=String(r); reset=true; upd();
            } catch(e) {
                cur='Error'; upd(); setTimeout(()=>{cur='0';upd();},1500);
            }
        }
        
        function toggleSign() {
            if(cur!=='0') { cur=cur.startsWith('-')?cur.slice(1):'-'+cur; upd(); }
        }
        
        function toggleDeg() {
            deg=!deg; document.getElementById('deg-btn').textContent=deg?'DEG':'RAD';
        }
        
        function clearAll() { cur='0'; prev=''; op=null; reset=false; histLine.textContent=''; upd(); }
        function clearEntry() { cur='0'; upd(); }
        
        function memClear() { mem=0; showMem(); }
        function memRecall() { cur=String(mem); reset=true; upd(); }
        function memAdd() { mem+=parseFloat(cur)||0; showMem(); }
        function memSub() { mem-=parseFloat(cur)||0; showMem(); }
        function showMem() {
            document.querySelectorAll('.mem-btn').forEach(b=>b.classList.toggle('active', mem!==0));
        }
        
        function addHist(ex, r) { hist.unshift({ex,r}); if(hist.length>50) hist.pop(); updHist(); }
        function updHist() {
            if(hist.length===0) { histList.innerHTML='<div class="hist-empty">No calculations</div>'; return; }
            histList.innerHTML=hist.map((h,i)=>`<div class="hist-item" onclick="loadHist(${i})"><div class="hist-expr">${h.ex}</div><div class="hist-res">= ${h.r}</div></div>`).join('');
        }
        function loadHist(i) { cur=String(hist[i].r); reset=true; upd(); toggleHistory(); }
        function clearHist() { hist=[]; updHist(); }
        function toggleHistory() { histPanel.classList.toggle('open'); }
        
        function setMode(m) {
            mode=m;
            document.getElementById('tab-basic').classList.toggle('active', m==='basic');
            document.getElementById('tab-sci').classList.toggle('active', m==='scientific');
            document.getElementById('kp-basic').style.display=m==='basic'?'grid':'none';
            document.getElementById('kp-sci').style.display=m==='scientific'?'grid':'none';
        }
        
        // Keyboard
        document.addEventListener('keydown', e=>{
            if(e.key>='0'&&e.key<='9') num(e.key);
            if(e.key==='.') num('.');
            if(e.key==='+') opFn('+');
            if(e.key==='-') opFn('-');
            if(e.key==='*') opFn('*');
            if(e.key==='/') opFn('/');
            if(e.key==='^') opFn('^');
            if(e.key==='%') opFn('%');
            if(e.key==='Enter'||e.key==='=') calc();
            if(e.key==='Escape') clearAll();
            if(e.key==='Backspace') { cur=cur.length>1?cur.slice(0,-1):'0'; upd(); }
        });
        
        // Prevent double-tap zoom
        let lastTouch=0;
        document.addEventListener('touchend', e=>{
            const now=Date.now();
            if(now-lastTouch<300) e.preventDefault();
            lastTouch=now;
        }, {passive:false});
    </script>
</body>
</html>'''

with open('/mnt/agents/output/calc_pro_compact.html', 'w', encoding='utf-8') as f:
    f.write(html_code)

print("✅ Compact Calc Pro saved!")
print(f"Size: {len(html_code)} chars")


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Pro Scientific Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            touch-action: manipulation;
        }

        :root {
            --bg-dark: #050508;
            --bg-card: #0a0a10;
            --bg-display: #06060a;
            --accent-cyan: #00f0ff;
            --accent-purple: #b829dd;
            --accent-green: #00ff9d;
            --accent-red: #ff4757;
            --text-primary: #ffffff;
            --text-secondary: #5a5a6a;
            --border-subtle: rgba(255, 255, 255, 0.03);
        }

        html, body {
            height: 100vh;
            width: 100vw;
            overflow: hidden;
            position: fixed;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Segoe UI', Roboto, sans-serif;
            background: var(--bg-dark);
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Background grid */
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(0, 240, 255, 0.015) 1px, transparent 1px),
                linear-gradient(90deg, rgba(0, 240, 255, 0.015) 1px, transparent 1px);
            background-size: 40px 40px;
            pointer-events: none;
        }

        /* Floating particles */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: var(--accent-cyan);
            border-radius: 50%;
            opacity: 0;
            animation: float 25s infinite;
            box-shadow: 0 0 6px var(--accent-cyan);
        }

        @keyframes float {
            0% { opacity: 0; transform: translateY(100vh) scale(0); }
            10% { opacity: 0.6; }
            90% { opacity: 0.6; }
            100% { opacity: 0; transform: translateY(-10vh) scale(1); }
        }

        /* Main container - FULL SCREEN */
        .calculator-wrapper {
            width: 100vw;
            height: 100vh;
            max-width: 100vw;
            max-height: 100vh;
            display: flex;
            flex-direction: column;
            background: var(--bg-card);
            position: relative;
            z-index: 1;
            overflow: hidden;
        }

        /* Top bar */
        .top-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 2vh 4vw;
            border-bottom: 1px solid var(--border-subtle);
            background: rgba(0, 0, 0, 0.3);
            flex-shrink: 0;
            height: 8vh;
            min-height: 50px;
        }

        .brand {
            display: flex;
            align-items: center;
            gap: 2vw;
        }

        .brand-icon {
            width: 5vh;
            height: 5vh;
            min-width: 35px;
            min-height: 35px;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2vh;
            font-weight: 800;
            color: var(--bg-dark);
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.3);
        }

        .brand-info {
            display: flex;
            flex-direction: column;
        }

        .brand-name {
            color: var(--text-primary);
            font-size: 2vh;
            font-weight: 700;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .brand-tag {
            color: var(--text-secondary);
            font-size: 1.2vh;
            letter-spacing: 3px;
            text-transform: uppercase;
        }

        .system-info {
            display: flex;
            gap: 3vw;
            align-items: center;
        }

        .info-item {
            display: flex;
            align-items: center;
            gap: 1vw;
            color: var(--text-secondary);
            font-size: 1.3vh;
            font-family: 'Courier New', monospace;
        }

        .info-dot {
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background: var(--accent-green);
            box-shadow: 0 0 8px var(--accent-green);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.4; }
        }

        /* Main content */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            padding: 2vh 4vw;
            gap: 2vh;
            overflow: hidden;
        }

        /* Mode switcher */
        .mode-switcher {
            display: flex;
            gap: 2vw;
            flex-shrink: 0;
            height: 5vh;
            min-height: 35px;
        }

        .mode-tab {
            flex: 1;
            padding: 0 3vw;
            border: 1px solid var(--border-subtle);
            border-radius: 8px;
            background: transparent;
            color: var(--text-secondary);
            font-size: 1.5vh;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .mode-tab.active {
            background: linear-gradient(135deg, rgba(0, 240, 255, 0.1), rgba(184, 41, 221, 0.1));
            color: var(--accent-cyan);
            border-color: rgba(0, 240, 255, 0.3);
        }

        /* Memory section */
        .memory-section {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-shrink: 0;
            height: 4vh;
            min-height: 30px;
        }

        .mem-indicator {
            color: var(--accent-cyan);
            font-size: 1.5vh;
            font-family: 'Courier New', monospace;
            letter-spacing: 2px;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .mem-indicator.show {
            opacity: 1;
        }

        .memory-buttons {
            display: flex;
            gap: 2vw;
        }

        .mem-btn {
            padding: 1vh 2vw;
            font-size: 1.2vh;
            background: transparent;
            border: 1px solid var(--border-subtle);
            border-radius: 6px;
            color: var(--text-secondary);
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .mem-btn:hover {
            border-color: var(--accent-cyan);
            color: var(--accent-cyan);
        }

        /* Display */
        .display-container {
            background: var(--bg-display);
            border-radius: 16px;
            padding: 3vh 4vw;
            border: 1px solid var(--border-subtle);
            position: relative;
            overflow: hidden;
            flex-shrink: 0;
            height: 18vh;
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .display-container::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: linear-gradient(90deg, transparent, var(--accent-cyan), transparent);
            opacity: 0.5;
        }

        .history {
            color: var(--text-secondary);
            text-align: right;
            font-size: 2vh;
            min-height: 3vh;
            margin-bottom: 1vh;
            font-family: 'Courier New', monospace;
            overflow-x: auto;
            white-space: nowrap;
            letter-spacing: 1px;
        }

        .display {
            color: var(--text-primary);
            font-size: 6vh;
            text-align: right;
            font-weight: 300;
            font-family: 'Courier New', monospace;
            word-break: break-all;
            letter-spacing: 2px;
            text-shadow: 0 0 20px rgba(0, 240, 255, 0.1);
            transition: all 0.3s;
            line-height: 1.1;
        }

        .display.error {
            color: var(--accent-red);
            text-shadow: 0 0 20px rgba(255, 71, 87, 0.4);
            animation: shake 0.5s ease;
        }

        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            75% { transform: translateX(10px); }
        }

        /* Scientific panel */
        .scientific-panel {
            display: none;
            grid-template-columns: repeat(6, 1fr);
            gap: 1.5vw;
            flex-shrink: 0;
            height: 8vh;
            min-height: 50px;
            animation: slideDown 0.3s ease;
        }

        .scientific-panel.active {
            display: grid;
        }

        @keyframes slideDown {
            from { opacity: 0; transform: translateY(-10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Buttons area */
        .buttons-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            min-height: 0;
        }

        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 2vw;
            height: 100%;
        }

        button {
            font-size: 2.5vh;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.15s ease;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            min-height: 0;
        }

        button::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.4s, height 0.4s;
        }

        button:active::after {
            width: 200px;
            height: 200px;
        }

        .num-btn {
            background: rgba(255, 255, 255, 0.03);
            color: var(--text-primary);
            border: 1px solid rgba(255, 255, 255, 0.05);
            font-size: 3vh;
            font-weight: 500;
        }

        .num-btn:hover {
            background: rgba(255, 255, 255, 0.08);
            transform: translateY(-2px);
        }

        .op-btn {
            background: rgba(0, 240, 255, 0.05);
            color: var(--accent-cyan);
            border: 1px solid rgba(0, 240, 255, 0.1);
            font-size: 2.5vh;
        }

        .op-btn:hover {
            background: rgba(0, 240, 255, 0.1);
            box-shadow: 0 0 15px rgba(0, 240, 255, 0.1);
        }

        .op-btn.active {
            background: var(--accent-cyan);
            color: var(--bg-dark);
            box-shadow: 0 0 20px rgba(0, 240, 255, 0.3);
        }

        .func-btn {
            background: rgba(184, 41, 221, 0.05);
            color: var(--accent-purple);
            border: 1px solid rgba(184, 41, 221, 0.1);
            font-size: 1.8vh;
        }

        .func-btn:hover {
            background: rgba(184, 41, 221, 0.1);
            box-shadow: 0 0 15px rgba(184, 41, 221, 0.1);
        }

        .clear-btn {
            background: rgba(255, 71, 87, 0.05);
            color: var(--accent-red);
            border: 1px solid rgba(255, 71, 87, 0.1);
            font-size: 2vh;
        }

        .clear-btn:hover {
            background: rgba(255, 71, 87, 0.1);
        }

        .eq-btn {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
            color: var(--bg-dark);
            grid-column: span 2;
            font-weight: 800;
            font-size: 3vh;
            border: none;
        }

        .eq-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(0, 240, 255, 0.2);
            filter: brightness(1.1);
        }

        .zero-btn {
            grid-column: span 2;
        }

        /* Scrollbar */
        .history::-webkit-scrollbar {
            height: 2px;
        }

        .history::-webkit-scrollbar-thumb {
            background: var(--accent-cyan);
        }

        /* Landscape mode */
        @media (orientation: landscape) and (max-height: 500px) {
            .top-bar {
                height: 12vh;
                padding: 1vh 4vw;
            }
            .display-container {
                height: 22vh;
            }
            .buttons-grid {
                gap: 1.5vw;
            }
            button {
                font-size: 3vh;
            }
            .num-btn {
                font-size: 3.5vh;
            }
        }

        /* Small phones */
        @media (max-width: 360px) {
            .brand-tag, .system-info {
                display: none;
            }
            .display {
                font-size: 5vh;
            }
        }

        /* Tablets */
        @media (min-width: 768px) {
            .calculator-wrapper {
                max-width: 600px;
                margin: 0 auto;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>

    <div class="calculator-wrapper">
        <div class="top-bar">
            <div class="brand">
                <div class="brand-icon">∑</div>
                <div class="brand-info">
                    <div class="brand-name">Calc Pro</div>
                    <div class="brand-tag">v2.0</div>
                </div>
            </div>
            <div class="system-info">
                <div class="info-item">
                    <div class="info-dot"></div>
                    <span>ACTIVE</span>
                </div>
                <div class="info-item">
                    <span id="mem-status">0KB</span>
                </div>
            </div>
        </div>

        <div class="main-content">
            <div class="mode-switcher">
                <button class="mode-tab active" onclick="calc.setMode('basic')">Basic</button>
                <button class="mode-tab" onclick="calc.setMode('scientific')">Scientific</button>
            </div>

            <div class="memory-section">
                <div class="mem-indicator" id="mem-indicator">M = 0</div>
                <div class="memory-buttons">
                    <button class="mem-btn" onclick="calc.memoryClear()">MC</button>
                    <button class="mem-btn" onclick="calc.memoryRecall()">MR</button>
                    <button class="mem-btn" onclick="calc.memoryAdd()">M+</button>
                    <button class="mem-btn" onclick="calc.memorySubtract()">M-</button>
                </div>
            </div>

            <div class="display-container">
                <div class="history" id="history"></div>
                <div class="display" id="display">0</div>
            </div>

            <div class="scientific-panel" id="scientific-panel">
                <button class="func-btn" onclick="calc.appendFunc('sin(')">sin</button>
                <button class="func-btn" onclick="calc.appendFunc('cos(')">cos</button>
                <button class="func-btn" onclick="calc.appendFunc('tan(')">tan</button>
                <button class="func-btn" onclick="calc.appendFunc('log(')">log</button>
                <button class="func-btn" onclick="calc.appendFunc('ln(')">ln</button>
                <button class="func-btn" onclick="calc.appendFunc('sqrt(')">√</button>
                <button class="func-btn" onclick="calc.appendFunc('^')">^</button>
                <button class="func-btn" onclick="calc.appendFunc('!')">!</button>
                <button class="func-btn" onclick="calc.appendFunc('pi')">π</button>
                <button class="func-btn" onclick="calc.appendFunc('e')">e</button>
                <button class="func-btn" onclick="calc.appendFunc('(')">(</button>
                <button class="func-btn" onclick="calc.appendFunc(')')">)</button>
            </div>

            <div class="buttons-area">
                <div class="buttons-grid">
                    <button class="clear-btn" onclick="calc.clearAll()">AC</button>
                    <button class="clear-btn" onclick="calc.clearEntry()">CE</button>
                    <button class="func-btn" onclick="calc.appendOp('%')">%</button>
                    <button class="op-btn" onclick="calc.appendOp('/')" id="op-/">÷</button>

                    <button class="num-btn" onclick="calc.appendNum('7')">7</button>
                    <button class="num-btn" onclick="calc.appendNum('8')">8</button>
                    <button class="num-btn" onclick="calc.appendNum('9')">9</button>
                    <button class="op-btn" onclick="calc.appendOp('*')" id="op-*">×</button>

                    <button class="num-btn" onclick="calc.appendNum('4')">4</button>
                    <button class="num-btn" onclick="calc.appendNum('5')">5</button>
                    <button class="num-btn" onclick="calc.appendNum('6')">6</button>
                    <button class="op-btn" onclick="calc.appendOp('-')" id="op--">−</button>

                    <button class="num-btn" onclick="calc.appendNum('1')">1</button>
                    <button class="num-btn" onclick="calc.appendNum('2')">2</button>
                    <button class="num-btn" onclick="calc.appendNum('3')">3</button>
                    <button class="op-btn" onclick="calc.appendOp('+')" id="op-+">+</button>

                    <button class="num-btn zero-btn" onclick="calc.appendNum('0')">0</button>
                    <button class="num-btn" onclick="calc.appendNum('.')">.</button>
                    <button class="eq-btn" onclick="calc.calculate()">=</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 25 + 's';
                particle.style.animationDuration = (20 + Math.random() * 10) + 's';
                container.appendChild(particle);
            }
        }
        createParticles();

        function updateMemStatus() {
            const mem = Math.floor(Math.random() * 50) + 10;
            const el = document.getElementById('mem-status');
            if (el) el.textContent = mem + 'KB';
        }
        setInterval(updateMemStatus, 3000);

        class Calculator {
            constructor() {
                this.currentInput = '0';
                this.history = '';
                this.shouldReset = false;
                this.lastResult = null;
                this.memory = 0;
                this.mode = 'basic';
                this.display = document.getElementById('display');
                this.historyEl = document.getElementById('history');
                this.scientificPanel = document.getElementById('scientific-panel');
                this.memIndicator = document.getElementById('mem-indicator');
                this.setupKeyboard();
            }

            appendNum(num) {
                if (this.currentInput === 'Error') this.currentInput = '0';
                if (this.currentInput === '0' || this.shouldReset) {
                    this.currentInput = num;
                    this.shouldReset = false;
                } else {
                    if (num === '.' && this.getLastNumber().includes('.')) return;
                    this.currentInput += num;
                }
                this.updateDisplay();
                this.clearActiveOps();
            }

            appendOp(op) {
                if (this.currentInput === 'Error') return;
                if (this.shouldReset) {
                    this.shouldReset = false;
                    if (this.lastResult !== null) this.currentInput = String(this.lastResult);
                }
                const lastChar = this.currentInput.slice(-1);
                const operators = '+-*/%';
                if (operators.includes(lastChar) && operators.includes(op)) {
                    this.currentInput = this.currentInput.slice(0, -1) + op;
                } else {
                    this.currentInput += op;
                }
                this.updateDisplay();
                this.highlightOp(op);
            }

            appendFunc(func) {
                if (this.currentInput === 'Error') this.currentInput = '0';
                if (this.shouldReset || this.currentInput === '0') {
                    this.currentInput = func;
                    this.shouldReset = false;
                } else {
                    this.currentInput += func;
                }
                this.updateDisplay();
            }

            calculate() {
                if (this.currentInput === 'Error') return;
                try {
                    let expr = this.currentInput;
                    this.history = expr + ' =';
                    expr = this.parseScientific(expr);
                    const result = Function('"use strict"; return (' + expr + ')')();
                    if (!isFinite(result) || isNaN(result)) throw new Error('Invalid');
                    this.currentInput = this.formatResult(result);
                    this.lastResult = parseFloat(this.currentInput);
                    this.shouldReset = true;
                    this.historyEl.textContent = this.history + ' ' + this.currentInput;
                    this.updateDisplay();
                    this.clearActiveOps();
                } catch (e) {
                    this.showError();
                }
            }

            parseScientific(expr) {
                expr = expr.replace(/(\d+)!/g, (match, n) => this.factorial(parseInt(n)));
                expr = expr.replace(/\bsin\b/g, 'Math.sin');
                expr = expr.replace(/\bcos\b/g, 'Math.cos');
                expr = expr.replace(/\btan\b/g, 'Math.tan');
                expr = expr.replace(/\blog\b/g, 'Math.log10');
                expr = expr.replace(/\bln\b/g, 'Math.log');
                expr = expr.replace(/\bsqrt\b/g, 'Math.sqrt');
                expr = expr.replace(/\bpi\b/g, 'Math.PI');
                expr = expr.replace(/\be\b/g, 'Math.E');
                expr = expr.replace(/\^/g, '**');
                return expr;
            }

            factorial(n) {
                if (n < 0) return NaN;
                if (n === 0 || n === 1) return 1;
                let result = 1;
                for (let i = 2; i <= n; i++) result *= i;
                return result;
            }

            formatResult(num) {
                if (Math.abs(num) > 1e15 || (Math.abs(num) < 1e-10 && num !== 0)) return num.toExponential(6);
                return String(parseFloat(num.toPrecision(12)));
            }

            getLastNumber() {
                const match = this.currentInput.match(/[\d.]+$/);
                return match ? match[0] : '';
            }

            clearAll() {
                this.currentInput = '0';
                this.history = '';
                this.lastResult = null;
                this.shouldReset = false;
                this.historyEl.textContent = '';
                this.updateDisplay();
                this.clearActiveOps();
            }

            clearEntry() {
                this.currentInput = '0';
                this.updateDisplay();
            }

            deleteLast() {
                if (this.currentInput === 'Error') { this.clearAll(); return; }
                if (this.currentInput.length > 1) this.currentInput = this.currentInput.slice(0, -1);
                else this.currentInput = '0';
                this.updateDisplay();
            }

            showError() {
                this.currentInput = 'Error';
                this.display.classList.add('error');
                this.shouldReset = true;
                this.updateDisplay();
                setTimeout(() => this.display.classList.remove('error'), 500);
            }

            updateDisplay() { this.display.textContent = this.currentInput; }

            highlightOp(op) {
                this.clearActiveOps();
                const id = 'op-' + op;
                const btn = document.getElementById(id);
                if (btn) btn.classList.add('active');
            }

            clearActiveOps() {
                document.querySelectorAll('.op-btn').forEach(b => b.classList.remove('active'));
            }

            setMode(mode) {
                this.mode = mode;
                document.querySelectorAll('.mode-tab').forEach(btn => {
                    btn.classList.toggle('active', btn.textContent.toLowerCase() === mode);
                });
                this.scientificPanel.classList.toggle('active', mode === 'scientific');
            }

            memoryClear() { this.memory = 0; this.updateMemIndicator(); }
            memoryRecall() {
                if (this.shouldReset || this.currentInput === '0') {
                    this.currentInput = String(this.memory);
                    this.shouldReset = false;
                } else this.currentInput += String(this.memory);
                this.updateDisplay();
            }
            memoryAdd() { this.memory += parseFloat(this.currentInput) || 0; this.updateMemIndicator(); }
            memorySubtract() { this.memory -= parseFloat(this.currentInput) || 0; this.updateMemIndicator(); }
            updateMemIndicator() {
                this.memIndicator.textContent = 'M = ' + this.memory;
                this.memIndicator.classList.toggle('show', this.memory !== 0);
            }

            setupKeyboard() {
                document.addEventListener('keydown', (e) => {
                    const key = e.key;
                    if (key >= '0' && key <= '9') this.appendNum(key);
                    else if (key === '.') this.appendNum('.');
                    else if (['+', '-', '*', '/', '%'].includes(key)) { e.preventDefault(); this.appendOp(key); }
                    else if (key === 'Enter' || key === '=') { e.preventDefault(); this.calculate(); }
                    else if (key === 'Escape') this.clearAll();
                    else if (key === 'Backspace') this.deleteLast();
                    else if (key === '(' || key === ')') this.appendFunc(key);
                });
            }
        }

        const
