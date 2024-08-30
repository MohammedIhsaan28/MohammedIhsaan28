<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Engineering Scientific Calculator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #1c1c1c;
            font-family: 'Courier New', Courier, monospace;
            color: #ffffff;
            margin: 0;
        }
        .calculator {
            background-color: #2b2b2b; /* Darker silver mixed with black */
            padding: 15px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.2), 0 0 30px rgba(255, 255, 255, 0.1);
            max-width: 100%;
            width: 350px;
            height: 70vh;
            display: flex;
            flex-direction: column;
        }
        .display {
            width: 100%;
            height: 50px;
            margin-bottom: 10px;
            padding: 10px;
            text-align: right;
            font-size: 20px;
            color: #000000;
            background-color: #e5e4e2; /* Light silver */
            border: none;
            border-radius: 8px;
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.2);
        }
        .buttons {
            flex-grow: 1;
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 5px;
            overflow: hidden;
        }
        .buttons button {
            padding: 10px;
            font-size: 16px;
            border-radius: 8px;
            border: none;
            background-color: #3c3c3c; /* Medium silver mixed with black */
            color: #ffffff;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            transition: background-color 0.3s, transform 0.3s;
        }
        .buttons button:hover {
            background-color: #5c5c5c;
            transform: scale(1.05);
        }
        .buttons button.special {
            background-color: #5a5a5a; /* Darker silver */
            color: #ffffff;
        }
        .buttons button.special:hover {
            background-color: #7a7a7a;
        }
        .buttons button.equal {
            background-color: #ff4500; /* Dark orange for equal button */
            color: #ffffff;
            grid-column: span 4;
        }
        .buttons button.equal:hover {
            background-color: #ff6347;
        }
        .section-title {
            grid-column: span 4;
            text-align: center;
            font-size: 14px;
            color: #dcdcdc;
            margin: 5px 0;
        }
        .nav-buttons {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
        }
        .nav-buttons button {
            padding: 5px 10px;
            font-size: 16px;
            border-radius: 5px;
            border: none;
            background-color: #3c3c3c;
            color: #ffffff;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            transition: background-color 0.3s;
        }
        .nav-buttons button:hover {
            background-color: #5c5c5c;
        }
    </style>
</head>
<body>

