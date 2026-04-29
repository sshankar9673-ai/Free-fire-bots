<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Glory Demo</title>

<style>
body{margin:0;font-family:Arial;background:#020617;color:white}
.center{display:flex;justify-content:center;align-items:center;height:100vh}
.box{background:#1e293b;padding:20px;border-radius:10px;width:250px}
input,button,select{width:100%;padding:10px;margin-top:10px;border:none;border-radius:5px}
button{background:#22c55e;color:white}
#app{display:none}

.header{padding:15px;text-align:center;background:black}
.top{display:flex;justify-content:space-around;padding:10px}
.card{background:#1e293b;padding:15px;margin:10px;border-radius:10px}
.log{background:black;height:120px;overflow:auto;padding:10px;font-size:12px}
.stat{background:#334155;padding:10px;border-radius:10px;text-align:center;width:30%}
.stats{display:flex;justify-content:space-between}
</style>
</head>

<body>

<!-- LOGIN -->
<div id="login" class="center">
  <div class="box">
    <h3>Login</h3>
    <input id="user" placeholder="Username">
    <input id="pass" placeholder="Password">
    <button onclick="login()">Login</button>
  </div>
</div>

<!-- APP -->
<div id="app">

<div class="header">🔥 Glory Dashboard</div>

<div class="top">
  <div>💰 Credits: <span id="credits">100</span></div>
  <div>👥 Users: <span id="users">120</span></div>
</div>

<div class="card">
<input id="guild" placeholder="Guild ID">

<select id="region">
<option>India</option>
<option>USA</option>
<option>Pakistan</option>
<option>Brazil</option>
</select>

<button onclick="start()">Start Boost</button>
<button onclick="buy()">Buy Credits</button>
</div>

<div class="card stats">
<div class="stat">Glory<br><span id="glory">0</span></div>
<div class="stat">Bots<br>4</div>
<div class="stat">Status<br><span id="status">Idle</span></div>
</div>

<div class="card">
<h3>Activity</h3>
<div id="log" class="log"></div>
</div>

</div>

<script>
let glory = 0;
let running = false;
let credits = 100;

const bots = ["Bot-1","Bot-2","Bot-3","Bot-4"];

function login(){
  if(user.value && pass.value){
    document.getElementById("login").style.display="none";
    document.getElementById("app").style.display="block";
  }
}

function log(msg){
  let box = document.getElementById("log");
  box.innerHTML += msg + "<br>";
  box.scrollTop = box.scrollHeight;
}

function start(){
  let guild = document.getElementById("guild").value;
  let region = document.getElementById("region").value;

  if(guild==="") return alert("Enter Guild ID");
  if(running) return;

  running=true;
  document.getElementById("status").innerText="Running";

  log("🚀 Connecting to "+region+" server...");
  log("🤖 Bots starting...");

  bots.forEach(bot=>{
    setInterval(()=>{
      let fail = Math.random();

      if(fail < 0.2){
        log("⚠️ "+bot+" retrying...");
        return;
      }

      let add = Math.floor(Math.random()*50)+10;
      glory += add;

      document.getElementById("glory").innerText = glory;
      log("🤖 "+bot+" gave +"+add+" glory");

    }, Math.random()*3000+1000);
  });

  setInterval(()=>{
    users.innerText = parseInt(users.innerText)+Math.floor(Math.random()*3);
  },5000);
}

function buy(){
  credits += 50;
  document.getElementById("credits").innerText = credits;
  alert("Credits Added (Demo)");
}
</script>

</body>
</html>
