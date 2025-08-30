




































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


































     <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Solech — Solar ROI Calculator</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<style>
  :root{
    --primary:#2d9cdb; --secondary:#0ea5a4; --bg:#f6fbff; --text:#0f172a; --muted:#64748b;
    --card:#ffffff; --shadow:0 10px 28px rgba(2,8,23,.10); --r:18px;
  }
  *{box-sizing:border-box}
  html,body{margin:0;background:var(--bg);color:var(--text);font-family:'Inter',system-ui,Segoe UI,Roboto,Arial,sans-serif}
  a{color:inherit;text-decoration:none}
  header{position:sticky;top:0;z-index:10;background:linear-gradient(90deg,var(--primary),#1d7fb8);color:#fff;box-shadow:var(--shadow)}
  .nav{max-width:1100px;margin:0 auto;padding:14px 18px;display:flex;align-items:center;justify-content:space-between}
  .brand{display:flex;gap:10px;align-items:center}
  .logo{width:36px;height:36px;border-radius:10px;background:linear-gradient(135deg,var(--secondary),#4bd7c7)}
  .menu{display:flex;gap:18px;align-items:center}
  .cta{background:#fff;color:#0b4e74;padding:8px 14px;border-radius:10px;font-weight:700}
  .hero{max-width:1100px;margin:0 auto;padding:56px 18px 24px;display:grid;grid-template-columns:1.1fr .9fr;gap:22px;align-items:center}
  .hero h1{margin:0 0 10px;font-size:clamp(2rem,4vw,3rem);line-height:1.1}
  .hero p{margin:0 0 14px;color:var(--muted)}
  .btn{display:inline-flex;align-items:center;gap:10px;background:var(--primary);color:#fff;padding:12px 16px;border-radius:12px;font-weight:700}
  .btn.alt{background:var(--secondary)}
  .card{background:var(--card);border-radius:var(--r);box-shadow:var(--shadow);padding:18px}
  .section{max-width:1100px;margin:0 auto;padding:26px 18px 40px}
  .lead{color:var(--muted);margin:6px 0 18px}
  .calculator{display:grid;grid-template-columns:1fr 1fr;gap:18px}
  label{font-size:.9rem;font-weight:600}
  input{width:100%;margin-top:6px;padding:10px 12px;border:1px solid #e2e8f0;border-radius:12px;background:#fbfdff}
  .row{display:grid;grid-template-columns:1fr 1fr;gap:14px}
  .stats{display:grid;gap:8px;margin-top:10px}
  .stat{display:flex;justify-content:space-between;gap:12px;background:#f2f8ff;border:1px solid #dceafe;border-radius:12px;padding:10px 12px}
  canvas{max-width:100%}
  footer{background:#0b1220;color:#cbd5e1;margin-top:40px}
  .foot{max-width:1100px;margin:0 auto;padding:18px;display:flex;flex-wrap:wrap;gap:10px;justify-content:space-between}
  @media (max-width:980px){.hero{grid-template-columns:1fr}.calculator{grid-template-columns:1fr}.row{grid-template-columns:1fr}}
  @media (max-width:560px){.menu{display:none}}
</style>
</head>
<body>
<header>
  <div class="nav">
    <div class="brand"><div class="logo" aria-hidden="true"></div><strong>Solech</strong></div>
    <nav class="menu">
      <a href="#calculator">ROI Calculator</a>
      <a href="#contact">Contact</a>
      <a class="cta" href="#contact">Get a Quote</a>
    </nav>
  </div>
</header>

<section class="hero">
  <div>
    <h1>Affordable Solar Solutions, <span style="color:#bfe7ff">Powered by AI</span></h1>
    <p>Estimate your payback time and see cumulative savings with a single click.</p>
    <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:8px">
      <a class="btn" href="#calculator">Try the Calculator</a>
      <a class="btn alt" href="#contact">Talk to Us</a>
    </div>
  </div>
  <div class="card" role="img" aria-label="Illustration">
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;align-items:center">
      <div style="background:linear-gradient(135deg,#0ea5a4,#5fe0cb);height:120px;border-radius:14px"></div>
      <div style="background:linear-gradient(135deg,#2d9cdb,#9ed6f3);height:160px;border-radius:14px"></div>
      <div style="background:linear-gradient(135deg,#fcd34d,#f59e0b);height:80px;border-radius:14px"></div>
      <div style="background:linear-gradient(135deg,#a78bfa,#60a5fa);height:110px;border-radius:14px"></div>
    </div>
  </div>
</section>

<section id="calculator" class="section">
  <h2>Solar ROI Calculator</h2>
  <p class="lead">Enter your numbers to estimate payback and visualize savings vs. your net installation cost.</p>

  <div class="calculator">
    <!-- Inputs -->
    <div class="card">
      <h3 style="margin:0 0 12px;color:#1d7fb8">Inputs</h3>
      <div class="row">
        <div>
          <label for="install">Installation Cost (₹)</label>
          <input id="install" type="number" min="0" placeholder="120000">
        </div>
        <div>
          <label for="subsidy">Government Subsidy (₹)</label>
          <input id="subsidy" type="number" min="0" placeholder="20000">
        </div>
        <div>
          <label for="monthly">Monthly Savings (₹)</label>
          <input id="monthly" type="number" min="0" placeholder="3000">
        </div>
        <div>
          <label for="maint">Annual Maintenance (₹)</label>
          <input id="maint" type="number" min="0" placeholder="1500">
        </div>
        <div>
          <label for="months">Projection Horizon (months)</label>
          <input id="months" type="number" min="12" max="360" value="60">
        </div>
        <div>
          <label for="location">Location (optional)</label>
          <input id="location" type="text" placeholder="Bengaluru, India">
        </div>
      </div>
      <div style="display:flex;gap:10px;margin-top:14px">
        <button id="calcBtn" class="btn" type="button">Calculate</button>
        <button id="resetBtn" class="btn alt" type="button">Reset</button>
      </div>
    </div>

    <!-- Results -->
    <div class="card">
      <h3 style="margin:0 0 12px;color:#1d7fb8">Results</h3>
      <div class="stats" aria-live="polite">
        <div class="stat"><span>Net Installation Cost</span><span id="netCost">—</span></div>
        <div class="stat"><span>Effective Monthly Savings</span><span id="effMonthly">—</span></div>
        <div class="stat"><span>Estimated Payback</span><span id="payback">—</span></div>
      </div>
      <div style="height:260px;margin-top:12px">
        <canvas id="roiChart" role="img" aria-label="Cumulative savings vs net cost"></canvas>
      </div>
      <p id="caption" class="lead" style="margin-top:8px">Cumulative savings (blue) vs. dashed net-cost line.</p>
    </div>
  </div>
</section>

<section id="contact" class="section">
  <h2>Contact Us</h2>
  <p class="lead">Have a project in mind? Get a free assessment.</p>
  <div class="card">
    <form onsubmit="event.preventDefault(); alert('Thanks! We will contact you soon.'); this.reset();">
      <div class="row">
        <div><label>Name</label><input type="text" required placeholder="Your name"></div>
        <div><label>Email</label><input type="email" required placeholder="you@example.com"></div>
      </div>
      <label>Phone</label><input type="tel" placeholder="+91 98765 43210">
      <label>Message</label><input type="text" placeholder="Tell us your goals / power usage">
      <div style="margin-top:10px"><button class="btn" type="submit">Send Message</button></div>
    </form>
  </div>
</section>

<footer>
  <div class="foot">
    <div>© <span id="year"></span> Solech. All rights reserved.</div>
    <div style="opacity:.8">Affordable Solar • AI-Optimized</div>
  </div>
</footer>

<script>
  const $ = id => document.getElementById(id);
  const INR = n => new Intl.NumberFormat('en-IN',{style:'currency',currency:'INR',maximumFractionDigits:0}).format(n||0);

  let chart;

  function calculate(){
    const install = parseFloat($('install').value)||0;
    const subsidy = parseFloat($('subsidy').value)||0;
    const monthly = parseFloat($('monthly').value)||0;
    const maint   = parseFloat($('maint').value)||0; // yearly
    const horizon = Math.min(Math.max(parseInt($('months').value)||60,12),360);

    if(install<=0 || monthly<=0){ alert('Enter positive values for Installation Cost and Monthly Savings.'); return; }

    const netCost    = Math.max(install - subsidy, 0);
    const effMonthly = monthly - (maint/12);

    $('netCost').textContent    = INR(netCost);
    $('effMonthly').textContent = effMonthly>0 ? INR(effMonthly) : '—';

    let paybackM = Infinity;
    if(effMonthly>0){
      paybackM = netCost / effMonthly;
      $('payback').textContent = `${paybackM.toFixed(1)} months (~${(paybackM/12).toFixed(2)} years)`;
    }else{
      $('payback').textContent = 'Not achievable (negative/zero savings)';
    }

    // Build series
    const labels = Array.from({length:horizon}, (_,i)=>`M${i+1}`);
    const savings = [];
    let acc=0;
    for(let i=0;i<horizon;i++){ acc += effMonthly; savings.push(acc); }

    // Make/replace chart
    const ctx = $('roiChart').getContext('2d');
    if(chart) chart.destroy();
    chart = new Chart(ctx,{
      type:'line',
      data:{
        labels,
        datasets:[
          { label:'Cumulative Savings (₹)', data:savings, tension:.25, fill:true,
            backgroundColor:'rgba(45,156,219,.18)', borderColor:'rgba(45,156,219,1)', borderWidth:2, pointRadius:0 },
          { label:'Net Cost Threshold (₹)', data:Array(horizon).fill(netCost),
            borderDash:[6,6], borderColor:'rgba(15,23,42,.45)', borderWidth:1, pointRadius:0 }
        ]
      },
      options:{
        responsive:true, maintainAspectRatio:false,
        interaction:{mode:'index',intersect:false},
        scales:{
          y:{beginAtZero:true, ticks:{callback:v=>new Intl.NumberFormat('en-IN').format(v)}},
          x:{ticks:{autoSkip:true,maxRotation:0}}
        },
        plugins:{
          legend:{display:true},
          title:{display:true, text:`Savings Projection (${horizon} months${$('location').value? ' – '+$('location').value:''})`}
        }
      }
    });

    $('caption').textContent = 'Break-even occurs where the blue savings curve crosses the dashed net-cost line.';
  }

  $('calcBtn').addEventListener('click', calculate);
  $('resetBtn').addEventListener('click', ()=>{
    document.querySelectorAll('input').forEach(i=>{ if(i.type!=='button') i.value=''; });
    $('months').value=60; $('netCost').textContent='—'; $('effMonthly').textContent='—'; $('payback').textContent='—';
    if(chart) chart.destroy();
    $('caption').textContent = 'Cumulative savings (blue) vs. dashed net-cost line.';
  });

  $('year').textContent = new Date().getFullYear();
</script>
</body>
</html>










import express from "express";
import cors from "cors";
import dotenv from "dotenv";
import Groq from "groq-sdk";

dotenv.config();

const app = express();
const port = process.env.PORT || 3000;

app.use(cors());
app.use(express.json());

const groq = new Groq({ apiKey: process.env.GROQ_API_KEY });

app.post("/chat", async (req, res) => {
  try {
    const userMessage = req.body.message || "Hello from user!";

    const completion = await groq.chat.completions.create({
      model: "llama-3.1-8b-instant",
      messages: [{ role: "user", content: userMessage }],
    });

    const reply = completion.choices[0].message.content;
    res.json({ reply });
  } catch (error) {
    console.error("Groq API error:", error);
    res.status(500).json({ reply: "⚠️ Error connecting to AI provider." });
  }
});

app.listen(port, () => {
  console.log(`✅ Backend running at http://localhost:${port}`);
});











{
  "name": "chatbot-backend",
  "version": "1.0.0",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^17.2.1",
    "express": "^5.1.0",
    "groq-sdk": "^0.30.0"
  }
}
