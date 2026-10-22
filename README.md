
<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#087f5b">
<title>Daily Hisab</title>
<script src="https://accounts.google.com/gsi/client" async defer></script>
<style>
:root{--green:#087f5b;--bg:#f3f7f5;--red:#ed5365;--blue:#4388e8}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);font-family:Arial,sans-serif;color:#20332b;padding-bottom:80px}
button,input{font:inherit}button{cursor:pointer}
.top{background:linear-gradient(145deg,#087f5b,#08a77b);color:white;padding:23px 18px 35px;border-radius:0 0 25px 25px}
.brand{font-size:23px;font-weight:bold}.sub{font-size:13px;margin-top:8px}
main{max-width:600px;margin:auto;padding:0 15px}
.cards{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:9px;margin-top:-17px}
.card,.panel{background:white;border-radius:15px;padding:14px;box-shadow:0 4px 15px #00000008}
.card{padding:13px 8px;min-width:0}.card small{display:block;color:#718078;font-size:11px;margin:9px 0 6px}
.card strong{display:block;font-size:clamp(12px,3.4vw,18px);overflow-wrap:anywhere}
.green{color:#07865f}.red{color:#e4485b}.blue{color:#3978d8}
.page{display:none;padding-top:18px}.page.active{display:block}
h2{font-size:19px;margin:0 0 15px}h3{font-size:15px;margin:0 0 13px}
.panel{margin-bottom:15px;padding:17px}
.btn{border:0;border-radius:11px;padding:13px;background:var(--green);color:white;font-weight:bold}
.full{width:100%}.secondary{background:#e8f5ef;color:var(--green)}
.danger{background:#fff0f1;color:#d93649}
.quick{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.quick button{border:0;border-radius:13px;padding:15px 8px;text-align:left;min-height:80px;font-weight:bold;color:#176b50;background:#e3f7eb}
.quick button:nth-child(2){background:#f0e8ff;color:#7850c8}
.quick button:nth-child(3){background:#fff0d8;color:#b97912}
.quick button:nth-child(4){background:#e4efff;color:#3574c7}
label{display:block;font-size:13px;margin:13px 0 6px;color:#52655b}
input{width:100%;padding:12px;border:1px solid #dce6e0;border-radius:10px;background:#fcfdfc;color:#20332b}
.tabs{display:flex;gap:8px;margin:10px 0}.tabs button{flex:1;border:0;border-radius:10px;padding:12px;background:#edf2ef;color:#43584c}
.tabs button.active{background:var(--green);color:white}
.entry{padding:14px 0;border-bottom:1px solid #edf1ee}
.entrytop{display:flex;justify-content:space-between;gap:8px}
.entry p{margin:6px 0;color:#7a8981;font-size:12px;overflow-wrap:anywhere}
.actions{display:flex;gap:7px;margin-top:9px}.actions button{border:0;border-radius:8px;padding:8px 12px}
.reportline{display:flex;justify-content:space-between;gap:10px;margin:15px 0;font-size:14px}
.barrow{display:grid;grid-template-columns:43px 1fr 35px;gap:8px;align-items:center;margin:12px 0;font-size:12px}
.bar{height:10px;background:#edf1ef;border-radius:8px;overflow:hidden}
.bar span{display:block;height:100%;border-radius:8px}
.note{font-size:12px;color:#718078;line-height:1.6;overflow-wrap:anywhere}
.bottom{position:fixed;bottom:0;left:0;right:0;background:white;display:flex;justify-content:space-around;padding:9px 2px max(9px,env(safe-area-inset-bottom));box-shadow:0 -3px 16px #0000000b;z-index:5}
.bottom button{flex:1;border:0;background:white;color:#76847c;font-size:11px;padding:5px 0}
.bottom button b{display:block;font-size:21px;margin-bottom:3px}
.bottom button.active{color:var(--green)}
.avatar{width:52px;height:52px;border-radius:50%;background:#dff5e9;display:grid;place-items:center;font-size:25px}
.status{padding:10px;border-radius:10px;background:#f0f5f2;font-size:13px;line-height:1.6;overflow-wrap:anywhere}
</style>
</head>
<body>
<header class="top">
 <div class="brand">▣ Daily Hisab</div>
 <div class="sub">আপনার প্রতিদিনের আয়-খরচ</div>
</header>

<main>
<div id="home" class="page active">
 <div class="cards">
  <div class="card">🟢<small>মোট আয়</small><strong class="green" id="totalIn">৳০</strong></div>
  <div class="card">🔴<small>মোট খরচ</small><strong class="red" id="totalOut">৳০</strong></div>
  <div class="card">👛<small>অবশিষ্ট</small><strong class="blue" id="balance">৳০</strong></div>
 </div>
 <div class="panel" style="margin-top:17px"><button class="btn full" onclick="openPage('add')">＋ নতুন হিসাব যোগ করুন</button></div>
 <div class="panel"><h2>দ্রুত অপশন</h2><div class="quick">
  <button onclick="openPage('add');setType('income')">🟢<br><br>আজকের আয়</button>
  <button onclick="openPage('report')">📊<br><br>মাসিক রিপোর্ট</button>
  <button onclick="openPage('records')">📒<br><br>পুরোনো হিসাব</button>
  <button onclick="openPage('profile')">⚙️<br><br>সেটিংস</button>
 </div></div>
 <div class="panel"><h2>সাম্প্রতিক হিসাব</h2><div id="recent"></div><button class="btn secondary full" onclick="openPage('records')">সব হিসাব দেখুন →</button></div>
</div>

<div id="add" class="page"><div class="panel">
 <h2 id="formTitle">＋ নতুন হিসাব যোগ করুন</h2>
 <form id="hisabForm">
  <label for="date">তারিখ</label><input type="date" id="date" required>
  <label>হিসাবের ধরন</label><div class="tabs">
   <button type="button" id="incomeTab" class="active" onclick="setType('income')">⬆ আয়</button>
   <button type="button" id="expenseTab" onclick="setType('expense')">⬇ খরচ</button>
  </div>
  <input type="hidden" id="type" value="income">
  <label for="amount">টাকার পরিমাণ (৳)</label><input type="number" id="amount" min="0.01" step="0.01" placeholder="যেমন: ৫০০" required>
  <label for="details">বিবরণ</label><input id="details" maxlength="200" placeholder="যেমন: বেতন, বাজার খরচ">
  <button class="btn full" id="saveBtn" style="margin-top:18px">হিসাব সেভ করুন</button>
  <button class="btn secondary full" type="button" id="cancelBtn" hidden onclick="resetForm()">বাতিল করুন</button>
 </form>
</div></div>

<div id="records" class="page"><div class="panel">
 <h2>📒 সব হিসাব</h2><input id="search" placeholder="🔎 বিবরণ দিয়ে খুঁজুন">
 <div class="tabs">
  <button class="active" id="allTab" onclick="setFilter('all')">সব</button>
  <button id="inTab" onclick="setFilter('income')">আয়</button>
  <button id="outTab" onclick="setFilter('expense')">খরচ</button>
 </div><div id="entries"></div>
</div></div>

<div id="report" class="page">
 <div class="panel"><h2>📊 মাসিক রিপোর্ট</h2>
  <label for="month">মাস নির্বাচন করুন</label><input type="month" id="month">
  <div class="cards" style="margin-top:15px">
   <div class="card"><small>মোট আয়</small><strong class="green" id="monthIn">৳০</strong></div>
   <div class="card"><small>মোট খরচ</small><strong class="red" id="monthOut">৳০</strong></div>
   <div class="card"><small>অবশিষ্ট</small><strong class="blue" id="monthBalance">৳০</strong></div>
  </div>
 </div>
 <div class="panel"><h3>আয় ও খরচের তুলনা</h3><div id="chart"></div><p class="note">নির্বাচিত মাসের হিসাব।</p></div>
</div>

<div id="profile" class="page">
 <div class="panel"><div style="display:flex;align-items:center;gap:13px">
  <div class="avatar">👤</div><div><h2 style="margin:0">আমার Daily Hisab</h2><p class="note">ব্যক্তিগত হিসাব ব্যবস্থাপনা</p></div>
 </div></div>
 <div class="panel"><h2>☁️ Google Drive ব্যাকআপ</h2>
  <p class="note">প্রথমবার Google Cloud থেকে Client ID সেট করে Google Drive অনুমতি দিতে হবে।</p>
  <div id="driveStatus" class="status">Drive সংযুক্ত নয়।</div>
  <button class="btn full" style="margin-top:10px" onclick="connectDrive()">Google Drive সংযুক্ত করুন</button>
  <button class="btn secondary full" style="margin-top:8px" onclick="syncNow()">এখনই Drive-এ সেভ করুন</button>
  <button class="btn secondary full" style="margin-top:8px" onclick="restoreDrive()">Drive থেকে হিসাব ফিরিয়ে আনুন</button>
  <button class="btn secondary full" style="margin-top:8px" onclick="exportData()">হিসাব ডাউনলোড করুন (JSON)</button>
  <p class="note">ইন্টারনেট না থাকলে ব্যাকআপ অপেক্ষা করবে। Drive-এ সেভ সম্পন্ন হয়েছে কি না স্ট্যাটাস দেখে নিশ্চিত হও।</p>
 </div>
 <div class="panel"><h3>এই অ্যাপ সম্পর্কে</h3><p class="note">Daily Hisab — দৈনিক আয়, খরচ ও মাসিক রিপোর্ট।</p></div>
</div>
</main>

<nav class="bottom">
 <button class="active" data-page="home" onclick="openPage('home')"><b>⌂</b>হোম</button>
 <button data-page="report" onclick="openPage('report')"><b>▥</b>রিপোর্ট</button>
 <button data-page="records" onclick="openPage('records')"><b>▤</b>হিসাব</button>
 <button data-page="profile" onclick="openPage('profile')"><b>♙</b>প্রোফাইল</button>
</nav>

<script>
const $=id=>document.getElementById(id);
const KEY="dailyHisab_full_v1";
const DRIVE_FILE="DailyHisabBackup.json";

/*
  SETUP:
  1) নিচের CLIENT_ID-তে নিজের Google OAuth Web Client ID বসাও।
  2) Google Drive API enable করে OAuth Web application তৈরি করো।
  3) Authorized JavaScript origins-এ তোমার GitHub Pages origin যোগ করো।
  Client Secret কখনো এখানে বসাবে না।
*/
const CLIENT_ID="PASTE_YOUR_GOOGLE_OAUTH_CLIENT_ID_HERE";

let records=[],editingId=null,filter="all";
let accessToken=null,driveFileId=null,syncTimer=null,syncBusy=false,syncAgain=false;

try{
 let saved=localStorage.getItem(KEY);
 // পুরোনো সংস্করণের ডেটা থাকলে নতুন কী-তে কপি করার চেষ্টা
 if(saved===null){
  saved=localStorage.getItem("dailyHisab_v2");
 }
 records=JSON.parse(saved||"[]");
 if(!Array.isArray(records))records=[];
}catch(e){records=[]}

const now=new Date();
const today=new Date(now.getTime()-now.getTimezoneOffset()*60000).toISOString().slice(0,10);
$("date").value=today;$("month").value=today.slice(0,7);

function status(msg){$("driveStatus").textContent=msg}
function money(n){return "৳"+Number(n).toLocaleString("bn-BD",{maximumFractionDigits:2})}

function openPage(id){
 document.querySelectorAll(".page").forEach(p=>p.classList.toggle("active",p.id===id));
 document.querySelectorAll(".bottom button").forEach(b=>b.classList.toggle("active",b.dataset.page===id));
 if(id==="add"&&!editingId)$("date").value=today;
 render();window.scrollTo(0,0);
}
function setType(type){
 $("type").value=type;
 $("incomeTab").classList.toggle("active",type==="income");
 $("expenseTab").classList.toggle("active",type==="expense");
}
function setFilter(value){
 filter=value;
 [["allTab","all"],["inTab","income"],["outTab","expense"]].forEach(([id,v])=>$(id).classList.toggle("active",v===value));
 render();
}
function persist(){
 try{
  localStorage.setItem(KEY,JSON.stringify(records));
  scheduleSync();
  return true;
 }catch(e){alert("ফোনে ডেটা সেভ হয়নি। স্টোরেজ পরীক্ষা করুন।");return false}
}
function sum(list,type){return list.reduce((n,r)=>n+(r.type===type?Number(r.amount):0),0)}

function createEntry(r){
 const div=document.createElement("div");div.className="entry";
 const top=document.createElement("div");top.className="entrytop";
 const title=document.createElement("strong");
 title.textContent=(r.type==="income"?"🟢 ":"🔴 ")+(r.details||(r.type==="income"?"আয়":"খরচ"));
 const amount=document.createElement("strong");amount.className=r.type==="income"?"green":"red";
 amount.textContent=(r.type==="income"?"+":"−")+money(r.amount);
 top.append(title,amount);
 const p=document.createElement("p");p.textContent=r.date;
 const actions=document.createElement("div");actions.className="actions";
 const edit=document.createElement("button");edit.className="secondary";edit.textContent="✏️ এডিট";edit.onclick=()=>editRecord(r.id);
 const del=document.createElement("button");del.className="danger";del.textContent="🗑 ডিলিট";del.onclick=()=>deleteRecord(r.id);
 actions.append(edit,del);div.append(top,p,actions);return div;
}

function render(){
 const ti=sum(records,"income"),to=sum(records,"expense");
 $("totalIn").textContent=money(ti);$("totalOut").textContent=money(to);$("balance").textContent=money(ti-to);
 const recent=[...records].sort((a,b)=>b.date.localeCompare(a.date)).slice(0,4);
 $("recent").replaceChildren();
 if(!recent.length)$("recent").textContent="এখনো কোনো হিসাব যোগ করা হয়নি।";
 recent.forEach(r=>$("recent").append(createEntry(r)));
 const q=$("search").value.trim().toLowerCase();
 const found=[...records].filter(r=>(filter==="all"||r.type===filter))
 .filter(r=>(r.details||"").toLowerCase().includes(q)).sort((a,b)=>b.date.localeCompare(a.date));
 $("entries").replaceChildren();
 if(!found.length)$("entries").textContent="কোনো হিসাব পাওয়া যায়নি।";
 found.forEach(r=>$("entries").append(createEntry(r)));
 const month=$("month").value;
 const monthly=records.filter(r=>r.date.startsWith(month));
 const mi=sum(monthly,"income"),mo=sum(monthly,"expense");
 $("monthIn").textContent=money(mi);$("monthOut").textContent=money(mo);$("monthBalance").textContent=money(mi-mo);
 $("chart").replaceChildren();const max=Math.max(mi,mo,1);
 [["আয়",mi,"#0aa879"],["খরচ",mo,"#ed5365"]].forEach(([label,val,color])=>{
  const row=document.createElement("div");row.className="barrow";
  const name=document.createElement("span");name.textContent=label;
  const track=document.createElement("div");track.className="bar";
  const fill=document.createElement("span");fill.style.width=(val/max*100)+"%";fill.style.background=color;track.append(fill);
  const value=document.createElement("span");value.textContent=Number(val).toLocaleString("bn-BD");
  row.append(name,track,value);$("chart").append(row);
 });
}

$("hisabForm").addEventListener("submit",e=>{
 e.preventDefault();
 const amount=Number($("amount").value);
 if(!Number.isFinite(amount)||amount<=0){alert("সঠিক টাকার পরিমাণ লিখুন।");return}
 const item={id:editingId||Date.now().toString(36)+Math.random().toString(36).slice(2),
 date:$("date").value,type:$("type").value,amount,details:$("details").value.trim()};
 if(!item.date){alert("তারিখ দিন।");return}
 const previous=records;
 records=editingId?records.map(r=>r.id===editingId?item:r):[...records,item];
 if(!persist()){records=previous;return}
 resetForm();openPage("home");
});
function editRecord(id){
 const r=records.find(x=>x.id===id);if(!r)return;
 editingId=id;$("date").value=r.date;$("amount").value=r.amount;$("details").value=r.details||"";
 setType(r.type);$("formTitle").textContent="✏️ হিসাব এডিট করুন";
 $("saveBtn").textContent="পরিবর্তন সেভ করুন";$("cancelBtn").hidden=false;openPage("add");
}
function deleteRecord(id){
 if(!confirm("এই হিসাবটি ডিলিট করতে চান?"))return;
 const previous=records;records=records.filter(r=>r.id!==id);
 if(!persist()){records=previous;return}
 if(editingId===id)resetForm();render();
}
function resetForm(){
 editingId=null;$("hisabForm").reset();$("date").value=today;setType("income");
 $("formTitle").textContent="＋ নতুন হিসাব যোগ করুন";$("saveBtn").textContent="হিসাব সেভ করুন";$("cancelBtn").hidden=true;
}
function exportData(){
 const blob=new Blob([JSON.stringify(records,null,2)],{type:"application/json"});
 const url=URL.createObjectURL(blob);const a=document.createElement("a");
 a.href=url;a.download="daily-hisab-backup.json";a.click();setTimeout(()=>URL.revokeObjectURL(url),1000);
}

/* Google Drive connection */
function connectDrive(){
 if(!CLIENT_ID||CLIENT_ID.includes("PASTE_YOUR")){
  alert("আগে কোডে নিজের Google OAuth Web Client ID বসাতে হবে।");
  return;
 }
 if(!window.google?.accounts?.oauth2){
  alert("Google লগইন লাইব্রেরি লোড হয়নি। ইন্টারনেট চালু করে পেজ রিফ্রেশ করুন।");return;
 }
 const client=google.accounts.oauth2.initTokenClient({
  client_id:CLIENT_ID,
  scope:"https://www.googleapis.com/auth/drive.file",
  callback:async response=>{
   if(response.error){status("Google অনুমতি পাওয়া যায়নি: "+response.error);return}
   accessToken=response.access_token;
   status("Google Drive সংযুক্ত হয়েছে। ব্যাকআপ ফাইল খোঁজা হচ্ছে…");
   try{
    await findDriveFile();
    await uploadBackup();
   }catch(err){status("Drive সংযোগে সমস্যা: "+err.message)}
  }
 });
 client.requestAccessToken();
}
async function driveFetch(url,options={}){
 if(!accessToken)throw new Error("আগে Google Drive সংযুক্ত করুন।");
 const headers=new Headers(options.headers||{});
 headers.set("Authorization","Bearer "+accessToken);
 const res=await fetch(url,{...options,headers});
 if(res.status===401){accessToken=null;throw new Error("Google অনুমতি শেষ হয়েছে। আবার Drive সংযুক্ত করুন।")}
 if(!res.ok)throw new Error("Google Drive API error "+res.status+": "+(await res.text()).slice(0,250));
 if(res.status===204)return null;
 return res.json();
}
async function findDriveFile(){
 const q=encodeURIComponent("name='"+DRIVE_FILE+"' and trashed=false");
 const data=await driveFetch("https://www.googleapis.com/drive/v3/files?q="+q+"&fields=files(id,name,modifiedTime)&pageSize=100");
 const files=data.files||[];
 if(files.length){
  files.sort((a,b)=>new Date(b.modifiedTime)-new Date(a.modifiedTime));
  driveFileId=files[0].id;
 }else driveFileId=null;
}
function scheduleSync(){
 if(!accessToken)return;
 clearTimeout(syncTimer);
 status("ফোনে সেভ হয়েছে। Drive-এ সিঙ্কের অপেক্ষায়…");
 syncTimer=setTimeout(()=>uploadBackup().catch(e=>status("Drive সিঙ্ক হয়নি: "+e.message)),1200);
}
async function uploadBackup(){
 if(!accessToken){status("ফোনে সেভ হয়েছে। Drive অটো সেভের জন্য একবার সংযুক্ত করুন।");return}
 if(syncBusy){syncAgain=true;return}
 syncBusy=true;
 try{
  do{
   syncAgain=false;
   const body=JSON.stringify({app:"Daily Hisab",version:1,updatedAt:new Date().toISOString(),records},null,2);
   if(!driveFileId){
    await findDriveFile();
   }
   if(driveFileId){
    await driveFetch("https://www.googleapis.com/upload/drive/v3/files/"+encodeURIComponent(driveFileId)+"?uploadType=media",{
     method:"PATCH",headers:{"Content-Type":"application/json"},body
    });
   }else{
    const boundary="dailyhisab_boundary_9274";
    const metadata={name:DRIVE_FILE,mimeType:"application/json"};
    const multipart="--"+boundary+"\r\nContent-Type: application/json; charset=UTF-8\r\n\r\n"+JSON.stringify(metadata)+"\r\n--"+boundary+"\r\nContent-Type: application/json\r\n\r\n"+body+"\r\n--"+boundary+"--";
    const created=await driveFetch("https://www.googleapis.com/upload/drive/v3/files?uploadType=multipart&fields=id,name",{
     method:"POST",headers:{"Content-Type":"multipart/related; boundary="+boundary},body:multipart
    });
    driveFileId=created.id;
   }
   status("✅ Google Drive-এ ব্যাকআপ সেভ হয়েছে। "+new Date().toLocaleTimeString("bn-BD"));
  }while(syncAgain);
 }finally{syncBusy=false}
}
async function syncNow(){
 try{
  if(!accessToken){connectDrive();return}
  await uploadBackup();
 }catch(e){status("ব্যাকআপ ব্যর্থ: "+e.message)}
}
async function restoreDrive(){
 if(!accessToken){alert("প্রথমে Google Drive সংযুক্ত করুন।");return}
 if(!confirm("Drive-এর ব্যাকআপ দিয়ে এই ফোনের বর্তমান হিসাব প্রতিস্থাপন করবেন? আগে বর্তমান হিসাব ডাউনলোড করে রাখুন।"))return;
 try{
  status("Drive থেকে ব্যাকআপ খোঁজা হচ্ছে…");
  await findDriveFile();
  if(!driveFileId){status("Drive-এ Daily Hisab-এর ব্যাকআপ পাওয়া যায়নি।");return}
  const data=await driveFetch("https://www.googleapis.com/drive/v3/files/"+encodeURIComponent(driveFileId)+"?alt=media");
  const imported=Array.isArray(data)?data:data.records;
  if(!Array.isArray(imported))throw new Error("ব্যাকআপ ফাইলের ফরম্যাট সঠিক নয়।");
  if(!imported.every(r=>r&&r.id&&r.date&&["income","expense"].includes(r.type)&&Number.isFinite(Number(r.amount))))throw new Error("ব্যাকআপে কিছু হিসাবের তথ্য সঠিক নয়।");
  records=imported.map(r=>({...r,amount:Number(r.amount)}));
  localStorage.setItem(KEY,JSON.stringify(records));
  render();status("✅ Drive থেকে "+records.length+"টি হিসাব ফিরিয়ে আনা হয়েছে।");
  alert("হিসাব ফিরিয়ে আনা হয়েছে।");
 }catch(e){status("হিসাব ফিরিয়ে আনা যায়নি: "+e.message)}
}
$("month").addEventListener("change",render);
$("search").addEventListener("input",render);
render();
</script>
</body>
</html>
