# My-first-<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .calculator-container {
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
            padding: 20px;
            width: 100%;
            max-width: 400px;
        }

        .calculator-title {
            text-align: center;
            font-size: 28px;
            font-weight: bold;
            color: #333;
            margin-bottom: 20px;
        }

        .display {
            background: #1a1a1a;
            color: #00ff00;
            font-size: 2.5em;
            padding: 20px;
            border-radius: 10px;
            text-align: right;
            margin-bottom: 20px;
            min-height: 60px;
            font-family: 'Courier New', monospace;
            word-wrap: break-word;
            word-break: break-all;
            overflow-y: auto;
            max-height: 120px;
        }

        .buttons-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }

        button {
            padding: 20px;
            font-size: 1.5em;
            font-weight: bold;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        button:hover {
            transform: scale(1.05);
        }

        button:active {
            transform: scale(0.95);
        }

        .number-btn {
            background: #f0f0f0;
            color: #333;
        }

        .number-btn:hover {
            background: #e0e0e0;
        }

        .operator-btn {
            background: #667eea;
            color: white;
        }

        .operator-btn:hover {
            background: #5568d3;
        }

        .equals-btn {
            background: #48bb78;
            color: white;
            grid-column: span 2;
        }

        .equals-btn:hover {
            background: #38a169;
        }

        .clear-btn {
            background: #f56565;
            color: white;
            grid-column: span 2;
        }

        .clear-btn:hover {
            background: #e53e3e;
        }

        .delete-btn {
            background: #ed8936;
            color: white;
        }

        .delete-btn:hover {
            background: #dd6b20;
        }

        .toggle-sign-btn {
            background: #9f7aea;
            color: white;
        }

        .toggle-sign-btn:hover {
            background: #805ad5;
        }

        .decimal-btn {
            background: #f0f0f0;
            color: #333;
        }

        .decimal-btn:hover {
            background: #e0e0e0;
        }

        .history-section {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 2px solid #e0e0e0;
        }

        .history-title {
            font-size: 14px;
            font-weight: bold;
            color: #666;
            margin-bottom: 10px;
        }

        .history-list {
            background: #f9f9f9;
            border-radius: 10px;
            padding: 10px;
            max-height: 150px;
            overflow-y: auto;
            font-size: 12px;
        }

        .history-item {
            padding: 5px;
            color: #333;
            border-bottom: 1px solid #e0e0e0;
        }

        .history-item:last-child {
            border-bottom: none;
        }

        .clear-history-btn {
            width: 100%;
            margin-top: 10px;
            padding: 10px;
            background: #cbd5e0;
            color: #333;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
        }

        .clear-history-btn:hover {
            background: #a0aec0;
        }

        @media (max-width: 480px) {
            .calculator-container {
                max-width: 100%;
                margin: 10px;
            }

            button {
                padding: 15px;
                font-size: 1.2em;
            }

            .display {
                font-size: 2em;
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="calculator-container">
        <div class="calculator-title">🧮 Calculator</div>
        
        <div class="display" id="display">0</div>

        <div class="buttons-grid">
            <button class="clear-btn" onclick="clearDisplay()">AC</button>
            <button class="delete-btn" onclick="deleteLast()">DEL</button>
            <button class="toggle-sign-btn" onclick="toggleSign()">+/-</button>
            <button class="operator-btn" onclick="appendOperator('/')">÷</button>

            <button class="number-btn" onclick="appendNumber('7')">7</button>
            <button class="number-btn" onclick="appendNumber('8')">8</button>
            <button class="number-btn" onclick="appendNumber('9')">9</button>
            <button class="operator-btn" onclick="appendOperator('*')">×</button>

            <button class="number-btn" onclick="appendNumber('4')">4</button>
            <button class="number-btn" onclick="appendNumber('5')">5</button>
            <button class="number-btn" onclick="appendNumber('6')">6</button>
            <button class="operator-btn" onclick="appendOperator('-')">−</button>

            <button class="number-btn" onclick="appendNumber('1')">1</button>
            <button class="number-btn" onclick="appendNumber('2')">2</button>
            <button class="number-btn" onclick="appendNumber('3')">3</button>
            <button class="operator-btn" onclick="appendOperator('+')">+</button>

            <button class="number-btn" onclick="appendNumber('0')">0</button>
            <button class="decimal-btn" onclick="appendDecimal()">.</button>
            <button class="equals-btn" onclick="calculate()">=</button>
        </div>

        <div class="history-section">
            <div class="history-title">Calculation History</div>
            <div class="history-list" id="historyList"></div>
            <button class="clear-history-btn" onclick="clearHistory()">Clear History</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let historyList = document.getElementById('historyList');
        let currentInput = '0';
        let previousInput = '';
        let operator = null;
        let shouldResetDisplay = false;
        let history = JSON.parse(localStorage.getItem('calcHistory')) || [];

        // Initialize display and history
        updateDisplay();
        displayHistory();

        function updateDisplay() {
            display.textContent = currentInput;
        }

        function appendNumber(num) {
            if (shouldResetDisplay) {
                currentInput = num;
                shouldResetDisplay = false;
            } else {
                currentInput = currentInput === '0' ? num : currentInput + num;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operator !== null && !shouldResetDisplay) {
                calculate();
            }
            previousInput = currentInput;
            operator = op;
            shouldResetDisplay = true;
        }

        function appendDecimal() {
            if (shouldResetDisplay) {
                currentInput = '0.';
                shouldResetDisplay = false;
            } else if (!currentInput.includes('.')) {
                currentInput += '.';
            }
            updateDisplay();
        }

        function toggleSign() {
            currentInput = String(parseFloat(currentInput) * -1);
            updateDisplay();
        }

        function deleteLast() {
            if (currentInput.length > 1) {
                currentInput = currentInput.slice(0, -1);
            } else {
                currentInput = '0';
            }
            updateDisplay();
        }

        function clearDisplay() {
            currentInput = '0';
            previousInput = '';
            operator = null;
            shouldResetDisplay = false;
            updateDisplay();
        }

        function calculate() {
            if (operator === null || shouldResetDisplay) return;

            let result;
            const prev = parseFloat(previousInput);
            const current = parseFloat(currentInput);

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
                    result = current === 0 ? 'Error' : prev / current;
                    break;
                default:
                    return;
            }

            // Add to history
            const calculation = `${prev} ${operator} ${current} = ${result}`;
            addToHistory(calculation);

            currentInput = String(result);
            operator = null;
            shouldResetDisplay = true;
            updateDisplay();
        }

        function addToHistory(calculation) {
            history.unshift(calculation);
            if (history.length > 10) history.pop();
            localStorage.setItem('calcHistory', JSON.stringify(history));
            displayHistory();
        }

        function displayHistory() {
            historyList.innerHTML = '';
            if (history.length === 0) {
                historyList.innerHTML = '<div class="history-item">No history yet</div>';
                return;
            }
            history.forEach(item => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                historyItem.textContent = item;
                historyList.appendChild(historyItem);
            });
        }

        function clearHistory() {
            history = [];
            localStorage.removeItem('calcHistory');
            displayHistory();
        }

        // Keyboard support
        document.addEventListener('keydown', function(event) {
            if (event.key >= '0' && event.key <= '9') appendNumber(event.key);
            if (event.key === '.') appendDecimal();
            if (event.key === '+' || event.key === '-') appendOperator(event.key);
            if (event.key === '*') { event.preventDefault(); appendOperator('*'); }
            if (event.key === '/') { event.preventDefault(); appendOperator('/'); }
            if (event.key === 'Enter' || event.key === '=') { event.preventDefault(); calculate(); }
            if (event.key === 'Backspace') deleteLast();
            if (event.key === 'Escape') clearDisplay();
        });
    </script>
</body>
</html>

