pro calc 

html_code = '''<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Calc Pro - Expert Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        :root {
            --bg-primary: #0a0a0f;
            --bg-secondary: #12121a;
            --bg-card: #1a1a2e;
            --bg-button: #1e1e2e;
            --bg-button-hover: #2a2a3e;
            --text-primary: #ffffff;
            --text-secondary: #a0a0b0;
            --accent-cyan: #00d4ff;
            --accent-purple: #a855f7;
            --accent-pink: #ec4899;
            --accent-red: #ef4444;
            --accent-green: #22c55e;
            --accent-orange: #f97316;
            --border-glow: rgba(0, 212, 255, 0.3);
        }
        
        body {
            background: var(--bg-primary);
            color: var(--text-primary);
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
        }
        
        /* Animated background particles */
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
            opacity: 0.3;
            animation: float 15s infinite;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0) translateX(0); opacity: 0.3; }
            25% { transform: translateY(-100px) translateX(50px); opacity: 0.6; }
            50% { transform: translateY(-50px) translateX(-30px); opacity: 0.4; }
            75% { transform: translateY(-150px) translateX(20px); opacity: 0.5; }
        }
        
        .calculator-container {
            width: 100%;
            max-width: 420px;
            height: 100vh;
            max-height: 900px;
            background: var(--bg-secondary);
            display: flex;
            flex-direction: column;
            position: relative;
            z-index: 1;
            overflow: hidden;
            box-shadow: 0 0 50px rgba(0, 212, 255, 0.1);
        }
        
        @media (min-width: 421px) {
            .calculator-container {
                height: 90vh;
                border-radius: 20px;
                border: 1px solid rgba(255,255,255,0.05);
            }
        }
        
        /* Header */
        .header {
            padding: 15px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logo-icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            font-weight: bold;
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.3);
        }
        
        .logo-text {
            font-size: 18px;
            font-weight: 700;
            letter-spacing: 2px;
            background: linear-gradient(90deg, var(--accent-cyan), var(--accent-purple));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .header-actions {
            display: flex;
            gap: 15px;
        }
        
        .header-btn {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 20px;
            cursor: pointer;
            transition: color 0.3s;
        }
        
        .header-btn:hover {
            color: var(--accent-cyan);
        }
        
        /* Mode Switcher */
        .mode-switcher {
            display: flex;
            padding: 10px 15px;
            gap: 10px;
        }
        
        .mode-btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 12px;
            background: var(--bg-button);
            color: var(--text-secondary);
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            letter-spacing: 1px;
        }
        
        .mode-btn.active {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.2), rgba(168, 85, 247, 0.2));
            color: var(--accent-cyan);
            border: 1px solid var(--border-glow);
            box-shadow: 0 0 15px rgba(0, 212, 255, 0.1);
        }
        
        .mode-btn:hover:not(.active) {
            background: var(--bg-button-hover);
        }
        
        /* Memory Buttons */
        .memory-bar {
            display: flex;
            padding: 5px 15px;
            gap: 8px;
        }
        
        .mem-btn {
            flex: 1;
            padding: 8px;
            border: none;
            border-radius: 8px;
            background: var(--bg-button);
            color: var(--text-secondary);
            font-size: 12px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .mem-btn:hover {
            background: var(--bg-button-hover);
            color: var(--accent-cyan);
        }
        
        .mem-btn.active {
            color: var(--accent-cyan);
            background: rgba(0, 212, 255, 0.1);
        }
        
        /* Display */
        .display-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
            padding: 20px;
            background: linear-gradient(180deg, transparent 0%, rgba(0, 212, 255, 0.02) 100%);
            position: relative;
            overflow: hidden;
        }
        
        .display-container::before {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 1px;
            background: linear-gradient(90deg, transparent, var(--accent-cyan), transparent);
            opacity: 0.3;
        }
        
        .history-display {
            text-align: right;
            font-size: 16px;
            color: var(--text-secondary);
            min-height: 24px;
            margin-bottom: 8px;
            opacity: 0.7;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        
        .main-display {
            text-align: right;
            font-size: 48px;
            font-weight: 300;
            color: var(--text-primary);
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            text-shadow: 0 0 20px rgba(0, 212, 255, 0.1);
            transition: all 0.3s;
        }
        
        .main-display.small {
            font-size: 36px;
        }
        
        .main-display.very-small {
            font-size: 28px;
        }
        
        /* Keypad */
        .keypad {
            padding: 10px 15px 20px;
            display: grid;
            gap: 8px;
        }
        
        .keypad.basic {
            grid-template-columns: repeat(4, 1fr);
            grid-template-rows: repeat(5, 1fr);
        }
        
        .keypad.scientific {
            grid-template-columns: repeat(5, 1fr);
            grid-template-rows: repeat(6, 1fr);
        }
        
        .calc-btn {
            border: none;
            border-radius: 16px;
            font-size: 22px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.15s;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
            user-select: none;
            -webkit-user-select: none;
            height: 60px;
        }
        
        .calc-btn::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255,255,255,0.1);
            transform: translate(-50%, -50%);
            transition: width 0.3s, height 0.3s;
        }
        
        .calc-btn:active::after {
            width: 200px;
            height: 200px;
        }
        
        .calc-btn:active {
            transform: scale(0.95);
        }
        
        .btn-number {
            background: var(--bg-button);
            color: var(--text-primary);
            font-size: 26px;
        }
        
        .btn-number:hover {
            background: var(--bg-button-hover);
        }
        
        .btn-operator {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.15), rgba(0, 212, 255, 0.05));
            color: var(--accent-cyan);
            font-size: 28px;
        }
        
        .btn-operator:hover {
            background: linear-gradient(135deg, rgba(0, 212, 255, 0.25), rgba(0, 212, 255, 0.1));
            box-shadow: 0 0 15px rgba(0, 212, 255, 0.2);
        }
        
        .btn-operator.active {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
            color: white;
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.4);
        }
        
        .btn-function {
            background: rgba(239, 68, 68, 0.1);
            color: var(--accent-red);
            font-size: 18px;
        }
        
        .btn-function:hover {
            background: rgba(239, 68, 68, 0.2);
        }
        
        .btn-scientific {
            background: rgba(168, 85, 247, 0.1);
            color: var(--accent-purple);
            font-size: 16px;
            font-weight: 600;
        }
        
        .btn-scientific:hover {
            background: rgba(168, 85, 247, 0.2);
            box-shadow: 0 0 10px rgba(168, 85, 247, 0.2);
        }
        
        .btn-equals {
            background: linear-gradient(135deg, var(--accent-cyan), var(--accent-purple));
            color: white;
            font-size: 28px;
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.3);
        }
        
        .btn-equals:hover {
            box-shadow: 0 0 30px rgba(0, 212, 255, 0.5);
            transform: scale(1.02);
        }
        
        .btn-zero {
            grid-column: span 2;
        }
        
        /* Scientific keypad specific */
        .scientific .btn-number,
        .scientific .btn-operator,
        .scientific .btn-function,
        .scientific .btn-scientific,
        .scientific .btn-equals {
            height: 50px;
            font-size: 18px;
        }
        
        .scientific .btn-number {
            font-size: 22px;
        }
        
        /* History Panel */
        .history-panel {
            position: absolute;
            top: 0;
            right: -100%;
            width: 100%;
            height: 100%;
            background: var(--bg-secondary);
            z-index: 100;
            transition: right 0.3s ease;
            display: flex;
            flex-direction: column;
        }
        
        .history-panel.open {
            right: 0;
        }
        
        .history-header {
            padding: 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }
        
        .history-title {
            font-size: 18px;
            font-weight: 600;
            color: var(--accent-cyan);
        }
        
        .history-close {
            background: none;
            border: none;
            color: var(--text-secondary);
            font-size: 24px;
            cursor: pointer;
        }
        
        .history-list {
            flex: 1;
            overflow-y: auto;
            padding: 10px;
        }
        
        .history-item {
            padding: 15px;
            border-bottom: 1px solid rgba(255,255,255,0.03);
            cursor: pointer;
            transition: background 0.3s;
            border-radius: 10px;
            margin-bottom: 5px;
        }
        
        .history-item:hover {
            background: rgba(0, 212, 255, 0.05);
        }
        
        .history-expr {
            font-size: 14px;
            color: var(--text-secondary);
            margin-bottom: 5px;
        }
        
        .history-result {
            font-size: 20px;
            color: var(--accent-cyan);
            font-weight: 600;
        }
        
        .history-empty {
            text-align: center;
            padding: 50px;
            color: var(--text-secondary);
            font-size: 16px;
        }
        
        .clear-history {
            padding: 15px;
            border-top: 1px solid rgba(255,255,255,0.05);
        }
        
        .clear-history-btn {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 12px;
            background: rgba(239, 68, 68, 0.1);
            color: var(--accent-red);
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .clear-history-btn:hover {
            background: rgba(239, 68, 68, 0.2);
        }
        
        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 4px;
        }
        
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        
        ::-webkit-scrollbar-thumb {
            background: var(--accent-cyan);
            border-radius: 2px;
        }
        
        /* Animation for display update */
        @keyframes displayUpdate {
            0% { transform: scale(1); }
            50% { transform: scale(1.02); }
            100% { transform: scale(1); }
        }
        
        .display-update {
            animation: displayUpdate 0.2s ease;
        }
        
        /* Error state */
        .error {
            color: var(--accent-red) !important;
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <div class="calculator-container">
        <!-- Header -->
        <div class="header">
            <div class="logo">
                <div class="logo-icon">Σ</div>
                <div class="logo-text">CALC PRO</div>
            </div>
            <div class="header-actions">
                <button class="header-btn" onclick="toggleHistory()" title="History">📋</button>
                <button class="header-btn" onclick="toggleTheme()" title="Theme">🌙</button>
            </div>
        </div>
        
        <!-- Mode Switcher -->
        <div class="mode-switcher">
            <button class="mode-btn active" onclick="setMode('basic')" id="mode-basic">BASIC</button>
            <button class="mode-btn" onclick="setMode('scientific')" id="mode-scientific">SCIENTIFIC</button>
        </div>
        
        <!-- Memory Bar -->
        <div class="memory-bar">
            <button class="mem-btn" onclick="memoryClear()">MC</button>
            <button class="mem-btn" onclick="memoryRecall()">MR</button>
            <button class="mem-btn" onclick="memoryAdd()">M+</button>
            <button class="mem-btn" onclick="memorySubtract()">M−</button>
        </div>
        
        <!-- Display -->
        <div class="display-container">
            <div class="history-display" id="history-display"></div>
            <div class="main-display" id="main-display">0</div>
        </div>
        
        <!-- Basic Keypad -->
        <div class="keypad basic" id="keypad-basic">
            <button class="calc-btn btn-function" onclick="clearAll()">AC</button>
            <button class="calc-btn btn-function" onclick="clearEntry()">CE</button>
            <button class="calc-btn btn-scientific" onclick="appendOperator('%')">%</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('/')">÷</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('7')">7</button>
            <button class="calc-btn btn-number" onclick="appendNumber('8')">8</button>
            <button class="calc-btn btn-number" onclick="appendNumber('9')">9</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('*')">×</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('4')">4</button>
            <button class="calc-btn btn-number" onclick="appendNumber('5')">5</button>
            <button class="calc-btn btn-number" onclick="appendNumber('6')">6</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('-')">−</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('1')">1</button>
            <button class="calc-btn btn-number" onclick="appendNumber('2')">2</button>
            <button class="calc-btn btn-number" onclick="appendNumber('3')">3</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('+')">+</button>
            
            <button class="calc-btn btn-number btn-zero" onclick="appendNumber('0')">0</button>
            <button class="calc-btn btn-number" onclick="appendNumber('.')">.</button>
            <button class="calc-btn btn-equals" onclick="calculate()">=</button>
        </div>
        
        <!-- Scientific Keypad -->
        <div class="keypad scientific" id="keypad-scientific" style="display: none;">
            <button class="calc-btn btn-scientific" onclick="scientificFunc('sin')">sin</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('cos')">cos</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('tan')">tan</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('log')">log</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('ln')">ln</button>
            
            <button class="calc-btn btn-scientific" onclick="scientificFunc('asin')">sin⁻¹</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('acos')">cos⁻¹</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('atan')">tan⁻¹</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('sqrt')">√</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('cbrt')">∛</button>
            
            <button class="calc-btn btn-scientific" onclick="appendOperator('^')">xʸ</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('square')">x²</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('cube')">x³</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('factorial')">n!</button>
            <button class="calc-btn btn-scientific" onclick="appendOperator('(')">(</button>
            
            <button class="calc-btn btn-scientific" onclick="appendOperator(')')">)</button>
            <button class="calc-btn btn-scientific" onclick="appendNumber('3.14159')">π</button>
            <button class="calc-btn btn-scientific" onclick="appendNumber('2.71828')">e</button>
            <button class="calc-btn btn-function" onclick="clearAll()">AC</button>
            <button class="calc-btn btn-function" onclick="clearEntry()">CE</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('7')">7</button>
            <button class="calc-btn btn-number" onclick="appendNumber('8')">8</button>
            <button class="calc-btn btn-number" onclick="appendNumber('9')">9</button>
            <button class="calc-btn btn-scientific" onclick="appendOperator('%')">%</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('/')">÷</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('4')">4</button>
            <button class="calc-btn btn-number" onclick="appendNumber('5')">5</button>
            <button class="calc-btn btn-number" onclick="appendNumber('6')">6</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('abs')">|x|</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('*')">×</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('1')">1</button>
            <button class="calc-btn btn-number" onclick="appendNumber('2')">2</button>
            <button class="calc-btn btn-number" onclick="appendNumber('3')">3</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('reciprocal')">1/x</button>
            <button class="calc-btn btn-operator" onclick="appendOperator('-')">−</button>
            
            <button class="calc-btn btn-number" onclick="appendNumber('0')">0</button>
            <button class="calc-btn btn-number" onclick="appendNumber('.')">.</button>
            <button class="calc-btn btn-scientific" onclick="toggleSign()">+/-</button>
            <button class="calc-btn btn-scientific" onclick="scientificFunc('deg')">DEG</button>
            <button class="calc-btn btn-equals" onclick="calculate()">=</button>
        </div>
        
        <!-- History Panel -->
        <div class="history-panel" id="history-panel">
            <div class="history-header">
                <div class="history-title">📋 Calculation History</div>
                <button class="history-close" onclick="toggleHistory()">✕</button>
            </div>
            <div class="history-list" id="history-list">
                <div class="history-empty">No calculations yet</div>
            </div>
            <div class="clear-history">
                <button class="clear-history-btn" onclick="clearHistory()">Clear History</button>
            </div>
        </div>
    </div>
    
    <script>
        // Calculator State
        let currentInput = '0';
        let previousInput = '';
        let operator = null;
        let shouldResetScreen = false;
        let memory = 0;
        let history = [];
        let isDegree = true;
        let currentMode = 'basic';
        
        // DOM Elements
        const mainDisplay = document.getElementById('main-display');
        const historyDisplay = document.getElementById('history-display');
        const historyList = document.getElementById('history-list');
        const historyPanel = document.getElementById('history-panel');
        const keypadBasic = document.getElementById('keypad-basic');
        const keypadScientific = document.getElementById('keypad-scientific');
        
        // Create particles
        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.left = Math.random() * 100 + '%';
                particle.style.top = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 15 + 's';
                particle.style.animationDuration = (10 + Math.random() * 10) + 's';
                container.appendChild(particle);
            }
        }
        createParticles();
        
        // Update Display
        function updateDisplay() {
            mainDisplay.textContent = currentInput;
            
            // Adjust font size based on length
            mainDisplay.classList.remove('small', 'very-small');
            if (currentInput.length > 12) {
                mainDisplay.classList.add('small');
            }
            if (currentInput.length > 18) {
                mainDisplay.classList.add('very-small');
            }
            
            mainDisplay.classList.add('display-update');
            setTimeout(() => mainDisplay.classList.remove('display-update'), 200);
        }
        
        // Append Number
        function appendNumber(num) {
            if (shouldResetScreen) {
                currentInput = '';
                shouldResetScreen = false;
            }
            
            if (currentInput === '0' && num !== '.') {
                currentInput = num;
            } else if (num === '.' && currentInput.includes('.')) {
                return;
            } else {
                currentInput += num;
            }
            
            updateDisplay();
        }
        
        // Append Operator
        function appendOperator(op) {
            if (operator !== null && !shouldResetScreen) {
                calculate();
            }
            
            previousInput = currentInput;
            operator = op;
            shouldResetScreen = true;
            
            historyDisplay.textContent = previousInput + ' ' + getOperatorSymbol(op);
        }
        
        function getOperatorSymbol(op) {
            const symbols = {
                '+': '+',
                '-': '−',
                '*': '×',
                '/': '÷',
                '^': '^',
                '%': '%'
            };
            return symbols[op] || op;
        }
        
        // Calculate
        function calculate() {
            if (operator === null || shouldResetScreen) return;
            
            let result;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);
            
            try {
                switch (operator) {
                    case '+':
                        result = prev + current;
                        break;
                    case '-':
                        result = prev - current;
                        break;
                    case '*':
                        result = prev * current;
                        break;
                    case '/':
                        if (current === 0) throw new Error('Division by zero');
                        result = prev / current;
                        break;
                    case '^':
                        result = Math.pow(prev, current);
                        break;
                    case '%':
                        result = prev % current;
                        break;
                    default:
                        return;
                }
                
                // Format result
                result = formatResult(result);
                
                // Add to history
                addToHistory(`${previousInput} ${getOperatorSymbol(operator)} ${currentInput}`, result);
                
                currentInput = result.toString();
                operator = null;
                shouldResetScreen = true;
                historyDisplay.textContent = '';
                updateDisplay();
                
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(() => {
                    currentInput = '0';
                    updateDisplay();
                }, 2000);
            }
        }
        
        // Format Result
        function formatResult(num) {
            if (!isFinite(num)) return 'Error';
            if (Math.abs(num) < 1e-10) return 0;
            
            // Round to avoid floating point errors
            let result = Math.round(num * 1e10) / 1e10;
            
            // Convert to string with max precision
            let str = result.toString();
            
            // If too long, use scientific notation
            if (str.length > 15) {
                str = result.toExponential(10);
            }
            
            return parseFloat(str);
        }
        
        // Scientific Functions
        function scientificFunc(func) {
            let num = parseFloat(currentInput);
            let result;
            let expr = func + '(' + currentInput + ')';
            
            try {
                switch (func) {
                    case 'sin':
                        result = isDegree ? Math.sin(num * Math.PI / 180) : Math.sin(num);
                        break;
                    case 'cos':
                        result = isDegree ? Math.cos(num * Math.PI / 180) : Math.cos(num);
                        break;
                    case 'tan':
                        result = isDegree ? Math.tan(num * Math.PI / 180) : Math.tan(num);
                        break;
                    case 'asin':
                        result = isDegree ? Math.asin(num) * 180 / Math.PI : Math.asin(num);
                        break;
                    case 'acos':
                        result = isDegree ? Math.acos(num) * 180 / Math.PI : Math.acos(num);
                        break;
                    case 'atan':
                        result = isDegree ? Math.atan(num) * 180 / Math.PI : Math.atan(num);
                        break;
                    case 'log':
                        if (num <= 0) throw new Error('Invalid input');
                        result = Math.log10(num);
                        break;
                    case 'ln':
                        if (num <= 0) throw new Error('Invalid input');
                        result = Math.log(num);
                        break;
                    case 'sqrt':
                        if (num < 0) throw new Error('Invalid input');
                        result = Math.sqrt(num);
                        break;
                    case 'cbrt':
                        result = Math.cbrt(num);
                        break;
                    case 'square':
                        result = num * num;
                        expr = currentInput + '²';
                        break;
                    case 'cube':
                        result = num * num * num;
                        expr = currentInput + '³';
                        break;
                    case 'factorial':
                        if (num < 0 || !Number.isInteger(num)) throw new Error('Invalid input');
                        result = 1;
                        for (let i = 2; i <= num; i++) result *= i;
                        expr = currentInput + '!';
                        break;
                    case 'abs':
                        result = Math.abs(num);
                        expr = '|' + currentInput + '|';
                        break;
                    case 'reciprocal':
                        if (num === 0) throw new Error('Division by zero');
                        result = 1 / num;
                        expr = '1/' + currentInput;
                        break;
                    case 'deg':
                        isDegree = !isDegree;
                        currentInput = isDegree ? 'DEG' : 'RAD';
                        updateDisplay();
                        setTimeout(() => {
                            currentInput = num.toString();
                            updateDisplay();
                        }, 1000);
                        return;
                    default:
                        return;
                }
                
                result = formatResult(result);
                addToHistory(expr, result);
                currentInput = result.toString();
                shouldResetScreen = true;
                updateDisplay();
                
            } catch (error) {
                currentInput = 'Error';
                updateDisplay();
                setTimeout(() => {
                    currentInput = '0';
                    updateDisplay();
                }, 2000);
            }
        }
        
        // Toggle Sign
        function toggleSign() {
            if (currentInput !== '0') {
                currentInput = currentInput.startsWith('-') ? currentInput.slice(1) : '-' + currentInput;
                updateDisplay();
            }
        }
        
        // Clear All
        function clearAll() {
            currentInput = '0';
            previousInput = '';
            operator = null;
            shouldResetScreen = false;
            historyDisplay.textContent = '';
            updateDisplay();
        }
        
        // Clear Entry
        function clearEntry() {
            currentInput = '0';
            updateDisplay();
        }
        
        // Memory Functions
        function memoryClear() {
            memory = 0;
            showMemoryIndicator();
        }
        
        function memoryRecall() {
            currentInput = memory.toString();
            shouldResetScreen = true;
            updateDisplay();
        }
        
        function memoryAdd() {
            memory += parseFloat(currentInput) || 0;
            showMemoryIndicator();
        }
        
        function memorySubtract() {
            memory -= parseFloat(currentInput) || 0;
            showMemoryIndicator();
        }
        
        function showMemoryIndicator() {
            const memBtns = document.querySelectorAll('.mem-btn');
            memBtns.forEach(btn => {
                if (memory !== 0) {
                    btn.classList.add('active');
                } else {
                    btn.classList.remove('active');
                }
            });
        }
        
        // History Functions
        function addToHistory(expression, result) {
            history.unshift({ expression, result });
            if (history.length > 50) history.pop();
            updateHistoryDisplay();
        }
        
        function updateHistoryDisplay() {
            if (history.length === 0) {
                historyList.innerHTML = '<div class="history-empty">No calculations yet</div>';
                return;
            }
            
            historyList.innerHTML = history.map((item, index) => `
                <div class="history-item" onclick="loadHistory(${index})">
                    <div class="history-expr">${item.expression}</div>
                    <div class="history-result">= ${item.result}</div>
                </div>
            `).join('');
        }
        
        function loadHistory(index) {
            currentInput = history[index].result.toString();
            shouldResetScreen = true;
            updateDisplay();
            toggleHistory();
        }
        
        function clearHistory() {
            history = [];
            updateHistoryDisplay();
        }
        
        function toggleHistory() {
            historyPanel.classList.toggle('open');
        }
        
        // Mode Switcher
        function setMode(mode) {
            currentMode = mode;
            document.getElementById('mode-basic').classList.toggle('active', mode === 'basic');
            document.getElementById('mode-scientific').classList.toggle('active', mode === 'scientific');
            
            keypadBasic.style.display = mode === 'basic' ? 'grid' : 'none';
            keypadScientific.style.display = mode === 'scientific' ? 'grid' : 'none';
        }
        
        // Theme Toggle
        function toggleTheme() {
            document.body.classList.toggle('light-theme');
        }
        
        // Keyboard Support
        document.addEventListener('keydown', (e) => {
            if (e.key >= '0' && e.key <= '9') appendNumber(e.key);
            if (e.key === '.') appendNumber('.');
            if (e.key === '+') appendOperator('+');
            if (e.key === '-') appendOperator('-');
            if (e.key === '*') appendOperator('*');
            if (e.key === '/') appendOperator('/');
            if (e.key === '^') appendOperator('^');
            if (e.key === '%') appendOperator('%');
            if (e.key === 'Enter' || e.key === '=') calculate();
            if (e.key === 'Escape') clearAll();
            if (e.key === 'Backspace') {
                if (currentInput.length > 1) {
                    currentInput = currentInput.slice(0, -1);
                } else {
                    currentInput = '0';
                }
                updateDisplay();
            }
        });
        
        // Prevent zoom on double tap
        document.addEventListener('touchend', (e) => {
            e.preventDefault();
            e.target.click();
        }, { passive: false });
        
        // Prevent context menu
        document.addEventListener('contextmenu', (e) => e.preventDefault());
    </script>
</body>
</html>'''

# Save the file
with open('/mnt/agents/output/calc_pro.html', 'w', encoding='utf-8') as f:
    f.write(html_code)

print("File saved successfully!")
print(f"File size: {len(html_code)} characters")
        
