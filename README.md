Ex.04 Design a Website for Server Side Processing
Date: 10.05.2026
AIM:
To create a web page to calculate total bill amount with GST from price and GST percentage, using server-side scripts.

FORMULA:
Bill = P + (P * GST / 100)
P --> Price (in Rupees)
GST --> GST (in Percentage)
Bill --> Total Bill Amount (in Rupees)

DESIGN STEPS:
Step 1:
Clone the repository from GitHub.

Step 2:
Create Django Admin project.

Step 3:
Create a New App under the Django Admin project.

Step 4:
Create python programs for views and urls to perform server side processing.

Step 5:
Create a HTML file to implement form based input and output.

Step 6:
Publish the website in the given URL.

PROGRAM:
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Cylinder Surface Area · K SRISARAN KARTHIK</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #05060f;
      --surface:   #0c0e1e;
      --card:      #10132a;
      --border:    rgba(99, 120, 255, 0.18);
      --glow:      #4f63ff;
      --glow2:     #00e5c0;
      --accent:    #7c8dff;
      --text:      #e8eaff;
      --muted:     #7278a8;
      --label:     #a0a8d8;
      --result-bg: rgba(0, 229, 192, 0.06);
      --result-border: rgba(0, 229, 192, 0.35);
    }

    body {
      min-height: 100vh;
      background-color: var(--bg);
      background-image:
        radial-gradient(ellipse 80% 60% at 20% 10%, rgba(79, 99, 255, 0.18) 0%, transparent 60%),
        radial-gradient(ellipse 60% 50% at 80% 80%, rgba(0, 229, 192, 0.12) 0%, transparent 60%),
        radial-gradient(ellipse 40% 40% at 60% 30%, rgba(120, 60, 200, 0.10) 0%, transparent 55%);
      font-family: 'DM Mono', monospace;
      color: var(--text);
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 40px 20px;
      overflow-x: hidden;
    }

    /* Animated grid background */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(79, 99, 255, 0.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(79, 99, 255, 0.04) 1px, transparent 1px);
      background-size: 48px 48px;
      pointer-events: none;
      z-index: 0;
    }

    .page-wrapper {
      position: relative;
      z-index: 1;
      width: 100%;
      max-width: 520px;
    }

    /* Student badge */
    .student-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(79, 99, 255, 0.12);
      border: 1px solid rgba(79, 99, 255, 0.28);
      border-radius: 999px;
      padding: 6px 16px 6px 10px;
      font-size: 11px;
      letter-spacing: 0.08em;
      color: var(--accent);
      text-transform: uppercase;
      font-weight: 500;
      margin-bottom: 28px;
      animation: fadeSlideDown 0.6s ease both;
    }
    .student-badge::before {
      content: '';
      width: 7px; height: 7px;
      border-radius: 50%;
      background: var(--glow);
      box-shadow: 0 0 8px var(--glow);
      animation: pulse 2s ease-in-out infinite;
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.4; }
    }

    /* Main card */
    .card {
      background: var(--card);
      border: 1px solid var(--border);
      border-radius: 24px;
      padding: 44px 40px 40px;
      position: relative;
      overflow: hidden;
      animation: fadeSlideDown 0.7s ease 0.1s both;
      box-shadow:
        0 0 0 1px rgba(79, 99, 255, 0.06),
        0 20px 60px rgba(0, 0, 0, 0.5),
        0 0 80px rgba(79, 99, 255, 0.06);
    }

    /* Decorative top shine */
    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 15%; right: 15%;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(99, 120, 255, 0.6), transparent);
    }

    /* Cylinder illustration */
    .cylinder-icon {
      display: flex;
      justify-content: center;
      margin-bottom: 28px;
    }
    .cylinder-icon svg {
      filter: drop-shadow(0 0 16px rgba(79, 99, 255, 0.5));
      animation: floatY 4s ease-in-out infinite;
    }
    @keyframes floatY {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-6px); }
    }

    /* Title */
    h1 {
      font-family: 'Syne', sans-serif;
      font-weight: 800;
      font-size: 26px;
      letter-spacing: -0.02em;
      text-align: center;
      color: var(--text);
      line-height: 1.2;
      margin-bottom: 6px;
    }
    h1 span {
      background: linear-gradient(135deg, var(--glow), var(--glow2));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }
    .subtitle {
      text-align: center;
      font-size: 12px;
      color: var(--muted);
      letter-spacing: 0.06em;
      text-transform: uppercase;
      margin-bottom: 36px;
    }

    /* Formula chip */
    .formula-chip {
      background: rgba(79, 99, 255, 0.08);
      border: 1px solid rgba(79, 99, 255, 0.2);
      border-radius: 10px;
      padding: 12px 18px;
      text-align: center;
      font-size: 13px;
      color: var(--muted);
      margin-bottom: 32px;
      letter-spacing: 0.02em;
    }
    .formula-chip code {
      color: var(--accent);
      font-size: 14px;
      font-weight: 500;
    }

    /* Field group */
    .field-group {
      display: flex;
      flex-direction: column;
      gap: 18px;
      margin-bottom: 28px;
    }
    .field {
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
    .field label {
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--label);
      font-weight: 500;
    }
    .input-row {
      display: flex;
      align-items: center;
      gap: 0;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      transition: border-color 0.2s, box-shadow 0.2s;
      overflow: hidden;
    }
    .input-row:focus-within {
      border-color: rgba(99, 120, 255, 0.55);
      box-shadow: 0 0 0 3px rgba(79, 99, 255, 0.12);
    }
    .input-icon {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 44px;
      height: 52px;
      color: var(--muted);
      flex-shrink: 0;
      border-right: 1px solid var(--border);
    }
    .input-row input[type="text"] {
      flex: 1;
      background: transparent;
      border: none;
      outline: none;
      padding: 0 16px;
      height: 52px;
      font-family: 'DM Mono', monospace;
      font-size: 17px;
      color: var(--text);
      letter-spacing: 0.02em;
    }
    .input-row input[type="text"]::placeholder {
      color: var(--muted);
    }
    .unit-tag {
      font-size: 12px;
      color: var(--muted);
      padding: 0 14px;
      letter-spacing: 0.04em;
      border-left: 1px solid var(--border);
      height: 52px;
      display: flex;
      align-items: center;
      flex-shrink: 0;
    }

    /* Submit button */
    .btn-calculate {
      width: 100%;
      height: 54px;
      border: none;
      border-radius: 14px;
      background: linear-gradient(135deg, var(--glow) 0%, #6a40ff 50%, var(--glow) 100%);
      background-size: 200% 100%;
      color: #fff;
      font-family: 'Syne', sans-serif;
      font-size: 15px;
      font-weight: 700;
      letter-spacing: 0.06em;
      text-transform: uppercase;
      cursor: pointer;
      transition: background-position 0.4s, transform 0.15s, box-shadow 0.2s;
      box-shadow: 0 4px 24px rgba(79, 99, 255, 0.38);
      margin-bottom: 28px;
      position: relative;
      overflow: hidden;
    }
    .btn-calculate::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(180deg, rgba(255,255,255,0.12) 0%, transparent 60%);
      pointer-events: none;
    }
    .btn-calculate:hover {
      background-position: 100% 0;
      transform: translateY(-2px);
      box-shadow: 0 8px 32px rgba(79, 99, 255, 0.5);
    }
    .btn-calculate:active {
      transform: translateY(0);
    }

    /* Result box */
    .result-box {
      background: var(--result-bg);
      border: 1px solid var(--result-border);
      border-radius: 16px;
      padding: 20px 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }
    .result-label {
      font-size: 11px;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--glow2);
      font-weight: 500;
      margin-bottom: 4px;
    }
    .result-value {
      font-family: 'Syne', sans-serif;
      font-size: 30px;
      font-weight: 800;
      color: var(--text);
      letter-spacing: -0.02em;
    }
    .result-value sup {
      font-size: 14px;
      font-weight: 600;
      color: var(--glow2);
    }
    .result-icon {
      width: 52px; height: 52px;
      border-radius: 14px;
      background: rgba(0, 229, 192, 0.1);
      border: 1px solid rgba(0, 229, 192, 0.2);
      display: flex;
      align-items: center;
      justify-content: center;
      flex-shrink: 0;
    }

    /* Result pop animation */
    @keyframes resultPop {
      0%   { opacity: 0; transform: scale(0.95) translateY(8px); }
      100% { opacity: 1; transform: scale(1) translateY(0); }
    }
    .result-box.show {
      animation: resultPop 0.35s cubic-bezier(0.34, 1.56, 0.64, 1) both;
    }
    .result-box { display: none; }

    /* Animations */
    @keyframes fadeSlideDown {
      from { opacity: 0; transform: translateY(-16px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* Scrollbar */
    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }
  </style>
</head>
<body>

<div class="page-wrapper">

  <div class="student-badge">Shaik Sophie fatima</div>

  <div class="card">

    <!-- Floating cylinder SVG -->
    <div class="cylinder-icon">
      <svg width="72" height="80" viewBox="0 0 72 80" fill="none" xmlns="http://www.w3.org/2000/svg">
        <ellipse cx="36" cy="14" rx="28" ry="10" fill="url(#topFill)" stroke="url(#topStroke)" stroke-width="1.5"/>
        <path d="M8 14 Q8 66 36 66 Q64 66 64 14" fill="url(#bodyFill)" stroke="url(#bodyStroke)" stroke-width="1.5"/>
        <ellipse cx="36" cy="66" rx="28" ry="10" fill="url(#botFill)" stroke="url(#botStroke)" stroke-width="1.5"/>
        <defs>
          <linearGradient id="topFill" x1="8" y1="14" x2="64" y2="14" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#4f63ff" stop-opacity="0.8"/>
            <stop offset="100%" stop-color="#00e5c0" stop-opacity="0.8"/>
          </linearGradient>
          <linearGradient id="topStroke" x1="8" y1="14" x2="64" y2="14" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#7c8dff"/>
            <stop offset="100%" stop-color="#00e5c0"/>
          </linearGradient>
          <linearGradient id="bodyFill" x1="36" y1="14" x2="36" y2="66" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#4f63ff" stop-opacity="0.25"/>
            <stop offset="100%" stop-color="#00e5c0" stop-opacity="0.15"/>
          </linearGradient>
          <linearGradient id="bodyStroke" x1="8" y1="40" x2="64" y2="40" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#4f63ff" stop-opacity="0.5"/>
            <stop offset="100%" stop-color="#00e5c0" stop-opacity="0.5"/>
          </linearGradient>
          <linearGradient id="botFill" x1="8" y1="66" x2="64" y2="66" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#4f63ff" stop-opacity="0.5"/>
            <stop offset="100%" stop-color="#00e5c0" stop-opacity="0.5"/>
          </linearGradient>
          <linearGradient id="botStroke" x1="8" y1="66" x2="64" y2="66" gradientUnits="userSpaceOnUse">
            <stop offset="0%" stop-color="#7c8dff"/>
            <stop offset="100%" stop-color="#00e5c0"/>
          </linearGradient>
        </defs>
      </svg>
    </div>

    <h1>Surface Area of a <span>Right Cylinder</span></h1>
    <p class="subtitle">Geometry Calculator · Mathematics</p>

    <div class="formula-chip">
      <code>A = 2πr(h + r)</code>
    </div>

    <form id="calcForm" onsubmit="calculate(event)">

      <div class="field-group">

        <div class="field">
          <label>Radius</label>
          <div class="input-row">
            <div class="input-icon">
              <svg width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="9"/><line x1="12" y1="12" x2="21" y2="12"/>
              </svg>
            </div>
            <input type="text" id="radius" placeholder="Enter radius" autocomplete="off">
            <span class="unit-tag">m</span>
          </div>
        </div>

        <div class="field">
          <label>Height</label>
          <div class="input-row">
            <div class="input-icon">
              <svg width="16" height="16" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <line x1="12" y1="2" x2="12" y2="22"/><polyline points="7 7 12 2 17 7"/><polyline points="7 17 12 22 17 17"/>
              </svg>
            </div>
            <input type="text" id="height" placeholder="Enter height" autocomplete="off">
            <span class="unit-tag">m</span>
          </div>
        </div>

      </div>

      <button type="submit" class="btn-calculate">Calculate Surface Area</button>

      <div class="result-box" id="resultBox">
        <div>
          <div class="result-label">Total Surface Area</div>
          <div class="result-value" id="resultValue">— <sup>m²</sup></div>
        </div>
        <div class="result-icon">
          <svg width="24" height="24" fill="none" viewBox="0 0 24 24" stroke="#00e5c0" stroke-width="2">
            <polyline points="22 7 13.5 15.5 8.5 10.5 2 17"/>
            <polyline points="16 7 22 7 22 13"/>
          </svg>
        </div>
      </div>

    </form>

    <script>
      function calculate(e) {
        e.preventDefault();
        const r = parseFloat(document.getElementById('radius').value);
        const h = parseFloat(document.getElementById('height').value);
        if (isNaN(r) || isNaN(h) || r <= 0 || h <= 0) {
          document.getElementById('resultValue').innerHTML = 'Invalid input <sup>m²</sup>';
          document.getElementById('resultBox').style.display = 'flex';
          document.getElementById('resultBox').classList.remove('show');
          void document.getElementById('resultBox').offsetWidth;
          document.getElementById('resultBox').classList.add('show');
          return;
        }
        const area = (2 * Math.PI * r * (h + r)).toFixed(4);
        document.getElementById('resultValue').innerHTML = area + ' <sup>m²</sup>';
        const box = document.getElementById('resultBox');
        box.style.display = 'flex';
        box.classList.remove('show');
        void box.offsetWidth; // force reflow for re-animation
        box.classList.add('show');
      }
    </script>

  </div>
</div>

</body>
</html>
OUTPUT - SERVER SIDE:
alt text alt text

OUTPUT - WEBPAGE:
alt text alt text alt text alt text

RESULT:
The a web page to calculate vehicle mileage and fuel efficiency using server-side scripts is created successfully.
