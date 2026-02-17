# G6-Intake
4ID G6 Service Request Portal
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>4ID G6 Service Request</title>
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(135deg, #0f0f0f, #1a1a1a);
      color: white;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    .card {
      background: #1f1f1f;
      width: 420px;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 20px rgba(0, 128, 0, 0.4);
      border: 1px solid #2e5e2e;
    }

    h2 {
      text-align: center;
      color: #4CAF50;
      margin-bottom: 20px;
    }

    input, select {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border-radius: 6px;
      border: none;
      background: #2c2c2c;
      color: white;
    }

    button {
      width: 100%;
      padding: 12px;
      margin-top: 15px;
      border: none;
      border-radius: 6px;
      background: #4CAF50;
      color: black;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #66ff66;
    }

    .hidden {
      display: none;
    }

    .footer {
      text-align: center;
      font-size: 12px;
      margin-top: 15px;
      color: #777;
    }
  </style>
</head>
<body>

<div class="card">

  <!-- SCREEN 1 -->
  <div id="screen1">
    <h2>4ID G6 Service Request</h2>
    <input id="rank" placeholder="Rank">
    <input id="firstName" placeholder="First Name">
    <input id="lastName" placeholder="Last Name">
    <button onclick="next(2)">Next</button>
  </div>

  <!-- SCREEN 2 -->
  <div id="screen2" class="hidden">
    <h2>Select Network</h2>
    <select id="network">
      <option value="">Choose Network</option>
      <option value="NIPR">NIPR</option>
      <option value="SIPR">SIPR</option>
    </select>
    <button onclick="next(3)">Next</button>
  </div>

  <!-- SCREEN 3 -->
  <div id="screen3" class="hidden">
    <h2>Request Type</h2>
    <select id="requestType"></select>
    <button onclick="submitTicket()">Submit</button>
  </div>

  <div class="footer">
    4th Infantry Division • Fort Carson
  </div>

</div>

<script>

function next(screen) {
  document.getElementById("screen1").classList.add("hidden");
  document.getElementById("screen2").classList.add("hidden");
  document.getElementById("screen3").classList.add("hidden");

  document.getElementById("screen" + screen).classList.remove("hidden");

  if (screen === 3) {
    loadRequests();
  }
}

function loadRequests() {
  const network = document.getElementById("network").value;
  const requestSelect = document.getElementById("requestType");
  requestSelect.innerHTML = "";

  let options = [];

  if (network === "NIPR") {
    options = [
      "New Account",
      "Office 365 Entitlements",
      "Laptop Turn-In",
      "Printer Access",
      "Share Drive Access",
      "Account Reset"
    ];
  }

  if (network === "SIPR") {
    options = [
      "SIPR Account Creation",
      "SIPR Entitlements",
      "Token Issue",
      "Account Unlock"
    ];
  }

  options.forEach(option => {
    let opt = document.createElement("option");
    opt.value = option;
    opt.text = option;
    requestSelect.appendChild(opt);
  });
}

async function submitTicket() {

  const data = {
    rank: document.getElementById("rank").value,
    firstName: document.getElementById("firstName").value,
    lastName: document.getElementById("lastName").value,
    network: document.getElementById("network").value,
    requestType: document.getElementById("requestType").value
  };

  await fetch("PASTE_POWER_AUTOMATE_URL_HERE", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data)
  });

  alert("Ticket Submitted Successfully");
  location.reload();
}

</script>

</body>
</html>