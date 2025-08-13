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




































   <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Solech – Solar ROI Calculator</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body { background: #f4f8f9; font-family: Arial, sans-serif; }
    .container { max-width: 800px; margin-top: 30px; }
    .card { padding: 20px; border-radius: 15px; }
    #result { margin-top: 20px; font-weight: bold; }
  </style>
</head>
<body>
  <div class="container">
    <h1 class="text-center">Solech Solar ROI Calculator</h1>
    <div class="card shadow">
      <label>Installation Cost (₹):</label>
      <input type="number" id="installCost" class="form-control" placeholder="100000">

      <label>Estimated Monthly Energy Savings (₹):</label>
      <input type="number" id="monthlySavings" class="form-control" placeholder="3000">

      <label>Solar Panel Capacity (kW):</label>
      <input type="number" id="panelCapacity" class="form-control" placeholder="5">

      <label>Government Subsidy (₹):</label>
      <input type="number" id="subsidy" class="form-control" placeholder="20000">

      <label>Annual Maintenance Cost (₹):</label>
      <input type="number" id="maintenance" class="form-control" placeholder="1000">

      <label>Location:</label>
      <input type="text" id="location" class="form-control" placeholder="Bangalore, India">

      <button class="btn btn-primary mt-3" onclick="calculateROI()">Calculate ROI</button>
      <div id="result" class="alert alert-success" style="display:none;"></div>

      <canvas id="roiChart" style="max-width:100%; margin-top:20px;"></canvas>

      <hr>
      <h4>Get a Quote</h4>
      <form id="leadForm">
        <input type="text" id="name" class="form-control mb-2" placeholder="Your Name" required>
        <input type="email" id="email" class="form-control mb-2" placeholder="Email" required>
        <input type="tel" id="phone" class="form-control mb-2" placeholder="Phone Number" required>
        <button type="submit" class="btn btn-success">Submit</button>
      </form>

      <hr>
      <h4>Pay Now</h4>
      <button id="payBtn" class="btn btn-warning">Pay with Razorpay</button>
    </div>
  </div>

<script src="https://checkout.razorpay.com/v1/checkout.js"></script>
<script>
let chart;
function calculateROI() {
  const installCost = parseFloat(document.getElementById('installCost').value) || 0;
  const monthlySavings = parseFloat(document.getElementById('monthlySavings').value) || 0;
  const panelCapacity = parseFloat(document.getElementById('panelCapacity').value) || 0;
  const subsidy = parseFloat(document.getElementById('subsidy').value) || 0;
  const maintenance = parseFloat(document.getElementById('maintenance').value) || 0;

  const netCost = installCost - subsidy;
  const annualSavings = (monthlySavings * 12) - maintenance;
  const roiYears = netCost / annualSavings;

  document.getElementById('result').style.display = 'block';
  document.getElementById('result').innerText = `ROI Period: ${roiYears.toFixed(2)} years`;

  const labels = [];
  const savingsData = [];
  let cumulative = 0;
  for (let year = 1; year <= 25; year++) {
    cumulative += annualSavings;
    labels.push(`Year ${year}`);
    savingsData.push(cumulative);
  }

  if (chart) chart.destroy();
  chart = new Chart(document.getElementById('roiChart'), {
    type: 'line',
    data: { labels, datasets: [{ label: 'Cumulative Savings (₹)', data: savingsData, borderColor: '#007bff', fill: false }] },
    options: { responsive: true }
  });
}

document.getElementById('leadForm').addEventListener('submit', function(e) {
  e.preventDefault();
  alert('Thanks! We will contact you soon.');
});

document.getElementById('payBtn').onclick = function(){
  const options = {
    key: 'YOUR_RAZORPAY_KEY',
    amount: 50000,
    currency: 'INR',
    name: 'Solech',
    description: 'Solar Advance Payment',
    handler: function (response) { alert('Payment ID: ' + response.razorpay_payment_id); }
  };
  new Razorpay(options).open();
};
</script>
</body>
</html>

     
