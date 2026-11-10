<!DOCTYPE html>
<html lang="en"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Warrior Timer</title>
<style>
:root{--bg:#f6f3ee;--card:#fff;--tx:#1d1b18;--mu:#7a746b;--ac:#d9480f;--bd:#e4ded5;color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#14120f;--card:#201d19;--tx:#f3eee6;--mu:#a39b8f;--ac:#ff8a3d;--bd:#332f29;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#14120f;--card:#201d19;--tx:#f3eee6;--mu:#a39b8f;--ac:#ff8a3d;--bd:#332f29;color-scheme:dark}
:root[data-theme="saffron"]{--bg:#fff1dc;--card:#fffaf0;--tx:#3b1d00;--mu:#8a5a2b;--ac:#e8590c;--bd:#f2d3a5;color-scheme:light}
:root[data-theme="forest"]{--bg:#0f1f17;--card:#18301f;--tx:#e6f4ea;--mu:#8fb39b;--ac:#4ade80;--bd:#24442f;color-scheme:dark}
:root[data-theme="ocean"]{--bg:#0b1b2e;--card:#122a46;--tx:#e4f0ff;--mu:#8aa8c8;--ac:#38bdf8;--bd:#1d3d63;color-scheme:dark}
*{box-sizing:border-box}html,body{margin:0;background:var(--bg);color:var(--tx);font-family:system-ui,-apple-system,"Segoe UI",sans-serif}
body{min-height:100vh}button,input{font:inherit;color:inherit}
#splash{position:fixed;inset:0;background:var(--bg);z-index:9;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:18px;padding:24px;text-align:center}
.idol{width:170px;height:170px;border-radius:50%;object-fit:cover;border:4px solid var(--ac);background:var(--card);display:flex;align-items:center;justify-content:center;font-size:76px}
#splash h1{font-size:2.3rem;margin:0;letter-spacing:.5px;color:var(--ac)}
.btn{background:var(--ac);color:#fff;border:0;border-radius:12px;padding:12px 22px;font-weight:600;cursor:pointer}
.btn.ghost{background:transparent;color:var(--tx);border:1px solid var(--bd)}
select{background:var(--card);color:var(--tx);border:1px solid var(--bd);border-radius:10px;padding:9px}
#app{max-width:560px;margin:0 auto;padding:16px 14px 90px}
header{display:flex;align-items:center;gap:12px;margin-bottom:14px}
header .idol{width:46px;height:46px;font-size:24px;border-width:2px}
header b{font-size:1.1rem;color:var(--ac)}
.card{background:var(--card);border:1px solid var(--bd);border-radius:16px;padding:14px;margin-bottom:10px}
.row{display:flex;align-items:center;gap:10px}.grow{flex:1;min-width:0}
.name{font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.time{font-variant-numeric:tabular-nums;font-size:1.5rem;font-weight:700}
.run .time{color:var(--ac)}
.sm{padding:8px 14px;border-radius:10px}
.x{background:none;border:0;color:var(--mu);font-size:18px;cursor:pointer}
input[type=text]{flex:1;min-width:0;background:var(--card);border:1px solid var(--bd);border-radius:10px;padding:11px}
.chips{display:flex;flex-wrap:wrap;gap:8px;margin:6px 0}
.chip{border:1px solid var(--bd);background:var(--card);border-radius:20px;padding:7px 13px;cursor:pointer}
.chip.on{background:var(--ac);color:#fff;border-color:var(--ac)}
.bar{height:10px;border-radius:6px;background:var(--bd);overflow:hidden;margin-top:6px}.bar i{display:block;height:100%;background:var(--ac)}
nav{position:fixed;left:0;right:0;bottom:0;display:flex;background:var(--card);border-top:1px solid var(--bd);padding-bottom:env(safe-area-inset-bottom,0px)}
nav button{flex:1;background:none;border:0;padding:14px 0;color:var(--mu);font-weight:600;cursor:pointer}
nav button.on{color:var(--ac)}
h3{margin:14px 0 6px}.mu{color:var(--mu);font-size:.9rem}
.hero{display:flex;flex-direction:column;align-items:center;gap:12px;margin-bottom:16px;text-align:center}.hero .idol{width:150px;height:150px;overflow:hidden}#pick{width:100%}.hero .time{font-size:2.2rem;color:var(--ac)}.hero .btn{width:100%;font-size:1.1rem}
.hide{display:none!important}
</style></head><body>
<div id="splash">
  <div id="sIdol" class="idol">⚔️</div>
  <h1 id="sTitle"></h1>
  <select id="sLang"><option value="en">English</option><option value="hi">हिन्दी</option><option value="hx">Hinglish</option></select>
  <button class="btn" id="enter"></button>
</div>
<div id="app" class="hide">
  <header><div id="hIdol" class="idol">⚔️</div><b id="hTitle"></b></header>
  <section id="p-timers">
    <div class="hero"><div id="bIdol" class="idol">⚔️</div><select id="pick"></select><div class="time" id="pTime">00:00:00</div><div id="pToday" style="font-weight:600"></div><button class="btn" id="go"></button><button class="btn ghost sm" id="rstAll"></button></div>
    <div class="row" style="margin-bottom:10px"><input type="text" id="newName"><button class="btn" id="add"></button></div>
    <div id="quick" class="chips"></div>
    <div id="list"></div>
  </section>
  <section id="p-report" class="hide">
    <p class="mu" id="rHint"></p><div id="rChips" class="chips"></div><div id="rOut"></div>
  </section>
  <section id="p-hist" class="hide"><div id="hOut"></div><button class="btn ghost sm" id="clrH"></button></section>
  <section id="p-set" class="hide">
    <h3 id="tLang"></h3><select id="lang"><option value="en">English</option><option value="hi">हिन्दी</option><option value="hx">Hinglish</option></select>
    <h3 id="tTheme"></h3><div id="themes" class="chips"></div>
    <h3 id="tIdol"></h3><div class="row"><button class="btn ghost sm" id="upl"></button><input type="file" id="file" accept="image/*" style="position:absolute;opacity:0;width:1px;height:1px;pointer-events:none" tabindex="-1"><button class="btn ghost sm" id="rmIdol"></button></div>
    <h3></h3><button class="btn ghost sm" id="reset"></button>
  </section>
  <nav><button data-p="timers"></button><button data-p="report"></button><button data-p="hist"></button><button data-p="set"></button></nav>
</div>
<script>
const T={
en:{warrior:"I am Warrior",enter:"Enter",timers:"Timers",report:"Report",settings:"Settings",ph:"Subject name (e.g. Physics)",add:"Add",start:"Start",pause:"Pause",hint:"Select subjects to see your report",lang:"Language",theme:"Theme",idol:"Idol photo",upl:"Upload photo",rm:"Remove",reset:"Reset all time",total:"Total",none:"Select at least one subject",quick:"Quick add:",sure:"Reset all timers?",th:{auto:"Auto",light:"Light",dark:"Dark",saffron:"Saffron",forest:"Forest",ocean:"Ocean"},subs:["Math","English","Science","Hindi"],today:"Studied",tdy:"Today",hist:"History",nohist:"No history yet",clr:"Clear history",rst:"Reset all",sure2:"Sure? Tap again"},
hi:{warrior:"मैं योद्धा हूँ",enter:"प्रवेश करें",timers:"टाइमर",report:"रिपोर्ट",settings:"सेटिंग्स",ph:"विषय का नाम (जैसे भौतिकी)",add:"जोड़ें",start:"शुरू",pause:"रोकें",hint:"रिपोर्ट देखने के लिए विषय चुनें",lang:"भाषा",theme:"थीम",idol:"आराध्य की फोटो",upl:"फोटो चुनें",rm:"हटाएँ",reset:"सारा समय रीसेट करें",total:"कुल",none:"कम से कम एक विषय चुनें",quick:"जल्दी जोड़ें:",sure:"सभी टाइमर रीसेट करें?",th:{auto:"ऑटो",light:"लाइट",dark:"डार्क",saffron:"केसरिया",forest:"जंगल",ocean:"सागर"},subs:["गणित","अंग्रेज़ी","विज्ञान","हिंदी"],today:"पढ़ाई",tdy:"आज",hist:"हिस्ट्री",nohist:"अभी कोई हिस्ट्री नहीं",clr:"हिस्ट्री मिटाएँ",rst:"सब रीसेट",sure2:"पक्का? फिर दबाएँ"},
hx:{warrior:"I am Warrior",enter:"Enter karo",timers:"Timers",report:"Report",settings:"Settings",ph:"Subject ka naam (jaise Physics)",add:"Add",start:"Start",pause:"Pause",hint:"Report dekhne ke liye subjects chuno",lang:"Language",theme:"Theme",idol:"Idol ki photo",upl:"Photo chuno",rm:"Hatao",reset:"Saara time reset karo",total:"Total",none:"Kam se kam 1 subject chuno",quick:"Jaldi add:",sure:"Saare timers reset karein?",th:{auto:"Auto",light:"Light",dark:"Dark",saffron:"Saffron",forest:"Forest",ocean:"Ocean"},subs:["Math","English","Science","Hindi"],today:"Padhai",tdy:"Aaj",hist:"History",nohist:"Abhi koi history nahi",clr:"History saaf karo",rst:"Sab reset",sure2:"Pakka? Fir dabao"}};
let S={lang:"hx",theme:"auto",idol:"",subs:[],sel:[],log:{}};
try{const r=localStorage.getItem("wt");if(r)S=Object.assign(S,JSON.parse(r))}catch(e){}
const $=id=>document.getElementById(id),t=()=>T[S.lang];
const save=()=>{try{localStorage.setItem("wt",JSON.stringify(S))}catch(e){}};
const el=(s,tag="div",c="")=>{const e=document.createElement(tag);if(c)e.className=c;e.innerHTML=s;return e};
const el_=x=>x;
const ms=s=>s.total+(s.start?Date.now()-s.start:0);
const fmt=m=>{const s=Math.floor(m/1000),h=Math.floor(s/3600),mi=Math.floor(s%3600/60),se=s%60,p=n=>String(n).padStart(2,"0");return p(h)+":"+p(mi)+":"+p(se)};
const esc=s=>s.replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
let page="timers",pickId=null;
const dk=ts=>{const d=new Date(ts);return d.getFullYear()+"-"+String(d.getMonth()+1).padStart(2,"0")+"-"+String(d.getDate()).padStart(2,"0")};
const mid=ts=>{const d=new Date(ts);d.setHours(0,0,0,0);return d.getTime()};
const nm=ts=>{const d=new Date(ts);d.setHours(24,0,0,0);return d.getTime()};
function addLog(s,a,b){S.log=S.log||{};while(a<b){const e=Math.min(b,nm(a)),k=dk(a),D=S.log[k]=S.log[k]||{},r=D[s.id]=D[s.id]||{n:s.name,t:0};r.n=s.name;r.t+=e-a;a=e}}
function stopSub(s){if(s.start){const n=Date.now();s.total+=n-s.start;addLog(s,s.start,n);s.start=null}}
function dayMap(k){const m={},L=(S.log&&S.log[k])||{};for(const i in L)m[i]={n:L[i].n,t:L[i].t};if(k===dk(Date.now())){const n=Date.now(),m0=mid(n);S.subs.forEach(s=>{if(s.start){const r=m[s.id]=m[s.id]||{n:s.name,t:0};r.t+=n-Math.max(s.start,m0)}})}return m}
function tick2(){const a=Object.values(dayMap(dk(Date.now()))).reduce((c,r)=>c+r.t,0);$("pToday").textContent=t().tdy+": "+fmt(a)}
function resetAll(){S.subs.forEach(s=>{stopSub(s);s.total=0});save();renderList();renderReport()}
function twoTap(b,fn){let armed=0,orig;b.onclick=()=>{if(armed){armed=0;b.textContent=orig;fn();return}orig=b.textContent;armed=1;b.textContent=t().sure2;setTimeout(()=>{if(armed){armed=0;b.textContent=orig}},3000)}}
function renderHist(){const L=t(),o=$("hOut"),keys=new Set(Object.keys(S.log||{}));if(S.subs.some(s=>s.start))keys.add(dk(Date.now()));const ks=[...keys].sort().reverse();if(!ks.length){o.innerHTML='<p class="mu">'+L.nohist+'</p>';return}
o.innerHTML=ks.map(k=>{const a=Object.values(dayMap(k)).sort((x,y)=>y.t-x.t),tot=a.reduce((c,r)=>c+r.t,0),mx=Math.max(...a.map(r=>r.t),1);return '<div class="card"><div class="row"><b class="grow">'+k+(k===dk(Date.now())?" · "+L.tdy:"")+'</b><b style="color:var(--ac)">'+fmt(tot)+'</b></div>'+a.map(r=>'<div class="row" style="margin-top:8px"><div class="grow"><div>'+esc(r.n)+'</div><div class="bar"><i style="width:'+Math.round(r.t/mx*100)+'%"></i></div></div><span class="mu">'+fmt(r.t)+'</span></div>').join("")+'</div>'}).join("")}
function fillPick(){const L=t(),p=$("pick");p.innerHTML="";S.subs.forEach(s=>{const o=document.createElement("option");o.value=s.id;o.textContent=s.name;p.appendChild(o)});if(!S.subs.some(s=>String(s.id)===String(pickId)))pickId=S.subs[0]?S.subs[0].id:null;if(pickId!=null)p.value=pickId;const s=S.subs.find(x=>String(x.id)===String(pickId));$("go").textContent=s&&s.start?L.pause:L.start;$("go").disabled=!s;$("pTime").textContent=s?fmt(ms(s)):"00:00:00";tick2()}
function applyTheme(){if(S.theme==="auto")document.documentElement.removeAttribute("data-theme");else document.documentElement.setAttribute("data-theme",S.theme)}
function idolEls(){[$("sIdol"),$("hIdol"),$("bIdol")].forEach(e=>{e.innerHTML=S.idol?'<img class="idol" style="width:100%;height:100%;border:0" src="'+S.idol+'" alt="">':"⚔️"})}
function labels(){const L=t();document.documentElement.lang=S.lang==="hi"?"hi":"en";
$("sTitle").textContent=L.warrior;$("hTitle").textContent=L.warrior;$("enter").textContent=L.enter;
$("newName").placeholder=L.ph;$("add").textContent=L.add;$("rHint").textContent=L.hint;
$("tLang").textContent=L.lang;$("tTheme").textContent=L.theme;$("tIdol").textContent=L.idol;
$("upl").textContent=L.upl;$("rstAll").textContent=L.rst;$("clrH").textContent=L.clr;$("rmIdol").textContent=L.rm;$("reset").textContent=L.reset;
$("lang").value=S.lang;$("sLang").value=S.lang;
document.querySelectorAll("nav button").forEach(b=>{b.textContent=L[{timers:"timers",report:"report",hist:"hist",set:"settings"}[b.dataset.p]]});
$("themes").innerHTML="";Object.keys(L.th).forEach(k=>{const c=el(L.th[k],"button","chip"+(S.theme===k?" on":""));c.onclick=()=>{S.theme=k;save();applyTheme();labels()};$("themes").appendChild(c)});
const q=$("quick");q.innerHTML="";const lb=el(L.quick,"span","mu");q.appendChild(lb);
L.subs.forEach(n=>{const c=el("+ "+esc(n),"button","chip");c.onclick=()=>addSub(n);q.appendChild(c)});
idolEls();renderList();renderReport();show(page)}
function addSub(n){n=n.trim();if(!n)return;S.subs.push({id:Date.now()+Math.random(),name:n,total:0,start:null});save();renderList();renderReport()}
function renderList(){const L=t(),box=$("list");box.innerHTML="";fillPick();
S.subs.forEach(s=>{const c=el("","div","card");c.id="c"+s.id;
c.innerHTML='<div class="row"><div class="grow"><div class="name">'+esc(s.name)+'</div><div class="time" data-t="'+s.id+'">'+fmt(ms(s))+'</div></div><button class="btn sm">'+(s.start?L.pause:L.start)+'</button><button class="x" aria-label="delete">✕</button></div>';
if(s.start)c.classList.add("run");
c.querySelector(".btn").onclick=()=>{if(s.start)stopSub(s);else s.start=Date.now();save();renderList()};
c.querySelector(".x").onclick=()=>{stopSub(s);S.subs=S.subs.filter(x=>x!==s);S.sel=S.sel.filter(i=>i!==s.id);save();renderList();renderReport()};
box.appendChild(c)})}
function renderReport(){const L=t(),ch=$("rChips");ch.innerHTML="";
S.subs.forEach(s=>{const c=el(esc(s.name),"button","chip"+(S.sel.includes(s.id)?" on":""));c.onclick=()=>{S.sel=S.sel.includes(s.id)?S.sel.filter(i=>i!==s.id):S.sel.concat(s.id);save();renderReport()};ch.appendChild(c)});
const out=$("rOut");const ch2=S.subs.filter(s=>S.sel.includes(s.id));
if(!ch2.length){out.innerHTML='<p class="mu">'+L.none+'</p>';return}
const tot=ch2.reduce((a,s)=>a+ms(s),0),mx=Math.max(...ch2.map(ms),1);
out.innerHTML='<div class="card"><div class="mu">'+L.total+'</div><div class="time" id="rTot" style="color:var(--ac)">'+fmt(tot)+'</div></div>'+
ch2.map(s=>'<div class="card"><div class="row"><div class="grow name">'+esc(s.name)+'</div><b data-r="'+s.id+'">'+fmt(ms(s))+'</b></div><div class="bar"><i data-b="'+s.id+'" style="width:'+Math.round(ms(s)/mx*100)+'%"></i></div><div class="mu" data-p="'+s.id+'">'+(tot?Math.round(ms(s)/tot*100):0)+'%</div></div>').join("")}
function show(p){page=p;["timers","report","hist","set"].forEach(k=>$("p-"+k).classList.toggle("hide",k!==p));
document.querySelectorAll("nav button").forEach(b=>b.classList.toggle("on",b.dataset.p===p));if(p==="report")renderReport();if(p==="hist")renderHist()}
$("pick").onchange=e=>{pickId=e.target.value;fillPick()};
$("go").onclick=()=>{const s=S.subs.find(x=>String(x.id)===String(pickId));if(!s)return;if(s.start)stopSub(s);else s.start=Date.now();save();renderList()};
setInterval(()=>{const ps=S.subs.find(x=>String(x.id)===String(pickId));if(ps)$("pTime").textContent=fmt(ms(ps));tick2();if(page==="hist")renderHist();S.subs.forEach(s=>{const e=document.querySelector('[data-t="'+s.id+'"]');if(e)e.textContent=fmt(ms(s))});
if(page==="report"&&S.subs.some(s=>s.start&&S.sel.includes(s.id)))renderReport()},500);
document.querySelectorAll("nav button").forEach(b=>b.onclick=()=>show(b.dataset.p));
$("add").onclick=()=>{addSub($("newName").value);$("newName").value=""};
$("newName").onkeydown=e=>{if(e.key==="Enter")$("add").click()};
$("enter").onclick=()=>{$("splash").classList.add("hide");$("app").classList.remove("hide")};
function setLang(v){S.lang=v;save();labels()}
$("lang").onchange=e=>setLang(e.target.value);$("sLang").onchange=e=>setLang(e.target.value);
$("upl").onclick=()=>$("file").click();
["sIdol","hIdol","bIdol"].forEach(i=>{$(i).style.cursor="pointer";$(i).onclick=()=>$("file").click()});
$("file").onchange=e=>{const f=e.target.files[0];if(!f)return;const u=URL.createObjectURL(f),im=new Image();im.onload=()=>{const c=document.createElement("canvas"),k=Math.min(1,400/Math.max(im.width,im.height));c.width=Math.round(im.width*k);c.height=Math.round(im.height*k);c.getContext("2d").drawImage(im,0,0,c.width,c.height);S.idol=c.toDataURL("image/jpeg",.85);URL.revokeObjectURL(u);save();idolEls()};im.onerror=()=>alert("Photo open nahi hui, JPG ya PNG try karo");im.src=u;e.target.value=""};
$("rmIdol").onclick=()=>{S.idol="";save();idolEls()};
twoTap($("reset"),resetAll);twoTap($("rstAll"),resetAll);twoTap($("clrH"),()=>{S.log={};save();renderHist()});
if(!S.subs.length)T[S.lang].subs.slice(0,2).forEach(n=>S.subs.push({id:Date.now()+Math.random(),name:n,total:0,start:null}));
applyTheme();labels();
</script></body></html>