<div class="calculator">
    <div class="nav-buttons">
        <button onclick="showPage(1)">Basic</button>
        <button onclick="showPage(2)">Scientific</button>
        <button onclick="showPage(3)">Conversions</button>
    </div>
    <input type="text" class="display" id="display" disabled>
    <div id="page1" class="buttons">
        <!-- Basic Arithmetic -->
        <div class="section-title">Basic Arithmetic</div>
        <button class="special" onclick="clearDisplay()">C</button>
        <button class="special" onclick="deleteNumber()">DEL</button>
        <button class="special" onclick="appendOperator('(')">(</button>
        <button class="special" onclick="appendOperator(')')">)</button>
        <button class="special" onclick="appendOperator('/')">/</button>
        <button onclick="appendNumber('7')">7</button>
        <button onclick="appendNumber('8')">8</button>
        <button onclick="appendNumber('9')">9</button>
        <button class="special" onclick="appendOperator('*')">*</button>
        <button class="special" onclick="appendOperator('%')">%</button>
        <button onclick="appendNumber('4')">4</button>
        <button onclick="appendNumber('5')">5</button>
        <button onclick="appendNumber('6')">6</button>
        <button class="special" onclick="appendOperator('-')">-</button>
        <button class="special" onclick="appendFunction('Math.pow(10,')">10^x</button>
        <button onclick="appendNumber('1')">1</button>
        <button onclick="appendNumber('2')">2</button>
        <button onclick="appendNumber('3')">3</button>
        <button class="special" onclick="appendOperator('+')">+</button>
        <button onclick="appendNumber('0')">0</button>
        <button onclick="appendOperator('.')">.</button>
        <button class="special" onclick="appendFunction('Math.sqrt(')">√x</button>
        <button class="equal" onclick="calculate()">=</button>
    </div>
    <div id="page2" class="buttons" style="display:none;">
        <!-- Scientific Operations -->
        <div class="section-title">Trigonometric Functions</div>
        <button class="special" onclick="appendFunction('Math.sin(')">sin</button>
        <button class="special" onclick="appendFunction('Math.cos(')">cos</button>
        <button class="special" onclick="appendFunction('Math.tan(')">tan</button>
        <button class="special" onclick="appendFunction('Math.asin(')">asin</button>
        <button class="special" onclick="appendFunction('Math.acos(')">acos</button>
        <button class="special" onclick="appendFunction('Math.atan(')">atan</button>
        <button class="special" onclick="appendFunction('Math.sinh(')">sinh</button>
        <button class="special" onclick="appendFunction('Math.cosh(')">cosh</button>
        <button class="special" onclick="appendFunction('Math.tanh(')">tanh</button>

        <div class="section-title">Logarithmic & Exponential</div>
        <button class="special" onclick="appendFunction('Math.log(')">ln</button>
        <button class="special" onclick="appendFunction('Math.log10(')">log</button>
        <button class="special" onclick="appendFunction('Math.exp(')">e^x</button>
        <button class="special" onclick="appendFunction('Math.pow(2,')">2^x</button>

        <div class="section-title">Power & Roots</div>
        <button class="special" onclick="appendFunction('Math.pow(')">x^y</button>
        <button class="special" onclick="appendFunction('Math.sqrt(')">√x</button>
        <button class="special" onclick="appendFunction('Math.cbrt(')">∛x</button>
        <button class="special" onclick="appendFunction('factorial(')">n!</button>

        <div class="section-title">Constants</div>
        <button class="special" onclick="appendFunction('Math.PI')">π</button>
        <button class="special" onclick="appendFunction('Math.E')">e</button>
    </div>
    <div id="page3" class="buttons" style="display:none;">
        <!-- Conversion Functions -->
        <div class="section-title">Conversions</div>
        <button class="special" onclick="convertToBinary()">Dec → Bin</button>
        <button class="special" onclick="convertToOctal()">Dec → Oct</button>
        <button class="special" onclick="convertToHex()">Dec → Hex</button>
        <button class="special" onclick="convertFromBinary()">Bin → Dec</button>
        <button class="special" onclick="convertFromHex()">Hex → Dec</button>
        <button class="special" onclick="convertToRadians()">Deg → Rad</button>
        <button class="special" onclick="convertToDegrees()">Rad → Deg</button>

        <!-- Boolean Operations -->
        <!-- Boolean Operations -->
        <div class="section-title">Boolean & Bitwise</div>
        <button class="special" onclick="appendOperator('&')">AND</button>
        <button class="special" onclick="appendOperator('|')">OR</button>
        <button class="special" onclick="appendOperator('^')">XOR</button>
        <button class="special" onclick="appendOperator('~')">NOT</button>
        <button class="special" onclick="appendOperator('<<')">Shift Left</button>
        <button class="special" onclick="appendOperator('>>')">Shift Right</button>
    </div>
</div>

<script>
    let expression = '';
    const display = document.getElementById('display');

    function appendNumber(number) {
        expression += number;
        display.value = expression;
    }

    function appendOperator(operator) {
        expression += operator;
        display.value = expression;
    }

    function appendFunction(func) {
        expression += func;
        display.value = expression;
    }

    function clearDisplay() {
        expression = '';
        display.value = '';
    }

    function deleteNumber() {
        expression = expression.slice(0, -1);
        display.value = expression;
    }

    function calculate() {
        try {
            expression = eval(expression).toString();
            display.value = expression;
        } catch (error) {
            display.value = 'Error';
            expression = '';
        }
    }

    function factorial(n) {
        if (n === 0 || n === 1) return 1;
        let result = 1;
        for (let i = 2; i <= n; i++) {
            result *= i;
        }
        return result;
    }

    function convertToBinary() {
        expression = parseInt(expression).toString(2);
        display.value = expression;
    }

    function convertToOctal() {
        expression = parseInt(expression).toString(8);
        display.value = expression;
    }

    function convertToHex() {
        expression = parseInt(expression).toString(16).toUpperCase();
        display.value = expression;
    }

    function convertFromBinary() {
        expression = parseInt(expression, 2).toString(10);
        display.value = expression;
    }

    function convertFromHex() {
        expression = parseInt(expression, 16).toString(10);
        display.value = expression;
    }

    function convertToRadians() {
        expression = (eval(expression) * Math.PI) / 180;
        display.value = expression;
    }

    function convertToDegrees() {
        expression = (eval(expression) * 180) / Math.PI;
        display.value = expression;
    }

    function showPage(pageNumber) {
        document.getElementById('page1').style.display = 'none';
        document.getElementById('page2').style.display = 'none';
        document.getElementById('page3').style.display = 'none';
        document.getElementById('page' + pageNumber).style.display = 'grid';
    }
</script>

</body>
</html>
