




































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

     
