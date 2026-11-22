
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#101510">
<title>PH | Projeto Evolução</title>
<style>
:root {
  --bg:#101510;
  --card:#1b241d;
  --green:#a5e65b;
  --white:#f5f7f2;
  --muted:#9ca99b;
  --border:#303c30;
}
*{box-sizing:border-box}
body{
  margin:0;background:var(--bg);color:var(--white);
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
}
header{padding:26px 20px 16px}
.brand{color:var(--green);font-size:13px;font-weight:800;letter-spacing:2px}
h1{font-size:27px;margin:8px 0}
.subtitle{color:var(--muted);font-size:13px}
main{padding:0 16px 105px;max-width:650px;margin:auto}
h2{font-size:19px;margin:23px 0 13px}
h3{font-size:15px;margin:0 0 12px}
.card{
  background:var(--card);border:1px solid var(--border);
  border-radius:17px;padding:17px;margin-bottom:13px;
}
.hero{background:linear-gradient(135deg,#263b20,#172318)}
.hero strong{font-size:34px;color:var(--green)}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:11px}
.metric{background:var(--card);padding:15px;border-radius:15px;border:1px solid var(--border)}
.metric strong{display:block;font-size:23px;margin-top:8px}
.muted{color:var(--muted);font-size:12px}
input,select,textarea{
  width:100%;padding:13px;margin:7px 0 12px;
  border-radius:10px;border:1px solid var(--border);
  background:#101810;color:white;font-size:15px;
}
button{
  background:var(--green);color:#15200e;border:0;
  padding:13px 17px;border-radius:11px;font-weight:800;
  font-size:14px;cursor:pointer;
}
button.secondary{background:#303d31;color:white}
button.danger{background:#542e2e;color:white}
label{font-size:12px;color:var(--muted)}
.progress{height:9px;background:#303b30;border-radius:20px;overflow:hidden;margin:12px 0}
.progress div{height:100%;background:var(--green);width:0%;border-radius:20px}
nav{
  position:fixed;bottom:0;left:0;right:0;
  background:#172018;border-top:1px solid var(--border);
  display:flex;justify-content:space-around;padding:12px 3px;
  padding-bottom:max(12px,env(safe-area-inset-bottom));
  z-index:5;
}
nav button{background:transparent;color:var(--muted);padding:8px 4px;font-size:11px}
nav button.active{color:var(--green)}
section{display:none}
section.active{display:block}
.record{padding:12px 0;border-bottom:1px solid var(--border)}
.record:last-child{border:0}
.record strong{font-size:14px}
.record small{display:block;color:var(--muted);margin-top:5px}
canvas{width:100%;height:180px}
.tag{color:var(--green);font-size:11px;font-weight:bold}
.empty{color:var(--muted);font-size:13px;padding:12px 0}
</style>
</head>
<body>

<header>
  <div class="brand">PH | PROJETO EVOLUÇÃO</div>
  <h1>Minha evolução. Minha história.</h1>
  <div class="subtitle" id="today"></div>
</header>

<main>

<section id="home" class="active">
  <div class="card hero">
    <div class="tag">MINHA META</div>
    <h2>Construindo um físico forte.</h2>
    <strong id="homeWeight">100 kg</strong>
    <p class="muted">Meta: 95 kg · Evolução diária</p>
    <div class="progress"><div id="mainProgress"></div></div>
    <span class="muted" id="progressText"></span>
  </div>

  <h2>Resumo de hoje</h2>
  <div class="grid">
    <div class="metric">
      <span class="muted">Peso atual</span>
      <strong id="metricWeight">100 kg</strong>
    </div>
    <div class="metric">
      <span class="muted">Água consumida</span>
      <strong id="metricWater">0 ml</strong>
    </div>
    <div class="metric">
      <span class="muted">Calorias</span>
      <strong id="metricCalories">0</strong>
    </div>
    <div class="metric">
      <span class="muted">Treinos</span>
      <strong id="metricWorkouts">0</strong>
    </div>
  </div>

  <h2>Acompanhamento diário</h2>
  <div class="card">
    <h3>Hidratação</h3>
    <div class="progress"><div id="waterProgress"></div></div>
    <p class="muted" id="waterText">0 de 3500 ml</p>
    <button onclick="addWater(250)">+ 250 ml</button>
    <button class="secondary" onclick="addWater(500)">+ 500 ml</button>
  </div>
</section>

<section id="weight">
  <h2>⚖️ Evolução do peso</h2>
  <div class="card">
    <label>Registrar peso (kg)</label>
    <input id="weightInput" type="number" step="0.1" placeholder="Ex.: 100.5">
    <label>Data da pesagem</label>
    <input id="weightDate" type="date">
    <button onclick="saveWeight()">Salvar pesagem</button>
  </div>
  <div class="card">
    <h3>Histórico de peso</h3>
    <canvas id="weightChart"></canvas>
    <div id="weightHistory"></div>
  </div>
</section>

<section id="training">
  <h2>🏋️ Treinos e corrida</h2>
  <div class="card">
    <label>Tipo de atividade</label>
    <select id="activityType">
      <option>Musculação</option>
      <option>Corrida</option>
      <option>Caminhada</option>
      <option>Bicicleta</option>
      <option>Cardio</option>
    </select>
    <label>Treino / descrição</label>
    <input id="activityName" placeholder="Ex.: Treino de peito">
    <label>Duração (minutos)</label>
    <input id="activityDuration" type="number" placeholder="60">
    <label>Distância (km), se aplicável</label>
    <input id="activityDistance" type="number" step="0.1" placeholder="5">
    <label>Data</label>
    <input id="activityDate" type="date">
    <button onclick="saveActivity()">Registrar atividade</button>
  </div>
  <div class="card">
    <h3>Histórico de atividades</h3>
    <div id="activityHistory"></div>
  </div>
</section>

<section id="nutrition">
  <h2>🥗 Alimentação</h2>
  <div class="card">
    <label>Refeição</label>
    <select id="mealType">
      <option>Café da manhã</option>
      <option>Almoço</option>
      <option>Lanche</option>
      <option>Jantar</option>
      <option>Ceia</option>
    </select>
    <label>Alimentos</label>
    <input id="mealName" placeholder="Ex.: Frango, arroz e salada">
    <label>Calorias estimadas (kcal)</label>
    <input id="mealCalories" type="number" placeholder="500">
    <label>Data</label>
    <input id="mealDate" type="date">
    <button onclick="saveMeal()">Registrar refeição</button>
  </div>
  <div class="card">
    <h3>Calorias do dia</h3>
    <strong id="calorieTotal" style="font-size:28px;color:var(--green)">0 kcal</strong>
    <p class="muted">Soma das refeições registradas hoje.</p>
    <div id="mealHistory"></div>
  </div>
</section>

<section id="measurements">
  <h2>📏 Medidas corporais</h2>
  <div class="card">
    <label>Data</label>
    <input id="measureDate" type="date">
    <label>Peito (cm)</label>
    <input id="chest" type="number" step="0.1">
    <label>Cintura (cm)</label>
    <input id="waist" type="number" step="0.1">
    <label>Abdômen (cm)</label>
    <input id="abdomen" type="number" step="0.1">
    <label>Braço (cm)</label>
    <input id="arm" type="number" step="0.1">
    <label>Coxa (cm)</label>
    <input id="thigh" type="number" step="0.1">
    <button onclick="saveMeasurements()">Salvar medidas</button>
  </div>
  <div class="card">
    <h3>Histórico de medidas</h3>
    <div id="measureHistory"></div>
  </div>
</section>

<section id="settings">
  <h2>⚙️ Configurações</h2>
  <div class="card">
    <label>Meta de peso (kg)</label>
    <input id="goalInput" type="number" step="0.1" value="95">
    <label>Meta diária de água (ml)</label>
    <input id="waterGoalInput" type="number" value="3500">
    <button onclick="saveSettings()">Salvar configurações</button>
  </div>
  <div class="card">
    <h3>Seus dados</h3>
    <p class="muted">Os registros ficam salvos neste navegador.</p>
    <button class="secondary" onclick="exportData()">Exportar meus dados</button>
    <p></p>
    <button class="danger" onclick="clearData()">Apagar todos os dados</button>
  </div>
  <p class="muted">PH | Projeto Evolução · Versão 1.0</p>
</section>

</main>

<nav>
  <button class="active" onclick="showTab('home',this)">⌂<br>Início</button>
  <button onclick="showTab('weight',this)">⚖<br>Peso</button>
  <button onclick="showTab('training',this)">🏋<br>Treino</button>
  <button onclick="showTab('nutrition',this)">🥗<br>Dieta</button>
  <button onclick="showTab('measurements',this)">📏<br>Medidas</button>
  <button onclick="showTab('settings',this)">⚙<br>Mais</button>
</nav>

<script>
const KEY="phProjetoEvolucaoV1";
let db=JSON.parse(localStorage.getItem(KEY)||"{}");
db.weights ||= [];
db.activities ||= [];
db.meals ||= [];
db.measurements ||= [];
db.water ||= {};
db.settings ||= {goal:95,waterGoal:3500};

const today=()=>new Date().toLocaleDateString("en-CA");
const el=id=>document.getElementById(id);
const num=id=>Number(el(id).value);
const fmt=n=>Number(n).toLocaleString("pt-BR");
function save(){localStorage.setItem(KEY,JSON.stringify(db));render();}
function showTab(id,btn){
 document.querySelectorAll("main section").forEach(s=>s.classList.remove("active"));
 el(id).classList.add("active");
 document.querySelectorAll("nav button").forEach(b=>b.classList.remove("active"));
 btn.classList.add("active");
 render();
}
function latestWeight(){
 return db.weights.length ? [...db.weights].sort((a,b)=>b.date.localeCompare(a.date))[0].value : 100;
}
function addWater(amount){
 const d=today();
 db.water[d]=(db.water[d]||0)+amount;
 save();
}
function saveWeight(){
 const value=num("weightInput");
 if(!value||value<20||value>400)return alert("Digite um peso válido.");
 db.weights.push({value,date:el("weightDate").value||today()});
 save();el("weightInput").value="";
}
function saveActivity(){
 const name=el("activityName").value.trim();
 if(!name)return alert("Informe o nome da atividade.");
 db.activities.push({
 type:el("activityType").value,name,
 duration:num("activityDuration"),
 distance:num("activityDistance"),
 date:el("activityDate").value||today()
 });
 save();el("activityName").value="";
 el("activityDuration").value="";
 el("activityDistance").value="";
}
function saveMeal(){
 const name=el("mealName").value.trim();
 const calories=num("mealCalories");
 if(!name||calories<0)return alert("Preencha a refeição e as calorias.");
 db.meals.push({type:el("mealType").value,name,calories,date:el("mealDate").value||today()});
 save();el("mealName").value="";el("mealCalories").value="";
}
function saveMeasurements(){
 const fields=["chest","waist","abdomen","arm","thigh"];
 const values={};
 fields.forEach(f=>values[f]=num(f)||null);
 if(!fields.some(f=>values[f]))return alert("Preencha pelo menos uma medida.");
 db.measurements.push({date:el("measureDate").value||today(),...values});
 save();
 fields.forEach(f=>el(f).value="");
}
function saveSettings(){
 db.settings.goal=num("goalInput")||95;
 db.settings.waterGoal=num("waterGoalInput")||3500;
 save();alert("Configurações salvas!");
}
function list(items,format){
 return items.length ? [...items].sort((a,b)=>b.date.localeCompare(a.date)).map(format).join("") : '<div class="empty">Nenhum registro ainda.</div>';
}
function render(){
 const w=latestWeight(),goal=db.settings.goal;
 const water=db.water[today()]||0;
 const calories=db.meals.filter(x=>x.date===today()).reduce((s,x)=>s+x.calories,0);
 const workouts=db.activities.filter(x=>x.date===today()).length;
 el("homeWeight").textContent=w+" kg";
 el("metricWeight").textContent=w+" kg";
 el("metricWater").textContent=fmt(water)+" ml";
 el("metricCalories").textContent=fmt(calories);
 el("metricWorkouts").textContent=workouts;
 const start=141;
 const progress=Math.max(0,Math.min(100,(start-w)/(start-goal)*100));
 el("mainProgress").style.width=progress+"%";
 el("progressText").textContent=Math.max(0,start-w).toFixed(1)+" kg eliminados desde 141 kg · Meta "+goal+" kg";
 el("waterProgress").style.width=Math.min(100,water/db.settings.waterGoal*100)+"%";
 el("waterText").textContent=fmt(water)+" de "+fmt(db.settings.waterGoal)+" ml";
 el("calorieTotal").textContent=fmt(calories)+" kcal";
 el("weightHistory").innerHTML=list(db.weights,x=>`<div class="record"><strong>${x.value} kg</strong><small>${x.date}</small></div>`);
 el("activityHistory").innerHTML=list(db.activities,x=>`<div class="record"><strong>${x.type}: ${x.name}</strong><small>${x.date} · ${x.duration||0} min · ${x.distance||0} km</small></div>`);
 el("mealHistory").innerHTML=list(db.meals.filter(x=>x.date===today()),x=>`<div class="record"><strong>${x.type}: ${x.name}</strong><small>${fmt(x.calories)} kcal</small></div>`);
 el("measureHistory").innerHTML=list(db.measurements,x=>`<div class="record"><strong>${x.date}</strong><small>Peito: ${x.chest||"-"} · Cintura: ${x.waist||"-"} · Abdômen: ${x.abdomen||"-"} · Braço: ${x.arm||"-"} · Coxa: ${x.thigh||"-"} cm</small></div>`);
 el("goalInput").value=goal;
 el("waterGoalInput").value=db.settings.waterGoal;
 drawChart();
}
function drawChart(){
 const c=el("weightChart"),ctx=c.getContext("2d");
 const width=c.clientWidth||300;
 c.width=width*2;c.height=360;
 ctx.scale(2,2);
 const h=180,w=width;
 ctx.clearRect(0,0,w,h);
 const data=[...db.weights].sort((a,b)=>a.date.localeCompare(b.date)).slice(-12);
 if(!data.length){
 ctx.fillStyle="#9ca99b";ctx.font="13px sans-serif";
 ctx.fillText("Registre seu peso para ver o gráfico.",10,85);return;
 }
 const min=Math.min(...data.map(x=>x.value))-2;
 const max=Math.max(...data.map(x=>x.value))+2;
 ctx.strokeStyle="#a5e65b";ctx.lineWidth=2;ctx.beginPath();
 data.forEach((p,i)=>{
 const x=12+(w-24)*(data.length===1?0.5:i/(data.length-1));
 const y=145-(p.value-min)/(max-min||1)*115;
 if(i===0)ctx.moveTo(x,y);else ctx.lineTo(x,y);
 ctx.fillStyle="#a5e65b";ctx.fillRect(x-3,y-3,6,6);
 });
 ctx.stroke();
 ctx.fillStyle="#9ca99b";ctx.font="11px sans-serif";
 ctx.fillText(data[0].value+" kg",5,165);
 ctx.fillText(data[data.length-1].value+" kg",w-55,165);
}
function exportData(){
 const blob=new Blob([JSON.stringify(db,null,2)],{type:"application/json"});
 const url=URL.createObjectURL(blob);
 const a=document.createElement("a");a.href=url;a.download="ph-projeto-evolucao.json";a.click();
 URL.revokeObjectURL(url);
}
function clearData(){
 if(confirm("Tem certeza que deseja apagar TODOS os registros? Esta ação não pode ser desfeita.")){
 localStorage.removeItem(KEY);location.reload();
 }
}
el("today").textContent=new Date().toLocaleDateString("pt-BR",{weekday:"long",day:"numeric",month:"long",year:"numeric"});
["weightDate","activityDate","mealDate","measureDate"].forEach(id=>el(id).value=today());
render();
window.addEventListener("resize",drawChart);
</script>
</body>
</html>

