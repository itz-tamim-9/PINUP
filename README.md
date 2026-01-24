<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PINUP PREMIUM | ULTIMATE</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #09090b;
            --card-glass: rgba(30, 30, 35, 0.8);
            --gold: #FFD700;
            --ff-orange: #FF9900;
            --ff-yellow: #FFFF00;
            --neon: #00f3ff;
            --text-main: #ffffff;
            --font-head: 'Orbitron', sans-serif;
            --font-body: 'Poppins', sans-serif;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; outline: none; }
        body { 
            background: var(--bg-dark); 
            color: var(--text-main); 
            font-family: var(--font-body); 
            height: 100vh; 
            overflow: hidden;
            background-image: radial-gradient(circle at 50% 10%, #1a1a2e 0%, #000 100%);
        }

        .hidden { display: none !important; }
        .glass {
            background: var(--card-glass); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.08); box-shadow: 0 4px 30px rgba(0, 0, 0, 0.5);
        }

        /* --- AUTH SCREEN --- */
        #auth-screen { position: fixed; inset: 0; z-index: 9999; background: url('https://wallpapers.com/s/hd/free-fire-cool-background-1920-x-1080-3l3k6p5w5z5w5z5w.jpg') no-repeat center center/cover; }
        .auth-box { width: 90%; max-width: 350px; padding: 30px; border-radius: 20px; text-align: center; border: 1px solid var(--gold); background: rgba(0,0,0,0.85); position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
        .inp-field { width: 100%; background: rgba(255,255,255,0.08); border: 1px solid #444; padding: 15px; border-radius: 12px; color: white; margin: 15px 0; transition: 0.3s; font-family: var(--font-body); }
        .inp-field:focus { border-color: var(--gold); }
        .btn-main { width: 100%; padding: 14px; background: linear-gradient(135deg, var(--gold), #ffa500); color: #000; border: none; border-radius: 10px; font-weight: 700; font-family: var(--font-head); cursor: pointer; clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px); transition: transform 0.1s; }
        .btn-main:active { transform: scale(0.95); }
        
        /* --- MAIN LAYOUT --- */
        #main-app { height: 100%; display: flex; flex-direction: column; }
        .app-header { padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05); }
        .u-img { width: 45px; height: 45px; border-radius: 50%; border: 2px solid var(--gold); object-fit: cover; }
        .balance-pill { background: rgba(0,0,0,0.6); border: 1px solid var(--gold); padding: 8px 16px; border-radius: 50px; display: flex; align-items: center; gap: 8px; cursor: pointer; }
        .content-area { flex: 1; overflow-y: auto; padding: 20px; padding-bottom: 100px; }
        .section-head { font-family: var(--font-head); font-size: 1.2rem; color: var(--gold); margin-bottom: 20px; border-left: 4px solid var(--neon); padding-left: 12px; }

        /* --- TASKS --- */
        .task-item { background: linear-gradient(90deg, #1a1a1a, #0d0d0d); border: 1px solid #333; padding: 15px; margin-bottom: 15px; border-radius: 12px; }
        .task-link-box { background: #000; color: var(--neon); padding: 8px; border-radius: 4px; font-family: monospace; font-size: 0.8rem; border: 1px solid #333; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; flex: 1; margin-right: 10px; }
        .btn-copy { background: #333; color: white; border: none; padding: 8px 15px; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 0.8rem; }
        .btn-claim { width: 100%; padding: 12px; border: none; margin-top: 15px; background: linear-gradient(to bottom, var(--ff-yellow), var(--ff-orange)); color: black; font-weight: 800; font-family: var(--font-head); border-radius: 8px; cursor: pointer; border-bottom: 3px solid #b36b00; }
        .btn-claim:active { border-bottom: 1px solid #b36b00; transform: translateY(2px); }

        /* --- STORE --- */
        .topup-tabs { display: flex; gap: 10px; margin-bottom: 20px; overflow-x: auto; padding-bottom: 5px; }
        .tab-btn { background: #222; color: #aaa; padding: 8px 16px; border-radius: 20px; border: 1px solid #333; white-space: nowrap; font-size: 0.85rem; cursor: pointer; }
        .tab-btn.active { background: var(--gold); color: black; font-weight: bold; border-color: var(--gold); }
        .topup-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
        .topup-card { text-align: center; padding: 15px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.1); position: relative; overflow: hidden; transition: 0.3s; }
        .topup-card:active { transform: scale(0.98); border-color: var(--gold); }
        .topup-price { background: var(--gold); color: black; display: inline-block; padding: 2px 10px; border-radius: 4px; font-weight: bold; font-size: 0.9rem; margin-top: 5px; }

        /* --- CHAT & HISTORY --- */
        #chat-window { height: 60vh; display: flex; flex-direction: column; background: #000; border-radius: 20px; border: 1px solid #222; overflow: hidden; background-image: url('https://www.transparenttextures.com/patterns/carbon-fibre.png'); }
        #msg-container { flex: 1; overflow-y: auto; padding: 15px; display: flex; flex-direction: column; gap: 10px; }
        .chat-bubble { max-width: 75%; padding: 10px 14px; font-size: 0.9rem; border-radius: 15px; word-wrap: break-word; }
        .mine { align-self: flex-end; background: linear-gradient(135deg, var(--gold), #e6b800); color: black; border-bottom-right-radius: 2px; }
        .theirs { align-self: flex-start; background: #222; border: 1px solid #333; color: white; border-bottom-left-radius: 2px; }
        .history-item { display: flex; justify-content: space-between; padding: 12px; background: rgba(255,255,255,0.03); margin-bottom: 8px; border-radius: 8px; font-size: 0.85rem; border-left: 2px solid #333; }

        /* --- BOTTOM NAV --- */
        .btm-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; background: rgba(15, 15, 15, 0.95); backdrop-filter: blur(20px); border-radius: 25px; padding: 15px 30px; border: 1px solid rgba(255,215,0,0.2); display: flex; justify-content: space-between; z-index: 100; box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
        .nav-icon { font-size: 1.4rem; color: #555; transition: 0.3s; }
        .nav-icon.active { color: var(--gold); transform: translateY(-5px); text-shadow: 0 0 10px var(--gold); }

        /* --- MODALS --- */
        .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 2000; display: flex; justify-content: center; align-items: center; opacity: 0; pointer-events: none; transition: 0.3s; }
        .modal-bg.active { opacity: 1; pointer-events: all; }
        .modal-content { background: #121214; width: 90%; max-width: 350px; padding: 25px; border-radius: 20px; border: 1px solid var(--gold); text-align: center; transform: scale(0.8); transition: 0.3s; }
        .modal-bg.active .modal-content { transform: scale(1); }

        /* --- ADMIN PANEL (Hidden) --- */
        #admin-panel { background: #f4f6f9; color: #333; position: fixed; inset: 0; z-index: 5000; overflow-y: auto; display: none; font-family: sans-serif; }
        .ad-header { background: #1e1e2d; color: #fff; padding: 15px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 10; }
        .ad-container { padding: 15px; }
        .ad-card { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); margin-bottom: 15px; }
        .ad-nav { position: fixed; bottom: 0; width: 100%; background: white; display: flex; border-top: 1px solid #ddd; padding: 10px 0; }
        .ad-nav-item { flex: 1; text-align: center; color: #666; cursor: pointer; padding: 5px; }
        .ad-nav-item.active { color: #007bff; font-weight: bold; }
        .ad-section { display: none; } .ad-section.active { display: block; }
        
        /* Switch UI */
        .switch { position: relative; display: inline-block; width: 46px; height: 24px; }
        .slider { position: absolute; cursor: pointer; inset: 0; background-color: #333; border-radius: 34px; border: 1px solid #555; transition: .4s; }
        .slider:before { position: absolute; content: ""; height: 18px; width: 18px; left: 3px; bottom: 2px; background-color: white; border-radius: 50%; transition: .4s; }
        input:checked + .slider { background-color: var(--gold); }
        input:checked + .slider:before { transform: translateX(21px); }
    </style>
</head>
<body onclick="initAudio()">

    <audio id="bgMusic" src="https://files.catbox.moe/p9r1m0.mp3" loop preload="auto"></audio> <audio id="snd-tap" src="https://www.soundjay.com/buttons/sounds/button-16.mp3" preload="auto"></audio> <audio id="snd-success" src="https://files.catbox.moe/nbt2p7.mp3" preload="auto"></audio> <audio id="snd-error" src="https://www.soundjay.com/buttons/sounds/button-10.mp3" preload="auto"></audio> <audio id="snd-close" src="https://www.soundjay.com/buttons/sounds/button-50.mp3" preload="auto"></audio> <audio id="snd-key" src="https://www.soundjay.com/buttons/sounds/button-37.mp3" preload="auto"></audio> <div id="auth-screen">
        <div class="auth-box glass">
            <h1 style="font-family: 'Orbitron'; color: var(--gold); font-size: 2.5rem;">PINUP</h1>
            <p style="color: #ccc; margin-bottom: 20px;">Elite Rewards Engine</p>
            <input type="email" id="login-email" class="inp-field" placeholder="Enter Valid Gmail..." oninput="playSnd('key')">
            <button class="btn-main" onclick="playSnd('tap'); app.login()">START ENGINE</button>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <div class="app-header glass">
            <div class="user-info" onclick="playSnd('tap'); app.nav('page-profile')">
                <img src="" id="head-img" class="u-img">
                <div><div id="head-name" style="font-weight: 600;">Player</div><div style="font-size: 0.7rem; color: var(--gold);">ELITE MEMBER</div></div>
            </div>
            <div class="balance-pill" onclick="playSnd('tap'); app.openWithdraw()"><i class="fas fa-gem" style="color: var(--gold);"></i><span id="head-bal">0</span></div>
        </div>

        <div class="content-area">
            <div id="page-home" class="page-sec">
                <div style="width: 100%; margin-bottom: 25px; border-radius: 15px; overflow: hidden; background: #000;">
                    <iframe width="100%" height="200" src="https://www.youtube.com/embed/MeamyO9UxPk" frameborder="0"></iframe>
                </div>
                <h3 class="section-head"><i class="fas fa-crosshairs"></i> MISSIONS</h3>
                <div id="task-list"></div>
            </div>

            <div id="page-topup" class="page-sec hidden">
                <h3 class="section-head"><i class="fas fa-bolt"></i> STORE</h3>
                <div class="topup-tabs">
                    <button class="tab-btn active" onclick="playSnd('tap'); app.renderTopUp('regular', this)">Diamonds</button>
                    <button class="tab-btn" onclick="playSnd('tap'); app.renderTopUp('special', this)">Special Packs</button>
                    <button class="tab-btn" onclick="playSnd('tap'); app.renderTopUp('member', this)">Memberships</button>
                </div>
                <div id="topup-grid" class="topup-grid"></div>
            </div>

            <div id="page-rank" class="page-sec hidden">
                <div class="glass" style="padding: 20px; text-align: center; margin-bottom: 20px;">
                    <p style="color: #888;">TOTAL PLAYERS</p>
                    <h1 style="color: var(--neon); font-family: 'Orbitron';"><i class="fas fa-users"></i> <span id="total-players">0</span></h1>
                </div>
                <h3 class="section-head"><i class="fas fa-trophy"></i> LEADERBOARD</h3>
                <div id="lb-list"></div>
            </div>

            <div id="page-chat" class="page-sec hidden" style="height: 100%;">
                <h3 class="section-head"><i class="fas fa-headset"></i> SUPPORT</h3>
                <div id="chat-window">
                    <div id="msg-container"></div>
                    <div style="padding: 10px; background: #111; display: flex; gap: 10px; align-items: center; border-top: 1px solid #333;">
                        <input id="chat-inp" class="inp-field" style="margin:0; border-radius: 50px; padding: 10px 20px;" placeholder="Type message..." oninput="playSnd('key')">
                        <button onclick="playSnd('tap'); app.sendMsg()" style="background: var(--gold); width: 40px; height: 40px; border-radius: 50%; border: none;"><i class="fas fa-paper-plane"></i></button>
                    </div>
                </div>
            </div>

            <div id="page-profile" class="page-sec hidden">
                <div class="glass" style="padding: 30px; border-radius: 20px; position: relative;">
                    <div class="profile-head">
                        <img src="" id="p-img" class="u-img" style="width: 100px; height: 100px; border: 4px solid var(--gold);">
                        <div onclick="playSnd('tap'); tryAdminAccess()" style="position: absolute; bottom: 0; right: 35%; background: var(--gold); color: black; width: 30px; height: 30px; border-radius: 50%; display: grid; place-items: center; cursor: pointer;">
                            <i class="fas fa-shield-alt"></i>
                        </div>
                        <h2 id="p-name" style="margin-top: 15px; color: white;">Name</h2>
                        <p id="p-email" style="color: #777; font-size: 0.8rem;">email@gmail.com</p>
                    </div>

                    <div style="background: rgba(255,255,255,0.05); padding: 15px; border-radius: 12px; display: flex; justify-content: space-between; align-items: center; margin-top: 20px; border: 1px solid #444;">
                        <span><i class="fas fa-music" style="color: var(--gold);"></i> Phonk BGM</span>
                        <label class="switch">
                            <input type="checkbox" id="musicToggle" onchange="playSnd('tap'); toggleBGM(this.checked)" checked>
                            <span class="slider"></span>
                        </label>
                    </div>
                </div>
                <h3 class="section-head" style="margin-top: 30px;"><i class="fas fa-history"></i> HISTORY</h3>
                <div id="history-list"></div>
            </div>
        </div>

        <div class="btm-nav">
            <i class="fas fa-home nav-icon active" onclick="playSnd('tap'); app.nav('page-home', this)"></i>
            <i class="fas fa-shopping-cart nav-icon" onclick="playSnd('tap'); app.nav('page-topup', this)"></i>
            <i class="fas fa-chart-bar nav-icon" onclick="playSnd('tap'); app.nav('page-rank', this)"></i>
            <i class="fas fa-comments nav-icon" onclick="playSnd('tap'); app.nav('page-chat', this)"></i>
            <i class="fas fa-user nav-icon" onclick="playSnd('tap'); app.nav('page-profile', this)"></i>
        </div>
    </div>

    <div id="modal-claim" class="modal-bg">
        <div class="modal-content glass">
            <h3 style="color: var(--gold); font-family: 'Orbitron';">MISSION CODE</h3>
            <input id="claim-inp" class="inp-field" placeholder="Enter Code..." oninput="playSnd('key')" style="text-align: center; letter-spacing: 2px;">
            <button class="btn-main" onclick="app.doClaim()">CLAIM REWARD</button>
            <button onclick="playSnd('close'); document.getElementById('modal-claim').classList.remove('active')" style="background:none; border:none; color:#777; margin-top:15px; cursor:pointer;">CLOSE</button>
        </div>
    </div>

    <div id="modal-wd" class="modal-bg">
        <div class="modal-content glass">
            <h2 style="color:var(--gold);">WITHDRAW</h2>
            <input id="wd-uid" class="inp-field" placeholder="Enter Player UID" oninput="playSnd('key')" style="text-align:center">
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:20px">
                <button class="tab-btn" onclick="playSnd('tap'); app.selWd(100,this)">100 💎</button>
                <button class="tab-btn" onclick="playSnd('tap'); app.selWd(300,this)">300 💎</button>
            </div>
            <button class="btn-main" onclick="playSnd('tap'); app.submitWd()">CONFIRM</button>
            <button onclick="playSnd('close'); document.getElementById('modal-wd').classList.remove('active')" style="background:none;color:#777;border:none;margin-top:15px">Cancel</button>
        </div>
    </div>

    <div id="modal-pay" class="modal-bg">
        <div class="modal-content glass">
            <h3>Confirm Payment</h3>
            <p style="margin:10px 0;color:#ccc">Send <b style="color:var(--gold)" id="pay-amt">0</b> to 01965613742</p>
            <input id="pay-trx" class="inp-field" placeholder="TrxID / Last 4 Digits" oninput="playSnd('key')">
            <button class="btn-main" onclick="playSnd('tap'); app.doPay()">SUBMIT</button>
            <button onclick="playSnd('close'); document.getElementById('modal-pay').classList.remove('active')" style="background:none;border:none;color:#555;margin-top:10px">Close</button>
        </div>
    </div>

    <div id="admin-panel">
        <div class="ad-header"><h3>ADMIN PANEL</h3><button class="btn-main" style="width:auto; padding:5px 15px; background:red; color:white;" onclick="playSnd('close'); closeAdmin()">EXIT</button></div>
        
        <div id="ad-dash" class="ad-container ad-section active">
            <div class="ad-card"><h4>Total Users: <span id="st-users" style="color:blue">0</span></h4><button style="color:red; border:none; background:none; cursor:pointer; margin-top:5px;" onclick="if(confirm('Reset DB?')){localStorage.removeItem('pinup_ult_v5');location.reload();}">Reset All Data</button></div>
            <div class="ad-card"><h4>Requests</h4><div id="req-list"></div></div>
        </div>

        <div id="ad-users" class="ad-container ad-section">
            <div class="ad-card" id="user-list"></div>
        </div>

        <div id="ad-tasks" class="ad-container ad-section">
            <div class="ad-card"><h4>Add Task</h4><input id="t-tit" placeholder="Title"><input id="t-lnk" placeholder="Link"><input id="t-cod" placeholder="Code"><input id="t-rew" type="number" placeholder="Reward"><button class="btn-main" onclick="adm.addTask()">ADD</button></div>
            <div id="active-tasks"></div>
        </div>

        <div class="ad-nav">
            <div class="ad-nav-item active" onclick="playSnd('tap'); adNav('ad-dash',this)">Home</div>
            <div class="ad-nav-item" onclick="playSnd('tap'); adNav('ad-users',this)">Users</div>
            <div class="ad-nav-item" onclick="playSnd('tap'); adNav('ad-tasks',this)">Tasks</div>
        </div>
    </div>

    <script>
        const DB = 'pinup_ult_v5';
        let audioActive = false;

        // --- SOUND ENGINE ---
        function playSnd(type) {
            const snds = {
                tap: document.getElementById('snd-tap'),
                success: document.getElementById('snd-success'),
                error: document.getElementById('snd-error'),
                close: document.getElementById('snd-close'),
                key: document.getElementById('snd-key')
            };
            if(snds[type]) { snds[type].currentTime = 0; snds[type].play().catch(e=>{}); }
        }

        function initAudio() {
            if(!audioActive) {
                const bgm = document.getElementById('bgMusic');
                bgm.volume = 0.4;
                bgm.play().then(()=>audioActive=true).catch(e=>{});
            }
        }
        function toggleBGM(isOn) {
            const bgm = document.getElementById('bgMusic');
            isOn ? bgm.play() : bgm.pause();
        }

        // --- ADMIN SECRET LOGIC ---
        let admClicks = 0, admTimer;
        function tryAdminAccess() {
            clearTimeout(admTimer); admClicks++; admTimer = setTimeout(()=>admClicks=0, 2000);
            if(admClicks >= 8) {
                admClicks = 0; playSnd('key');
                const pin = prompt("ENTER ADMIN PIN:");
                if(pin === "41420") { playSnd('success'); openAdmin(); } else { playSnd('error'); }
            }
        }
        function openAdmin() { document.getElementById('main-app').classList.add('hidden'); document.getElementById('admin-panel').style.display='block'; adm.init(); }
        function closeAdmin() { document.getElementById('admin-panel').style.display='none'; document.getElementById('main-app').classList.remove('hidden'); }
        function adNav(id, el) { document.querySelectorAll('.ad-section').forEach(s=>s.classList.remove('active')); document.getElementById(id).classList.add('active'); document.querySelectorAll('.ad-nav-item').forEach(i=>i.classList.remove('active')); el.classList.add('active'); if(id==='ad-users') adm.renderUsers(); if(id==='ad-tasks') adm.renderTasks(); }

        // --- MAIN APP LOGIC ---
        const app = {
            user: null, tempTask: null, wdVal: 0, payItem: null, payCost: null,
            init: () => {
                if(!localStorage.getItem(DB)) localStorage.setItem(DB, JSON.stringify({ users: [], tasks: [], withdrawals: [], msgs: [] }));
                const sess = localStorage.getItem('pinup_sess_v5');
                if(sess) {
                    app.user = JSON.parse(localStorage.getItem(DB)).users.find(u => u.email === sess);
                    if(app.user && !app.user.blocked) app.load();
                }
            },
            login: () => {
                const e = document.getElementById('login-email').value.trim().toLowerCase();
                if(!e.endsWith('@gmail.com')) { playSnd('error'); return alert("Invalid Gmail"); }
                const db = JSON.parse(localStorage.getItem(DB));
                let u = db.users.find(x => x.email === e);
                if(!u) {
                    u = { email:e, name:e.split('@')[0], photo:'https://ui-avatars.com/api/?name='+e+'&background=FFD700&color=000', diamonds:0, history:[], tasks:[], blocked:false };
                    db.users.push(u); localStorage.setItem(DB, JSON.stringify(db));
                }
                if(u.blocked) { playSnd('error'); return alert("BANNED!"); }
                app.user = u; localStorage.setItem('pinup_sess_v5', e);
                playSnd('success'); app.load();
            },
            load: () => {
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                app.refresh(); app.renderTasks(); app.renderTopUp('regular', document.querySelector('.tab-btn')); app.renderChat(); app.renderRank();
            },
            refresh: () => {
                const db = JSON.parse(localStorage.getItem(DB));
                app.user = db.users.find(u => u.email === app.user.email);
                document.getElementById('head-name').innerText = app.user.name;
                document.getElementById('head-bal').innerText = app.user.diamonds;
                document.getElementById('head-img').src = app.user.photo;
                document.getElementById('p-img').src = app.user.photo;
                document.getElementById('p-name').innerText = app.user.name;
                document.getElementById('p-email').innerText = app.user.email;
                document.getElementById('total-players').innerText = db.users.length;
                
                const hl = document.getElementById('history-list'); hl.innerHTML = '';
                [...app.user.history].reverse().forEach(h => {
                    hl.innerHTML += `<div class="history-item"><span>${h.desc}</span><span style="color:${h.type==='in'?'#00ff00':'#ff4757'}">${h.type==='in'?'+':'-'}${h.amt}</span></div>`;
                });
            },
            nav: (pid, el) => {
                document.querySelectorAll('.page-sec').forEach(p => p.classList.add('hidden'));
                document.getElementById(pid).classList.remove('hidden');
                if(el) { document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('active')); el.classList.add('active'); }
            },
            // TASKS
            renderTasks: () => {
                const db = JSON.parse(localStorage.getItem(DB));
                const list = document.getElementById('task-list'); list.innerHTML = '';
                db.tasks.forEach(t => {
                    if(!app.user.tasks.includes(t.id)) {
                        list.innerHTML += `<div class="task-item"><div style="display:flex;justify-content:space-between;align-items:center;"><b>${t.title}</b><span style="color:var(--gold);">+${t.reward} 💎</span></div><div style="margin-top:10px;display:flex;"><div class="task-link-box">${t.link}</div><button class="btn-copy" onclick="playSnd('tap');navigator.clipboard.writeText('${t.link}')">COPY</button></div><button class="btn-claim" onclick="playSnd('tap'); app.initClaim(${t.id}, '${t.code}', ${t.reward})">CLAIM REWARD</button></div>`;
                    }
                });
            },
            initClaim: (id, code, rew) => { app.tempTask = {id, code, rew}; document.getElementById('claim-inp').value=''; document.getElementById('modal-claim').classList.add('active'); },
            doClaim: () => {
                if(document.getElementById('claim-inp').value !== app.tempTask.code) { playSnd('error'); return alert("Wrong Code!"); }
                const db = JSON.parse(localStorage.getItem(DB));
                const u = db.users.find(x => x.email === app.user.email);
                u.diamonds += app.tempTask.rew; u.tasks.push(app.tempTask.id);
                u.history.push({ desc:'Mission', amt:`${app.tempTask.rew}💎`, type:'in' });
                localStorage.setItem(DB, JSON.stringify(db));
                playSnd('success'); document.getElementById('modal-claim').classList.remove('active'); app.refresh(); app.renderTasks(); alert("Success!");
            },
            // STORE
            renderTopUp: (cat, btn) => {
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active')); btn.classList.add('active');
                const grid = document.getElementById('topup-grid'); grid.innerHTML = '';
                let data = [];
                if(cat==='regular') data=[{n:'25💎',p:'25'},{n:'50💎',p:'40'},{n:'115💎',p:'80'},{n:'355💎',p:'240'},{n:'610💎',p:'405'}];
                else if(cat==='special') data=[{n:'Level Up',p:'160'},{n:'Evo Pass',p:'340'}];
                else data=[{n:'Weekly',p:'160'},{n:'Monthly',p:'795'}];
                data.forEach(d => {
                    grid.innerHTML += `<div class="topup-card glass" onclick="playSnd('tap'); app.initPay('${d.n}','${d.p}')"><i class="fas fa-gem" style="font-size:1.5rem;color:var(--neon)"></i><div style="margin:5px 0;">${d.n}</div><div class="topup-price">৳ ${d.p}</div></div>`;
                });
            },
            initPay: (n, p) => { app.payItem=n; app.payCost=p; document.getElementById('pay-amt').innerText=p; document.getElementById('modal-pay').classList.add('active'); },
            doPay: () => {
                const tr = document.getElementById('pay-trx').value; if(!tr) { playSnd('error'); return; }
                const db = JSON.parse(localStorage.getItem(DB));
                db.withdrawals.push({ user:app.user.email, type:'TopUp', item:app.payItem, price:app.payCost, trx:tr, status:'Pending' });
                localStorage.setItem(DB, JSON.stringify(db));
                playSnd('success'); document.getElementById('modal-pay').classList.remove('active'); alert("Submitted!");
            },
            // WITHDRAW
            openWithdraw: () => { document.getElementById('modal-wd').classList.add('active'); app.wdVal = 0; },
            selWd: (amt, el) => { app.wdVal = amt; document.querySelectorAll('#modal-wd .tab-btn').forEach(b => b.style.background='#222'); el.style.background = 'var(--gold)'; },
            submitWd: () => {
                const uid = document.getElementById('wd-uid').value; 
                if(!uid || app.wdVal===0 || app.user.diamonds < app.wdVal) { playSnd('error'); return alert("Invalid!"); }
                const db = JSON.parse(localStorage.getItem(DB));
                const u = db.users.find(x => x.email === app.user.email);
                u.diamonds -= app.wdVal;
                u.history.push({ desc:`Withdraw (${uid})`, amt:`${app.wdVal}💎`, type:'out' });
                db.withdrawals.push({ user:app.user.email, type:'Withdraw', item:`${app.wdVal} 💎`, price:0, trx:uid, status:'Pending' });
                localStorage.setItem(DB, JSON.stringify(db));
                playSnd('success'); document.getElementById('modal-wd').classList.remove('active'); app.refresh(); alert("Request Sent!");
            },
            // CHAT
            renderChat: () => {
                const db = JSON.parse(localStorage.getItem(DB)); const box = document.getElementById('msg-container'); box.innerHTML = '';
                db.msgs.filter(m => m.user === app.user.email).forEach(m => {
                    box.innerHTML += `<div class="chat-bubble ${m.from==='user'?'mine':'theirs'}">${m.txt}</div>`;
                });
            },
            sendMsg: () => {
                const txt = document.getElementById('chat-inp').value; if(!txt) return;
                const db = JSON.parse(localStorage.getItem(DB));
                db.msgs.push({ user:app.user.email, txt:txt, from:'user' });
                localStorage.setItem(DB, JSON.stringify(db));
                document.getElementById('chat-inp').value=''; app.renderChat();
            },
            renderRank: () => {
                const db = JSON.parse(localStorage.getItem(DB));
                const list = document.getElementById('lb-list'); list.innerHTML = '';
                [...db.users].sort((a,b)=>b.diamonds-a.diamonds).slice(0,10).forEach((u,i) => {
                    list.innerHTML += `<div class="lb-row"><div style="display:flex;align-items:center;gap:10px;"><b>#${i+1}</b> ${u.name}</div><span style="color:var(--gold)">${u.diamonds}💎</span></div>`;
                });
            }
        };

        // --- ADMIN LOGIC ---
        const adm = {
            init: () => { adm.renderDash(); },
            renderDash: () => {
                const db = JSON.parse(localStorage.getItem(DB)); document.getElementById('st-users').innerText = db.users.length;
                const l = document.getElementById('req-list'); l.innerHTML = '';
                db.withdrawals.forEach((w, i) => {
                    if(w.status === 'Pending') {
                        l.innerHTML += `<div style="border-bottom:1px solid #eee; padding:5px;"><div style="font-weight:bold;">${w.type} | ${w.user}</div><div>${w.item} (Trx:${w.trx})</div><button onclick="playSnd('success'); adm.act(${i},'Success')">✔</button> <button onclick="playSnd('error'); adm.act(${i},'Reject')">✖</button></div>`;
                    }
                });
            },
            act: (i, st) => { const db = JSON.parse(localStorage.getItem(DB)); db.withdrawals[i].status = st; localStorage.setItem(DB, JSON.stringify(db)); adm.renderDash(); },
            renderUsers: () => {
                const db = JSON.parse(localStorage.getItem(DB)); const l = document.getElementById('user-list'); l.innerHTML = '';
                db.users.forEach(u => {
                    l.innerHTML += `<div style="padding:10px; border-bottom:1px solid #eee;"><b>${u.name}</b> (${u.diamonds}💎)</div>`;
                });
            },
            renderTasks: () => {
                const db = JSON.parse(localStorage.getItem(DB)); const l = document.getElementById('active-tasks'); l.innerHTML = '';
                db.tasks.forEach((t, i) => {
                    l.innerHTML += `<div style="background:#eee; padding:5px; margin-bottom:5px;">${t.title} [${t.code}] <button onclick="adm.delTask(${i})">X</button></div>`;
                });
            },
            addTask: () => {
                const t = { id:Date.now(), title:document.getElementById('t-tit').value, link:document.getElementById('t-lnk').value, code:document.getElementById('t-cod').value, reward:parseInt(document.getElementById('t-rew').value) };
                const db = JSON.parse(localStorage.getItem(DB)); db.tasks.push(t); localStorage.setItem(DB, JSON.stringify(db)); adm.renderTasks();
            },
            delTask: (i) => { const db = JSON.parse(localStorage.getItem(DB)); db.tasks.splice(i,1); localStorage.setItem(DB, JSON.stringify(db)); adm.renderTasks(); }
        };

        window.addEventListener('storage', () => app.refresh());
        app.init();
    </script>
</body>
</html>
