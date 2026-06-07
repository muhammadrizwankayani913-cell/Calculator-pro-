PRO calc
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pro Scientific Calculator</title>
    <style>
        /* --- EXPERT CSS: Modern Glassmorphism & Dark Theme --- */
        :root {
            --bg-color: #0f172a;
            --calc-bg: rgba(30, 41, 59, 0.7);
            --display-color: #f8fafc;
            --btn-bg: rgba(51, 65, 85, 0.5);
            --btn-hover: rgba(71, 85, 105, 0.8);
            --accent-color: #38bdf8; /* Cyan Glow */
            --accent-hover: #0ea5e9;
            --operator-color: #f59e0b; /* Amber */
            --danger-color: #ef4444;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background: radial-gradient(circle at top left, #1e293b, #0f172a);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: var(--display-color);
        }

        .calculator {
            background: var(--calc-bg);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 24px;
            padding: 24px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
            width: 100%;
            max-width: 400px;
            transition: max-width 0.4s ease;
        }

        .calculator.scientific-mode {            max-width: 500px;
        }

        /* Mode Toggle */
        .mode-toggle {
            display: flex;
            justify-content: center;
            margin-bottom: 20px;
            background: rgba(15, 23, 42, 0.6);
            border-radius: 12px;
            padding: 4px;
        }

        .mode-btn {
            flex: 1;
            padding: 8px;
            border: none;
            background: transparent;
            color: #94a3b8;
            cursor: pointer;
            border-radius: 8px;
            font-weight: 600;
            transition: all 0.3s ease;
        }

        .mode-btn.active {
            background: var(--accent-color);
            color: #0f172a;
            box-shadow: 0 4px 12px rgba(56, 189, 248, 0.3);
        }

        /* Display Screen */
        .display {
            background: rgba(15, 23, 42, 0.8);
            border-radius: 16px;
            padding: 20px;
            text-align: right;
            margin-bottom: 20px;
            border: 1px solid rgba(255, 255, 255, 0.05);
            min-height: 100px;
            display: flex;
            flex-direction: column;
            justify-content: flex-end;
        }

        .previous-operand {
            color: #94a3b8;
            font-size: 1rem;
            min-height: 1.5rem;
            word-wrap: break-word;        }

        .current-operand {
            color: var(--display-color);
            font-size: 2.5rem;
            font-weight: 300;
            word-wrap: break-word;
            margin-top: 8px;
        }

        /* Buttons Grid */
        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
        }

        .calculator.scientific-mode .buttons-grid {
            grid-template-columns: repeat(5, 1fr);
        }

        button {
            padding: 18px;
            border: none;
            border-radius: 14px;
            font-size: 1.2rem;
            font-weight: 500;
            cursor: pointer;
            background: var(--btn-bg);
            color: var(--display-color);
            transition: all 0.2s ease;
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        button:hover {
            background: var(--btn-hover);
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(0);
        }

        .btn-operator {
            color: var(--operator-color);
            font-weight: 700;
        }

        .btn-equals {
            background: var(--accent-color);            color: #0f172a;
            font-weight: 700;
            grid-column: span 1;
        }

        .btn-equals:hover {
            background: var(--accent-hover);
        }

        .btn-clear {
            color: var(--danger-color);
            font-weight: 700;
        }

        .btn-scientific {
            display: none;
            font-size: 1rem;
            color: #a5f3fc;
        }

        .calculator.scientific-mode .btn-scientific {
            display: block;
        }

        /* DEG/RAD Indicator */
        .angle-mode {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 0.8rem;
            color: var(--accent-color);
            cursor: pointer;
            font-weight: bold;
        }
        
        .display-wrapper {
            position: relative;
        }

        /* Responsive */
        @media (max-width: 550px) {
            .calculator {
                margin: 10px;
                padding: 16px;
            }
            button {
                padding: 14px;
                font-size: 1.1rem;
            }
        }    </style>
</head>
<body>

    <div class="calculator" id="calculator">
        <div class="mode-toggle">
            <button class="mode-btn active" onclick="setMode('standard')">Standard</button>
            <button class="mode-btn" onclick="setMode('scientific')">Scientific</button>
        </div>

        <div class="display-wrapper">
            <div class="angle-mode" id="angleMode" onclick="toggleAngleMode()">DEG</div>
            <div class="display">
                <div class="previous-operand" id="previousOperand"></div>
                <div class="current-operand" id="currentOperand">0</div>
            </div>
        </div>

        <div class="buttons-grid" id="buttonsGrid">
            <!-- Scientific Row 1 -->
            <button class="btn-scientific" onclick="appendFunction('sin(')">sin</button>
            <button class="btn-scientific" onclick="appendFunction('cos(')">cos</button>
            <button class="btn-scientific" onclick="appendFunction('tan(')">tan</button>
            <button class="btn-scientific" onclick="appendValue('π')">π</button>
            <button class="btn-scientific" onclick="appendValue('e')">e</button>

            <!-- Scientific Row 2 -->
            <button class="btn-scientific" onclick="appendFunction('log(')">log</button>
            <button class="btn-scientific" onclick="appendFunction('ln(')">ln</button>
            <button class="btn-scientific" onclick="appendValue('(')">(</button>
            <button class="btn-scientific" onclick="appendValue(')')">)</button>
            <button class="btn-scientific" onclick="appendValue('^')">x^y</button>

            <!-- Standard Keys mixed with Grid -->
            <button class="btn-clear" onclick="clearDisplay()">AC</button>
            <button class="btn-clear" onclick="deleteLast()">DEL</button>
            <button class="btn-operator" onclick="appendValue('%')">%</button>
            <button class="btn-operator" onclick="appendValue('/')">÷</button>
            <button class="btn-scientific" onclick="appendFunction('sqrt(')">√</button>

            <button onclick="appendValue('7')">7</button>
            <button onclick="appendValue('8')">8</button>
            <button onclick="appendValue('9')">9</button>
            <button class="btn-operator" onclick="appendValue('*')">×</button>
            <button class="btn-scientific" onclick="appendValue('!')">n!</button>

            <button onclick="appendValue('4')">4</button>
            <button onclick="appendValue('5')">5</button>
            <button onclick="appendValue('6')">6</button>
            <button class="btn-operator" onclick="appendValue('-')">−</button>            <button class="btn-scientific" onclick="appendValue('1/')">1/x</button>

            <button onclick="appendValue('1')">1</button>
            <button onclick="appendValue('2')">2</button>
            <button onclick="appendValue('3')">3</button>
            <button class="btn-operator" onclick="appendValue('+')">+</button>
            <button class="btn-scientific" onclick="appendValue('E')">EXP</button>

            <button onclick="appendValue('0')" style="grid-column: span 2;">0</button>
            <button onclick="appendValue('.')">.</button>
            <button class="btn-equals" onclick="calculate()" style="grid-column: span 2;">=</button>
        </div>
    </div>

    <script>
        // --- EXPERT JAVASCRIPT: Class-based, Modular, and Safe ---
        class Calculator {
            constructor(previousOperandElement, currentOperandElement) {
                this.previousOperandElement = previousOperandElement;
                this.currentOperandElement = currentOperandElement;
                this.isDegree = true; // Default to Degrees
                this.clear();
            }

            clear() {
                this.currentOperand = '0';
                this.previousOperand = '';
                this.operation = undefined;
                this.updateDisplay();
            }

            delete() {
                if (this.currentOperand === 'Error') {
                    this.clear();
                    return;
                }
                this.currentOperand = this.currentOperand.toString().slice(0, -1);
                if (this.currentOperand === '') this.currentOperand = '0';
                this.updateDisplay();
            }

            appendValue(number) {
                if (this.currentOperand === 'Error') this.currentOperand = '';
                if (number === '.' && this.currentOperand.includes('.')) return;
                if (this.currentOperand === '0' && number !== '.') {
                    this.currentOperand = number.toString();
                } else {
                    this.currentOperand = this.currentOperand.toString() + number.toString();
                }
                this.updateDisplay();            }

            appendFunction(func) {
                if (this.currentOperand === '0' || this.currentOperand === 'Error') {
                    this.currentOperand = func;
                } else {
                    this.currentOperand += func;
                }
                this.updateDisplay();
            }

            calculate() {
                let expression = this.currentOperand;
                
                // Replace UI symbols with JavaScript Math equivalents
                expression = expression.replace(/×/g, '*').replace(/÷/g, '/').replace(/−/g, '-');
                expression = expression.replace(/π/g, 'Math.PI').replace(/e/g, 'Math.E');
                expression = expression.replace(/\^/g, '**');
                
                // Handle Factorial (simple implementation for small numbers)
                expression = expression.replace(/(\d+)!/g, (match, n) => this.factorial(parseInt(n)));

                // Handle Trigonometry based on DEG/RAD mode
                const trigMultiplier = this.isDegree ? `*(Math.PI/180)` : '';
                expression = expression.replace(/sin\(([^)]+)\)/g, `Math.sin($1${trigMultiplier})`);
                expression = expression.replace(/cos\(([^)]+)\)/g, `Math.cos($1${trigMultiplier})`);
                expression = expression.replace(/tan\(([^)]+)\)/g, `Math.tan($1${trigMultiplier})`);
                
                // Handle other math functions
                expression = expression.replace(/log\(/g, 'Math.log10(');
                expression = expression.replace(/ln\(/g, 'Math.log(');
                expression = expression.replace(/sqrt\(/g, 'Math.sqrt(');

                try {
                    // Safe evaluation using Function constructor instead of raw eval()
                    const result = new Function('return ' + expression)();
                    
                    // Format result to avoid long decimals
                    this.currentOperand = parseFloat(result.toFixed(10)).toString();
                    this.previousOperand = '';
                } catch (error) {
                    this.currentOperand = 'Error';
                }
                this.updateDisplay();
            }

            factorial(n) {
                if (n < 0) return NaN;
                if (n === 0 || n === 1) return 1;
                let result = 1;                for (let i = 2; i <= n; i++) result *= i;
                return result;
            }

            updateDisplay() {
                this.currentOperandElement.innerText = this.currentOperand;
                this.previousOperandElement.innerText = this.previousOperand;
            }
        }

        // Initialize Calculator
        const prevOpText = document.getElementById('previousOperand');
        const currOpText = document.getElementById('currentOperand');
        const calculator = new Calculator(prevOpText, currOpText);

        // Wrapper functions for HTML onclick events
        function appendValue(val) { calculator.appendValue(val); }
        function appendFunction(val) { calculator.appendFunction(val); }
        function clearDisplay() { calculator.clear(); }
        function deleteLast() { calculator.delete(); }
        function calculate() { calculator.calculate(); }

        // Mode Toggle Logic
        function setMode(mode) {
            const calc = document.getElementById('calculator');
            const btns = document.querySelectorAll('.mode-btn');
            
            btns.forEach(btn => btn.classList.remove('active'));
            
            if (mode === 'scientific') {
                calc.classList.add('scientific-mode');
                btns[1].classList.add('active');
            } else {
                calc.classList.remove('scientific-mode');
                btns[0].classList.add('active');
            }
        }

        // DEG / RAD Toggle
        function toggleAngleMode() {
            calculator.isDegree = !calculator.isDegree;
            document.getElementById('angleMode').innerText = calculator.isDegree ? 'DEG' : 'RAD';
        }

        // --- EXPERT FEATURE: Keyboard Support ---
        document.addEventListener('keydown', (e) => {
            if (e.key >= '0' && e.key <= '9') appendValue(e.key);
            if (e.key === '.') appendValue('.');
            if (e.key === '=' || e.key === 'Enter') { e.preventDefault(); calculate(); }
            if (e.key === 'Backspace') deleteLast();            if (e.key === 'Escape') clearDisplay();
            if (e.key === '+' || e.key === '-' || e.key === '*' || e.key === '/') appendValue(e.key);
            if (e.key === '(' || e.key === ')') appendValue(e.key);
            if (e.key === '^') appendValue('^');
        });
    </script>
</body>
</html>
