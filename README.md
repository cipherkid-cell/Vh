<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Solech Solar ROI Calculator</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background: #f4f8f9;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: flex-start;
    }
    .calculator {
        background: #fff;
        padding: 20px;
        max-width: 500px;
        width: 100%;
        box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        border-radius: 12px;
        margin: 30px;
    }
    h2 {
        text-align: center;
        color: #006b3c;
    }
    label {
        display: block;
        margin-top: 15px;
        font-weight: bold;
        color: #333;
    }
    input {
        width: 100%;
        padding: 10px;
        margin-top: 5px;
        border: 1px solid #ccc;
        border-radius: 6px;
        box-sizing: border-box;
    }
    button {
        background: #006b3c;
        color: #fff;
        border: none;
        padding: 12px;
        margin-top: 20px;
        width: 100%;
        border-radius: 6px;
        cursor: pointer;
        font-size: 16px;
    }
    button:hover {
        background: #004f2a;
    }
    .result {
        margin-top: 20px;
        padding: 15px;
        background: #e6f5e9;
        border: 1px solid #b2d8b7;
        border-radius: 6px;
        color: #006b3c;
        font-weight: bold;
    }
</style>
</head>
<body>

<div class="calculator">
    <h2>☀ Solech Solar ROI Calculator</h2>

    <label for="installCost">Installation Cost (₹):</label>
    <input type="number" id="installCost" placeholder="e.g. 100000" min="0">

    <label for="monthlySavings">Monthly Energy Savings (₹):</label>
    <input type="number" id="monthlySavings" placeholder="e.g. 3000" min="0">

    <label for="subsidy">Government Subsidy (₹):</label>
    <input type="number" id="subsidy" placeholder="e.g. 20000" min="0">

    <label for="maintenance">Annual Maintenance Cost (₹):</label>
    <input type="number" id="maintenance" placeholder="e.g. 1000" min="0">

    <button onclick="calculateROI()">Calculate ROI</button>

    <div id="result" class="result" style="display:none;"></div>
</div>

<script>
function calculateROI() {
    let installCost = parseFloat(document.getElementById('installCost').value) || 0;
    let monthlySavings = parseFloat(document.getElementById('monthlySavings').value) || 0;
    let subsidy = parseFloat(document.getElementById('subsidy').value) || 0;
    let maintenance = parseFloat(document.getElementById('maintenance').value) || 0;

    let netCost = installCost - subsidy;
    let annualSavings = (monthlySavings * 12) - maintenance;
    let roiYears = (annualSavings > 0) ? (netCost / annualSavings).toFixed(2) : Infinity;

    let resultText;
    if (roiYears === "Infinity") {
        resultText = "Your annual savings are not enough to recover costs.";
    } else {
        resultText = `You will recover your investment in approximately ${roiYears} years.`;
    }

    let resultBox = document.getElementById('result');
    resultBox.innerHTML = resultText;
    resultBox.style.display = "block";
}
</script>

</body>
</html>
        
