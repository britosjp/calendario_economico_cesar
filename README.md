# calendario_economico_cesar
<img width="1472" height="996" alt="image" src="https://github.com/user-attachments/assets/c33ecb1f-3781-4bb2-8ac6-3d2370f41dc1" />

<h2 class="sr-only">Calendário Econômico ao vivo — eventos 3 estrelas com SSE</h2>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
.wrap{background:#0f1117;border-radius:var(--border-radius-lg);border:0.5px solid #2a2d3a;overflow:hidden;font-family:var(--font-sans);}

.cfg-banner{background:#0d1526;border-bottom:0.5px solid #1e2d4a;padding:8px 12px;display:flex;align-items:center;gap:8px;flex-wrap:wrap;}
.cfg-label{font-size:10px;color:#4a6fa5;white-space:nowrap;}
.cfg-input{flex:1;min-width:140px;background:#0f1117;border:0.5px solid #2a2d3a;border-radius:5px;color:#7c9fd4;font-size:10px;padding:4px 7px;outline:none;font-family:var(--font-sans);}
.cfg-input:focus{border-color:#378ADD;}
.cfg-btn{background:#185FA5;border:none;border-radius:5px;color:#B5D4F4;font-size:10px;font-weight:500;padding:4px 10px;cursor:pointer;white-space:nowrap;}
.cfg-btn:hover{background:#0C447C;}

.header{padding:10px 12px 0;}
.h-top{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;}
.h-left{display:flex;align-items:center;gap:7px;}
.h-title{font-size:13px;font-weight:500;color:#e8eaf0;}
.badge{background:#1e2235;color:#7c85b0;font-size:10px;padding:2px 7px;border-radius:20px;display:flex;align-items:center;gap:3px;}
.h-right{display:flex;align-items:center;gap:4px;}
.icon-btn{background:none;border:none;cursor:pointer;color:#4a5175;padding:3px 4px;border-radius:5px;font-size:14px;line-height:1;}
.icon-btn:hover{color:#7c85b0;background:#1e2235;}
.live-dot{width:6px;height:6px;border-radius:50%;background:#639922;display:inline-block;animation:livepulse 2s infinite;}
.live-dot.off{background:#2e3450;animation:none;}
.live-dot.loading{background:#BA7517;animation:livepulse 0.8s infinite;}
@keyframes livepulse{0%,100%{opacity:1}50%{opacity:.3}}

.nav{display:flex;gap:4px;padding:0 12px 8px;}
.nb{flex:1;padding:5px 0;font-size:11px;font-weight:500;border:0.5px solid #2a2d3a;background:transparent;color:#4a5175;border-radius:6px;cursor:pointer;transition:all 0.15s;}
.nb.active{background:#185FA5;color:#B5D4F4;border-color:#185FA5;}
.nb:hover:not(.active){background:#1e2235;color:#7c85b0;}

.status{display:flex;align-items:center;gap:6px;padding:4px 12px;background:#090c12;font-size:10px;color:#3d4460;border-top:0.5px solid #1a1e2a;border-bottom:0.5px solid #1a1e2a;}
.status-txt{flex:1;}
.mode-badge{font-size:9px;padding:1px 6px;border-radius:20px;font-weight:500;}
.mode-badge.live{background:#173404;color:#639922;}
.mode-badge.static{background:#1e2235;color:#4a5175;}
.mode-badge.err{background:#501313;color:#E24B4A;}

.alert-box{display:none;align-items:flex-start;gap:8px;background:#1e160a;border-bottom:0.5px solid #854F0B;padding:8px 12px;}
.alert-box.show{display:flex;}
.a-title{font-size:10px;font-weight:500;color:#EF9F27;margin-bottom:3px;}
.a-ev{font-size:10px;color:#BA7517;display:flex;align-items:center;gap:5px;margin-top:2px;flex-wrap:wrap;}
.cd{background:#412402;color:#EF9F27;font-size:9px;font-weight:500;padding:1px 5px;border-radius:20px;}

.col-hdr{display:grid;grid-template-columns:46px 18px 1fr 48px 48px 48px;gap:5px;padding:4px 12px;background:#090c12;border-bottom:0.5px solid #1a1e2a;}
.col-hdr span{font-size:8px;text-transform:uppercase;letter-spacing:.5px;color:#2e3450;}
.col-hdr .cr{text-align:right;}

.scroll-area{max-height:340px;overflow-y:auto;padding-bottom:4px;}
.scroll-area::-webkit-scrollbar{width:3px;}
.scroll-area::-webkit-scrollbar-thumb{background:#2a2d3a;border-radius:3px;}

.day-sep{display:flex;align-items:center;gap:8px;padding:7px 12px 4px;}
.day-sep span{font-size:9px;font-weight:500;text-transform:uppercase;letter-spacing:.8px;color:#2e3450;white-space:nowrap;}
.day-sep::after{content:'';flex:1;height:0.5px;background:#1a1e2a;}

.ev-row{display:grid;grid-template-columns:46px 18px 1fr 48px 48px 48px;align-items:center;gap:5px;padding:5px 12px;border-bottom:0.5px solid #12151f;transition:background 0.4s;}
.ev-row:last-child{border-bottom:none;}
.ev-row.soon{background:#1a130a;border-left:1.5px solid #854F0B;border-radius:0;}
.ev-row.flash-green{background:#0d1a08;}
.ev-row.flash-red{background:#1a0808;}

.ev-time{font-size:10px;color:#3d4460;font-variant-numeric:tabular-nums;line-height:1.3;}
.ev-cur{font-size:9px;color:#2e3450;}
.ev-flag{font-size:13px;}
.ev-name{font-size:11px;font-weight:500;color:#c8ccd8;line-height:1.3;}
.ev-per{font-size:9px;color:#2e3450;margin-top:1px;}
.soon-tag{display:inline-block;background:#412402;color:#EF9F27;font-size:8px;font-weight:500;padding:1px 4px;border-radius:3px;margin-left:4px;vertical-align:middle;}

.val{text-align:right;font-size:11px;font-variant-numeric:tabular-nums;}
.val-lbl{font-size:8px;color:#2e3450;display:block;margin-bottom:1px;text-transform:uppercase;letter-spacing:.4px;}
.v-actual{color:#c8ccd8;font-weight:500;}
.v-actual.beat{color:#639922;}
.v-actual.miss{color:#E24B4A;}
.v-fore{color:#3d4460;}
.v-prev{color:#2e3450;}
.v-nd{color:#1e2235;font-size:10px;}

.skel{height:34px;background:#12151f;margin-bottom:0.5px;animation:shimmer 1.2s infinite;}
@keyframes shimmer{0%,100%{opacity:.4}50%{opacity:.8}}

.footer{display:flex;align-items:center;justify-content:space-between;padding:5px 12px;background:#090c12;border-top:0.5px solid #1a1e2a;}
.footer a{font-size:9px;color:#185FA5;text-decoration:none;}
.footer span{font-size:9px;color:#2e3450;}
</style>

<div class="wrap">

  <div class="cfg-banner" id="cfg-banner">
    <span class="cfg-label"><i class="ti ti-server" style="font-size:11px" aria-hidden="true"></i> Backend URL:</span>
    <input class="cfg-input" id="api-url" type="text" value="http://localhost:3001" placeholder="https://seu-backend.railway.app" aria-label="URL do backend">
    <button class="cfg-btn" onclick="conectar()">Conectar</button>
  </div>

  <div class="header">
    <div class="h-top">
      <div class="h-left">
        <i class="ti ti-chart-candle" style="font-size:15px;color:#378ADD" aria-hidden="true"></i>
        <span class="h-title">Calendário Econômico</span>
        <span class="badge"><span style="color:#EF9F27;font-size:9px">★★★</span> alto impacto</span>
      </div>
      <div class="h-right">
        <span class="live-dot off" id="live-dot" title="Status da conexão"></span>
        <button class="icon-btn" onclick="doRefresh()" aria-label="Atualizar"><i class="ti ti-refresh" aria-hidden="true"></i></button>
        <a class="icon-btn" href="https://br.investing.com/economic-calendar" target="_blank" aria-label="Abrir Investing.com"><i class="ti ti-external-link" aria-hidden="true"></i></a>
      </div>
    </div>
    <div class="nav">
      <button class="nb active" id="btn-today" onclick="switchPeriod('today')">Hoje</button>
      <button class="nb" id="btn-tomorrow" onclick="switchPeriod('tomorrow')">Amanhã</button>
      <button class="nb" id="btn-week" onclick="switchPeriod('week')">Esta semana</button>
    </div>
  </div>

  <div class="status">
    <div class="live-dot off" id="status-dot" style="width:5px;height:5px;flex-shrink:0;animation:none;"></div>
    <span class="status-txt" id="status-txt">Configure o backend acima para dados ao vivo</span>
    <span class="mode-badge static" id="mode-badge">demo</span>
  </div>

  <div class="alert-box" id="alert-box" role="alert">
    <i class="ti ti-bell" style="font-size:13px;color:#EF9F27;flex-shrink:0;margin-top:1px" aria-hidden="true"></i>
    <div style="flex:1">
      <div class="a-title">Eventos saindo em breve</div>
      <div id="alert-list"></div>
    </div>
    <button style="background:none;border:none;cursor:pointer;color:#854F0B;padding:0 0 0 8px;font-size:14px;align-self:flex-start;" onclick="document.getElementById('alert-box').classList.remove('show')" aria-label="Fechar"><i class="ti ti-x" aria-hidden="true"></i></button>
  </div>

  <div class="col-hdr">
    <span>Hora</span><span></span><span>Evento</span>
    <span class="cr">Real</span><span class="cr">Prev.</span><span class="cr">Ant.</span>
  </div>

  <div class="scroll-area" id="content">
    <div class="skel"></div>
    <div class="skel" style="opacity:.7"></div>
    <div class="skel" style="opacity:.5"></div>
    <div class="skel" style="opacity:.3"></div>
  </div>

  <div class="footer">
    <span id="footer-info">modo demonstração</span>
    <a href="https://br.investing.com/economic-calendar" target="_blank">br.investing.com</a>
  </div>
</div>

<script>
const FLAGS={'USD':'🇺🇸','EUR':'🇪🇺','GBP':'🇬🇧','JPY':'🇯🇵','BRL':'🇧🇷','CAD':'🇨🇦','AUD':'🇦🇺','CHF':'🇨🇭','CNY':'🇨🇳','NZD':'🇳🇿'};

function isoDate(o){const d=new Date();d.setDate(d.getDate()+(o||0));return d.toISOString().split('T')[0];}
const T=isoDate(0),T1=isoDate(1),T2=isoDate(2),T3=isoDate(3),T4=isoDate(4),T5=isoDate(5);

const DEMO={
  today:[
    {date:T,time:'09:00',currency:'BRL',event:'IPCA — IPC Amplo',period:'Mai 2025',actual:'0.38%',forecast:'0.40%',previous:'0.43%'},
    {date:T,time:'09:30',currency:'USD',event:'Pedidos Seguro-Desemprego',period:'Semanal',actual:'222K',forecast:'225K',previous:'219K'},
    {date:T,time:'10:00',currency:'EUR',event:'PMI Composto Zona do Euro',period:'Mai 2025',actual:'52.1',forecast:'51.8',previous:'50.4'},
    {date:T,time:'11:00',currency:'USD',event:'Estoques de Petróleo EIA',period:'Semanal',actual:null,forecast:'-1.2M',previous:'-2.0M'},
    {date:T,time:'14:00',currency:'GBP',event:'Taxa de Juros — BoE',period:'Jun 2025',actual:null,forecast:'4.25%',previous:'4.50%'},
    {date:T,time:'15:30',currency:'USD',event:'Balança Comercial EUA',period:'Abr 2025',actual:null,forecast:'-63.5B',previous:'-68.9B'},
    {date:T,time:'17:00',currency:'USD',event:'Discurso de Powell (Fed)',period:'',actual:null,forecast:null,previous:null},
  ],
  tomorrow:[
    {date:T1,time:'08:00',currency:'EUR',event:'IPC Alemanha (prévia)',period:'Mai 2025',actual:null,forecast:'2.2%',previous:'2.3%'},
    {date:T1,time:'09:30',currency:'USD',event:'Nonfarm Payrolls EUA',period:'Mai 2025',actual:null,forecast:'185K',previous:'177K'},
    {date:T1,time:'09:30',currency:'USD',event:'Taxa de Desemprego EUA',period:'Mai 2025',actual:null,forecast:'4.2%',previous:'4.2%'},
    {date:T1,time:'09:30',currency:'CAD',event:'Taxa de Desemprego Canadá',period:'Mai 2025',actual:null,forecast:'6.8%',previous:'6.9%'},
    {date:T1,time:'11:00',currency:'USD',event:'Confiança Michigan',period:'Jun 2025',actual:null,forecast:'69.1',previous:'67.4'},
    {date:T1,time:'14:00',currency:'BRL',event:'Ata do COPOM',period:'Jun 2025',actual:null,forecast:null,previous:null},
  ],
  week:[
    {date:T,time:'09:00',currency:'BRL',event:'IPCA — IPC Amplo',period:'Mai 2025',actual:'0.38%',forecast:'0.40%',previous:'0.43%'},
    {date:T,time:'09:30',currency:'USD',event:'Pedidos Seguro-Desemprego',period:'Semanal',actual:'222K',forecast:'225K',previous:'219K'},
    {date:T,time:'10:00',currency:'EUR',event:'PMI Composto Zona do Euro',period:'Mai 2025',actual:'52.1',forecast:'51.8',previous:'50.4'},
    {date:T,time:'14:00',currency:'GBP',event:'Taxa de Juros — BoE',period:'Jun 2025',actual:null,forecast:'4.25%',previous:'4.50%'},
    {date:T,time:'17:00',currency:'USD',event:'Discurso de Powell (Fed)',period:'',actual:null,forecast:null,previous:null},
    {date:T1,time:'09:30',currency:'USD',event:'Nonfarm Payrolls EUA',period:'Mai 2025',actual:null,forecast:'185K',previous:'177K'},
    {date:T1,time:'09:30',currency:'USD',event:'Taxa de Desemprego EUA',period:'Mai 2025',actual:null,forecast:'4.2%',previous:'4.2%'},
    {date:T1,time:'09:30',currency:'CAD',event:'Taxa de Desemprego Canadá',period:'Mai 2025',actual:null,forecast:'6.8%',previous:'6.9%'},
    {date:T2,time:'08:30',currency:'EUR',event:'PIB Zona do Euro (revisão)',period:'T1 2025',actual:null,forecast:'0.3%',previous:'0.2%'},
    {date:T2,time:'10:00',currency:'EUR',event:'Vendas no Varejo ZE',period:'Abr 2025',actual:null,forecast:'0.2%',previous:'-0.1%'},
    {date:T3,time:'09:30',currency:'USD',event:'IPC EUA (mensal)',period:'Mai 2025',actual:null,forecast:'0.2%',previous:'0.2%'},
    {date:T3,time:'09:30',currency:'USD',event:'IPC EUA (anual)',period:'Mai 2025',actual:null,forecast:'3.4%',previous:'3.4%'},
    {date:T4,time:'13:00',currency:'BRL',event:'Decisão Selic — COPOM',period:'Jun 2025',actual:null,forecast:'13.25%',previous:'13.75%'},
    {date:T5,time:'03:00',currency:'JPY',event:'Taxa de Juros — Banco do Japão',period:'Jun 2025',actual:null,forecast:'0.50%',previous:'0.50%'},
    {date:T5,time:'09:30',currency:'USD',event:'Vendas no Varejo EUA',period:'Mai 2025',actual:null,forecast:'0.1%',previous:'-0.1%'},
  ]
};

let curPeriod='today';
let apiBase='';
let esConn=null;
let alertInt=null;
let prevEvents={};
let isLive=false;

function minsUntil(t,d){
  try{const ev=new Date(d+'T'+t+':00-03:00');return Math.round((ev-new Date())/60000);}
  catch{return 9999;}
}
function fmtCd(m){if(m<=0)return'agora';if(m<60)return m+'min';const h=Math.floor(m/60),r=m%60;return r?h+'h '+r+'min':h+'h';}
function bm(a,f){
  const av=parseFloat((a||'').replace(/[^0-9.\-]/g,''));
  const fv=parseFloat((f||'').replace(/[^0-9.\-]/g,''));
  if(isNaN(av)||isNaN(fv))return'';
  return av>fv?'beat':av<fv?'miss':'';
}
function dayLbl(ds){
  const d=new Date(ds+'T12:00:00'),t=new Date();t.setHours(12,0,0,0);
  const tm=new Date(t);tm.setDate(tm.getDate()+1);
  const o={weekday:'short',day:'2-digit',month:'short'};
  if(d.toDateString()===t.toDateString())return'hoje · '+d.toLocaleDateString('pt-BR',o);
  if(d.toDateString()===tm.toDateString())return'amanhã · '+d.toLocaleDateString('pt-BR',o);
  return d.toLocaleDateString('pt-BR',o);
}

function setStatus(dot,txt,badge,badgeCls){
  const sd=document.getElementById('status-dot');
  const ld=document.getElementById('live-dot');
  sd.style.background=dot;
  sd.style.animation=badgeCls==='live'?'livepulse 2s infinite':'none';
  ld.style.background=dot;
  ld.style.animation=badgeCls==='live'?'livepulse 2s infinite':'none';
  document.getElementById('status-txt').textContent=txt;
  const mb=document.getElementById('mode-badge');
  mb.textContent=badge;
  mb.className='mode-badge '+badgeCls;
}

function checkAlerts(evs){
  const soon=evs.filter(ev=>{if(ev.actual)return false;const m=minsUntil(ev.time,ev.date);return m>=0&&m<=90;})
    .sort((a,b)=>minsUntil(a.time,a.date)-minsUntil(b.time,b.date));
  const box=document.getElementById('alert-box');
  if(!soon.length){box.classList.remove('show');return;}
  document.getElementById('alert-list').innerHTML=soon.slice(0,4).map(ev=>{
    const m=minsUntil(ev.time,ev.date);
    return`<div class="a-ev">${FLAGS[ev.currency]||'🌐'} ${ev.event}<span class="cd">${fmtCd(m)}</span></div>`;
  }).join('');
  box.classList.add('show');
}

function flashRow(id,cls){
  const row=document.querySelector(`[data-id="${CSS.escape(id)}"]`);
  if(!row)return;
  row.classList.add(cls);
  setTimeout(()=>row.classList.remove(cls),1200);
}

function render(evs,animate){
  const groups={};
  evs.forEach(ev=>{if(!groups[ev.date])groups[ev.date]=[];groups[ev.date].push(ev);});
  const dates=Object.keys(groups).sort();
  const el=document.getElementById('content');
  let html='';
  dates.forEach(ds=>{
    html+=`<div class="day-sep"><span>${dayLbl(ds)}</span></div>`;
    groups[ds].sort((a,b)=>a.time.localeCompare(b.time)).forEach(ev=>{
      const flag=FLAGS[ev.currency]||'🌐';
      const m=minsUntil(ev.time,ds);
      const soon=!ev.actual&&m>=0&&m<=90;
      const bmc=ev.actual?bm(ev.actual,ev.forecast):'';
      const eid=ev.id||(ev.date+ev.time+ev.currency+ev.event).replace(/\s/g,'');
      html+=`<div class="ev-row${soon?' soon':''}" data-id="${eid}">
        <div class="ev-time">${ev.time}<br><span class="ev-cur">${ev.currency}</span></div>
        <div class="ev-flag">${flag}</div>
        <div>
          <div class="ev-name">${ev.event}${soon?'<span class="soon-tag">breve</span>':''}</div>
          ${ev.period?`<div class="ev-per">${ev.period}</div>`:''}
        </div>
        <div class="val"><span class="val-lbl">Real</span><span class="${ev.actual?'v-actual '+bmc:'v-nd'}">${ev.actual||'—'}</span></div>
        <div class="val"><span class="val-lbl">Prev.</span><span class="${ev.forecast?'v-fore':'v-nd'}">${ev.forecast||'—'}</span></div>
        <div class="val"><span class="val-lbl">Ant.</span><span class="${ev.previous?'v-prev':'v-nd'}">${ev.previous||'—'}</span></div>
      </div>`;
    });
  });
  el.innerHTML=html||'<div style="text-align:center;padding:2rem;color:#2e3450"><i class="ti ti-calendar-off" aria-hidden="true"></i><p style="margin-top:6px;font-size:11px">Sem eventos</p></div>';

  if(animate){
    evs.forEach(ev=>{
      const eid=ev.id||(ev.date+ev.time+ev.currency+ev.event).replace(/\s/g,'');
      const prev=prevEvents[eid];
      if(ev.actual&&(!prev||!prev.actual)){
        const cls=bm(ev.actual,ev.forecast)==='beat'?'flash-green':'flash-red';
        setTimeout(()=>flashRow(eid,cls),100);
        playBeep(cls==='flash-green');
      }
    });
  }

  prevEvents={};
  evs.forEach(ev=>{
    const eid=ev.id||(ev.date+ev.time+ev.currency+ev.event).replace(/\s/g,'');
    prevEvents[eid]=ev;
  });

  checkAlerts(evs);
  document.getElementById('footer-info').textContent=evs.length+' eventos · '+new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});
  if(alertInt)clearInterval(alertInt);
  alertInt=setInterval(()=>checkAlerts(evs),60000);
}

let audioCtx=null;
function playBeep(positive){
  try{
    if(!audioCtx)audioCtx=new(window.AudioContext||window.webkitAudioContext)();
    const o=audioCtx.createOscillator();
    const g=audioCtx.createGain();
    o.connect(g);g.connect(audioCtx.destination);
    o.frequency.value=positive?880:440;
    o.type='sine';
    g.gain.setValueAtTime(0.15,audioCtx.currentTime);
    g.gain.exponentialRampToValueAtTime(0.001,audioCtx.currentTime+0.25);
    o.start();o.stop(audioCtx.currentTime+0.25);
  }catch(e){}
}

function showSkeleton(){
  document.getElementById('content').innerHTML='<div class="skel"></div><div class="skel" style="opacity:.7"></div><div class="skel" style="opacity:.5"></div><div class="skel" style="opacity:.3"></div>';
}

function loadDemo(period){
  const evs=DEMO[period]||[];
  render(evs,false);
  setStatus('#2e3450','modo demonstração — conecte o backend para dados ao vivo','demo','static');
  document.getElementById('footer-info').textContent=evs.length+' eventos (demo)';
}

function conectar(){
  const url=(document.getElementById('api-url').value||'').replace(/\/+$/,'').trim();
  if(!url){loadDemo(curPeriod);return;}
  apiBase=url;
  isLive=false;
  setStatus('#BA7517','Verificando backend...','conectando','static');
  showSkeleton();

  fetch(apiBase+'/health',{signal:AbortSignal.timeout(5000)})
    .then(r=>r.json())
    .then(d=>{
      if(d.status==='ok'){
        document.getElementById('cfg-banner').style.borderBottomColor='#3B6D11';
        startSSE(curPeriod);
      }else throw new Error('health check falhou');
    })
    .catch(err=>{
      setStatus('#A32D2D','Backend inacessível: '+err.message,'erro','err');
      loadDemo(curPeriod);
    });
}

function startSSE(period){
  if(esConn){esConn.close();esConn=null;}
  isLive=true;
  setStatus('#BA7517','Conectando SSE...','ao vivo','live');

  const url=`${apiBase}/api/calendar/stream?period=${period}`;
  esConn=new EventSource(url);

  esConn.addEventListener('events',(e)=>{
    try{
      const {events,fromCache,updatedAt}=JSON.parse(e.data);
      render(events,true);
      const time=new Date(updatedAt).toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});
      const src=fromCache?'cache':'ao vivo';
      setStatus('#639922',`${events.length} eventos · ${src} · ${time}`,'ao vivo','live');
    }catch(err){
      setStatus('#A32D2D','Erro ao processar dados','erro','err');
    }
  });

  esConn.addEventListener('error',()=>{
    setStatus('#A32D2D','Conexão perdida — tentando reconectar...','erro','err');
  });

  esConn.onopen=()=>{
    setStatus('#639922','Conectado — aguardando dados...','ao vivo','live');
  };
}

function switchPeriod(p){
  curPeriod=p;
  ['today','tomorrow','week'].forEach(k=>document.getElementById('btn-'+k).className='nb'+(k===p?' active':''));
  if(isLive&&apiBase){
    showSkeleton();
    startSSE(p);
  }else{
    loadDemo(p);
  }
}

function doRefresh(){
  if(isLive&&apiBase){
    fetch(apiBase+`/api/calendar?period=${curPeriod}`)
      .then(r=>r.json())
      .then(d=>{if(d.ok)render(d.events,true);})
      .catch(()=>setStatus('#A32D2D','Erro ao atualizar','erro','err'));
  }else{
    loadDemo(curPeriod);
  }
}

loadDemo('today');
</script>
