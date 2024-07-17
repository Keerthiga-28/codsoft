// script.js
document.addEventListener('DOMContentLoaded', () => {
    const display = document.getElementById('display');
    let currentInput = '';
    let operator = '';
    let firstOperand = '';

    const calculate = () => {
        try {
            return String(eval(currentInput));
        } catch {
            return 'Error';
        }
    };

    const handleButtonClick = (value) => {
        if (value === 'C') {
            currentInput = '';
            operator = '';
            firstOperand = '';
            display.textContent = '0';
        } else if (value === '=') {
            if (operator && firstOperand) {
                currentInput = String(eval(`${firstOperand}${operator}${currentInput}`));
                display.textContent = currentInput;
                operator = '';
                firstOperand = '';
            } else {
                display.textContent = calculate();
            }
        } else if (['+', '-', '*', '/'].includes(value)) {
            operator = value;
            firstOperand = currentInput;
            currentInput = '';
        } else if (value === '%') {
            currentInput = (parseFloat(currentInput) / 100).toString();
            display.textContent = currentInput;
        } else if (value === 'sqrt') {
            currentInput = Math.sqrt(parseFloat(currentInput)).toString();
            display.textContent = currentInput;
        } else if (value === 'pow') {
            currentInput = `${currentInput}**`;
        } else {
            currentInput += value;
            display.textContent = currentInput;
        }
    };

    document.querySelectorAll('.btn').forEach(button => {
        button.addEventListener('click', (event) => {
            handleButtonClick(event.target.dataset.value);
        });
    });
});
