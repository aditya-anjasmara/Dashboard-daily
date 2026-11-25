# Dashboard-daily
Dashboard daily sales tangban

<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard Daily Sales</title>
<style>
:root {
 --bg:#dfe5ee;
 --panel:#edf1f6;
 --panel2:#e4eaf2;
 --line:#c3cfde;
 --ink:#10294d;
 --muted:#536d91;
 --teal:#008d87;
 --gold:#9b6b0b;
 --red:#d34242;
 --green:#008f80;
}
*{box-sizing:border-box}
body{
 margin:0;
 background:var(--bg);
 color:var(--ink);
 font:14px/1.35 Inter,Segoe UI,Arial,sans-serif
}
body.dark{
 --bg:#101827;
 --panel:#1b2738;
 --panel2:#263448;
 --line:#3b4c63;
 --ink:#edf4ff;
 --muted:#aabbd2;
 --teal:#41c9bd;
 --gold:#e0b34f;
 --red:#ff7777;
 --green:#40d1b5;
}
header{
 padding:12px 14px;
 display:flex;
 gap:14px;
 align-items:flex-start;
 justify-content:space-between;
 flex-wrap:wrap
}
h1{font-size:29px;margin:0;font-weight:800}
.sub{color:var(--muted);font-weight:650}
.filters{
 display:flex;
 align-items:center;
 gap:9px;
 flex-wrap:wrap;
 margin-top:8px
}
.filter{
 display:flex;
 align-items:center;
 gap:7px;
 color:var(--muted);
 font-weight:650
}
select,input[type=date]{
 background:var(--panel2);
 border:1px solid var(--line);
 border-radius:9px;
 padding:9px 11px;
 color:var(--ink);
 min-width:150px
}
select.channel,select.month{
 border:1px solid var(--teal);
 color:var(--teal);
 font-weight:750;
 min-width:190px
}
.rightfilters{
 display:flex;
 align-items:center;
 gap:8px;
 flex-wrap:wrap;
 margin-top:30px
}
.btn{
 border:1px solid var(--line);
 background:var(--panel);
 color:var(--ink);
 border-radius:10px;
 padding:8px 11px;
 cursor:pointer;
 font-weight:750;
 min-height:36px
}
.btn.teal{border-color:var(--teal);color:var(--teal)}
.btn.gold{border-color:var(--gold);color:var(--gold)}
.btn.active{background:var(--teal);color:white}
.btn.small{padding:5px 9px;min-height:30px}
main{
 display:grid;
 grid-template-columns:minmax(285px,.95fr) minmax(600px,2.9fr) minmax(280px,1fr);
 gap:13px;
 padding:0 14px 14px;
 min-height:calc(100vh - 130px)
}
.panel{
 background:var(--panel);
 border:1px solid var(--line);
 border-radius:19px;
 padding:16px;
 min-width:0;
 box-shadow:0 4px 18px rgba(31,55,86,.08)
}
.panelhead{
 display:flex;
 align-items:center;
 justify-content:space-between;
 gap:8px;
 margin-bottom:8px
}
.paneltitle{
 font-size:15px;
 color:var(--teal);
 font-weight:850
}
.actions{display:flex;gap:7px}
.datecaption{
 font-weight:650;
 color:var(--muted);
 margin:8px 0 12px
}
.goldtxt{color:var(--gold)}
.overview{
 display:grid;
 grid-template-columns:1fr 150px 1fr;
 align-items:center;
 text-align:center;
 gap:5px;
 margin:10px 0
}
.metric label{
 display:block;
 color:var(--teal);
 font-weight:750
}
.metric strong{font-size:20px}
.ring{
 width:145px;
 height:145px;
 border-radius:50%;
 margin:auto;
 display:grid;
 place-items:center;
 position:relative;
 background:conic-gradient(var(--gold) 0 87.3%,#8fa0b7 87.3% 100%)
}
.ring:before{
 content:"";
 position:absolute;
 inset:15px;
 border-radius:50%;
 background:var(--panel)
}
.ringinner{z-index:1;text-align:center}
.ringinner small{display:block;font-weight:750}
.ringinner b{display:block;font-size:27px}
.trends{
 display:flex;
 justify-content:space-between;
 margin:0 8px 14px;
 font-weight:750
}
.trends span{
 display:block;
 color:var(--teal);
 font-size:12px
}
.trends b{font-size:20px}
.negative{color:var(--red)}
.positive{color:var(--green)}
.stats{
 border-top:1px dashed var(--line);
 padding-top:9px;
 display:grid;
 gap:5px
}
.statrow{
 display:flex;
 justify-content:space-between;
 gap:10px;
 color:var(--muted);
 font-weight:650
}
.statrow b{color:var(--ink);text-align:right}
.statrow.emph{
 padding-top:7px;
 margin-top:2px;
 border-top:1px dashed var(--line)
}
.centerpanel{padding:14px 16px}
.category-cards{
 display:grid;
 grid-template-columns:repeat(6,minmax(95px,1fr));
 gap:8px;
 margin:8px 0 10px
}
.catcard{
 background:var(--panel2);
 border:1px solid var(--line);
 border-radius:13px;
 text-align:center;
 padding:9px 5px;
 min-width:0
}
.catemoji{font-size:19px}
.catname{font-size:12px;font-weight:750}
.mini-ring{
 width:50px;
 height:50px;
 border-radius:50%;
 margin:5px auto;
 background:conic-gradient(var(--gold) 0 78%,var(--line) 78% 100%);
 position:relative
}
.mini-ring:before{
 content:"";
 position:absolute;
 inset:6px;
 background:var(--panel2);
 border-radius:50%
}
.mini-ring.green{
 background:conic-gradient(var(--green) 0 82%,var(--line) 82% 100%)
}
.mini-ring.red{
 background:conic-gradient(var(--red) 0 42%,#8e9db2 42% 100%)
}
.percent{font-weight:850;font-size:12px;color:var(--gold)}
table{
 width:100%;
 border-collapse:collapse;
 font-size:13px
}
th{
 color:var(--teal);
 text-align:center;
 padding:5px 6px;
 border-bottom:1px solid var(--line);
 white-space:nowrap
}
th:first-child,td:first-child{text-align:left}
td{
 padding:5px 6px;
 text-align:center;
 font-weight:650;
 border-bottom:1px solid var(--line);
 white-space:nowrap
}
tbody tr:nth-child(even){background:var(--panel2)}
td:first-child{font-weight:750}
td.target{color:var(--teal)}
.tablewrap{overflow-x:auto}
.note{
 font-size:12px;
 color:var(--muted);
 font-weight:600;
 margin:6px 0 10px
}
.gauges{
 display:flex;
 justify-content:center;
 gap:28px;
 flex-wrap:wrap;
 margin:14px 0
}
.gauge{
 text-align:center;
 min-width:92px;
 color:var(--muted);
 font-size:11px;
 font-weight:700
}
.gauge svg{width:92px;height:52px;display:block;margin:auto}
.gauge strong{display:block;color:var(--ink);font-size:13px}
.gauge em{font-style:normal}
.weekly{
 display:flex;
 flex-direction:column;
 min-height:400px
}
.weekly .empty{
 flex:1;
 display:grid;
 place-items:center;
 text-align:center;
 color:var(--muted);
 padding:20px
}
.weekly .empty b{
 display:block;
 color:var(--teal);
 margin-bottom:6px
}
.uploadbar{
 display:flex;
 gap:8px;
 align-items:center;
 flex-wrap:wrap;
 margin-top:9px
}
.toast{
 position:fixed;
 bottom:16px;
 left:50%;
 transform:translateX(-50%);
 background:#10294d;
 color:white;
 padding:10px 16px;
 border-radius:10px;
 display:none;
 z-index:5
}
@media(max-width:1100px){
 main{grid-template-columns:1fr 2fr}
 .weekly{grid-column:1/-1}
 .category-cards{grid-template-columns:repeat(3,1fr)}
}
@media(max-width:720px){
 h1{font-size:23px}
 .rightfilters{margin-top:0}
 main{display:flex;flex-direction:column;padding:0 9px 10px}
 .panel{border-radius:14px;padding:13px}
 .overview{grid-template-columns:1fr 125px 1fr}
 .ring{width:120px;height:120px}
 .ring:before{inset:13px}
 .ringinner b{font-size:23px}
 .category-cards{grid-template-columns:repeat(2,1fr)}
 .filters{gap:7px}
 .filter{flex-wrap:wrap}
}
</style>
</head>

<body>

<header>
 <div>
  <h1>DASHBOARD DAILY SALES</h1>
  <div class="sub">
   <span id="transactionCount">31.642</span> transaksi ·
   Bulan aktif: <span id="activeMonthText">November 2026</span>
  </div>

  <div class="filters">
   <label class="filter">Area
    <select id="area">
     <option>Semua Area (69 toko)</option>
     <option>Jakarta</option>
     <option>Banten</option>
     <option>Jawa Barat</option>
    </select>
   </label>

   <label class="filter">Toko
    <select id="store">
     <option>Semua Toko</option>
     <option>Erafone Telaga Bestari</option>
     <option>Erafone Citra Raya</option>
     <option>Erafone BSD</option>
    </select>
   </label>

   <label class="filter">Channel
    <select class="channel" id="channel">
     <option>🏬 Semua Channel</option>
     <option>Store</option>
     <option>Online</option>
     <option>Marketplace</option>
    </select>
   </label>

   <label class="filter">Bulan
    <select class="month" id="month">
     <option value="November 2026">November 2026</option>
     <option value="Oktober 2026">Oktober 2026</option>
     <option value="September 2026">September 2026</option>
    </select>
   </label>
  </div>
 </div>

 <div class="rightfilters">
  <button class="btn teal" id="themeBtn">☁️</button>
  <span class="sub">Dari</span>
  <input type="date" id="from" value="2026-11-01">
  <span class="sub">Sampai</span>
  <input type="date" id="to" value="2026-11-24">
  <button class="btn teal" id="moreBtn">⋮</button>
 </div>
</header>

<main>

<!-- DAILY SALES -->
<section class="panel daily">
 <div class="panelhead">
  <div class="paneltitle">DAILY SALES</div>
  <div class="actions">
   <button class="btn small gold" id="refreshBtn">↔</button>
   <button class="btn small" id="cameraBtn">▣</button>
   <button class="btn small teal" id="collapseBtn">−</button>
  </div>
 </div>

 <div id="dailyContent">
  <div class="datecaption">
   Per 01 - 24 November 2026 · <span class="goldtxt">Bulan Ini</span>
  </div>

  <div class="overview">
   <div class="metric">
    <label>MTD %</label>
    <strong>69,8%</strong>
   </div>

   <div class="ring">
    <div class="ringinner">
     <small>EST</small>
     <b>87,3%</b>
    </div>
   </div>

   <div class="metric">
    <label>Sisa Hari</label>
    <strong>6</strong>
   </div>
  </div>

  <div class="trends">
   <div><span>MoM</span><b class="negative">▼ 6,6%</b></div>
   <div><span>YoY</span><b class="negative">▼ 10,3%</b></div>
  </div>

  <div class="statrow" style="justify-content:center;margin-bottom:8px">
   <span>Target</span>
   <b>87.455.697.436</b>
  </div>

  <div class="stats">
   <div class="statrow"><span>MTD</span><b>61.055.383.653</b></div>
   <div class="statrow"><span>EST</span><b>76.319.229.566</b></div>
   <div class="statrow"><span>Deviasi</span><b class="negative">-26.400.313.783</b></div>
   <div class="statrow emph"><span class="goldtxt">Butuh/Hari</span><b class="goldtxt">4.400.052.297</b></div>
   <div class="statrow"><span>AVG/Hari</span><b>2.543.974.319</b></div>
   <div class="statrow"><span>ASP Device</span><b>7.460.814</b></div>
   <div class="statrow"><span>Qty Terjual</span><b>37.500</b></div>
  </div>
 </div>
</section>

<!-- CATEGORY -->
<section class="panel centerpanel">
 <div class="panelhead">
  <div class="paneltitle">PENCAPAIAN BY KATEGORI</div>
  <div class="actions">
   <button class="btn small active" id="valueBtn">💰 Value</button>
   <button class="btn small" id="qtyBtn">📦 Qty</button>
   <button class="btn small gold" id="sortBtn">↔</button>
   <button class="btn small" id="exportBtn">▣</button>
   <button class="btn small teal" id="tableToggle">−</button>
  </div>
 </div>

 <div id="categoryContent">
  <div class="category-cards">
   <div class="catcard">
    <div class="catemoji">📱</div>
    <div class="catname">Handphone</div>
    <div class="mini-ring"></div>
    <div class="percent">87,7%</div>
   </div>

   <div class="catcard">
    <div class="catemoji">🎧</div>
    <div class="catname">Accessories</div>
    <div class="mini-ring"></div>
    <div class="percent">80,1%</div>
   </div>

   <div class="catcard">
    <div class="catemoji">🛡️</div>
    <div class="catname">Repair Contract</div>
    <div class="mini-ring green"></div>
    <div class="percent positive">101,9%</div>
   </div>

   <div class="catcard">
    <div class="catemoji">📡</div>
    <div class="catname">Operator</div>
    <div class="mini-ring"></div>
    <div class="percent">89,7%</div>
   </div>

   <div class="catcard">
    <div class="catemoji">🖥️</div>
    <div class="catname">CE</div>
    <div class="mini-ring red"></div>
    <div class="percent negative">41,9%</div>
   </div>

   <div class="catcard">
    <div class="catemoji">💻</div>
    <div class="catname">Laptop</div>
    <div class="mini-ring"></div>
    <div class="percent">88,0%</div>
   </div>
  </div>

  <div class="tablewrap">
   <table id="categoryTable">
    <thead>
     <tr>
      <th>Kategori</th>
      <th>Target</th>
      <th>MTD</th>
      <th>EST</th>
      <th>Daily Sales</th>
      <th>Growth vs Bln Lalu</th>
     </tr>
    </thead>

    <tbody>
     <tr>
      <td>Handphone</td><td class="target">75.574.135.398</td>
      <td>53.009.082.480</td><td>66.261.353.100</td>
      <td>2.208.711.770</td><td class="negative">▼ 8,7%</td>
     </tr>
     <tr>
      <td>Accessories</td><td class="target">3.747.505.828</td>
      <td>2.401.283.472</td><td>3.001.604.340</td>
      <td>100.053.478</td><td class="negative">▼ 23,0%</td>
     </tr>
     <tr>
      <td>Repair Contract</td><td class="target">1.308.616.539</td>
      <td>1.066.708.900</td><td>1.333.386.125</td>
      <td>44.446.204</td><td class="positive">▲ 40,7%</td>
     </tr>
     <tr>
      <td>Operator</td><td class="target">4.573.189.067</td>
      <td>3.280.967.355</td><td>4.101.209.194</td>
      <td>136.706.973</td><td class="negative">▼ 1,6%</td>
     </tr>
     <tr>
      <td>CE</td><td class="target">782.388.816</td>
      <td>262.263.067</td><td>327.828.834</td>
      <td>10.927.628</td><td class="negative">▼ 7,3%</td>
     </tr>
     <tr>
      <td>Laptop</td><td class="target">1.469.861.788</td>
      <td>1.035.078.379</td><td>1.293.847.974</td>
      <td>43.128.266</td><td class="positive">▲ 9,1%</td>
     </tr>
    </tbody>
   </table>
  </div>

  <div class="note">
   Growth = EST bulan ini vs total Oktober 2026.
  </div>
 </div>

 <div class="uploadbar">
  <input type="file" id="csvFile" accept=".csv">
  <button class="btn small teal" id="importBtn">Import CSV</button>
  <span class="note">Format: Kategori,Target,MTD,EST,DailySales,Growth</span>
 </div>
</section>

<!-- WEEKLY REVENUE -->
<section class="panel weekly">
 <div class="panelhead">
  <div class="paneltitle">WEEKLY REVENUE</div>
  <div class="actions">
   <button class="btn small gold" id="weekReset">↔</button>
   <button class="btn small teal" id="weekAdd">＋</button>
  </div>
 </div>

 <div class="empty">
  <div>
   <b>Weekly Revenue</b>
   Grafik mingguan akan tampil setelah data mingguan tersedia.
  </div>
 </div>
</section>

</main>

<div class="toast" id="toast"></div>

<script>
const $ = id => document.getElementById(id);

function toast(message){
 const t=$('toast');
 t.textContent=message;
 t.style.display='block';
 setTimeout(()=>t.style.display='none',2600);
}

$('themeBtn').onclick=()=>{
 document.body.classList.toggle('dark');
 $('themeBtn').textContent=
 document.body.classList.contains('dark')?'☀️':'☁️';
};

$('month').onchange=e=>{
 $('activeMonthText').textContent=e.target.value;
 toast('Bulan aktif: '+e.target.value);
};

$('store').onchange=()=>{
 toast('Toko dipilih: '+$('store').value);
};

$('area').onchange=()=>{
 toast('Area dipilih: '+$('area').value);
};

$('channel').onchange=()=>{
 toast('Channel dipilih: '+$('channel').value);
};

$('refreshBtn').onclick=()=>toast('Tampilan diperbarui.');

$('cameraBtn').onclick=()=>window.print();

$('moreBtn').onclick=()=>{
 toast('Gunakan fitur Import CSV untuk memasukkan data.');
};

$('collapseBtn').onclick=()=>{
 const el=$('dailyContent');
 el.hidden=!el.hidden;
 $('collapseBtn').textContent=el.hidden?'＋':'−';
};

$('tableToggle').onclick=()=>{
 const el=$('categoryContent');
 el.hidden=!el.hidden;
 $('tableToggle').textContent=el.hidden?'＋':'−';
};

$('valueBtn').onclick=()=>{
 $('valueBtn').classList.add('active');
 $('qtyBtn').classList.remove('active');
 toast('Mode Value dipilih.');
};

$('qtyBtn').onclick=()=>{
 $('qtyBtn').classList.add('active');
 $('valueBtn').classList.remove('active');
 toast('Mode Qty dipilih.');
};

$('sortBtn').onclick=()=>{
 const body=$('categoryTable').tBodies[0];
 [...body.rows].reverse().forEach(row=>body.appendChild(row));
 toast('Urutan kategori dibalik.');
};

$('exportBtn').onclick=()=>{
 const rows=[...$('categoryTable').rows]
 .map(row=>[...row.cells]
 .map(cell=>'"'+cell.innerText+'"').join(','))
 .join('\n');

 const blob=new Blob(['\ufeff'+rows],{
  type:'text/csv;charset=utf-8;'
 });

 const a=document.createElement('a');
 a.href=URL.createObjectURL(blob);
 a.download='daily-sales-category.csv';
 a.click();
 URL.revokeObjectURL(a.href);
};

$('importBtn').onclick=()=>{
 const file=$('csvFile').files[0];

 if(!file){
  toast('Pilih file CSV terlebih dahulu.');
  return;
 }

 const reader=new FileReader();

 reader.onload=()=>{
  try{
   const lines=reader.result.trim().split(/\r?\n/);

   const parsed=lines.slice(1)
   .map(line=>line.split(/,(?=(?:[^"]*"[^"]*")*[^"]*$)/)
   .map(v=>v.replace(/^"|"$/g,'').replaceAll('""','"')))
   .filter(row=>row.length>=6);

   if(!parsed.length) throw Error();

   const tbody=$('categoryTable').tBodies[0];
   tbody.innerHTML='';

   parsed.forEach(row=>{
    const tr=document.createElement('tr');

    row.slice(0,6).forEach((value,index)=>{
     const td=document.createElement('td');
     td.textContent=value;

     if(index===1) td.className='target';
     if(index===5){
      td.className=/▲|\+/.test(value)?'positive':'negative';
     }

     tr.appendChild(td);
    });

    tbody.appendChild(tr);
   });

   toast(parsed.length+' kategori berhasil dimuat.');

  }catch(error){
   toast('Format CSV tidak sesuai. Periksa kolom data.');
  }
 };

 reader.readAsText(file);
};

$('weekAdd').onclick=()=>{
 toast('Modul data mingguan belum tersedia.');
};

$('weekReset').onclick=()=>{
 toast('Belum ada data mingguan.');
};
</script>

</body>
</html>
