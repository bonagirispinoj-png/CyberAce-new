<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1.0">
<meta http-equiv="X-Content-Type-Options" content="nosniff">
<title>CyberAce Quantum 5.0 — Digital Services Hub</title>
<link href="https://fonts.googleapis.com/css2?family=Lexend:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-storage-compat.js"></script>
<style>
:root{--ink:#040810;--surface:#090E1A;--panel:#0E1525;--card:#131E30;--card2:#192338;--lift:#1E2A3E;
--border:rgba(255,255,255,.06);--border2:rgba(255,255,255,.11);--border3:rgba(255,255,255,.18);
--fire:#FF5722;--fire2:#FF7043;--gold:#FFB300;--jade:#00BFA5;--sky:#29B6F6;--violet:#7C4DFF;
--text:#ECF0F1;--muted:#607080;--muted2:#8FA3B8;--success:#00E676;--danger:#FF5252;--warn:#FFD600;
--ff-head:'Lexend',sans-serif;--ff-mono:'JetBrains Mono',monospace;--r:12px;--r2:18px;--r3:24px;
--sh:0 16px 48px rgba(0,0,0,.55);--sh2:0 4px 20px rgba(0,0,0,.4)}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box}
html{font-size:14.5px;scroll-behavior:smooth}
body{font-family:var(--ff-head);background:var(--ink);color:var(--text);min-height:100vh;overflow-x:hidden}
body::before{content:'';position:fixed;inset:0;pointer-events:none;z-index:0;
background-image:linear-gradient(rgba(255,87,34,.025)1px,transparent 1px),linear-gradient(90deg,rgba(255,87,34,.025)1px,transparent 1px);background-size:40px 40px}
::-webkit-scrollbar{width:4px;height:4px}::-webkit-scrollbar-thumb{background:var(--fire);border-radius:9px}
.shell{display:flex;height:100vh;position:relative;z-index:1}
.sidebar{width:240px;min-width:240px;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow-y:auto;transition:width .25s;position:fixed;top:0;left:0;bottom:0;z-index:300}
.sidebar.slim{width:56px}.sidebar.slim .hide-slim{display:none!important}
.main-area{flex:1;margin-left:240px;display:flex;flex-direction:column;min-height:100vh;transition:margin .25s}
.sidebar.slim~.main-area{margin-left:56px}
.topbar{height:52px;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 18px;gap:12px;position:sticky;top:0;z-index:200;flex-shrink:0}
.page{flex:1;padding:20px;overflow-y:auto}
.sb-brand{padding:14px 12px;border-bottom:1px solid var(--border);display:flex;align-items:center;gap:9px;flex-shrink:0}
.sb-orb{width:34px;height:34px;border-radius:8px;background:linear-gradient(135deg,var(--fire),#C62828);display:flex;align-items:center;justify-content:center;font-size:1rem;flex-shrink:0;box-shadow:0 4px 12px rgba(255,87,34,.4)}
.sb-name{font-size:.9rem;font-weight:800;line-height:1.2}
.sb-name small{display:block;font-size:.58rem;font-weight:400;color:var(--muted2);margin-top:1px}
.sb-user{margin:7px 9px;background:var(--panel);border:1px solid var(--border);border-radius:var(--r);padding:8px 10px;display:flex;align-items:center;gap:8px}
.sb-avatar{width:28px;height:28px;border-radius:50%;background:linear-gradient(135deg,var(--fire),var(--gold));display:flex;align-items:center;justify-content:center;font-weight:800;font-size:.76rem;flex-shrink:0}
.sb-uinfo .n{font-size:.75rem;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.sb-uinfo .r{font-size:.58rem;color:var(--jade)}
.nav{flex:1;padding:4px 0}
.nav-sec{padding:7px 14px 2px;font-size:.56rem;letter-spacing:.1em;text-transform:uppercase;color:var(--muted)}
.nav-item{display:flex;align-items:center;gap:9px;padding:8px 12px;cursor:pointer;color:var(--muted2);border-left:2px solid transparent;transition:all .15s;font-size:.8rem;user-select:none;white-space:nowrap}
.nav-item:hover{background:rgba(255,255,255,.03);color:var(--text);border-left-color:rgba(255,87,34,.4)}
.nav-item.active{background:rgba(255,87,34,.1);color:var(--text);border-left-color:var(--fire)}
.nav-item i{width:16px;text-align:center;font-size:.82rem;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--fire);color:#fff;font-size:.56rem;padding:1px 5px;border-radius:99px;font-weight:700}
.sb-footer{padding:10px 9px;border-top:1px solid var(--border)}
.upi-pill{background:rgba(255,87,34,.08);border:1px solid rgba(255,87,34,.25);border-radius:8px;padding:8px 10px;font-size:.66rem}
.upi-pill strong{display:block;color:var(--fire);margin-bottom:2px;font-size:.7rem}
.upi-pill span{color:var(--muted2);word-break:break-all;font-family:var(--ff-mono)}
.tb-toggle{background:none;border:none;color:var(--muted2);cursor:pointer;font-size:.95rem;padding:5px;border-radius:6px}
.tb-title{font-size:1rem;font-weight:700;flex:1}
.tb-right{display:flex;align-items:center;gap:9px}
.tb-secure{background:rgba(0,230,118,.07);border:1px solid rgba(0,230,118,.2);border-radius:99px;padding:4px 11px;font-size:.68rem;color:var(--success);display:flex;align-items:center;gap:4px}
.tb-secure::before{content:'';width:6px;height:6px;border-radius:50%;background:var(--success);animation:blink 2s infinite}
@keyframes blink{0%,100%{opacity:1}50%{opacity:.3}}
.tb-logout{background:rgba(255,82,82,.09);border:1px solid rgba(255,82,82,.28);color:var(--danger);padding:5px 12px;border-radius:7px;font-size:.73rem;cursor:pointer;font-family:var(--ff-head)}
/* SEARCH */
.search-bar{position:relative;margin-bottom:18px}
.search-bar input{width:100%;padding:13px 18px 13px 44px;background:var(--card);border:1.5px solid var(--border2);border-radius:14px;color:var(--text);font-family:var(--ff-head);font-size:.9rem;outline:none;transition:all .2s}
.search-bar input:focus{border-color:var(--fire);box-shadow:0 0 0 3px rgba(255,87,34,.1)}
.search-bar input::placeholder{color:var(--muted)}
.search-bar i{position:absolute;left:15px;top:50%;transform:translateY(-50%);color:var(--muted);font-size:.95rem}
.search-results{position:absolute;top:100%;left:0;right:0;background:var(--panel);border:1px solid var(--border2);border-radius:12px;box-shadow:var(--sh);z-index:400;max-height:380px;overflow-y:auto;display:none}
.search-results.on{display:block}
.sr-item{padding:10px 14px;cursor:pointer;display:flex;align-items:center;gap:10px;border-bottom:1px solid var(--border);transition:background .15s}
.sr-item:hover{background:rgba(255,87,34,.07)}
.sr-item:last-child{border-bottom:none}
.sr-ico{font-size:1.1rem;flex-shrink:0;width:26px;text-align:center}
.sr-name{font-size:.83rem;font-weight:600;flex:1}
.sr-cat{font-size:.64rem;color:var(--muted);background:var(--card2);padding:2px 6px;border-radius:4px}
.sr-portal{font-size:.68rem;color:var(--jade);display:flex;align-items:center;gap:3px;margin-left:auto}
/* AUTH */
.auth-wrap{min-height:100vh;background:linear-gradient(160deg,#040810,#0a1520,#051020);display:flex;align-items:center;justify-content:center;padding:20px;position:relative;overflow:hidden}
.auth-glow{position:absolute;border-radius:50%;filter:blur(100px);pointer-events:none}
.auth-glow-1{width:500px;height:500px;background:var(--fire);opacity:.06;top:-100px;right:-100px;animation:gDrift 9s ease-in-out infinite}
.auth-glow-2{width:400px;height:400px;background:var(--sky);opacity:.05;bottom:-80px;left:-80px;animation:gDrift 11s ease-in-out infinite reverse}
@keyframes gDrift{0%,100%{transform:translateY(0) scale(1)}50%{transform:translateY(-40px) scale(1.06)}}
.auth-card{position:relative;z-index:1;background:var(--panel);border:1px solid var(--border2);border-radius:var(--r3);padding:32px 24px;width:100%;max-width:400px;box-shadow:var(--sh);animation:cardRise .4s cubic-bezier(.4,0,.2,1)}
@keyframes cardRise{from{opacity:0;transform:translateY(22px) scale(.97)}to{opacity:1;transform:none}}
.auth-icon{display:inline-flex;align-items:center;justify-content:center;width:58px;height:58px;border-radius:14px;background:linear-gradient(135deg,var(--fire),#B71C1C);font-size:1.6rem;margin-bottom:10px;box-shadow:0 8px 26px rgba(255,87,34,.38)}
.auth-logo{text-align:center;margin-bottom:22px}
.auth-logo h1{font-size:1.45rem;font-weight:800}
.auth-logo p{color:var(--muted2);font-size:.75rem;margin-top:3px}
.auth-tabs{display:flex;background:var(--card);border-radius:9px;padding:3px;margin-bottom:18px}
.auth-tab{flex:1;padding:8px;text-align:center;border-radius:7px;cursor:pointer;font-size:.8rem;font-weight:500;color:var(--muted2);transition:all .15s}
.auth-tab.on{background:var(--fire);color:#fff;font-weight:700}
.auth-note{background:rgba(255,183,0,.07);border:1px solid rgba(255,183,0,.2);border-radius:8px;padding:8px 12px;font-size:.7rem;color:var(--warn);margin-bottom:13px;display:flex;gap:7px}
.fld{margin-bottom:11px}
.fld-lbl{font-size:.7rem;color:var(--muted2);margin-bottom:4px;display:block;font-weight:500}
.fld-wrap{position:relative}
.fld-ico{position:absolute;left:11px;top:50%;transform:translateY(-50%);color:var(--muted);font-size:.78rem;pointer-events:none}
.fld-in{width:100%;padding:10px 11px 10px 34px;background:var(--card2);border:1px solid var(--border2);border-radius:8px;color:var(--text);font-family:var(--ff-head);font-size:.83rem;outline:none;transition:all .15s}
.fld-in:focus{border-color:var(--fire);box-shadow:0 0 0 3px rgba(255,87,34,.1)}
.fld-in::placeholder{color:var(--muted)}
.fld-in.err{border-color:var(--danger)}
.fld-err{font-size:.66rem;color:#FF8A80;margin-top:2px;display:none}
.fld-err.on{display:block}
.fld-eye{position:absolute;right:10px;top:50%;transform:translateY(-50%);background:none;border:none;color:var(--muted);cursor:pointer;font-size:.83rem}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.pwd-bar{height:3px;border-radius:99px;background:var(--card2);margin-top:4px;overflow:hidden}
.pwd-fill{height:100%;border-radius:99px;transition:width .3s,background .3s;width:0}
.alert{border-radius:8px;padding:8px 12px;font-size:.76rem;margin-bottom:11px;display:none;align-items:center;gap:7px}
.alert.on{display:flex}
.alert-err{background:rgba(255,82,82,.09);border:1px solid rgba(255,82,82,.28);color:#FF8A80}
.alert-ok{background:rgba(0,230,118,.09);border:1px solid rgba(0,230,118,.28);color:#A5D6A7}
.alert-warn{background:rgba(255,183,0,.09);border:1px solid rgba(255,183,0,.28);color:var(--warn)}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;padding:10px 18px;border-radius:9px;font-family:var(--ff-head);font-size:.83rem;font-weight:600;cursor:pointer;border:none;transition:all .18s;width:100%}
.btn-fire{background:linear-gradient(135deg,var(--fire),#C62828);color:#fff;box-shadow:0 4px 16px rgba(255,87,34,.3)}
.btn-fire:hover{transform:translateY(-1px);box-shadow:0 8px 24px rgba(255,87,34,.4)}
.btn-fire:disabled{opacity:.45;cursor:not-allowed;transform:none!important}
.btn-outline{background:transparent;border:1px solid var(--border2);color:var(--muted2);width:auto}
.btn-outline:hover{border-color:var(--border3);color:var(--text)}
.btn-jade{background:linear-gradient(135deg,var(--jade),#00796B);color:#fff}
.btn-sm{padding:5px 12px;font-size:.73rem}
.btn-xs{padding:3px 9px;font-size:.68rem}
.spin{width:15px;height:15px;border:2px solid rgba(255,255,255,.2);border-top-color:var(--fire);border-radius:50%;animation:rot .6s linear infinite;flex-shrink:0}
@keyframes rot{to{transform:rotate(360deg)}}
/* STATS */
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:11px;margin-bottom:20px}
.stat-c{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:14px;position:relative;overflow:hidden;transition:all .2s}
.stat-c:hover{border-color:var(--border2);transform:translateY(-2px)}
.stat-c::after{content:'';position:absolute;top:0;left:0;right:0;height:2px;background:var(--ln,var(--fire))}
.stat-c:nth-child(2){--ln:var(--gold)}.stat-c:nth-child(3){--ln:var(--jade)}.stat-c:nth-child(4){--ln:var(--sky)}
.stat-lbl{font-size:.66rem;color:var(--muted2);text-transform:uppercase;letter-spacing:.05em}
.stat-v{font-size:1.7rem;font-weight:800;margin:4px 0 1px;line-height:1}
.stat-s{font-size:.66rem;color:var(--muted)}
.stat-ico{position:absolute;right:12px;top:50%;transform:translateY(-50%);font-size:1.8rem;opacity:.07}
/* SECTION */
.sec-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:13px;flex-wrap:wrap;gap:9px}
.sec-title{font-size:1.05rem;font-weight:700}
.ftabs{display:flex;gap:4px;flex-wrap:wrap}
.ft{padding:3px 11px;border-radius:99px;font-size:.71rem;cursor:pointer;border:1px solid var(--border);color:var(--muted2);background:transparent;font-family:var(--ff-head);transition:all .15s}
.ft:hover{border-color:var(--fire);color:var(--fire)}
.ft.on{background:var(--fire);border-color:var(--fire);color:#fff}
/* SERVICE GRID */
.svc-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:11px}
.svc-c{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:15px;cursor:pointer;transition:all .2s;position:relative;overflow:hidden}
.svc-c:hover{transform:translateY(-3px);border-color:rgba(255,87,34,.4);box-shadow:0 10px 32px rgba(0,0,0,.3)}
.svc-cat{font-size:.58rem;letter-spacing:.07em;text-transform:uppercase;color:var(--muted);margin-bottom:7px;display:flex;align-items:center;gap:4px}
.cat-dot{width:5px;height:5px;border-radius:50%}
.svc-name{font-size:.9rem;font-weight:700;line-height:1.3;margin-bottom:8px}
.svc-foot{display:flex;justify-content:space-between;align-items:center;padding-top:10px;border-top:1px solid var(--border)}
.svc-price{font-size:.95rem;font-weight:700;color:var(--fire)}
.svc-comm{font-size:.7rem;color:var(--jade)}
.auto-tag{position:absolute;top:9px;right:9px;background:rgba(0,191,165,.12);border:1px solid rgba(0,191,165,.3);color:var(--jade);font-size:.56rem;padding:2px 6px;border-radius:99px}
.portal-btn{display:inline-flex;align-items:center;gap:5px;margin-top:8px;padding:6px 12px;background:linear-gradient(135deg,var(--jade),#00796B);color:#fff;border-radius:7px;font-size:.72rem;font-weight:700;text-decoration:none;border:none;cursor:pointer;transition:all .15s;font-family:var(--ff-head)}
.portal-btn:hover{transform:translateY(-1px);box-shadow:0 4px 12px rgba(0,191,165,.35)}
/* JOB CARDS */
.job-list{display:flex;flex-direction:column;gap:8px}
.job-c{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:13px 15px;display:flex;align-items:center;gap:12px;transition:all .18s}
.job-c:hover{border-color:rgba(41,182,246,.4);transform:translateX(3px)}
.job-dept-ico{width:38px;height:38px;border-radius:8px;background:var(--card2);display:flex;align-items:center;justify-content:center;font-size:.95rem;flex-shrink:0}
.job-info{flex:1;min-width:0}
.job-title{font-size:.85rem;font-weight:700;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.job-meta{font-size:.66rem;color:var(--muted2);margin-top:2px}
.job-meta span{margin-right:9px}
.job-r{text-align:right;flex-shrink:0}
.job-fee{font-size:.78rem;color:var(--fire);font-weight:600}
.job-date{font-size:.65rem;color:var(--muted);margin-top:2px}
.hot-btn{display:inline-block;background:rgba(41,182,246,.1);border:1px solid rgba(41,182,246,.28);color:var(--sky);padding:3px 11px;border-radius:6px;font-size:.7rem;cursor:pointer;margin-top:4px;transition:all .15s;font-family:var(--ff-head);font-weight:500}
.hot-btn:hover{background:rgba(41,182,246,.2)}
.fire-tag{color:var(--fire2);font-size:.66rem;font-weight:700}
.new-tag{background:rgba(0,230,118,.12);border:1px solid rgba(0,230,118,.3);color:var(--success);font-size:.58rem;padding:2px 6px;border-radius:99px;font-weight:700}
.job-portal-link{display:inline-flex;align-items:center;gap:4px;padding:4px 10px;background:linear-gradient(135deg,var(--jade),#00796B);color:#fff;border-radius:6px;font-size:.7rem;font-weight:600;text-decoration:none;margin-top:4px;transition:all .15s}
/* TABLE */
.tbl-wrap{background:var(--card);border:1px solid var(--border);border-radius:var(--r);overflow:hidden}
table{width:100%;border-collapse:collapse}
thead tr{background:rgba(255,255,255,.025)}
th{padding:9px 13px;font-size:.62rem;letter-spacing:.06em;text-transform:uppercase;color:var(--muted);text-align:left;font-weight:500;border-bottom:1px solid var(--border)}
td{padding:10px 13px;font-size:.77rem;border-bottom:1px solid rgba(255,255,255,.03)}
tr:last-child td{border-bottom:none}
tr:hover td{background:rgba(255,255,255,.015)}
.pill{padding:2px 8px;border-radius:99px;font-size:.63rem;font-weight:600}
.p-pending{background:rgba(255,183,0,.12);color:var(--warn)}
.p-submitted{background:rgba(0,230,118,.12);color:var(--success)}
.p-failed{background:rgba(255,82,82,.12);color:var(--danger)}
.p-verified{background:rgba(0,191,165,.12);color:var(--jade)}
/* MODAL */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.72);backdrop-filter:blur(9px);z-index:500;display:none;align-items:center;justify-content:center;padding:14px}
.overlay.open{display:flex}
.modal{background:var(--panel);border:1px solid var(--border2);border-radius:var(--r3);width:100%;max-width:500px;max-height:92vh;overflow-y:auto;box-shadow:var(--sh);animation:mIn .22s cubic-bezier(.4,0,.2,1)}
@keyframes mIn{from{opacity:0;transform:scale(.95) translateY(12px)}to{opacity:1;transform:none}}
.modal-hd{padding:18px 20px 0;display:flex;justify-content:space-between;align-items:flex-start;position:sticky;top:0;background:var(--panel);z-index:2;padding-bottom:12px;border-bottom:1px solid var(--border)}
.modal-title{font-size:1.1rem;font-weight:700}
.modal-sub{font-size:.7rem;color:var(--muted2);margin-top:2px}
.modal-close{background:none;border:none;color:var(--muted);cursor:pointer;font-size:1rem;padding:3px;border-radius:5px}
.modal-body{padding:16px 20px 20px}
/* STEPS */
.steps{display:flex;align-items:center;margin-bottom:20px}
.step-n{display:flex;flex-direction:column;align-items:center;gap:3px;min-width:50px}
.step-dot{width:24px;height:24px;border-radius:50%;background:var(--card2);border:2px solid var(--border2);display:flex;align-items:center;justify-content:center;font-size:.72rem;font-weight:700}
.step-n.active .step-dot{background:var(--fire);border-color:var(--fire);color:#fff}
.step-n.done .step-dot{background:var(--jade);border-color:var(--jade);color:#fff}
.step-lbl{font-size:.58rem;color:var(--muted);white-space:nowrap}
.step-conn{flex:1;height:2px;background:var(--border2)}
.step-conn.done{background:var(--jade)}
/* UPLOAD */
.up-zone{border:2px dashed var(--border2);border-radius:var(--r);padding:24px;text-align:center;cursor:pointer;position:relative;transition:border-color .2s;margin-bottom:11px}
.up-zone:hover{border-color:var(--fire)}
.up-zone input{position:absolute;inset:0;opacity:0;cursor:pointer}
.u-ico{font-size:1.8rem;margin-bottom:7px;color:var(--muted)}
.u-txt{font-size:.83rem;font-weight:600;margin-bottom:3px}
.u-sub{font-size:.7rem;color:var(--muted)}
.up-ok{background:rgba(0,191,165,.1);border:1px solid rgba(0,191,165,.3);border-radius:8px;padding:8px 12px;font-size:.78rem;color:var(--jade);display:none;align-items:center;gap:7px}
.up-ok.on{display:flex}
.up-prog{height:5px;background:var(--card2);border-radius:99px;overflow:hidden;margin-top:7px;display:none}
.up-prog.on{display:block}
.up-prog-fill{height:100%;background:linear-gradient(90deg,var(--jade),var(--sky));border-radius:99px;transition:width .3s}
/* QR/PAYMENT */
.qr-box{text-align:center;padding:12px 0}
.qr-box canvas,.qr-box img{width:160px!important;height:160px!important;border-radius:10px;border:3px solid var(--fire);padding:4px;background:#fff;display:block;margin:0 auto}
.qr-amt{font-size:1.9rem;font-weight:800;color:var(--fire);margin:10px 0 2px}
.qr-upi{font-size:.74rem;color:var(--muted2);font-family:var(--ff-mono)}
.qr-txn{font-family:var(--ff-mono);font-size:.67rem;background:var(--card2);border-radius:6px;padding:5px 9px;margin-top:8px;color:var(--muted2);word-break:break-all;cursor:pointer}
.pay-breakdown{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:11px;margin:11px 0;font-size:.76rem}
.pb-row{display:flex;justify-content:space-between;padding:3px 0;border-bottom:1px solid var(--border)}
.pb-row:last-child{border-bottom:none;font-weight:700;padding-top:7px}
.utr-wrap{background:rgba(255,183,0,.07);border:1px solid rgba(255,183,0,.2);border-radius:8px;padding:11px;margin:9px 0;font-size:.76rem}
.success-scr{text-align:center;padding:16px 0}
.s-ico{font-size:3rem;animation:pop .4s cubic-bezier(.34,1.56,.64,1)}
@keyframes pop{from{transform:scale(.2);opacity:0}to{transform:scale(1);opacity:1}}
.s-title{font-size:1.3rem;font-weight:800;color:var(--jade);margin-top:9px}
.track-box{background:var(--card2);border:1px solid var(--border);border-radius:8px;padding:11px;margin:11px 0;text-align:left}
.track-box .tl{font-size:.64rem;color:var(--muted)}
.track-box .tv{font-family:var(--ff-mono);font-size:.83rem;color:var(--fire);margin-top:2px}
/* EARNINGS */
.calc-grid{display:grid;grid-template-columns:1fr 1fr;gap:13px;margin-bottom:18px}
.calc-out{background:var(--card2);border:1px solid var(--border);border-radius:var(--r);padding:14px}
.calc-out .cl{font-size:.66rem;color:var(--muted2);text-transform:uppercase;letter-spacing:.05em}
.calc-out .cv{font-size:1.5rem;font-weight:800;margin-top:4px}
/* ADMIN */
.admin-card{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:15px}
.admin-card h4{font-size:.8rem;font-weight:700;margin-bottom:12px;color:var(--muted2)}
.franchise-item{display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid var(--border);font-size:.76rem}
.franchise-item:last-child{border-bottom:none}
.fi-name{font-weight:600}
.fi-stat{text-align:right}
.fi-stat .v{color:var(--jade)}
.fi-stat .s{font-size:.63rem;color:var(--muted)}
.badge-admin{background:rgba(255,183,0,.15);border:1px solid rgba(255,183,0,.3);color:var(--gold);font-size:.58rem;padding:2px 6px;border-radius:99px;font-weight:600}
/* OCR */
.ocr-result{background:var(--card2);border:1px solid var(--border);border-radius:var(--r);padding:13px;margin-top:10px;display:none}
.ocr-result.on{display:block}
.ocr-row{display:flex;justify-content:space-between;padding:4px 0;border-bottom:1px solid var(--border);font-size:.75rem}
.ocr-row:last-child{border-bottom:none}
.ocr-row .l{color:var(--muted2)}.ocr-row .v{color:var(--jade);font-weight:600}
/* CAT TILES */
.cat-tiles{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:10px;margin-bottom:20px}
.cat-tile{background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:14px 12px;text-align:center;cursor:pointer;transition:all .18s}
.cat-tile:hover{border-color:var(--fire);transform:translateY(-2px)}
.cat-tile .ico{font-size:1.7rem;margin-bottom:6px}
.cat-tile .nm{font-size:.75rem;font-weight:700}
.cat-tile .cnt{font-size:.6rem;color:var(--muted);margin-top:2px}
/* TOASTS */
.toasts{position:fixed;bottom:18px;right:18px;z-index:999;display:flex;flex-direction:column;gap:8px;pointer-events:none}
.toast{background:var(--card2);border:1px solid var(--border2);border-radius:8px;padding:10px 14px;font-size:.77rem;min-width:230px;display:flex;align-items:center;gap:8px;animation:tIn .26s ease;pointer-events:all;box-shadow:var(--sh2);max-width:320px}
.toast.ok{border-color:rgba(0,230,118,.35)}.toast.err{border-color:rgba(255,82,82,.35)}.toast.warn{border-color:rgba(255,183,0,.35)}
@keyframes tIn{from{opacity:0;transform:translateX(20px)}to{opacity:1;transform:none}}
/* LOADER */
.loader{position:fixed;inset:0;background:var(--ink);display:flex;flex-direction:column;align-items:center;justify-content:center;z-index:9999;gap:13px;transition:opacity .4s}
.loader.off{opacity:0;pointer-events:none}
.loader-bar{width:190px;height:3px;background:var(--card2);border-radius:99px;overflow:hidden}
.loader-fill{height:100%;background:linear-gradient(90deg,var(--fire),var(--gold));border-radius:99px;animation:lBar 1.5s ease-in-out infinite}
@keyframes lBar{0%{transform:translateX(-100%)}100%{transform:translateX(200px)}}
/* SECURITY STRIP */
.sec-strip{display:flex;align-items:center;justify-content:center;gap:16px;flex-wrap:wrap;background:rgba(0,230,118,.04);border:1px solid rgba(0,230,118,.1);border-radius:var(--r);padding:8px 13px;margin-bottom:18px;font-size:.67rem;color:var(--jade)}
.sec-strip span{display:flex;align-items:center;gap:3px}
/* DP (Data Panel) */
#__dp__{position:fixed;bottom:68px;right:11px;z-index:99999;width:264px;font-family:Arial,sans-serif}
.dp-inner{background:#0C1220;border:1.5px solid rgba(255,87,34,.45);border-radius:13px;box-shadow:0 16px 52px rgba(0,0,0,.75);overflow:hidden}
.dp-hd{background:linear-gradient(135deg,#FF5722,#B71C1C);padding:9px 12px;display:flex;align-items:center;cursor:grab;user-select:none}
.dp-hd:active{cursor:grabbing}
.dp-ht{color:#fff;font-weight:700;font-size:.8rem;flex:1}
.dp-min,.dp-close{background:none;border:none;color:rgba(255,255,255,.75);cursor:pointer;font-size:.88rem;padding:0 3px}
.dp-bd{padding:9px 11px;max-height:320px;overflow-y:auto}
.dp-svc{font-size:.63rem;color:var(--muted);text-transform:uppercase;letter-spacing:.06em;margin-bottom:5px;padding-bottom:4px;border-bottom:1px solid rgba(255,255,255,.07)}
.dp-row{display:flex;align-items:center;gap:5px;padding:4px 0;border-bottom:1px solid rgba(255,255,255,.05)}
.dp-row:last-child{border-bottom:none}
.dp-lbl{font-size:.63rem;color:var(--muted);min-width:50px;flex-shrink:0}
.dp-val{font-size:.76rem;color:var(--text);font-weight:600;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.dp-cp{background:rgba(255,255,255,.08);border:none;border-radius:4px;padding:2px 6px;font-size:.66rem;cursor:pointer;color:var(--muted2);transition:all .15s}
.dp-cp:hover{background:rgba(0,191,165,.25);color:var(--jade)}
.dp-ft{padding:7px 11px;border-top:1px solid rgba(255,255,255,.07);display:flex;gap:5px}
.dp-ft button{flex:1;padding:5px;border-radius:6px;font-size:.68rem;font-weight:600;cursor:pointer;border:none;font-family:inherit}
.dp-btn-copy{background:rgba(255,87,34,.15);color:var(--fire2)}
.dp-btn-hide{background:rgba(255,255,255,.06);color:var(--muted2)}
.dp-minimized .dp-bd,.dp-minimized .dp-ft{display:none!important}
.fd-list{display:flex;flex-direction:column;gap:3px}
.fd-row{display:flex;align-items:center;gap:7px;padding:6px 9px;background:rgba(255,255,255,.03);border-radius:7px;border:1px solid rgba(255,255,255,.05)}
.fd-k{font-size:.68rem;color:var(--muted);min-width:60px;flex-shrink:0;font-weight:500}
.fd-v{font-size:.78rem;color:var(--text);font-weight:600;flex:1;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.fd-copy{background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.12);border-radius:5px;padding:2px 6px;font-size:.66rem;cursor:pointer;color:var(--muted2);transition:all .15s}
.fd-copy:hover{background:rgba(0,191,165,.2);color:var(--jade)}
/* CAT COLORS */
.cat-central .cat-dot{background:#7C4DFF}.cat-state .cat-dot{background:var(--fire)}.cat-job .cat-dot{background:var(--sky)}.cat-utility .cat-dot{background:var(--gold)}.cat-travel .cat-dot{background:#EC407A}.cat-financial .cat-dot{background:var(--jade)}.cat-food .cat-dot{background:#FF7043}.cat-shopping .cat-dot{background:#26C6DA}
@media(max-width:1024px){.stats{grid-template-columns:1fr 1fr}}
@media(max-width:768px){.sidebar{transform:translateX(-100%);width:240px!important}.sidebar.mob-open{transform:translateX(0)}.main-area{margin-left:0!important}.stats{grid-template-columns:1fr 1fr}.row2{grid-template-columns:1fr}.calc-grid{grid-template-columns:1fr}}
@media(max-width:480px){.stats{grid-template-columns:1fr}.page{padding:13px}}
.view{animation:viewIn .2s ease}
@keyframes viewIn{from{opacity:0;transform:translateY(7px)}to{opacity:1;transform:none}}
</style>
</head>
<body>
<div class="loader" id="loader"><div style="font-size:2.2rem">🧠</div><div style="font-size:1.5rem;font-weight:800">CyberAce Quantum</div><div class="loader-bar"><div class="loader-fill"></div></div><div style="font-size:.7rem;color:var(--muted)">Connecting…</div></div>
<div class="toasts" id="toasts"></div>
<div class="overlay" id="overlay" onclick="if(event.target.id==='overlay')closeModal()">
  <div class="modal"><div class="modal-hd"><div><div class="modal-title" id="mTitle">Apply</div><div class="modal-sub" id="mSub"></div></div><button class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></button></div><div class="modal-body" id="mBody"></div></div>
</div>
<div id="root"></div>
<script>
'use strict';
const FB_CFG={apiKey:"AIzaSyBIebPXVjzVBZl380ZCELg2LUSCLr-6QrE",authDomain:"neurocoin-ntc.firebaseapp.com",databaseURL:"https://neurocoin-ntc-default-rtdb.firebaseio.com",projectId:"neurocoin-ntc",storageBucket:"neurocoin-ntc.firebasestorage.app",messagingSenderId:"1040732555800",appId:"1:1040732555800:web:55e63b5ff81781c6b1916d",measurementId:"G-6X8T0YQTQ3"};
const UPI="bonagirispinoj-1@oksbi",ADMIN_EMAIL="bonagirispinoj@gmail.com",PLATFORM_CUT=0.15,SUB_FEE=2000;
firebase.initializeApp(FB_CFG);
const auth=firebase.auth(),db=firebase.firestore(),storage=firebase.storage();
db.enablePersistence({synchronizeTabs:true}).catch(()=>{});

const S={
  esc(s){if(s==null)return'';const d=document.createElement('div');d.textContent=String(s);return d.innerHTML},
  clean(s,n=500){return String(s||'').replace(/<[^>]*>/g,'').replace(/[`\\]/g,'').trim().slice(0,n)},
  isEmail:v=>/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test((v||'').trim()),
  isPhone:v=>/^[6-9]\d{9}$/.test((v||'').replace(/\s/g,'')),
  isAadhaar:v=>/^\d{12}$/.test((v||'').replace(/\s/g,'')),
  isPAN:v=>/^[A-Z]{5}[0-9]{4}[A-Z]$/.test((v||'').trim().toUpperCase()),
  pwdStr(p){let s=0;if(p.length>=8)s++;if(/[A-Z]/.test(p))s++;if(/\d/.test(p))s++;if(/[!@#$%^&*\-_]/.test(p))s++;return s},
  _rl:{},rateLimit(k,m,ms){const n=Date.now(),e=this._rl[k]||{n:0,t:n};if(n-e.t>ms){e.n=0;e.t=n;}e.n++;this._rl[k]=e;return e.n<=m},
  token(n=12){const a=new Uint8Array(n);crypto.getRandomValues(a);return Array.from(a,b=>b.toString(16).padStart(2,'0')).join('').toUpperCase().slice(0,n)}
};
const A={user:null,isAdmin:false,svc:null,txnId:null,formData:{},uploadedFiles:{}};

/* ━━━ MASSIVE SERVICES DATA ━━━ */
const SVCS=[
/* CENTRAL GOVT */
{id:'aadhaar_update',name:'Aadhaar Update / Correction',cat:'central',price:150,comm:100,url:'https://myaadhaar.uidai.gov.in/',tags:['aadhaar','uidai','update','address change']},
{id:'aadhaar_download',name:'Aadhaar Download / e-Aadhaar',cat:'central',price:50,comm:50,url:'https://myaadhaar.uidai.gov.in/',tags:['aadhaar','download','eaadhaar']},
{id:'aadhaar_new',name:'Aadhaar New Enrollment',cat:'central',price:100,comm:100,url:'https://uidai.gov.in/',tags:['aadhaar','new','enroll','uidai']},
{id:'pan_new',name:'PAN Card (New)',cat:'central',price:200,comm:150,url:'https://www.onlineservices.nsdl.com/paam/endUserRegisterContact.html',tags:['pan','income tax','nsdl','new']},
{id:'pan_correction',name:'PAN Card Correction',cat:'central',price:150,comm:100,url:'https://www.onlineservices.nsdl.com/',tags:['pan','correction','update']},
{id:'voter_new',name:'Voter ID (Form 6 - New)',cat:'central',price:100,comm:100,url:'https://voters.eci.gov.in/',tags:['voter','id','eci','election','form 6']},
{id:'voter_update',name:'Voter ID Update (Form 8)',cat:'central',price:100,comm:100,url:'https://voters.eci.gov.in/',tags:['voter','update','form 8','address']},
{id:'voter_pvt',name:'Voter ID Transfer (Form 8A)',cat:'central',price:100,comm:100,url:'https://voters.eci.gov.in/',tags:['voter','transfer','migration']},
{id:'passport_fresh',name:'Passport (Fresh)',cat:'central',price:500,comm:200,url:'https://passportindia.gov.in/',tags:['passport','fresh','new','travel']},
{id:'passport_renew',name:'Passport Renewal',cat:'central',price:400,comm:150,url:'https://passportindia.gov.in/',tags:['passport','renew','renewal']},
{id:'passport_tatkal',name:'Passport Tatkal',cat:'central',price:700,comm:200,url:'https://passportindia.gov.in/',tags:['passport','tatkal','urgent']},
{id:'digilocker',name:'DigiLocker Account',cat:'central',price:50,comm:50,url:'https://digilocker.gov.in/',tags:['digilocker','documents','digital']},
{id:'epfo_uan',name:'EPFO UAN Activation',cat:'central',price:100,comm:100,url:'https://unifiedportal-mem.epfindia.gov.in/',tags:['epfo','uan','pf','provident fund']},
{id:'epfo_claim',name:'PF Withdrawal / Claim',cat:'central',price:150,comm:150,url:'https://unifiedportal-mem.epfindia.gov.in/',tags:['pf','epfo','withdrawal','claim']},
{id:'eshram',name:'e-Shram Card',cat:'central',price:100,comm:100,url:'https://eshram.gov.in/',tags:['eshram','labour','worker','card']},
{id:'udyam',name:'Udyam (MSME) Registration',cat:'central',price:200,comm:200,url:'https://udyamregistration.gov.in/',tags:['udyam','msme','business','registration']},
{id:'pmay',name:'PMAY Housing Application',cat:'central',price:200,comm:200,url:'https://pmaymis.gov.in/',tags:['pmay','housing','pradhan mantri awas']},
{id:'pm_kisan',name:'PM Kisan Registration',cat:'central',price:100,comm:100,url:'https://pmkisan.gov.in/',tags:['pm kisan','farmer','agriculture']},
{id:'ayushman',name:'Ayushman Bharat (PMJAY)',cat:'central',price:100,comm:100,url:'https://beneficiary.nha.gov.in/',tags:['ayushman','pmjay','health','insurance']},
{id:'nsp',name:'NSP Scholarship',cat:'central',price:100,comm:100,url:'https://scholarships.gov.in/',tags:['nsp','scholarship','student','education']},
{id:'nps',name:'NPS Account Opening',cat:'central',price:300,comm:300,url:'https://enps.nsdl.com/',tags:['nps','pension','retirement']},
{id:'indiapost',name:'India Post / PLI Account',cat:'central',price:100,comm:100,url:'https://www.indiapost.gov.in/',tags:['post office','pli','savings']},
{id:'itr',name:'ITR / Income Tax Filing',cat:'central',price:300,comm:300,url:'https://eportal.incometax.gov.in/',tags:['itr','income tax','filing','return']},
{id:'gst_reg',name:'GST Registration',cat:'central',price:500,comm:500,url:'https://www.gst.gov.in/',tags:['gst','registration','business']},
{id:'gst_return',name:'GST Return Filing',cat:'central',price:300,comm:300,url:'https://www.gst.gov.in/',tags:['gst','return','filing']},
{id:'mudra',name:'PMMY Mudra Loan',cat:'central',price:500,comm:500,url:'https://udyamimitra.in/',tags:['mudra','loan','pmmy','business']},
{id:'pmsvaniidhi',name:'PM SVANidhi (Street Vendor)',cat:'central',price:200,comm:200,url:'https://pmsvanidhi.mohua.gov.in/',tags:['svanidhi','street vendor','loan']},
{id:'birth_cert',name:'Birth Certificate (Central)',cat:'central',price:100,comm:100,url:'https://crsorgi.gov.in/',tags:['birth','certificate']},
{id:'death_cert',name:'Death Certificate',cat:'central',price:100,comm:100,url:'https://crsorgi.gov.in/',tags:['death','certificate']},
/* STATE — TELANGANA */
{id:'meeseva_ts',name:'MeeSeva (Telangana)',cat:'state',price:50,comm:50,url:'https://ts.meeseva.gov.in/',tags:['meeseva','telangana','ts','caste','income','birth']},
{id:'tgpsc',name:'TGPSC Job Application',cat:'state',price:200,comm:200,url:'https://tgpsc.telangana.gov.in/',tags:['tgpsc','telangana psc','group 1','2','3','4']},
{id:'ghmc',name:'GHMC Services',cat:'state',price:100,comm:100,url:'https://ghmc.gov.in/',tags:['ghmc','hyderabad','municipality','property tax']},
{id:'ts_caste',name:'Caste Certificate (TS)',cat:'state',price:100,comm:100,url:'https://ts.meeseva.gov.in/',tags:['caste','certificate','telangana','sc st obc']},
{id:'ts_income',name:'Income Certificate (TS)',cat:'state',price:100,comm:100,url:'https://ts.meeseva.gov.in/',tags:['income','certificate','telangana']},
{id:'ts_residence',name:'Residence Certificate (TS)',cat:'state',price:100,comm:100,url:'https://ts.meeseva.gov.in/',tags:['residence','domicile','certificate','ts']},
{id:'ts_nativity',name:'Nativity Certificate (TS)',cat:'state',price:100,comm:100,url:'https://ts.meeseva.gov.in/',tags:['nativity','certificate','ts']},
{id:'ts_ration',name:'Ration Card (TS)',cat:'state',price:150,comm:150,url:'https://ts.meeseva.gov.in/',tags:['ration card','food','ts']},
/* STATE — ANDHRA PRADESH */
{id:'ap_edistrict',name:'eDistrict AP Services',cat:'state',price:50,comm:50,url:'https://edistrict.ap.gov.in/',tags:['edistrict','andhra pradesh','ap','certificate']},
{id:'ap_meeseva',name:'MeeSeva (AP)',cat:'state',price:50,comm:50,url:'https://ap.meeseva.gov.in/',tags:['meeseva','andhra pradesh','ap']},
/* STATE — OTHER */
{id:'mah_mahaonline',name:'MahaOnline (Maharashtra)',cat:'state',price:100,comm:100,url:'https://aaplesarkar.mahaonline.gov.in/',tags:['maharashtra','mahaonline','aaplesarkar']},
{id:'kar_seva',name:'Seva Sindhu (Karnataka)',cat:'state',price:100,comm:100,url:'https://sevasindhu.karnataka.gov.in/',tags:['karnataka','seva sindhu','certificate']},
{id:'tn_services',name:'TN eSevai (Tamil Nadu)',cat:'state',price:100,comm:100,url:'https://www.tn.gov.in/',tags:['tamil nadu','tn','esevai']},
{id:'up_services',name:'UP e-District',cat:'state',price:100,comm:100,url:'https://edistrict.up.gov.in/',tags:['uttar pradesh','up','edistrict']},
{id:'raj_emitra',name:'eMitra (Rajasthan)',cat:'state',price:100,comm:100,url:'https://emitra.rajasthan.gov.in/',tags:['rajasthan','emitra','certificate']},
{id:'wb_services',name:'West Bengal Services',cat:'state',price:100,comm:100,url:'https://edistrict.wb.gov.in/',tags:['west bengal','wb','certificate']},
/* RTO / DRIVING */
{id:'dl_new',name:'Driving Licence (New)',cat:'state',price:500,comm:150,url:'https://parivahan.gov.in/parivahan/',tags:['driving licence','dl','new','rto']},
{id:'dl_renew',name:'DL Renewal',cat:'state',price:400,comm:150,url:'https://sarathi.parivahan.gov.in/',tags:['driving licence','renewal','dl renew']},
{id:'learner',name:"Learner's Licence (LLR)",cat:'state',price:300,comm:150,url:'https://sarathi.parivahan.gov.in/',tags:['learner licence','llr','test','rto']},
{id:'rc',name:'Vehicle RC',cat:'state',price:400,comm:150,url:'https://vahan.parivahan.gov.in/',tags:['rc','vehicle','registration certificate']},
{id:'rc_tf',name:'RC Transfer',cat:'state',price:500,comm:150,url:'https://vahan.parivahan.gov.in/',tags:['rc transfer','vehicle transfer','ownership']},
{id:'puc',name:'Pollution Certificate (PUC)',cat:'state',price:200,comm:100,url:'https://vahan.parivahan.gov.in/',tags:['puc','pollution','emission']},
{id:'challan',name:'Traffic Challan Payment',cat:'state',price:50,comm:50,url:'https://echallan.parivahan.gov.in/',tags:['challan','traffic','fine','payment']},
{id:'vahan_status',name:'Vehicle Status / Vahan',cat:'state',price:50,comm:50,url:'https://vahan.parivahan.gov.in/',tags:['vahan','vehicle status','check']},
/* JOBS */
{id:'upsc',name:'UPSC Civil Services',cat:'job',price:200,comm:200,url:'https://upsconline.gov.in/',tags:['upsc','ias','ips','civil services']},
{id:'ssc_cgl',name:'SSC CGL',cat:'job',price:150,comm:150,url:'https://ssc.gov.in/',tags:['ssc','cgl','staff selection']},
{id:'ssc_chsl',name:'SSC CHSL',cat:'job',price:150,comm:150,url:'https://ssc.gov.in/',tags:['ssc','chsl']},
{id:'ssc_mts',name:'SSC MTS',cat:'job',price:150,comm:150,url:'https://ssc.gov.in/',tags:['ssc','mts','multi tasking']},
{id:'rrb_ntpc',name:'Railway NTPC',cat:'job',price:150,comm:150,url:'https://rrbapply.gov.in/',tags:['rrb','ntpc','railway']},
{id:'rrb_gd',name:'Railway Group D',cat:'job',price:150,comm:150,url:'https://rrbapply.gov.in/',tags:['rrb','group d','railway']},
{id:'rrb_je',name:'Railway JE / SE',cat:'job',price:150,comm:150,url:'https://rrbapply.gov.in/',tags:['rrb','je','junior engineer']},
{id:'ibps_po',name:'IBPS PO',cat:'job',price:150,comm:150,url:'https://ibps.in/',tags:['ibps','po','bank','probationary officer']},
{id:'ibps_clerk',name:'IBPS Clerk',cat:'job',price:150,comm:150,url:'https://ibps.in/',tags:['ibps','clerk','bank']},
{id:'ibps_so',name:'IBPS SO',cat:'job',price:150,comm:150,url:'https://ibps.in/',tags:['ibps','so','specialist officer']},
{id:'sbi_po',name:'SBI PO',cat:'job',price:150,comm:150,url:'https://www.sbi.co.in/careers',tags:['sbi','po','bank']},
{id:'sbi_clerk',name:'SBI Clerk',cat:'job',price:150,comm:150,url:'https://www.sbi.co.in/careers',tags:['sbi','clerk','bank']},
{id:'neet',name:'NEET UG',cat:'job',price:150,comm:150,url:'https://neet.nta.nic.in/',tags:['neet','medical','mbbs','ug']},
{id:'jee',name:'JEE Main',cat:'job',price:150,comm:150,url:'https://jeemain.nta.nic.in/',tags:['jee','engineering','nit','iit']},
{id:'ctet',name:'CTET',cat:'job',price:120,comm:120,url:'https://ctet.nic.in/',tags:['ctet','teacher','teaching']},
{id:'tgpsc_job',name:'TGPSC Group I/II/III',cat:'job',price:150,comm:150,url:'https://tgpsc.telangana.gov.in/',tags:['tgpsc','telangana psc','group 1 2 3']},
{id:'tstet',name:'TSTET (Telangana TET)',cat:'job',price:120,comm:120,url:'https://tstet.cgg.gov.in/',tags:['tstet','telangana tet','teacher']},
{id:'police',name:'Police Constable / SI',cat:'job',price:150,comm:150,url:'https://tslprb.in/',tags:['police','constable','si','tslprb']},
{id:'defence',name:'Indian Army / Navy / Air Force',cat:'job',price:150,comm:150,url:'https://joinindianarmy.nic.in/',tags:['army','navy','air force','defence','military']},
{id:'ap_psc',name:'APPSC Group I/II',cat:'job',price:150,comm:150,url:'https://psc.ap.gov.in/',tags:['appsc','andhra pradesh psc','group 1 2']},
/* UTILITIES */
{id:'elec',name:'Electricity Bill Pay',cat:'utility',price:20,comm:20,url:'https://www.billdesk.com/web/merchant-list',tags:['electricity','bill','payment','tsecl','apspdcl']},
{id:'gas_book',name:'LPG Gas Cylinder Booking',cat:'utility',price:25,comm:25,url:'https://ebharatgas.com/',tags:['gas','lpg','cylinder','booking','bharatgas']},
{id:'mobile',name:'Mobile Recharge',cat:'utility',price:15,comm:15,url:'https://prepaid.jio.com/',tags:['mobile','recharge','jio','airtel','vi']},
{id:'dth',name:'DTH Recharge',cat:'utility',price:15,comm:15,url:'https://www.tataplay.com/recharge',tags:['dth','tv','recharge','tata play','dish']},
{id:'water',name:'Water Bill Pay',cat:'utility',price:20,comm:20,url:'https://www.hmwssb.gov.in/',tags:['water','bill','hmwssb']},
{id:'fastag',name:'FASTag Recharge',cat:'utility',price:25,comm:25,url:'https://fastag.ihmcl.com/',tags:['fastag','toll','highway','recharge']},
{id:'broadband',name:'Broadband / Internet Bill',cat:'utility',price:15,comm:15,url:'https://www.bsnl.co.in/',tags:['broadband','internet','bill','bsnl']},
/* TRAVEL */
{id:'irctc',name:'Train Ticket (IRCTC)',cat:'travel',price:30,comm:30,url:'https://www.irctc.co.in/',tags:['train','irctc','ticket','railway','booking']},
{id:'flight',name:'Flight Booking',cat:'travel',price:199,comm:199,url:'https://www.makemytrip.com/flights/',tags:['flight','air ticket','booking','makemytrip']},
{id:'bus',name:'Bus Ticket (Redbus)',cat:'travel',price:20,comm:20,url:'https://www.redbus.in/',tags:['bus','ticket','redbus','booking']},
{id:'ola',name:'Ola Cab Booking',cat:'travel',price:20,comm:20,url:'https://book.olacabs.com/',tags:['ola','cab','taxi','booking']},
{id:'uber',name:'Uber Cab Booking',cat:'travel',price:20,comm:20,url:'https://m.uber.com/',tags:['uber','cab','taxi']},
{id:'rapido',name:'Rapido Bike / Auto',cat:'travel',price:15,comm:15,url:'https://rapido.bike/',tags:['rapido','bike','auto','booking']},
{id:'cinema',name:'Cinema Ticket (BookMyShow)',cat:'travel',price:30,comm:30,url:'https://in.bookmyshow.com/',tags:['cinema','movie','ticket','bookmyshow']},
{id:'hotel',name:'Hotel Booking (MakeMyTrip)',cat:'travel',price:50,comm:50,url:'https://www.makemytrip.com/hotels/',tags:['hotel','room','booking','makemytrip']},
/* FINANCIAL */
{id:'insure',name:'Insurance Application',cat:'financial',price:200,comm:200,url:'https://www.policybazaar.com/',tags:['insurance','policy','life health motor']},
{id:'lic',name:'LIC Policy / Premium',cat:'financial',price:100,comm:100,url:'https://licindia.in/',tags:['lic','life insurance','premium','policy']},
{id:'loan',name:'Loan Application',cat:'financial',price:500,comm:500,url:'https://www.paisabazaar.com/',tags:['loan','personal home car','paisabazaar']},
{id:'demat',name:'Demat / Trading Account',cat:'financial',price:150,comm:150,url:'https://zerodha.com/open-account',tags:['demat','zerodha','trading','groww','stock']},
{id:'groww',name:'Groww Investment Account',cat:'financial',price:100,comm:100,url:'https://groww.in/',tags:['groww','mutual fund','investment','sip']},
{id:'fd',name:'Fixed Deposit (Post Office)',cat:'financial',price:100,comm:100,url:'https://www.indiapost.gov.in/',tags:['fd','fixed deposit','post office']},
/* FOOD */
{id:'swiggy',name:'Swiggy Food Order',cat:'food',price:20,comm:20,url:'https://www.swiggy.com/',tags:['swiggy','food','delivery','order']},
{id:'zomato',name:'Zomato Food Order',cat:'food',price:20,comm:20,url:'https://www.zomato.com/',tags:['zomato','food','delivery','order','restaurant']},
/* SHOPPING */
{id:'flipkart',name:'Flipkart Order',cat:'shopping',price:20,comm:20,url:'https://www.flipkart.com/',tags:['flipkart','shopping','order','ecommerce']},
{id:'amazon',name:'Amazon India Order',cat:'shopping',price:20,comm:20,url:'https://www.amazon.in/',tags:['amazon','shopping','order','ecommerce']},
{id:'meesho',name:'Meesho Order',cat:'shopping',price:15,comm:15,url:'https://www.meesho.com/',tags:['meesho','shopping','reselling']},
{id:'myntra',name:'Myntra Fashion',cat:'shopping',price:20,comm:20,url:'https://www.myntra.com/',tags:['myntra','fashion','clothes','shopping']},
{id:'nykaa',name:'Nykaa Beauty / Fashion',cat:'shopping',price:20,comm:20,url:'https://www.nykaa.com/',tags:['nykaa','beauty','cosmetics','shopping']},
{id:'snapdeal',name:'Snapdeal Order',cat:'shopping',price:15,comm:15,url:'https://www.snapdeal.com/',tags:['snapdeal','shopping','order']},
];

/* ━━━ 2026 JOB NOTIFICATIONS ━━━ */
const JOBS=[
{id:'upsc26',title:'UPSC CSE 2026',dept:'UPSC',cat:'central',posts:1056,date:'2026-02-15',fee:100,hot:12000,url:'https://upsconline.gov.in/',isNew:true},
{id:'ssc_cgl26',title:'SSC CGL 2026',dept:'SSC',cat:'central',posts:17000,date:'2026-03-10',fee:100,hot:18000,url:'https://ssc.gov.in/',isNew:true},
{id:'ssc_chsl26',title:'SSC CHSL 2026',dept:'SSC',cat:'central',posts:8000,date:'2026-04-01',fee:100,hot:9500,url:'https://ssc.gov.in/',isNew:true},
{id:'rrb_ntpc26',title:'Railway NTPC 2026',dept:'RRB',cat:'central',posts:12000,date:'2026-03-20',fee:100,hot:22000,url:'https://rrbapply.gov.in/',isNew:true},
{id:'rrb_gd26',title:'Railway Group D 2026',dept:'RRB',cat:'central',posts:32000,date:'2026-04-15',fee:100,hot:28000,url:'https://rrbapply.gov.in/',isNew:true},
{id:'ibps_po26',title:'IBPS PO 2026',dept:'IBPS',cat:'banking',posts:4500,date:'2026-05-01',fee:850,hot:11000,url:'https://ibps.in/',isNew:true},
{id:'ibps_cl26',title:'IBPS Clerk 2026',dept:'IBPS',cat:'banking',posts:6500,date:'2026-05-15',fee:800,hot:9000,url:'https://ibps.in/',isNew:true},
{id:'sbi_po26',title:'SBI PO 2026',dept:'SBI',cat:'banking',posts:600,date:'2026-04-10',fee:750,hot:7000,url:'https://www.sbi.co.in/careers',isNew:true},
{id:'sbi_clerk26',title:'SBI Clerk 2026',dept:'SBI',cat:'banking',posts:1200,date:'2026-04-20',fee:750,hot:6500,url:'https://www.sbi.co.in/careers',isNew:true},
{id:'tgpsc26',title:'TGPSC Group-I 2026',dept:'TGPSC',cat:'state',posts:503,date:'2026-05-01',fee:200,hot:8000,url:'https://tgpsc.telangana.gov.in/',isNew:true},
{id:'tstet26',title:'TSTET 2026 (TG Teachers)',dept:'TSTET',cat:'state',posts:0,date:'2026-06-01',fee:200,hot:5500,url:'https://tstet.cgg.gov.in/',isNew:true},
{id:'tslprb26',title:'TS Police SI/Constable 2026',dept:'TSLPRB',cat:'state',posts:2000,date:'2026-06-15',fee:200,hot:9000,url:'https://tslprb.in/',isNew:true},
{id:'neet26',title:'NEET UG 2026',dept:'NTA',cat:'medical',posts:0,date:'2026-05-03',fee:1700,hot:45000,url:'https://neet.nta.nic.in/',isNew:true},
{id:'jee26',title:'JEE Main 2026 Session 1',dept:'NTA',cat:'engg',posts:0,date:'2026-01-22',fee:900,hot:32000,url:'https://jeemain.nta.nic.in/',isNew:true},
{id:'jee26s2',title:'JEE Main 2026 Session 2',dept:'NTA',cat:'engg',posts:0,date:'2026-04-01',fee:900,hot:30000,url:'https://jeemain.nta.nic.in/',isNew:true},
{id:'ctet26',title:'CTET 2026',dept:'CBSE',cat:'teaching',posts:0,date:'2026-07-01',fee:1000,hot:4500,url:'https://ctet.nic.in/',isNew:true},
{id:'nsp26',title:'NSP Scholarship 2025-26',dept:'MoE',cat:'scholar',posts:0,date:'2026-03-31',fee:0,hot:9000,url:'https://scholarships.gov.in/',isNew:true},
{id:'defence26',title:'Indian Army Recruitment 2026',dept:'Army',cat:'central',posts:5000,date:'2026-03-01',fee:0,hot:15000,url:'https://joinindianarmy.nic.in/',isNew:true},
{id:'appsc26',title:'APPSC Group I 2026',dept:'APPSC',cat:'state',posts:300,date:'2026-06-01',fee:200,hot:7000,url:'https://psc.ap.gov.in/',isNew:true},
{id:'dl_rto',title:'Driving Licence (RTO)',dept:'RTO',cat:'transport',posts:0,date:'Open',fee:200,hot:5500,url:'https://parivahan.gov.in/',isNew:false},
];

const CAT_META={central:'🏛️',state:'🏢',job:'💼',utility:'⚡',travel:'✈️',financial:'💳',food:'🍕',shopping:'🛒'};
const CAT_LABELS={central:'Central Govt',state:'State / RTO',job:'Jobs',utility:'Utilities',travel:'Travel & Cabs',financial:'Financial',food:'Food Delivery',shopping:'Online Shopping'};

/* ━━━ AUTH ━━━ */
auth.onAuthStateChanged(async user=>{
  A.user=user;
  if(user){
    A.isAdmin=user.email===ADMIN_EMAIL;
    try{const ref=db.collection('users').doc(user.uid);const snap=await ref.get();if(!snap.exists)await ref.set({email:user.email,role:A.isAdmin?'admin':'operator',createdAt:firebase.firestore.FieldValue.serverTimestamp(),shopName:'',isActive:true});}catch(e){}
  }
  setTimeout(()=>document.getElementById('loader').classList.add('off'),600);
  render();
});

function toast(msg,type='ok'){const icons={ok:'✅',err:'❌',warn:'⚠️'};const el=document.createElement('div');el.className=`toast ${type}`;el.innerHTML=`<span>${icons[type]||'ℹ️'}</span><span>${S.esc(msg)}</span>`;document.getElementById('toasts').appendChild(el);setTimeout(()=>el.style.opacity='0',3800);setTimeout(()=>el.remove(),4300);}

function render(){document.getElementById('root').innerHTML=A.user?renderShell():renderAuthHTML();if(A.user){wireShell();gotoView('dashboard');}}

/* ━━━ AUTH HTML ━━━ */
function renderAuthHTML(){return `<div class="auth-wrap"><div class="auth-glow auth-glow-1"></div><div class="auth-glow auth-glow-2"></div><div class="auth-card"><div class="auth-logo"><div class="auth-icon">🧠</div><h1>CyberAce Quantum 5.0</h1><p>Digital Services Automation Hub</p></div><div class="auth-note"><i class="fas fa-info-circle" style="flex-shrink:0;margin-top:1px"></i><span>Admin: <strong>${S.esc(ADMIN_EMAIL)}</strong></span></div><div class="auth-tabs"><div class="auth-tab on" id="tab-login" onclick="switchTab('login')">Login</div><div class="auth-tab" id="tab-signup" onclick="switchTab('signup')">Sign Up</div></div><div id="auth-err" class="alert alert-err"><i class="fas fa-exclamation-circle"></i><span id="auth-err-msg"></span></div><div id="auth-ok" class="alert alert-ok"><i class="fas fa-check-circle"></i><span id="auth-ok-msg"></span></div><div id="panel-login"><div class="fld"><label class="fld-lbl">Email</label><div class="fld-wrap"><i class="fas fa-envelope fld-ico"></i><input class="fld-in" id="li-email" type="email" placeholder="your@email.com" autocomplete="email" maxlength="100"></div></div><div class="fld"><label class="fld-lbl">Password</label><div class="fld-wrap"><i class="fas fa-lock fld-ico"></i><input class="fld-in" id="li-pass" type="password" placeholder="••••••••" autocomplete="current-password" maxlength="128" onkeydown="if(event.key==='Enter')doLogin()"><button class="fld-eye" onclick="toggleEye('li-pass',this)"><i class="fas fa-eye"></i></button></div></div><div style="text-align:right;margin-bottom:11px"><a href="#" onclick="doResetPwd()" style="font-size:.7rem;color:var(--sky)">Forgot password?</a></div><button class="btn btn-fire" id="btn-login" onclick="doLogin()"><i class="fas fa-sign-in-alt"></i> Login Securely</button></div><div id="panel-signup" style="display:none"><div class="fld"><label class="fld-lbl">Email</label><div class="fld-wrap"><i class="fas fa-envelope fld-ico"></i><input class="fld-in" id="su-email" type="email" placeholder="your@email.com" autocomplete="email" maxlength="100"></div></div><div class="fld"><label class="fld-lbl">Password <span id="pwd-lbl" style="font-size:.63rem;color:var(--muted);margin-left:5px"></span></label><div class="fld-wrap"><i class="fas fa-lock fld-ico"></i><input class="fld-in" id="su-pass" type="password" placeholder="Min 8 chars" autocomplete="new-password" maxlength="128" oninput="updatePwdStr(this.value)"><button class="fld-eye" onclick="toggleEye('su-pass',this)"><i class="fas fa-eye"></i></button></div><div class="pwd-bar"><div class="pwd-fill" id="pwd-fill"></div></div></div><div class="fld"><label class="fld-lbl">Confirm Password</label><div class="fld-wrap"><i class="fas fa-lock fld-ico"></i><input class="fld-in" id="su-pass2" type="password" placeholder="Repeat password" maxlength="128"></div></div><div class="fld"><label class="fld-lbl">Shop / Cafe Name</label><div class="fld-wrap"><i class="fas fa-store fld-ico"></i><input class="fld-in" id="su-shop" type="text" placeholder="My Internet Cafe" maxlength="80"></div></div><button class="btn btn-fire" id="btn-signup" onclick="doSignup()"><i class="fas fa-user-plus"></i> Create Account</button><div class="alert alert-err" id="su-err" style="margin-top:9px"><i class="fas fa-exclamation-circle"></i><span id="su-err-msg"></span></div></div><div style="margin-top:12px;text-align:center;font-size:.66rem;color:var(--muted)"><i class="fas fa-shield-alt" style="color:var(--jade)"></i> Firebase Auth • TLS Encrypted</div></div></div>`;}

function switchTab(t){document.getElementById('tab-login').classList.toggle('on',t==='login');document.getElementById('tab-signup').classList.toggle('on',t==='signup');document.getElementById('panel-login').style.display=t==='login'?'block':'none';document.getElementById('panel-signup').style.display=t==='signup'?'block':'none';['auth-err','auth-ok'].forEach(id=>document.getElementById(id).classList.remove('on'));}
function toggleEye(id,btn){const el=document.getElementById(id);const show=el.type==='password';el.type=show?'text':'password';btn.querySelector('i').className=show?'fas fa-eye-slash':'fas fa-eye';}
function updatePwdStr(p){const s=S.pwdStr(p);const w=s*25+'%';const cols=['','#EF5350','#FF7043','#FFB300','#00E676'];const lbls=['','Weak','Fair','Good','Strong'];document.getElementById('pwd-fill').style.width=w;document.getElementById('pwd-fill').style.background=cols[s]||'#555';document.getElementById('pwd-lbl').textContent=lbls[s]||'';document.getElementById('pwd-lbl').style.color=cols[s]||'';}

const FB_ERR={'auth/user-not-found':'No account found.','auth/wrong-password':'Incorrect password.','auth/invalid-credential':'Invalid email or password.','auth/too-many-requests':'Too many attempts. Try later.','auth/invalid-email':'Invalid email.','auth/email-already-in-use':'Email already in use.','auth/weak-password':'Password too weak (8+ chars).'};
function fbErr(code){return FB_ERR[code]||`Auth error (${code})`;}

async function doLogin(){const e2=document.getElementById('auth-err-msg');document.getElementById('auth-err').classList.remove('on');const email=(document.getElementById('li-email').value||'').trim();const pass=document.getElementById('li-pass').value||'';if(!email||!S.isEmail(email)){e2.textContent='Valid email required.';document.getElementById('auth-err').classList.add('on');return;}if(pass.length<6){e2.textContent='Password too short.';document.getElementById('auth-err').classList.add('on');return;}if(!S.rateLimit('login',5,5*60*1000)){e2.textContent='Too many attempts. Wait 5 min.';document.getElementById('auth-err').classList.add('on');return;}const btn=document.getElementById('btn-login');btn.disabled=true;btn.innerHTML='<div class="spin"></div> Please wait…';try{await auth.signInWithEmailAndPassword(email,pass);}catch(e){e2.textContent=fbErr(e.code);document.getElementById('auth-err').classList.add('on');btn.disabled=false;btn.innerHTML='<i class="fas fa-sign-in-alt"></i> Login Securely';}}

async function doSignup(){const errEl=document.getElementById('su-err'),em=document.getElementById('su-err-msg');errEl.classList.remove('on');const email=(document.getElementById('su-email').value||'').trim();const pass=document.getElementById('su-pass').value||'';const pass2=document.getElementById('su-pass2').value||'';const shop=S.clean(document.getElementById('su-shop').value||'My Cafe');if(!email||!S.isEmail(email)){em.textContent='Valid email required.';errEl.classList.add('on');return;}if(pass.length<8){em.textContent='Password must be 8+ characters.';errEl.classList.add('on');return;}if(S.pwdStr(pass)<2){em.textContent='Password too weak.';errEl.classList.add('on');return;}if(pass!==pass2){em.textContent='Passwords do not match.';errEl.classList.add('on');return;}if(!S.rateLimit('signup',3,10*60*1000)){em.textContent='Too many attempts. Try later.';errEl.classList.add('on');return;}const btn=document.getElementById('btn-signup');btn.disabled=true;btn.innerHTML='<div class="spin"></div> Creating…';try{const cred=await auth.createUserWithEmailAndPassword(email,pass);await db.collection('users').doc(cred.user.uid).set({email,shopName:shop,role:'operator',isActive:true,createdAt:firebase.firestore.FieldValue.serverTimestamp()});document.getElementById('auth-ok-msg').textContent='Account created! Logging in…';document.getElementById('auth-ok').classList.add('on');}catch(e){em.textContent=fbErr(e.code);errEl.classList.add('on');btn.disabled=false;btn.innerHTML='<i class="fas fa-user-plus"></i> Create Account';}}

async function doResetPwd(){const email=(document.getElementById('li-email').value||'').trim();if(!email||!S.isEmail(email)){document.getElementById('auth-err-msg').textContent='Enter email first.';document.getElementById('auth-err').classList.add('on');return;}try{await auth.sendPasswordResetEmail(email);document.getElementById('auth-ok-msg').textContent='Reset link sent! Check inbox.';document.getElementById('auth-ok').classList.add('on');}catch(e){document.getElementById('auth-err-msg').textContent=fbErr(e.code);document.getElementById('auth-err').classList.add('on');}}

/* ━━━ SHELL ━━━ */
function renderShell(){const em=A.user.email||'';const ini=em[0]?.toUpperCase()||'?';
return `<div class="shell"><aside class="sidebar" id="sb">
  <div class="sb-brand"><div class="sb-orb">🧠</div><div class="sb-name hide-slim">CyberAce Quantum<small>v5.0 Digital Hub</small></div></div>
  <div class="sb-user hide-slim"><div class="sb-avatar">${S.esc(ini)}</div><div class="sb-uinfo"><div class="n">${S.esc(em.split('@')[0])}</div><div class="r">${A.isAdmin?'👑 Admin':'✓ Operator'}</div></div></div>
  <nav class="nav">
    <div class="nav-sec hide-slim">Main</div>
    <div class="nav-item active" id="nv-dashboard" onclick="gotoView('dashboard')"><i class="fas fa-chart-pie"></i><span class="hide-slim">Dashboard</span></div>
    <div class="nav-item" id="nv-services" onclick="gotoView('services')"><i class="fas fa-th-large"></i><span class="hide-slim">All Services</span></div>
    <div class="nav-item" id="nv-jobs" onclick="gotoView('jobs')"><i class="fas fa-briefcase"></i><span class="hide-slim">Job Alerts 2026</span><span class="nav-badge hide-slim">${JOBS.filter(j=>j.isNew).length}</span></div>
    <div class="nav-item" id="nv-ocr" onclick="gotoView('ocr')"><i class="fas fa-file-image"></i><span class="hide-slim">OCR Scanner</span></div>
    ${A.isAdmin?`
    <div class="nav-sec hide-slim">Admin Only</div>
    <div class="nav-item" id="nv-applications" onclick="gotoView('applications')"><i class="fas fa-file-alt"></i><span class="hide-slim">Applications</span></div>
    <div class="nav-item" id="nv-earnings" onclick="gotoView('earnings')"><i class="fas fa-rupee-sign"></i><span class="hide-slim">Earnings</span></div>
    <div class="nav-item" id="nv-bookmarklet" onclick="gotoView('bookmarklet')"><i class="fas fa-magic"></i><span class="hide-slim">Auto-Fill Setup</span></div>
    <div class="nav-item" id="nv-admin" onclick="gotoView('admin')"><i class="fas fa-crown"></i><span class="hide-slim">Admin Panel</span><span class="nav-badge hide-slim" style="background:var(--gold);color:#000">ADM</span></div>`:''}
    <div class="nav-sec hide-slim">Account</div>
    <div class="nav-item" onclick="doLogout()"><i class="fas fa-sign-out-alt"></i><span class="hide-slim">Logout</span></div>
  </nav>
  <div class="sb-footer"><div class="upi-pill"><strong>💳 UPI Collection</strong><span>${UPI}</span></div></div>
</aside>
<div class="main-area">
  <div class="topbar">
    <button class="tb-toggle" onclick="toggleSB()"><i class="fas fa-bars"></i></button>
    <div class="tb-title" id="tb-title">Dashboard</div>
    <div class="tb-right"><div class="tb-secure">🔒 Secure</div><button class="tb-logout" onclick="doLogout()"><i class="fas fa-sign-out-alt"></i> Logout</button></div>
  </div>
  <div class="page" id="page"></div>
</div></div>`;}

function wireShell(){document.addEventListener('click',e=>{const sb=document.getElementById('sb');if(!sb)return;if(window.innerWidth<768&&sb.classList.contains('mob-open')){if(!sb.contains(e.target)&&!e.target.closest('.tb-toggle'))sb.classList.remove('mob-open');}});}
function toggleSB(){const sb=document.getElementById('sb');if(!sb)return;if(window.innerWidth<768){sb.classList.toggle('mob-open');return;}sb.classList.toggle('slim');const ma=document.querySelector('.main-area');if(ma)ma.style.marginLeft=sb.classList.contains('slim')?'56px':'240px';}
async function doLogout(){await auth.signOut();toast('Logged out');}

/* ━━━ ROUTER ━━━ */
const VIEW_TITLES={dashboard:'Dashboard',services:'All Services',jobs:'🆕 Job Alerts 2026',applications:'Applications (Admin)',earnings:'Earnings (Admin)',ocr:'OCR Scanner',bookmarklet:'Auto-Fill Setup (Admin)',admin:'Admin Panel'};
function gotoView(name){
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  const nv=document.getElementById('nv-'+name);if(nv)nv.classList.add('active');
  const t=document.getElementById('tb-title');if(t)t.textContent=VIEW_TITLES[name]||name;
  const pg=document.getElementById('page');if(!pg)return;pg.innerHTML='';
  const map={dashboard:vDashboard,services:vServices,jobs:vJobs,applications:vApplications,earnings:vEarnings,ocr:vOCR,bookmarklet:vBookmarklet,admin:vAdmin};
  if(map[name])map[name](pg);
}

/* ━━━ UNIVERSAL SEARCH ━━━ */
function buildSearchIdx(){
  const idx=[];
  SVCS.forEach(s=>{idx.push({type:'service',icon:CAT_META[s.cat]||'🔧',name:s.name,cat:CAT_LABELS[s.cat]||s.cat,url:s.url||'',obj:s,tags:(s.tags||[]).join(' ').toLowerCase()});});
  JOBS.forEach(j=>{idx.push({type:'job',icon:'💼',name:j.title,cat:j.dept,url:j.url||'',obj:j,tags:(j.title+' '+j.dept).toLowerCase()});});
  return idx;
}
let _searchIdx=null;
function searchAll(q){
  if(!_searchIdx)_searchIdx=buildSearchIdx();
  if(!q||q.length<2)return[];
  const lq=q.toLowerCase();
  return _searchIdx.filter(item=>item.name.toLowerCase().includes(lq)||item.tags.includes(lq)||item.cat.toLowerCase().includes(lq)).slice(0,12);
}
function renderSearchResults(q){
  const box=document.getElementById('search-results');if(!box)return;
  const res=searchAll(q);
  if(!res.length){box.classList.remove('on');return;}
  box.innerHTML=res.map(r=>`<div class="sr-item" onclick="onSearchClick(${JSON.stringify({type:r.type,url:r.url,name:r.name,obj:r.obj})})">
    <span class="sr-ico">${r.icon}</span>
    <span class="sr-name">${S.esc(r.name)}</span>
    <span class="sr-cat">${S.esc(r.cat)}</span>
    ${r.url?`<span class="sr-portal"><i class="fas fa-external-link-alt"></i>Portal</span>`:''}
  </div>`).join('');
  box.classList.add('on');
}
function onSearchClick(item){
  document.getElementById('search-results')?.classList.remove('on');
  document.getElementById('global-search').value='';
  if(item.type==='service'){openApplyModal(item.obj);}
  else if(item.type==='job'){openJobApply(item.obj);}
}
function searchBarHtml(){return`<div class="search-bar"><i class="fas fa-search"></i><input type="text" id="global-search" placeholder="🔍 Search any service, portal, scheme, job… (e.g. aadhaar, PAN, TGPSC, train ticket)" autocomplete="off" oninput="renderSearchResults(this.value)" onblur="setTimeout(()=>document.getElementById('search-results')?.classList.remove('on'),200)"><div class="search-results" id="search-results"></div></div>`;}

/* ━━━ DASHBOARD ━━━ */
async function vDashboard(pg){
  pg.innerHTML=`<div class="view">
  ${searchBarHtml()}
  <div class="sec-strip"><span><i class="fas fa-shield-alt"></i> Firebase Auth</span><span><i class="fas fa-database"></i> Firestore</span><span><i class="fas fa-upload"></i> Storage</span><span><i class="fas fa-lock"></i> XSS Safe</span></div>
  ${A.isAdmin?`<div class="stats" id="dash-stats">
    <div class="stat-c"><div class="stat-lbl">Total Applications</div><div class="stat-v" id="st-total">…</div><div class="stat-s">All time</div><div class="stat-ico">📋</div></div>
    <div class="stat-c"><div class="stat-lbl">Today</div><div class="stat-v" id="st-today">…</div><div class="stat-s">Applications today</div><div class="stat-ico">📅</div></div>
    <div class="stat-c"><div class="stat-lbl">Total Earnings</div><div class="stat-v" id="st-earn">…</div><div class="stat-s">Gross commission</div><div class="stat-ico">💰</div></div>
    <div class="stat-c"><div class="stat-lbl">This Month</div><div class="stat-v" id="st-month">…</div><div class="stat-s">Net earnings</div><div class="stat-ico">📈</div></div>
  </div>`:''}
  <div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:16px;display:flex;align-items:center;gap:20px;margin-bottom:18px;flex-wrap:wrap">
    <div style="flex:1;min-width:180px"><div style="font-size:1rem;font-weight:700;margin-bottom:5px">💳 Quick Fee Collection</div><div style="font-size:.78rem;color:var(--muted2)">Show QR → Customer pays via UPI</div><div style="margin-top:8px;font-family:var(--ff-mono);font-size:.73rem;color:var(--jade)">${UPI}</div></div>
    <div id="dash-qr" style="background:#fff;padding:5px;border-radius:9px;width:116px;height:116px;flex-shrink:0"></div>
  </div>
  <div class="sec-title" style="margin-bottom:12px">🚀 Quick Access</div>
  <div class="cat-tiles" id="cat-tiles"></div>
  <div style="display:grid;grid-template-columns:1fr 280px;gap:14px" id="dash-bot">
    <div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:15px">
      <div class="sec-title" style="margin-bottom:11px">🆕 Latest Job Alerts 2026</div>
      <div id="dash-trending"></div>
    </div>
    <div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:15px">
      <div class="sec-title" style="margin-bottom:11px">🏛️ Popular Portals</div>
      <div id="dash-portals"></div>
    </div>
  </div>
  </div>`;
  setTimeout(()=>{try{new QRCode(document.getElementById('dash-qr'),{text:`upi://pay?pa=${UPI}&pn=CyberAce&am=100&cu=INR`,width:106,height:106});}catch(e){}},100);
  const uniqueCats=[...new Set(SVCS.map(s=>s.cat))];
  document.getElementById('cat-tiles').innerHTML=uniqueCats.map(c=>`<div class="cat-tile" onclick="gotoViewFiltered('services','${S.esc(c)}')"><div class="ico">${CAT_META[c]||'🔧'}</div><div class="nm">${S.esc(CAT_LABELS[c]||c)}</div><div class="cnt">${SVCS.filter(s=>s.cat===c).length} services</div></div>`).join('');
  if(A.isAdmin){
    try{const snap=await db.collection('applications').where('uid','==',A.user.uid).get();const apps=snap.docs.map(d=>d.data());const today=new Date().toISOString().slice(0,10);document.getElementById('st-total').textContent=apps.length;document.getElementById('st-today').textContent=apps.filter(a=>(a.createdAt?.toDate?.()?.toISOString?.()||'').startsWith(today)).length;const earn=apps.reduce((s,a)=>s+(a.commission||0),0);document.getElementById('st-earn').textContent=fmtINR(earn);const mo=new Date().toISOString().slice(0,7);document.getElementById('st-month').textContent=fmtINR(apps.filter(a=>(a.createdAt?.toDate?.()?.toISOString?.()||'').startsWith(mo)).reduce((s,a)=>s+(a.commission||0),0));}catch(e){['st-total','st-today','st-earn','st-month'].forEach(id=>{const el=document.getElementById(id);if(el)el.textContent='0';});}
  }
  const trending=[...JOBS].filter(j=>j.isNew).sort((a,b)=>b.hot-a.hot).slice(0,6);
  document.getElementById('dash-trending').innerHTML=trending.map(j=>`<div style="display:flex;justify-content:space-between;align-items:center;padding:7px 0;border-bottom:1px solid var(--border);font-size:.76rem;cursor:pointer" onclick="openJobApply(${JSON.stringify(j)})">
    <div><div style="font-weight:600">${S.esc(j.title)}</div><div style="color:var(--muted);font-size:.65rem">${S.esc(j.dept)} • ${j.date}</div></div>
    <div style="text-align:right;flex-shrink:0"><span class="new-tag">NEW</span><div style="color:var(--fire);font-size:.65rem;margin-top:2px">🔥${(j.hot/1000).toFixed(1)}K</div></div>
  </div>`).join('');
  const popularSvcs=SVCS.filter(s=>s.url).slice(0,8);
  document.getElementById('dash-portals').innerHTML=popularSvcs.map(s=>`<a href="${S.esc(s.url)}" target="_blank" rel="noopener" onclick="saveJobData('${S.esc(s.name)}','${S.esc(s.url||'')}')" style="display:flex;align-items:center;gap:8px;padding:6px 0;border-bottom:1px solid var(--border);text-decoration:none;cursor:pointer;font-size:.76rem;color:var(--text)">
    <span style="font-size:.95rem">${CAT_META[s.cat]||'🔧'}</span><span style="flex:1;font-weight:600">${S.esc(s.name)}</span><i class="fas fa-external-link-alt" style="color:var(--jade);font-size:.7rem"></i>
  </a>`).join('');
}

let _filteredCat='';
function gotoViewFiltered(view,cat){_filteredCat=cat;gotoView(view);}

/* ━━━ SERVICES VIEW ━━━ */
function vServices(pg){
  pg.innerHTML=`<div class="view">
  ${searchBarHtml()}
  <div class="sec-hd"><div class="sec-title">🏛️ All Services (${SVCS.length})</div><div class="ftabs" id="svc-tabs"><button class="ft on" onclick="filterSvc('',this)">All</button>${[...new Set(SVCS.map(s=>s.cat))].map(c=>`<button class="ft" onclick="filterSvc('${S.esc(c)}',this)">${S.esc(CAT_META[c]||'')} ${S.esc(CAT_LABELS[c]||c)}</button>`).join('')}</div></div>
  <div class="svc-grid" id="svc-grid"></div></div>`;
  if(_filteredCat){const btn=[...document.querySelectorAll('#svc-tabs .ft')].find(b=>b.textContent.includes(CAT_LABELS[_filteredCat]||_filteredCat));if(btn){document.querySelectorAll('#svc-tabs .ft').forEach(b=>b.classList.remove('on'));btn.classList.add('on');}renderSvcGrid(SVCS.filter(s=>s.cat===_filteredCat));_filteredCat='';}else renderSvcGrid(SVCS);
}
function filterSvc(cat,el){document.querySelectorAll('#svc-tabs .ft').forEach(b=>b.classList.remove('on'));el.classList.add('on');renderSvcGrid(cat?SVCS.filter(s=>s.cat===cat):SVCS);}
function renderSvcGrid(list){
  const g=document.getElementById('svc-grid');if(!g)return;
  if(!list.length){g.innerHTML=`<div style="text-align:center;padding:60px;color:var(--muted);grid-column:1/-1"><div style="font-size:2.5rem;opacity:.3">🔍</div><div>No services found</div></div>`;return;}
  g.innerHTML=list.map(s=>`<div class="svc-c cat-${S.esc(s.cat)}">
    ${s.url?'<span class="auto-tag">⚡ Portal</span>':''}
    <div class="svc-cat"><span class="cat-dot"></span>${S.esc(CAT_META[s.cat]||'')} ${S.esc(CAT_LABELS[s.cat]||s.cat)}</div>
    <div class="svc-name">${S.esc(s.name)}</div>
    ${s.url?`<a class="portal-btn" href="${S.esc(s.url)}" target="_blank" rel="noopener" onclick="saveJobData('${S.esc(s.name)}','${S.esc(s.url)}')"><i class="fas fa-rocket"></i> Open Portal & Auto-Fill</a>`:''}
    <div class="svc-foot" style="margin-top:${s.url?'8px':'0'}">
      <span class="svc-price">₹${s.price}</span>
      <button class="btn btn-outline btn-xs" style="width:auto" onclick="openApplyModal(${JSON.stringify(s)})">📝 Apply</button>
    </div>
  </div>`).join('');
}

/* ━━━ JOBS VIEW ━━━ */
function vJobs(pg){
  pg.innerHTML=`<div class="view">
  ${searchBarHtml()}
  <div class="sec-hd"><div class="sec-title">💼 Latest Job Alerts 2026</div><div class="ftabs" id="job-tabs"><button class="ft on" onclick="filterJobs('',this)">All</button><button class="ft" onclick="filterJobs('central',this)">Central</button><button class="ft" onclick="filterJobs('banking',this)">Banking</button><button class="ft" onclick="filterJobs('state',this)">State PSC</button><button class="ft" onclick="filterJobs('teaching',this)">Teaching</button><button class="ft" onclick="filterJobs('medical',this)">Medical</button><button class="ft" onclick="filterJobs('engg',this)">Engineering</button><button class="ft" onclick="filterJobs('transport',this)">Transport</button><button class="ft" onclick="filterJobs('scholar',this)">Scholarship</button></div></div>
  <div class="job-list" id="job-list"></div></div>`;
  renderJobList(JOBS);
}
function filterJobs(cat,el){document.querySelectorAll('#job-tabs .ft').forEach(b=>b.classList.remove('on'));el.classList.add('on');renderJobList(cat?JOBS.filter(j=>j.cat===cat):JOBS);}
function renderJobList(list){
  const el=document.getElementById('job-list');if(!el)return;
  if(!list.length){el.innerHTML=`<div style="text-align:center;padding:60px;color:var(--muted)">No jobs found</div>`;return;}
  el.innerHTML=[...list].sort((a,b)=>b.hot-a.hot).map(j=>`<div class="job-c">
    <div class="job-dept-ico">${S.esc(j.dept[0])}</div>
    <div class="job-info">
      <div class="job-title">${S.esc(j.title)} ${j.isNew?'<span class="new-tag">2026</span>':''}</div>
      <div class="job-meta"><span>🏛️ ${S.esc(j.dept)}</span>${j.posts?`<span>👥 ${j.posts.toLocaleString('en-IN')} posts</span>`:''}<span class="fire-tag">🔥 ${(j.hot/1000).toFixed(1)}K</span></div>
      ${j.url?`<a href="${S.esc(j.url)}" target="_blank" rel="noopener" class="job-portal-link" onclick="saveJobData('${S.esc(j.title)}','${S.esc(j.url)}')"><i class="fas fa-rocket"></i> Direct Portal + Auto-Fill</a>`:''}
    </div>
    <div class="job-r"><div class="job-fee">₹${j.fee} fee</div><div class="job-date">📅 ${S.esc(j.date)}</div><div class="hot-btn" onclick="openJobApply(${JSON.stringify(j)})">Apply Now</div></div>
  </div>`).join('');
}
function openJobApply(j){const svc={id:j.id,name:j.title,cat:'job',price:100+(j.fee||0),comm:150,url:j.url||''};openApplyModal(svc);}

/* ━━━ ADMIN-ONLY VIEWS ━━━ */
async function vApplications(pg){
  if(!A.isAdmin){pg.innerHTML='<div style="text-align:center;padding:60px;color:var(--danger)"><div style="font-size:3rem">🔒</div><div style="font-weight:700;margin-top:10px">Admin access only</div></div>';return;}
  pg.innerHTML=`<div class="view"><div class="sec-hd"><div class="sec-title">📋 All Applications</div><button class="btn btn-outline btn-sm" onclick="gotoView('applications')"><i class="fas fa-sync"></i> Refresh</button></div><div class="tbl-wrap"><table><thead><tr><th>App No.</th><th>Service</th><th>Customer</th><th>Status</th><th>Payment</th><th>Commission</th><th>Date</th></tr></thead><tbody id="apps-body"><tr><td colspan="7" style="text-align:center;padding:40px"><div class="spin" style="margin:auto"></div></td></tr></tbody></table></div></div>`;
  try{const snap=await db.collection('applications').orderBy('createdAt','desc').limit(200).get();const apps=snap.docs.map(d=>({id:d.id,...d.data()}));const tb=document.getElementById('apps-body');tb.innerHTML=apps.length?apps.map(a=>`<tr><td style="font-family:var(--ff-mono);font-size:.7rem">${S.esc(a.appNumber||a.id?.slice(-8)||'—')}</td><td>${S.esc(a.serviceName||'—')}</td><td>${S.esc(a.customerName||'—')}</td><td><span class="pill p-${S.esc(a.status||'pending')}">${S.esc(a.status||'pending')}</span></td><td><span class="pill p-${a.paymentVerified?'verified':'pending'}">${a.paymentVerified?'Verified':'Pending'}</span></td><td style="color:var(--jade)">₹${a.commission||0}</td><td style="color:var(--muted)">${a.createdAt?.toDate?.()?.toLocaleDateString('en-IN')||'—'}</td></tr>`).join(''):`<tr><td colspan="7" style="text-align:center;padding:40px;color:var(--muted)">No applications yet.</td></tr>`;}catch(e){document.getElementById('apps-body').innerHTML=`<tr><td colspan="7" style="text-align:center;padding:20px;color:var(--muted)">${S.esc(e.message)}</td></tr>`;}
}

function vEarnings(pg){
  if(!A.isAdmin){pg.innerHTML='<div style="text-align:center;padding:60px;color:var(--danger)"><div style="font-size:3rem">🔒</div><div style="font-weight:700;margin-top:10px">Admin access only</div></div>';return;}
  pg.innerHTML=`<div class="view"><div class="sec-hd"><div class="sec-title">💰 Profit Calculator</div></div><div class="calc-grid"><div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:15px"><div style="font-size:.86rem;font-weight:700;margin-bottom:13px">⚙️ Inputs</div><div class="fld"><label class="fld-lbl">Apps / day</label><input class="fld-in" style="padding-left:12px" type="number" id="c-apps" value="20" min="1" max="500" oninput="recalc()"></div><div class="fld"><label class="fld-lbl">Commission / app (₹)</label><input class="fld-in" style="padding-left:12px" type="number" id="c-comm" value="100" min="10" oninput="recalc()"></div><div class="fld"><label class="fld-lbl">Working days / month</label><input class="fld-in" style="padding-left:12px" type="number" id="c-days" value="25" min="1" max="31" oninput="recalc()"></div></div><div style="display:grid;grid-template-columns:1fr 1fr;gap:10px"><div class="calc-out"><div class="cl">Revenue</div><div class="cv" id="c-rev" style="color:var(--fire)">—</div></div><div class="calc-out"><div class="cl">Platform (15%)</div><div class="cv" id="c-fee" style="color:var(--danger)">—</div></div><div class="calc-out"><div class="cl">Subscription</div><div class="cv" style="color:var(--muted2)">₹2,000</div></div><div class="calc-out"><div class="cl">Net Profit</div><div class="cv" id="c-net" style="color:var(--jade)">—</div></div></div></div><div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);overflow:hidden"><div style="padding:13px 15px;border-bottom:1px solid var(--border);font-weight:700">📊 Earnings Scale</div><table><thead><tr><th>Apps/Day</th><th>Monthly</th><th>Gross</th><th>Platform</th><th>Net Profit</th></tr></thead><tbody>${[10,20,30,50,100].map(d=>{const a=d*25,g=a*100,f=Math.round(g*.15),n=g-f-2000;return`<tr><td>${d}</td><td>${a}</td><td style="color:var(--fire)">${fmtINR(g)}</td><td style="color:var(--danger)">${fmtINR(f)}</td><td style="color:var(--jade);font-weight:700">${fmtINR(Math.max(0,n))}</td></tr>`;}).join('')}</tbody></table></div></div>`;
  recalc();
}
function recalc(){const a=parseInt(document.getElementById('c-apps')?.value)||0;const c=parseInt(document.getElementById('c-comm')?.value)||0;const d=parseInt(document.getElementById('c-days')?.value)||25;const r=a*d*c,f=Math.round(r*.15),n=r-f-2000;if(document.getElementById('c-rev')){document.getElementById('c-rev').textContent=fmtINR(r);document.getElementById('c-fee').textContent=fmtINR(f);document.getElementById('c-net').textContent=fmtINR(Math.max(0,n));}}
function fmtINR(n){return n>=100000?`₹${(n/100000).toFixed(2)}L`:`₹${n.toLocaleString('en-IN')}`;}

/* ━━━ OCR VIEW ━━━ */
function vOCR(pg){
  pg.innerHTML=`<div class="view"><div class="sec-hd"><div class="sec-title">📄 OCR Document Scanner</div></div><div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:18px;max-width:540px"><p style="font-size:.8rem;color:var(--muted2);margin-bottom:14px">Upload Aadhaar, PAN, or any document image. AI extracts Name, DOB, Aadhaar, PAN automatically.</p><div class="up-zone" id="ocr-zone"><div class="u-ico"><i class="fas fa-file-image"></i></div><div class="u-txt">Click or drag to upload document image</div><div class="u-sub">JPG, PNG, PDF • Max 10MB</div><input type="file" id="ocr-file" accept="image/*,.pdf" onchange="runOCR(this)"></div><div id="ocr-spin" style="display:none;text-align:center;padding:16px"><div class="spin" style="margin:auto;width:24px;height:24px;border-width:3px"></div><div style="color:var(--muted);font-size:.76rem;margin-top:8px">Running AI OCR…</div></div><div class="ocr-result" id="ocr-result"><div style="font-size:.73rem;color:var(--muted2);font-weight:600;margin-bottom:8px">Extracted Fields:</div><div id="ocr-fields"></div><div style="margin-top:11px"><div style="font-size:.66rem;color:var(--muted);margin-bottom:4px">Raw OCR Text:</div><textarea id="ocr-raw" style="width:100%;background:var(--ink);border:1px solid var(--border);border-radius:7px;padding:8px;color:var(--muted2);font-size:.7rem;height:80px;font-family:var(--ff-mono);resize:vertical" readonly></textarea></div><button class="btn btn-jade btn-sm" style="width:auto;margin-top:10px" onclick="useOCRData()"><i class="fas fa-fill-drip"></i> Use in Next Application</button></div></div></div>`;
}
async function runOCR(input){const file=input.files[0];if(!file)return;if(file.size>10*1024*1024){toast('File too large','err');return;}document.getElementById('ocr-spin').style.display='block';document.getElementById('ocr-result').classList.remove('on');try{if(typeof Tesseract!=='undefined'){const{data:{text}}=await Tesseract.recognize(file,'eng');displayOCRResult(text);}else{const reader=new FileReader();reader.onload=e=>displayOCRResult(e.target.result||'OCR lib loading...');reader.readAsText(file);}}catch(e){toast('OCR failed: '+e.message,'err');}finally{document.getElementById('ocr-spin').style.display='none';}}
function displayOCRResult(text){const f=extractOCRFields(text);A.formData={...A.formData,...f};document.getElementById('ocr-raw').value=text;const el=document.getElementById('ocr-fields');el.innerHTML=Object.entries(f).filter(([,v])=>v).map(([k,v])=>`<div class="ocr-row"><span class="l">${S.esc(k)}</span><span class="v">${S.esc(v)}</span></div>`).join('')||'<div style="color:var(--muted);font-size:.76rem">Could not extract structured fields.</div>';document.getElementById('ocr-result').classList.add('on');toast('OCR complete!');}
function extractOCRFields(txt){const find=pats=>{for(const p of pats){const m=txt.match(p);if(m)return(m[1]||'').trim();}return'';};return{Name:find([/name[:\s]+([A-Za-z\s]{3,40})/i,/^([A-Z][a-z]+ [A-Z][a-z]+)/m]),DOB:find([/dob[:\s]+(\d{2}[\/\-]\d{2}[\/\-]\d{4})/i,/date of birth[:\s]+(\d{2}[\/\-]\d{2}[\/\-]\d{4})/i]),Gender:find([/\b(Male|Female)\b/i]),Aadhaar:find([/(\d{4}\s\d{4}\s\d{4})/]),PAN:find([/([A-Z]{5}[0-9]{4}[A-Z])/]),Phone:find([/(\+91[-\s]?[6-9]\d{9})/,/\b([6-9]\d{9})\b/]),Address:find([/address[:\s]+(.{15,80})/i])};}
function useOCRData(){toast('OCR data ready — auto-fills next application form!');}

/* ━━━ ADMIN PANEL ━━━ */
async function vAdmin(pg){
  if(!A.isAdmin){pg.innerHTML='<div style="text-align:center;padding:60px;color:var(--danger)"><div style="font-size:3rem">🚫</div><div style="font-weight:700;margin-top:10px">Admin access only</div></div>';return;}
  pg.innerHTML=`<div class="view"><div class="sec-hd"><div class="sec-title">👑 Admin Panel <span class="badge-admin">ADMIN</span></div></div><div class="stats" style="margin-bottom:18px"><div class="stat-c"><div class="stat-lbl">Total Users</div><div class="stat-v" id="adm-users">…</div><div class="stat-ico">👥</div></div><div class="stat-c"><div class="stat-lbl">All Applications</div><div class="stat-v" id="adm-apps">…</div><div class="stat-ico">📋</div></div><div class="stat-c"><div class="stat-lbl">Platform Revenue</div><div class="stat-v" id="adm-rev">…</div><div class="stat-ico">💰</div></div><div class="stat-c"><div class="stat-lbl">Pending</div><div class="stat-v" id="adm-pend">…</div><div class="stat-ico">⏳</div></div></div><div style="display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:18px"><div class="admin-card"><h4>🏪 Operators</h4><div id="adm-franchises"><div class="spin" style="margin:auto"></div></div></div><div class="admin-card"><h4>🔔 Recent Applications</h4><div id="adm-recent-apps"><div class="spin" style="margin:auto"></div></div></div></div><div class="admin-card"><h4>⏳ Pending Verifications</h4><div id="adm-pending-pay"></div></div></div>`;
  try{
    const usersSnap=await db.collection('users').get();const users=usersSnap.docs.map(d=>({id:d.id,...d.data()}));document.getElementById('adm-users').textContent=users.length;
    const appsSnap=await db.collection('applications').orderBy('createdAt','desc').limit(200).get();const apps=appsSnap.docs.map(d=>({id:d.id,...d.data()}));document.getElementById('adm-apps').textContent=apps.length;document.getElementById('adm-rev').textContent=fmtINR(apps.reduce((s,a)=>s+Math.round((a.commission||0)*PLATFORM_CUT),0));const pending=apps.filter(a=>!a.paymentVerified).length;document.getElementById('adm-pend').textContent=pending;
    const ops=users.filter(u=>u.role!=='admin');document.getElementById('adm-franchises').innerHTML=ops.length?ops.map(u=>`<div class="franchise-item"><div class="fi-name">${S.esc(u.shopName||u.email?.split('@')[0]||'—')}<div style="font-size:.63rem;color:var(--muted)">${S.esc(u.email||'—')}</div></div><div class="fi-stat"><div class="v">${apps.filter(a=>a.uid===u.id).length} apps</div><div class="s">${u.isActive?'✅ Active':'❌ Inactive'}</div></div></div>`).join(''):'<div style="color:var(--muted);font-size:.76rem">No operators yet</div>';
    document.getElementById('adm-recent-apps').innerHTML=apps.slice(0,8).map(a=>`<div class="franchise-item"><div><div style="font-size:.76rem;font-weight:600">${S.esc(a.serviceName||'—')}</div><div style="font-size:.63rem;color:var(--muted)">${S.esc(a.customerName||'—')}</div></div><div class="fi-stat"><span class="pill p-${S.esc(a.status||'pending')}">${S.esc(a.status||'pending')}</span></div></div>`).join('');
    const unpaid=apps.filter(a=>!a.paymentVerified).slice(0,10);document.getElementById('adm-pending-pay').innerHTML=unpaid.length?unpaid.map(a=>`<div class="franchise-item"><div><div style="font-size:.76rem;font-weight:600">${S.esc(a.serviceName||'—')} — ${S.esc(a.customerName||'—')}</div><div style="font-size:.63rem;color:var(--muted);font-family:var(--ff-mono)">${S.esc(a.txnId||'—')} | UTR: ${S.esc(a.utrRef||'—')}</div></div><div class="fi-stat"><button onclick="adminVerifyPayment('${a.id}')" class="btn btn-jade btn-xs" style="width:auto">✓ Verify</button></div></div>`).join(''):'<div style="color:var(--jade);font-size:.76rem;padding:9px 0">✅ All payments verified</div>';
  }catch(e){toast('Admin error: '+e.message,'err');}
}
async function adminVerifyPayment(docId){try{await db.collection('applications').doc(docId).update({paymentVerified:true,status:'submitted',verifiedAt:firebase.firestore.FieldValue.serverTimestamp(),verifiedBy:A.user.uid});toast('Payment verified ✅');vAdmin(document.getElementById('page'));}catch(e){toast('Error: '+e.message,'err');}}

/* ━━━ BOOKMARKLET (ADMIN ONLY) ━━━ */
function vBookmarklet(pg){
  if(!A.isAdmin){pg.innerHTML='<div style="text-align:center;padding:60px;color:var(--danger)"><div style="font-size:3rem">🔒</div><div style="font-weight:700;margin-top:10px">Admin access only</div></div>';return;}
  const BM=`javascript:(function(){'use strict';var d=JSON.parse(localStorage.getItem('ca_autofill')||'null');if(!d||!d.data||Date.now()-d.ts>300000){alert('CyberAce: No session. Open CyberAce, fill customer data, click portal, then click this.');return;}var data=d.data,filled=0;var G={name:['input[name*="candidatename" i]','input[name*="applicantname" i]','input[name*="name" i]','input[id*="name" i]','input[placeholder*="name" i]','input[autocomplete="name"]'],dob:['input[type="date"]','input[name*="dob" i]','input[name*="dateofbirth" i]'],mobile:['input[name*="mobile" i]','input[name*="phone" i]','input[type="tel"]','input[placeholder*="mobile" i]'],email:['input[type="email"]','input[name*="email" i]'],aadhaar:['input[name*="aadhaar" i]','input[name*="aadhar" i]','input[id*="aadhaar" i]'],pan:['input[name*="pan" i]','input[id*="pan" i]','input[placeholder*="pan" i]'],address:['textarea[name*="address" i]','input[name*="address" i]'],pincode:['input[name*="pincode" i]','input[name*="zip" i]']};function fi(el,v){if(!el||el.disabled||el.readOnly||!v)return false;var p=el.tagName==='TEXTAREA'?HTMLTextAreaElement.prototype:HTMLInputElement.prototype;var ns=Object.getOwnPropertyDescriptor(p,'value');el.focus();if(ns&&ns.set)ns.set.call(el,v);else el.value=v;['input','change','blur'].forEach(function(e){el.dispatchEvent(new Event(e,{bubbles:true}))});return true;}function ts(ss,v){for(var i=0;i<ss.length;i++){try{var ee=document.querySelectorAll(ss[i]);for(var j=0;j<ee.length;j++){if(ee[j].offsetParent!==null&&fi(ee[j],v))return true;}}catch(e){}}return false;}var fm={name:data.name,dob:data.dob,mobile:data.mobile,email:data.email,aadhaar:data.aadhaar,pan:data.pan,address:data.address,pincode:data.pincode};Object.keys(fm).forEach(function(f){if(fm[f]&&ts(G[f]||[],fm[f]))filled++;});var old=document.getElementById('__ca__');if(old)old.remove();var el=document.createElement('div');el.id='__ca__';el.style.cssText='position:fixed;top:12px;right:12px;z-index:2147483647;font-family:Arial,sans-serif';el.innerHTML='<div style="background:#0D1421;border:1.5px solid rgba(255,87,34,.5);border-radius:12px;padding:13px 15px;box-shadow:0 16px 50px rgba(0,0,0,.75);min-width:220px"><div style="color:#FF5722;font-weight:700;font-size:13px;margin-bottom:6px">&#x1F9E0; CyberAce Auto-Fill</div><div style="color:'+(filled>0?'#00E676':'#FFD600')+';font-size:12px;margin-bottom:7px">'+(filled>0?'&#x2705; '+filled+' fields filled!':'&#x26A0;&#xFE0F; 0 filled — try Re-Fill')+'</div>'+(data.name?'<div style="color:#8FA3B8;font-size:11px">&#x1F464; '+data.name+'</div>':'')+(data.mobile?'<div style="color:#8FA3B8;font-size:11px">&#x1F4F1; '+data.mobile+'</div>':'')+'<div style="margin-top:8px;display:flex;gap:5px"><button onclick="document.getElementById(\'__ca__\').remove()" style="background:rgba(255,255,255,.08);color:#8FA3B8;border:1px solid rgba(255,255,255,.15);border-radius:6px;padding:4px 9px;cursor:pointer;font-size:11px">Close</button></div></div>';document.body.appendChild(el);})();`;
  pg.innerHTML=`<div class="view"><div class="sec-hd"><div class="sec-title">🔖 Auto-Fill Bookmarklet Setup</div></div>
  <div style="background:linear-gradient(135deg,rgba(0,191,165,.08),rgba(124,77,255,.06));border:1.5px solid rgba(0,191,165,.3);border-radius:13px;padding:16px;margin-bottom:18px">
    <div style="font-size:.96rem;font-weight:700;color:var(--jade);margin-bottom:7px">⚡ How Real Auto-Fill Works</div>
    <div style="display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:9px">
      ${['Setup Once: Drag 🧠 button below to bookmarks bar','Fill Data: Open service → fill customer details','Launch Portal: Click "Open Portal" button','Click Bookmarklet: Fields fill instantly!'].map((s,i)=>`<div style="background:rgba(255,255,255,.03);border-radius:9px;padding:11px;font-size:.78rem"><div style="font-weight:700;color:${['var(--fire)','var(--gold)','var(--jade)','var(--sky)'][i]};margin-bottom:3px">Step ${i+1}</div><div style="color:var(--muted2)">${s}</div></div>`).join('')}
    </div>
  </div>
  <div style="background:var(--card);border:1px solid var(--border);border-radius:13px;padding:20px;text-align:center;margin-bottom:18px">
    <div style="font-size:.85rem;color:var(--muted2);margin-bottom:13px"><i class="fas fa-grip-lines" style="color:var(--fire)"></i> <strong style="color:var(--text)">Drag this to your Bookmarks Bar:</strong> <span style="font-size:.72rem;color:var(--muted)">(Ctrl+Shift+B to show bar)</span></div>
    <a href="${BM.replace(/"/g,'&quot;')}" style="display:inline-flex;align-items:center;gap:7px;padding:12px 20px;background:linear-gradient(135deg,#FF5722,#B71C1C);color:#fff;border-radius:10px;font-weight:700;font-size:.95rem;text-decoration:none;box-shadow:0 6px 20px rgba(255,87,34,.4);cursor:grab;border:2px dashed rgba(255,255,255,.3);user-select:none" onclick="event.preventDefault();alert('Don\\'t click — DRAG to bookmarks bar!')">🧠 CyberAce Auto-Fill</a>
    <div style="font-size:.7rem;color:var(--muted);margin-top:10px"><i class="fas fa-info-circle" style="color:var(--jade)"></i> Hold and drag the button above to your browser's bookmarks bar</div>
  </div>
  <div style="background:var(--card);border:1px solid var(--border);border-radius:var(--r);padding:14px">
    <div style="font-weight:700;margin-bottom:9px">✅ Supported Portals (Site-Specific Auto-Fill)</div>
    <div style="display:flex;flex-wrap:wrap;gap:6px">${['parivahan.gov.in','myaadhaar.uidai.gov.in','ssc.gov.in','upsconline.gov.in','ibps.in','tgpsc.telangana.gov.in','neet.nta.nic.in','jeemain.nta.nic.in','scholarships.gov.in','irctc.co.in','incometax.gov.in','gst.gov.in','tspsc.gov.in','edistrict.ap.gov.in','ts.meeseva.gov.in','rrbapply.gov.in','psc.ap.gov.in'].map(s=>`<div style="background:rgba(0,230,118,.06);border:1px solid rgba(0,230,118,.2);border-radius:99px;padding:3px 9px;font-size:.66rem;color:var(--jade)">${s}</div>`).join('')}<div style="background:rgba(255,183,0,.06);border:1px solid rgba(255,183,0,.2);border-radius:99px;padding:3px 9px;font-size:.66rem;color:var(--warn)">+ 200 more via generic detection</div></div>
  </div></div>`;
}

/* ━━━ APPLY MODAL ━━━ */
function openApplyModal(svc){if(!A.user){toast('Please login first','err');return;}A.svc=svc;A.txnId=null;document.getElementById('mTitle').textContent=svc.name;document.getElementById('mSub').textContent=`₹${svc.price} total  •  ₹${svc.comm} commission`;document.getElementById('mBody').innerHTML=renderStep1(svc);document.getElementById('overlay').classList.add('open');}
function closeModal(){document.getElementById('overlay').classList.remove('open');}
function stepBar(step){const labels=['Details','Upload','Payment','Done'];return`<div class="steps">${labels.map((l,i)=>`${i>0?`<div class="step-conn ${i<step?'done':''}"></div>`:''}
<div class="step-n ${i+1<step?'done':i+1===step?'active':''}"><div class="step-dot">${i+1<step?'✓':i+1}</div><div class="step-lbl">${l}</div></div>`).join('')}</div>`;}

function renderStep1(svc){const d=A.formData;return stepBar(1)+`
<div class="row2"><div class="fld"><label class="fld-lbl">Customer Full Name *</label><div class="fld-wrap"><i class="fas fa-user fld-ico"></i><input class="fld-in" id="f-name" placeholder="As per Aadhaar" maxlength="100" value="${S.esc(d.Name||'')}"></div><div class="fld-err" id="e-name">Name required</div></div>
<div class="fld"><label class="fld-lbl">Date of Birth *</label><div class="fld-wrap"><i class="fas fa-calendar fld-ico"></i><input class="fld-in" id="f-dob" type="date" value="${S.esc(d.DOB||'')}"></div><div class="fld-err" id="e-dob">DOB required</div></div></div>
<div class="row2"><div class="fld"><label class="fld-lbl">Mobile Number *</label><div class="fld-wrap"><i class="fas fa-phone fld-ico"></i><input class="fld-in" id="f-mobile" placeholder="10-digit" maxlength="10" value="${S.esc(d.Phone||'')}"></div><div class="fld-err" id="e-mobile">Valid 10-digit required</div></div>
<div class="fld"><label class="fld-lbl">Email</label><div class="fld-wrap"><i class="fas fa-envelope fld-ico"></i><input class="fld-in" id="f-email" type="email" placeholder="optional" maxlength="100"></div></div></div>
<div class="row2"><div class="fld"><label class="fld-lbl">Aadhaar Number</label><div class="fld-wrap"><i class="fas fa-id-card fld-ico"></i><input class="fld-in" id="f-aadhaar" placeholder="12 digits" maxlength="12" value="${S.esc(d.Aadhaar||'')}"></div><div class="fld-err" id="e-aadhaar">Must be 12 digits</div></div>
<div class="fld"><label class="fld-lbl">PAN Number</label><div class="fld-wrap"><i class="fas fa-file fld-ico"></i><input class="fld-in" id="f-pan" placeholder="ABCDE1234F" maxlength="10" style="text-transform:uppercase" value="${S.esc(d.PAN||'')}"></div><div class="fld-err" id="e-pan">Invalid PAN</div></div></div>
<div class="fld"><label class="fld-lbl">Address</label><div class="fld-wrap"><i class="fas fa-map-marker-alt fld-ico"></i><input class="fld-in" id="f-addr" placeholder="Full address" maxlength="250" value="${S.esc(d.Address||'')}"></div></div>
<button class="btn btn-fire" onclick="validateStep1()"><i class="fas fa-arrow-right"></i> Next: Upload Documents</button>`;}

function validateStep1(){let ok=true;const setE=(id,eid,cond)=>{const el=document.getElementById(id),er=document.getElementById(eid);el?.classList.toggle('err',cond);er?.classList.toggle('on',cond);if(cond)ok=false;};const name=S.clean(document.getElementById('f-name')?.value||'');const dob=document.getElementById('f-dob')?.value||'';const mobile=(document.getElementById('f-mobile')?.value||'').trim();const aadhaar=(document.getElementById('f-aadhaar')?.value||'').trim();const pan=(document.getElementById('f-pan')?.value||'').trim().toUpperCase();setE('f-name','e-name',!name);setE('f-dob','e-dob',!dob);setE('f-mobile','e-mobile',!S.isPhone(mobile));setE('f-aadhaar','e-aadhaar',aadhaar&&!S.isAadhaar(aadhaar));setE('f-pan','e-pan',pan&&!S.isPAN(pan));if(!ok)return;A.formData={name,dob,mobile,email:S.clean(document.getElementById('f-email')?.value||''),aadhaar,pan,address:S.clean(document.getElementById('f-addr')?.value||'')};renderStep2();}

function renderStep2(){document.getElementById('mBody').innerHTML=stepBar(2)+`
<div style="font-size:.8rem;color:var(--muted2);margin-bottom:12px">Upload documents (Aadhaar, PAN, Photo). Stored securely in Firebase Storage.</div>
<div class="up-zone" id="up-zone"><div class="u-ico"><i class="fas fa-cloud-upload-alt"></i></div><div class="u-txt">Click or drag to upload files</div><div class="u-sub">PDF, JPG, PNG • Max 100MB</div><input type="file" id="up-files" multiple accept=".pdf,.jpg,.jpeg,.png" onchange="onFilesSelected(this)"></div>
<div class="up-ok" id="up-ok"><i class="fas fa-check-circle"></i><span id="up-ok-txt"></span></div>
<div class="up-prog" id="up-prog"><div class="up-prog-fill" id="up-fill" style="width:0%"></div></div>
<div id="up-file-list" style="margin-top:7px;font-size:.7rem;color:var(--muted2)"></div>
<div style="margin-top:12px;background:rgba(255,183,0,.07);border:1px solid rgba(255,183,0,.18);border-radius:8px;padding:10px;font-size:.75rem;color:var(--warn)"><i class="fas fa-info-circle"></i> For Aadhaar updates: only official UIDAI portal accepts uploads.</div>
<div style="display:flex;gap:9px;margin-top:12px"><button class="btn btn-outline" onclick="document.getElementById('mBody').innerHTML=renderStep1(A.svc)" style="flex:0 0 auto;width:auto">← Back</button><button class="btn btn-fire" id="btn-upload" onclick="uploadAndProceed()"><i class="fas fa-upload"></i> Upload & Continue</button></div>`;}

function onFilesSelected(input){const files=Array.from(input.files);if(!files.length)return;document.getElementById('up-ok-txt').textContent=`${files.length} file(s) selected`;document.getElementById('up-ok').classList.add('on');document.getElementById('up-file-list').innerHTML=files.map(f=>`<div>📄 ${S.esc(f.name)} (${(f.size/1024).toFixed(1)} KB)</div>`).join('');document.getElementById('up-zone').style.borderColor='var(--jade)';}

async function uploadAndProceed(){const input=document.getElementById('up-files');const files=input?.files?Array.from(input.files):[];const btn=document.getElementById('btn-upload');btn.disabled=true;btn.innerHTML='<div class="spin"></div> Uploading…';A.uploadedFiles={};if(files.length>0){const prog=document.getElementById('up-prog');const fill=document.getElementById('up-fill');prog.classList.add('on');let done=0;for(const file of files){try{const safeName=file.name.replace(/[^a-zA-Z0-9._-]/g,'_').slice(0,100);const path=`uploads/${A.user.uid}/${S.token(8)}_${safeName}`;const ref=storage.ref(path);await ref.put(file);const url=await ref.getDownloadURL();A.uploadedFiles[safeName]=url;done++;fill.style.width=(done/files.length*100)+'%';}catch(e){toast(`Upload failed: ${file.name}`,'warn');}}toast(`${done}/${files.length} files uploaded`);}renderStep3();}

function renderStep3(){const svc=A.svc;const txn='TXN'+S.token(8);A.txnId=txn;const upiStr=`upi://pay?pa=${UPI}&pn=CyberAce&am=${svc.price}&cu=INR&tn=${txn}`;document.getElementById('mBody').innerHTML=stepBar(3)+`
<div class="qr-box"><div style="font-size:.83rem;color:var(--muted2);margin-bottom:12px">Scan with PhonePe, GPay, Paytm, BHIM</div><div id="pay-qr"></div><div class="qr-amt">₹${svc.price}</div><div class="qr-upi">${UPI}</div><div class="qr-txn" onclick="navigator.clipboard.writeText('${txn}').then(()=>toast('Copied!'))" title="Click to copy"><i class="fas fa-copy"></i> ${txn}</div></div>
<div class="pay-breakdown"><div class="pb-row"><span>Government Fee</span><span style="color:var(--muted2)">₹${svc.price-svc.comm}</span></div><div class="pb-row"><span>Service Fee</span><span style="color:var(--jade)">₹${svc.comm}</span></div><div class="pb-row"><span>Total</span><span style="color:var(--fire)">₹${svc.price}</span></div></div>
<div class="utr-wrap"><div style="font-weight:600;margin-bottom:6px">✅ Enter UTR/Reference after payment:</div><input class="fld-in" style="padding-left:12px" id="utr-in" placeholder="12-digit UTR / Reference (optional)" maxlength="25"></div>
<button class="btn btn-fire" onclick="submitApplication()"><i class="fas fa-paper-plane"></i> Submit Application</button>
<button class="btn btn-outline" style="margin-top:7px" onclick="renderStep2()">← Back</button>`;
setTimeout(()=>{try{new QRCode(document.getElementById('pay-qr'),{text:upiStr,width:160,height:160});}catch(e){}},80);}

async function submitApplication(){const btn=document.querySelector('#mBody .btn-fire');if(btn){btn.disabled=true;btn.innerHTML='<div class="spin"></div> Saving…';}const svc=A.svc;const appNumber='APP'+S.token(8);const platformCut=Math.round(svc.comm*PLATFORM_CUT);
try{const docRef=await db.collection('applications').add({uid:A.user.uid,operatorEmail:A.user.email,appNumber,serviceId:svc.id,serviceName:svc.name,serviceCategory:svc.cat,customerName:A.formData.name||'',customerDob:A.formData.dob||'',customerPhone:A.formData.mobile||'',customerEmail:A.formData.email||'',aadhaar:A.formData.aadhaar||'',pan:A.formData.pan||'',address:A.formData.address||'',amount:svc.price,commission:svc.comm,platformCut,netCommission:svc.comm-platformCut,txnId:A.txnId||'',utrRef:S.clean(document.getElementById('utr-in')?.value||''),uploadedFiles:A.uploadedFiles||{},portalUrl:svc.url||'',status:'submitted',paymentVerified:false,createdAt:firebase.firestore.FieldValue.serverTimestamp()});
renderStep4(appNumber,docRef.id,svc);toast(`✅ ${svc.name} submitted! +₹${svc.comm} commission`);}
catch(e){toast('Save failed: '+e.message,'err');if(btn){btn.disabled=false;btn.innerHTML='<i class="fas fa-paper-plane"></i> Submit Application';}}}

function renderStep4(appNumber,docId,svc){
  const d=A.formData||{};
  let portalHost='';try{portalHost=new URL(svc.url||'https://x').hostname.replace('www.','');}catch(e){}
  // Save to localStorage for bookmarklet
  try{localStorage.setItem('ca_autofill',JSON.stringify({data:d,url:svc.url||'',service:svc.name,ts:Date.now()}));}catch(e){}
  showDataPanel(d,svc);
  const rawFields={name:d.name,dob:d.dob,mobile:d.mobile,email:d.email,aadhaar:d.aadhaar,pan:d.pan,address:d.address};
  const fieldRows=Object.entries(rawFields).filter(([,v])=>v).map(([k,v])=>`<div class="fd-row"><span class="fd-k">${k[0].toUpperCase()+k.slice(1)}</span><span class="fd-v">${k==='aadhaar'?v.replace(/\d(?=\d{4})/g,'×'):S.esc(v)}</span><button class="fd-copy" onclick="dpCopy('${k}',${JSON.stringify(v)},this)">📋</button></div>`).join('');
  document.getElementById('mBody').innerHTML=stepBar(4)+`<div class="success-scr"><div class="s-ico">🎉</div><div class="s-title">Application Submitted!</div>
<p style="font-size:.76rem;color:var(--muted2);margin-top:4px">App No: <strong style="color:var(--jade);font-family:var(--ff-mono)">${S.esc(appNumber)}</strong> • Commission: <strong style="color:var(--jade)">+₹${svc.comm}</strong></p>
${svc.url?`<div style="background:linear-gradient(135deg,rgba(0,191,165,.1),rgba(0,191,165,.03));border:2px solid rgba(0,191,165,.4);border-radius:13px;padding:15px;margin-top:13px;text-align:center">
<div style="font-weight:700;color:var(--jade);font-size:.9rem;margin-bottom:7px">🚀 Step 1 — Open Official Portal</div>
<a href="${S.esc(svc.url)}" target="_blank" rel="noopener noreferrer" onclick="onPortalClick()" style="display:inline-flex;align-items:center;gap:8px;padding:13px 24px;background:linear-gradient(135deg,#00BFA5,#00695C);color:#fff;border-radius:10px;font-weight:700;font-size:.9rem;text-decoration:none;box-shadow:0 6px 20px rgba(0,191,165,.4)"><i class="fas fa-external-link-alt"></i> Open ${S.esc(portalHost)}</a>
<div style="margin-top:7px;font-size:.68rem;color:var(--muted)">🔗 ${S.esc(svc.url)}</div></div>
<div style="background:rgba(255,183,0,.07);border:1px solid rgba(255,183,0,.25);border-radius:10px;padding:13px;margin-top:9px">
<div style="font-weight:700;color:var(--warn);margin-bottom:7px">📋 Step 2 — Copy Fields (tap 📋)</div>
<div class="fd-list">${fieldRows}</div>
<button class="btn btn-outline btn-sm" style="width:auto;margin-top:9px" onclick="dpCopyAll(${JSON.stringify(rawFields).replace(/"/g,'&quot;')})"><i class="fas fa-copy"></i> Copy All</button>
<button class="btn btn-outline btn-sm" style="width:auto;margin-top:9px;margin-left:6px" onclick="showDataPanel(A.formData,A.svc)"><i class="fas fa-window-restore"></i> Floating Panel</button>
</div>`:
`<div style="margin-top:13px;text-align:center"><a href="https://www.google.com/search?q=${encodeURIComponent(svc.name+' official portal apply India 2026')}" target="_blank" rel="noopener" style="display:inline-flex;align-items:center;gap:7px;padding:10px 18px;background:linear-gradient(135deg,#4285F4,#1565C0);color:#fff;border-radius:9px;font-weight:700;font-size:.83rem;text-decoration:none"><i class="fab fa-google"></i> Search Official Portal</a></div>`}
</div><button class="btn btn-fire" style="margin-top:11px" onclick="closeModal();${A.isAdmin?`gotoView('applications')`:`toast('Visit the portal to complete your application')`}"><i class="fas fa-check-circle"></i> Done</button>`;}

function onPortalClick(){try{localStorage.setItem('ca_autofill',JSON.stringify({data:A.formData||{},url:A.svc?.url||'',service:A.svc?.name||'',ts:Date.now()}));}catch(e){}setTimeout(()=>{if(!document.getElementById('__dp__'))showDataPanel(A.formData||{},A.svc||{});},500);}

/* ━━━ DATA PANEL + AUTO-FILL ━━━ */
function showDataPanel(data,svc){
  const old=document.getElementById('__dp__');if(old)old.remove();
  if(!data||!Object.values(data||{}).some(Boolean))return;
  const FM=[{k:'name',lbl:'Name'},{k:'mobile',lbl:'Mobile'},{k:'dob',lbl:'DOB'},{k:'email',lbl:'Email'},{k:'aadhaar',lbl:'Aadhaar'},{k:'pan',lbl:'PAN'},{k:'address',lbl:'Address'}];
  const rows=FM.filter(r=>data[r.k]).map(r=>`<div class="dp-row"><span class="dp-lbl">${r.lbl}</span><span class="dp-val" title="${S.esc(data[r.k])}">${r.k==='aadhaar'?(data[r.k]||'').replace(/\d(?=\d{4})/g,'×'):S.esc(data[r.k])}</span><button class="dp-cp" onclick="dpCopy('${r.lbl}',${JSON.stringify(data[r.k]||'')},this)">📋</button></div>`).join('');
  const panel=document.createElement('div');panel.id='__dp__';
  panel.innerHTML=`<div class="dp-inner" id="__dp_inner__"><div class="dp-hd" id="__dp_hd__"><span class="dp-ht">🧠 Customer Data</span><button class="dp-min" onclick="document.getElementById('__dp_inner__').classList.toggle('dp-minimized')">—</button><button class="dp-close" onclick="document.getElementById('__dp__').remove()">×</button></div><div class="dp-bd"><div class="dp-svc">${svc&&svc.name?S.esc(svc.name):'Tap 📋 to copy'}</div>${rows}</div><div class="dp-ft"><button class="dp-btn-copy" onclick="dpCopyAll(${JSON.stringify(data).replace(/"/g,'&quot;')})">📋 Copy All</button><button class="dp-btn-hide" onclick="document.getElementById('__dp__').remove()">✓ Done</button></div></div>`;
  document.body.appendChild(panel);
  const hd=document.getElementById('__dp_hd__');let ox=0,oy=0,drag=false;
  const ds=(cx,cy)=>{drag=true;panel.style.right='auto';ox=cx-panel.offsetLeft;oy=cy-panel.offsetTop;};
  hd.addEventListener('mousedown',e=>ds(e.clientX,e.clientY));
  hd.addEventListener('touchstart',e=>{const t=e.touches[0];ds(t.clientX,t.clientY);},{passive:true});
  document.addEventListener('mousemove',e=>{if(drag){panel.style.left=Math.max(0,e.clientX-ox)+'px';panel.style.top=Math.max(0,Math.min(window.innerHeight-60,e.clientY-oy))+'px';panel.style.bottom='auto';}});
  document.addEventListener('touchmove',e=>{if(drag){const t=e.touches[0];panel.style.left=Math.max(0,t.clientX-ox)+'px';panel.style.top=Math.max(0,t.clientY-oy)+'px';panel.style.bottom='auto';}},{passive:true});
  document.addEventListener('mouseup',()=>drag=false);document.addEventListener('touchend',()=>drag=false);
}
function dpCopy(lbl,val,btn){const text=String(val||'');const done=()=>{const o=btn.innerHTML;btn.innerHTML='✅';btn.style.color='#00E676';setTimeout(()=>{btn.innerHTML=o;btn.style.color='';},1400);toast(lbl+' copied!');};if(navigator.clipboard){navigator.clipboard.writeText(text).then(done).catch(()=>legacyCopy(text,done));}else legacyCopy(text,done);}
function dpCopyAll(data){const text=Object.entries(data||{}).filter(([,v])=>v).map(([k,v])=>k[0].toUpperCase()+k.slice(1)+': '+v).join('\n');const done=()=>toast('✅ All data copied!');if(navigator.clipboard){navigator.clipboard.writeText(text).then(done).catch(()=>legacyCopy(text,done));}else legacyCopy(text,done);}
function legacyCopy(text,cb){const t=document.createElement('textarea');t.value=text;t.style.cssText='position:fixed;opacity:0;top:0;left:0;width:1px;height:1px';document.body.appendChild(t);t.select();t.setSelectionRange(0,99999);try{document.execCommand('copy');if(cb)cb();}catch(e){}document.body.removeChild(t);}
function saveJobData(title,url){try{localStorage.setItem('ca_autofill',JSON.stringify({data:A.formData||{},url,service:title,ts:Date.now()}));}catch(e){}showDataPanel(A.formData||{},{name:title,url});}
function quickLaunch(svc){if(svc.url){window.open(svc.url,'_blank');toast('Opening '+svc.name+'…');}else openGoogleSearch(svc.name);}
function openGoogleSearch(q){window.open('https://www.google.com/search?q='+encodeURIComponent(q+' official portal India 2026'),'_blank');}

Object.assign(window,{switchTab,toggleEye,updatePwdStr,doLogin,doSignup,doResetPwd,doLogout,gotoView,gotoViewFiltered,toggleSB,filterSvc,filterJobs,openApplyModal,openJobApply,closeModal,validateStep1,renderStep1,renderStep2,uploadAndProceed,onFilesSelected,renderStep3,submitApplication,runOCR,useOCRData,adminVerifyPayment,recalc,fmtINR,showDataPanel,dpCopy,dpCopyAll,quickLaunch,openGoogleSearch,saveJobData,onPortalClick,searchAll,renderSearchResults,onSearchClick,searchBarHtml});
const ts=document.createElement('script');ts.src='https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js';document.head.appendChild(ts);
</script>
</body>
</html>
