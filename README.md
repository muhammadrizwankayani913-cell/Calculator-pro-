# Calculator-pro-
<!DOCTYPE html>
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

        const calc = new Calculator();
    </script>
</body>
</html>
