# Discipline<!DOCTYPE html>
<html>
<head>
<title>My Trading System</title>
<style>
body { font-family: Arial; background:#0d0d0d; color:#fff; padding:20px; }
.card { background:#1e1e1e; padding:15px; border-radius:10px; margin-bottom:15px; }
input, select, textarea, button { padding:8px; margin:5px; }
</style>
</head>

<body>

<h1>Trading + Life Tracker</h1>

<div class="card">
<h2>Add Trade</h2>
<input id="setup" placeholder="Setup">
<input id="reason" placeholder="Why entry">
<input id="mistake" placeholder="Mistake">

<select id="psych">
<option>Calm</option>
<option>FOMO</option>
<option>Revenge</option>
<option>Fear</option>
</select>

<select id="score">
<option value="3">3 Perfect</option>
<option value="2">2</option>
<option value="1">1</option>
<option value="0">0</option>
</select>

<select id="result">
<option value="1">+1R</option>
<option value="-1">-1R</option>
</select>

<button onclick="addTrade()">Add Trade</button>
</div>

<div class="card">
<h2>Habits</h2>
<label><input type="checkbox" id="namaz"> Namaz</label><br>
<label><input type="checkbox" id="reading"> Reading</label><br>
<label><input type="checkbox" id="discipline"> No Overtrade</label><br>
<label><input type="checkbox" id="journal"> Journal</label>
</div>

<div class="card">
<h2>Goals</h2>
<textarea id="goals"></textarea>
<button onclick="saveGoals()">Save</button>
<p id="showGoals"></p>
</div>

<div class="card">
<h2>Blueprint</h2>
<textarea id="blueprint"></textarea>
<button onclick="saveBlueprint()">Save</button>
<p id="showBlueprint"></p>
</div>

<div class="card">
<h2>Daily Journal</h2>
<textarea id="dailyNote"></textarea>
<button onclick="saveJournal()">Save</button>
<p id="showJournal"></p>
</div>

<div class="card">
<h2>Analysis</h2>
<p id="summary"></p>
<p id="level"></p>
<p id="missed"></p>
<button onclick="analyze()">Update</button>
</div>

<script>
let trades = JSON.parse(localStorage.getItem('trades')) || [];

function addTrade(){
 let trade = {
  score: parseInt(document.getElementById('score').value),
  result: parseInt(document.getElementById('result').value)
 };
 trades.push(trade);
 localStorage.setItem('trades', JSON.stringify(trades));
 alert('Saved');
}

function analyze(){
 let totalR = trades.reduce((a,b)=>a+b.result,0);
 let avg = trades.length ? (trades.reduce((a,b)=>a+b.score,0)/trades.length).toFixed(2):0;

 let level = avg<2 ? 'Weak' : avg<2.5 ? 'Improving' : 'Consistent';

 let missed = [];
 if(!document.getElementById('namaz').checked) missed.push('Namaz');
 if(!document.getElementById('reading').checked) missed.push('Reading');
 if(!document.getElementById('discipline').checked) missed.push('Discipline');
 if(!document.getElementById('journal').checked) missed.push('Journal');

 document.getElementById('summary').innerText = "Trades: "+trades.length+" | Total R: "+totalR;
 document.getElementById('level').innerText = "Level: "+level;
 document.getElementById('missed').innerText = "Missed: "+missed.join(', ');
}

function saveGoals(){
 let g = document.getElementById('goals').value;
 localStorage.setItem('goals', g);
 document.getElementById('showGoals').innerText = g;
}
document.getElementById('showGoals').innerText = localStorage.getItem('goals') || '';

function saveBlueprint(){
 let b = document.getElementById('blueprint').value;
 localStorage.setItem('blueprint', b);
 document.getElementById('showBlueprint').innerText = b;
}
document.getElementById('showBlueprint').innerText = localStorage.getItem('blueprint') || '';

function saveJournal(){
 let j = document.getElementById('dailyNote').value;
 localStorage.setItem('journal', j);
 document.getElementById('showJournal').innerText = j;
}
document.getElementById('showJournal').innerText = localStorage.getItem('journal') || '';
</script>

</body>
</html>
