```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta
    name="description"
    content="Simple Calculator Web App built with HTML, CSS, and JavaScript for CodeOrbit Tech Internship."
  />
  <title>Calculator Web App | Task 3</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, Helvetica, sans-serif;
    }

    body {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      background: linear-gradient(135deg, #0f172a, #1e293b);
      padding: 20px;
    }

    /* Main calculator box */
    .calculator-container {
      width: 100%;
      max-width: 350px;

      background: #1e293b;
      border: 1px solid #334155;
      border-radius: 20px;

      padding: 20px;

      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
    }

    /* Small heading */
    .calculator-title {
      text-align: center;
      color: #e2e8f0;
      font-size: 1.15rem;
      margin-bottom: 15px;
      font-weight: 600;
    }

    .calculator-title span {
      color: #38bdf8;
    }

    /* Screen display */
    .display {
      width: 100%;
      min-height: 115px;

      display: flex;
      flex-direction: column;
      justify-content: flex-end;

      background: #0f172a;
      border: 1px solid #334155;
      border-radius: 12px;

      padding: 15px;
      margin-bottom: 18px;

      text-align: right;
      color: #f8fafc;

      overflow: hidden;
    }

    .previous-operand {
      min-height: 20px;

      color: #94a3b8;
      font-size: 0.9rem;

      word-break: break-all;
    }

    .current-operand {
      font-size: 2.3rem;
      font-weight: bold;

      margin-top: 5px;

      word-break: break-all;
    }

    /* Keypad grid */
    .buttons-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    /* Common button style */
    button {
      height: 58px;

      border: none;
      border-radius: 10px;

      font-size: 1.15rem;
      font-weight: 600;

      color: #f8fafc;
      background-color: #334155;

      cursor: pointer;

      transition:
        background-color 0.2s ease,
        transform 0.1s ease;
    }

    button:hover {
      background-color: #475569;
    }

    button:active {
      transform: scale(0.95);
    }

    /* AC, DEL and percentage */
    .btn-action {
      background-color: #475569;
      color: #38bdf8;
    }

    .btn-action:hover {
      background-color: #64748b;
    }

    /* Operators */
    .btn-operator {
      background-color: #2563eb;
      color: white;
    }

    .btn-operator:hover {
      background-color: #1d4ed8;
    }

    /* Equal button */
    .btn-equal {
      background-color: #16a34a;
      color: white;

      grid-column: span 2;
    }

    .btn-equal:hover {
      background-color: #15803d;
    }

    /* Keyboard hint */
    .keyboard-hint {
      margin-top: 14px;

      text-align: center;
      color: #64748b;

      font-size: 0.75rem;
    }

    /* Footer */
    footer {
      margin-top: 18px;

      color: #64748b;
      font-size: 0.82rem;

      text-align: center;
    }

    footer span {
      color: #94a3b8;
    }

    /* Mobile */
    @media (max-width: 400px) {

      body {
        padding: 12px;
      }

      .calculator-container {
        padding: 16px;
      }

      button {
        height: 55px;
        font-size: 1.05rem;
      }

      .current-operand {
        font-size: 2rem;
      }

      .buttons-grid {
        gap: 8px;
      }
    }

    /* Small height screens */
    @media (max-height: 650px) {

      .calculator-container {
        padding: 15px;
      }

      .display {
        min-height: 90px;
        margin-bottom: 12px;
      }

      button {
        height: 48px;
      }

      .keyboard-hint {
        margin-top: 8px;
      }
    }
  </style>
</head>

<body>

  <main class="calculator-container">

    <div class="calculator-title">
      Simple <span>Calculator</span>
    </div>

    <!-- Display Output -->
    <div class="display">
      <div
        id="previous-operand"
        class="previous-operand"
      ></div>

      <div
        id="current-operand"
        class="current-operand"
      >
        0
      </div>
    </div>

    <!-- Keypad Layout -->
    <div class="buttons-grid">

      <button
        class="btn-action"
        onclick="clearAll()"
      >
        AC
      </button>

      <button
        class="btn-action"
        onclick="deleteDigit()"
      >
        DEL
      </button>

      <button
        class="btn-action"
        onclick="appendOperator('%')"
      >
        %
      </button>

      <button
        class="btn-operator"
        onclick="appendOperator('/')"
      >
        ÷
      </button>


      <button onclick="appendNumber('7')">7</button>
      <button onclick="appendNumber('8')">8</button>
      <button onclick="appendNumber('9')">9</button>

      <button
        class="btn-operator"
        onclick="appendOperator('*')"
      >
        ×
      </button>


      <button onclick="appendNumber('4')">4</button>
      <button onclick="appendNumber('5')">5</button>
      <button onclick="appendNumber('6')">6</button>

      <button
        class="btn-operator"
        onclick="appendOperator('-')"
      >
        −
      </button>


      <button onclick="appendNumber('1')">1</button>
      <button onclick="appendNumber('2')">2</button>
      <button onclick="appendNumber('3')">3</button>

      <button
        class="btn-operator"
        onclick="appendOperator('+')"
      >
        +
      </button>


      <button onclick="appendNumber('0')">0</button>

      <button onclick="appendNumber('.')">
        .
      </button>

      <button
        class="btn-equal"
        onclick="calculateResult()"
      >
        =
      </button>

    </div>

    <div class="keyboard-hint">
      Keyboard: 0-9 &nbsp; + &nbsp; − &nbsp; × &nbsp; ÷ &nbsp; Enter &nbsp; Backspace
    </div>

  </main>

  <footer>
    Task 3: Calculator Web App |
    <span>Built by Balaji</span>
  </footer>


  <script>

    // State variables
    let currentInput = '0';
    let previousInput = '';
    let selectedOperator = null;
    let shouldResetDisplay = false;

    const currentDisplay =
      document.getElementById('current-operand');

    const previousDisplay =
      document.getElementById('previous-operand');


    /*
     * Updates the calculator display
     */
    function updateDisplay() {

      currentDisplay.textContent = currentInput;

      if (selectedOperator !== null) {

        const symbol =
          selectedOperator === '*'
            ? '×'
            : selectedOperator === '/'
            ? '÷'
            : selectedOperator;

        previousDisplay.textContent =
          `${previousInput} ${symbol}`;

      } else {

        previousDisplay.textContent = '';

      }
    }


    /*
     * Adds numbers or decimal point
     */
    function appendNumber(number) {

      // Don't allow two decimal points
      if (
        number === '.' &&
        currentInput.includes('.')
      ) {
        return;
      }

      // Start a new number after an operation
      if (
        shouldResetDisplay
      ) {

        currentInput = number;
        shouldResetDisplay = false;

      }

      // Replace starting zero
      else if (
        currentInput === '0' &&
        number !== '.'
      ) {

        currentInput = number;

      }

      else {

        currentInput += number;

      }

      updateDisplay();
    }


    /*
     * Selects an operator
     */
    function appendOperator(operator) {

      // If an operator is already selected,
      // allow the user to change it
      if (
        selectedOperator !== null &&
        shouldResetDisplay
      ) {

        selectedOperator = operator;

        updateDisplay();

        return;
      }


      // Calculate previous operation first
      if (
        previousInput !== '' &&
        selectedOperator !== null
      ) {

        calculateResult();

      }


      selectedOperator = operator;

      previousInput = currentInput;

      shouldResetDisplay = true;

      updateDisplay();
    }


    /*
     * Performs the calculation
     */
    function calculateResult() {

      if (
        selectedOperator === null ||
        shouldResetDisplay
      ) {
        return;
      }


      const prev =
        parseFloat(previousInput);

      const curr =
        parseFloat(currentInput);


      if (
        isNaN(prev) ||
        isNaN(curr)
      ) {

        currentInput = 'Error';

        clearState();

        updateDisplay();

        return;
      }


      let result;


      switch (selectedOperator) {

        case '+':

          result = prev + curr;

          break;


        case '-':

          result = prev - curr;

          break;


        case '*':

          result = prev * curr;

          break;


        case '/':

          if (curr === 0) {

            currentInput =
              'Cannot divide by 0';

            clearState();

            shouldResetDisplay = true;

            updateDisplay();

            return;
          }

          result = prev / curr;

          break;


        case '%':

          result = prev % curr;

          break;


        default:

          return;
      }


      // Round the result
      result =
        Math.round(
          (result + Number.EPSILON) * 1e8
        ) / 1e8;


      currentInput =
        result.toString();


      clearState();

      shouldResetDisplay = true;

      updateDisplay();
    }


    /*
     * Clears selected operator and previous value
     */
    function clearState() {

      selectedOperator = null;
      previousInput = '';

    }


    /*
     * Resets the calculator
     */
    function clearAll() {

      currentInput = '0';

      clearState();

      shouldResetDisplay = false;

      updateDisplay();

    }


    /*
     * Deletes the last digit
     */
    function deleteDigit() {

      if (
        shouldResetDisplay ||
        currentInput === 'Error' ||
        currentInput === 'Cannot divide by 0'
      ) {

        clearAll();

        return;
      }


      if (
        currentInput.length === 1
      ) {

        currentInput = '0';

      }

      else {

        currentInput =
          currentInput.slice(0, -1);

      }


      updateDisplay();
    }


    /*
     * Keyboard support
     */
    document.addEventListener(
      'keydown',
      function(event) {

        const key = event.key;


        // Numbers
        if (
          key >= '0' &&
          key <= '9'
        ) {

          appendNumber(key);

        }


        // Decimal
        else if (
          key === '.'
        ) {

          appendNumber('.');

        }


        // Operators
        else if (
          key === '+' ||
          key === '-' ||
          key === '*' ||
          key === '/'
        ) {

          appendOperator(key);

        }


        // Enter
        else if (
          key === 'Enter' ||
          key === '='
        ) {

          event.preventDefault();

          calculateResult();

        }


        // Backspace
        else if (
          key === 'Backspace'
        ) {

          deleteDigit();

        }


        // Escape
        else if (
          key === 'Escape'
        ) {

          clearAll();

        }


        // Percentage
        else if (
          key === '%'
        ) {

          appendOperator('%');

        }

      }
    );


    // Initial display
    updateDisplay();

  </script>

</body>
</html>
```
