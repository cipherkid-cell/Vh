<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Solech - Solar Solutions</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    * { box-sizing: border-box; margin:0; padding:0; font-family: 'Poppins', sans-serif; }
    body { line-height:1.6; color:#333; }
    header { background:#2d9cdb; color:white; padding:20px 10%; display:flex; justify-content:space-between; align-items:center; position:sticky; top:0; z-index:1000; }
    header nav a { color:white; margin-left:20px; text-decoration:none; font-weight:600; }
    header .cta { background:#fff; color:#2d9cdb; padding:8px 16px; border-radius:8px; font-weight:bold; text-decoration:none; margin-left:20px; }
    .hero { display:flex; flex-direction:column; justify-content:center; align-items:center; text-align:center; padding:100px 10%; background:linear-gradient(135deg,#e0f7fa,#f0f8ff); }
    .hero h1 { font-size:3em; color:#2d9cdb; margin-bottom:20px; }
    .hero p { font-size:1.2em; margin-bottom:30px; }
    .hero .buttons a { background:#2d9cdb; color:white; padding:12px 25px; border-radius:8px; text-decoration:none; font-weight:bold; margin:0 10px; }
    .hero .buttons a:hover { background:#2380c6; }
    .features { display:flex; flex-wrap:wrap; justify-content:space-around; padding:60px 10%; background:#fff; }
    .feature { flex:1 1 250px; text-align:center; margin:20px; }
    .feature h3 { color:#2d9cdb; margin-bottom:10px; }
    .section { padding:60px 10%; }
    footer { background:#2d9cdb; color:white; padding:40px 10%; display:flex; justify-content:space-between; flex-wrap:wrap; }
    footer a { color:white; text-decoration:none; margin-right:20px; }
    /* Calculator Styles */
    .calculator { background:#ffffffcc; padding:30px; border-radius:15px; box-shadow:0 8px 20px rgba(0,0,0,0.15); max-width:450px; margin:0 auto; }
    .calculator h2 { color:#2d9cdb; text-align:center; margin-bottom:20px; }
    .calculator label { display:block; margin-top:15px; font-weight:600; color:#333; }
    .calculator input { width:100%; padding:10px; margin-top:5px; border-radius:8px; border:1px solid #999; font-size:14px; }
    .calculator button { margin-top:20px; padding:12px; width:100%; background-color:#2d9cdb; color:white; border:none; border-radius:8px; font-size:16px; cursor:pointer; font-weight:bold; }
    .calculator button:hover { background-color:#2380c6; }
    .calculator .result { margin-top:20px; padding:15px; background-color:#e0f7fa; border-radius:8px; font-weight:bold; font-size:16px; text-align:center; display:none; }
    @media(max-width:768px){ .features { flex-direction:column; align-items:center; } header { flex-direction:column; } }
  </style>
</head>
<body>

  <!-- Header -->
  <header>
    <div class="logo"><h2>Solech</h2></div>
    <nav>
      <a href="#solutions">Solutions</a>
      <a href="#calculator">ROI Calculator</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
      <a href="#contact" class="cta">Get a Quote</a>
    </nav>
  </header>

  <!-- Hero -->
  <section class="hero">
    <h1>Affordable Solar Solutions, Powered by AI</h1>
    <p>Cut energy costs and invest in a sustainable future.</p>
    <div class="buttons">
      <a href="#calculator">Calculate ROI</a>
      <a href="#solutions">Learn More</a>
    </div>
  </section>

  <!-- Features -->
  <section id="solutions" class="features">
    <div class="feature">
      <h3>Affordable</h3>
      <p>High-quality solar solutions that fit your budget.</p>
    </div>
    <div class="feature">
      <h3>AI-Optimized</h3>
      <p>Maximize efficiency with AI-powered predictions.</p>
    </div>
    <div class="feature">
      <h3>International Clients</h3>
      <p>Serving businesses and homes across the globe.</p>
    </div>
    <div class="feature">
      <h3>Hassle-Free Setup</h3>
      <p>We handle installation, permits, and maintenance.</p>
    </div>
  </section>

  <!-- ROI Calculator -->
  <section id="calculator" class="section">
    <div class="calculator">
      <h2>Solech Solar ROI Calculator</h2>
      <label for="installCost">Installation Cost (₹):</label>
      <input type="number" id="installCost" placeholder="e.g. 100000" min="0">

      <label for="monthlySavings">Estimated Monthly Energy Savings (₹):</label>
      <input type="number" id="monthlySavings" placeholder="e.g. 3000" min="0">

      <label for="panelCapacity">Solar Panel Capacity (kW):</label>
      <input type="number" id="panelCapacity" placeholder="e.g. 5" min="0">

      <label for="subsidy">Government Subsidy (₹):</label>
      <input type="number" id="subsidy" placeholder="e.g. 20000" min="0">

      <label for="maintenance">Annual Maintenance Cost (₹):</label>
      <input type="number" id="maintenance" placeholder="e.g. 1000" min="0">

      <label for="location">Location (City, Country):</label>
      <input type="text" id="location" placeholder="e.g. Bangalore, India">

      <button onclick="calculateROI()">Calculate ROI</button>
      <div id="result" class="result"></div>
      <canvas id="roiChart" style="max-width:100%; margin-top:20px;"></canvas>
    </div>
  </section>

  <!-- About -->
  <section id="about" class="section" style="background:#f0f8ff; text-align:center;">
    <h2>About Solech</h2>
    <p>At Solech, we are committed to delivering affordable, AI-driven solar solutions for homes and businesses worldwide.</p>
  </section>

  <!-- Contact -->
  <section id="contact" class="section">
    <h2>Contact Us</h2>
    <form style="display:flex; flex-direction:column; max-width:400px;">
      <input type="text" placeholder="Name" style="margin-bottom:10px; padding:10px; border-radius:8px; border:1px solid #999;">
      <input type="email" placeholder="Email" style="margin-bottom:10px; padding:10px; border-radius:8px; border:1px solid #999;">
      <input type="tel" placeholder="Phone" style="margin-bottom:10px; padding:10px; border-radius:8px; border:1px solid #999;">
      <textarea placeholder="Message" rows="4" style="margin-bottom:10px; padding:10px; border-radius:8px; border:1px solid #999;"></textarea>
      <button type="submit" style="background:#2d9cdb; color:white; padding:12px; border:none; border-radius:8px; font-weight:bold;">Send Message</button>
    </form>
  </section>

  <!-- Footer -->
  <footer>
    <div>&copy; 2025 Solech. All rights reserved.</div>
    <div>
      <a href="#">LinkedIn</a>
      <a href="#">Twitter</a>
      <a href="#">GitHub</a>
    </div>
  </footer>

  <script>
    function calculateROI() {
      const installCost = parseFloat(document.getElementById('installCost').value);
      const monthlySavings = parseFloat(document.getElementById('monthlySavings').value);
      const panelCapacity = parseFloat(document.getElementById('panelCapacity').value);
      const subsidy = parseFloat(document.getElementById('subsidy').value) || 0;
      const maintenance = parseFloat(document.getElementById('maintenance').value) || 0;
      const location = document.getElementById('location').value;

      const resultDiv = document.getElementById('result');

      if (!installCost || !monthlySavings || installCost <= 0 || monthlySavings <= 0) {
        resultDiv.style.display = 'block';
        resultDiv.style.color = 'red';
        resultDiv.textContent = 'Please enter valid positive numbers for installation cost and monthly savings.';
        return;
      }

      const netCost = installCost - subsidy;
      const effectiveSavings = monthlySavings - maintenance / 12;
      const roiMonths = netCost / effectiveSavings;
      const roiYears = roiMonths / 12;

      resultDiv.style.display = 'block';
      resultDiv.style.color = 'black';
      resultDiv.innerHTML = `
        <strong>Net Installation Cost:</strong> ₹${netCost.toFixed(2)}<br>
        <strong>Effective Monthly Savings:</strong> ₹${effectiveSavings.toFixed(2)}<br>
        <strong>Estimated ROI:</strong> ${roiMonths.toFixed(1)} months (~${roiYears.toFixed(2)} years)
      `;

      const months = Array.from({ length: 60 }, (_, i) => i + 1);
      const cumulativeSavings = months.map(m => m * effectiveSavings);

      const ctx = document.getElementById('roiChart').getContext('2d');
      if (window.roiChartInstance) window.roiChartInstance.destroy();

      window.roiChartInstance = new Chart(ctx, {
        type: 'line',
        data: {
          labels: months.map(m => `Month ${m}`),
          datasets: [{
            label: 'Cumulative Savings (₹)',
            data: cumulativeSavings,
            borderColor: '#2d9cdb',
            backgroundColor: '#2d9cdb33',
            fill: true,
            tension: 0.3
          }]
        },
        options: {
          responsive: true,
          plugins: {
            title: {
              display: true,
              text: `Projected Savings over 5 Years in ${location || 'Your Location'}`
            }
          },
          scales: { y: { beginAtZero:true } }
        }
      });
    }
  </script>

</body>
</html>
