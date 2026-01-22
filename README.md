<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PINUP | Ultimate Rewards</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #09090b;
            --card-glass: rgba(30, 30, 35, 0.6);
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
            border: 1px solid rgba(255, 255, 255, 0.08); box-shadow: 0 4px 30px rgba(0, 0, 0, 0.3);
        }

        /* Auth */
        #auth-screen { position: fixed; inset: 0; z-index: 9999; background: url('https://wallpapers.com/s/hd/free-fire-cool-background-1920-x-1080-3l3k6p5w5z5w5z5w.jpg') no-repeat center center/cover; }
        .auth-box { width: 100%; max-width: 350px; padding: 30px; border-radius: 20px; text-align: center; border: 1px solid var(--gold); background: rgba(0,0,0,0.85); position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
        .inp-field { width: 100%; background: rgba(255,255,255,0.05); border: 1px solid #333; padding: 15px; border-radius: 10px; color: white; margin: 15px 0; font-family: var(--font-body); }
        .btn-main { width: 100%; padding: 14px; background: linear-gradient(135deg, var(--gold), #ffa500); color: #000; border: none; border-radius: 10px; font-weight: 700; font-family: var(--font-head); cursor: pointer; clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px); }
        
        #main-app { height: 100%; display: flex; flex-direction: column; }
        .app-header { padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05); z-index: 50; }
        .user-info { display: flex; align-items: center; gap: 12px; }
        .u-img { width: 45px; height: 45px; border-radius: 50%; border: 2px solid var(--gold); object-fit: cover; }
        .balance-pill { background: rgba(0,0,0,0.5); border: 1px solid var(--gold); padding: 8px 16px; border-radius: 50px; display: flex; align-items: center; gap: 8px; cursor: pointer; }
        .content-area { flex: 1; overflow-y: auto; padding: 20px; padding-bottom: 100px; }
        .section-head { font-family: var(--font-head); font-size: 1.4rem; color: var(--gold); margin-bottom: 20px; border-left: 4px solid var(--neon); padding-left: 12px; text-transform: uppercase; }

        /* Tasks & Grid */
        .task-item { background: linear-gradient(90deg, #1a1a1a, #0d0d0d); border: 1px solid #333; padding: 15px; margin-bottom: 15px; border-radius: 12px; position: relative; overflow: hidden; }
        .task-link-box { background: #000; color: var(--neon); padding: 8px; border-radius: 4px; font-family: monospace; font-size: 0.8rem; border: 1px solid #333; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; flex: 1; }
        .btn-copy { background: #333; color: white; border: none; padding: 8px 15px; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 0.8rem; margin-left: 10px; }
        .btn-claim { width: 100%; padding: 12px; border: none; margin-top: 15px; background: linear-gradient(to bottom, var(--ff-yellow), var(--ff-orange)); color: black; font-weight: 800; font-family: var(--font-head); font-size: 1.1rem; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; border-radius: 6px; border-bottom: 4px solid #cc7a00; }

        /* TopUp Store */
        .topup-tabs { display: flex; gap: 10px; margin-bottom: 20px; overflow-x: auto; padding-bottom: 5px; }
        .tab-btn { background: #222; color: #aaa; padding: 8px 16px; border-radius: 20px; border: 1px solid #333; white-space: nowrap; font-size: 0.85rem; cursor: pointer; }
        .tab-btn.active { background: var(--gold); color: black; font-weight: bold; border-color: var(--gold); }
        .topup-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
        .topup-card { text-align: center; padding: 15px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.1); position: relative; overflow: hidden; transition: 0.3s; }
        .topup-price { background: var(--gold); color: black; display: inline-block; padding: 2px 10px; border-radius: 4px; font-weight: bold; font-size: 0.9rem; margin-top: 5px; }

        /* Navigation */
        .btm-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; background: rgba(20, 20, 20, 0.95); backdrop-filter: blur(15px); border-radius: 25px; padding: 15px 30px; border: 1px solid rgba(255,215,0,0.2); display: flex; justify-content: space-between; box-shadow: 0 10px 30px rgba(0,0,0,0.5); z-index: 100; }
        .nav-icon { font-size: 1.4rem; color: #555; transition: 0.3s; position: relative; }
        .nav-icon.active { color: var(--gold); transform: translateY(-5px); }
        
        /* Profile & Switch */
        .profile-head { text-align: center; margin-bottom: 25px; position: relative; }
        .switch { position: relative; display: inline-block; width: 46px; height: 24px; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider { position: absolute; cursor: pointer; inset: 0; background-color: #333; border-radius: 34px; transition: .4s; border: 1px solid #555; }
        .slider:before { position: absolute; content: ""; height: 18px; width: 18px; left: 3px; bottom: 2px; background-color: white; transition: .4s; border-radius: 50%; }
        input:checked + .slider { background-color: var(--gold); }
        input:checked + .slider:before { transform: translateX(21px); }

        /* Modal */
        .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 2000; display: flex; justify-content: center; align-items: center; opacity: 0; pointer-events: none; transition: 0.3s; }
        .modal-bg.active { opacity: 1; pointer-events: all; }
        .modal-content { background: #18181b; width: 90%; max-width: 350px; padding: 25px; border-radius: 20px; border: 1px solid var(--gold); text-align: center; }

        /* ADMIN SECTION */
        #admin-panel { background: #f4f6f9; color: #333; position: fixed; inset: 0; z-index: 5000; overflow-y: auto; font-family: sans-serif; display: none; }
        .ad-header { background: #1e1e2d; color: #fff; padding: 15px; display: flex; justify-content: space-between; align-items: center; }
        .ad-container { padding: 15px; }
        .ad-card { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); margin-bottom: 15px; }
        .btn { padding: 6px 12px; border: none; border-radius: 4px; cursor: pointer; color: white; }
        .btn-dark { background: #343a40; }
        .btn-blue { background: #007bff; }
        .ad-nav { position: fixed; bottom: 0; width: 100%; background: white; display: flex; border-top: 1px solid #ddd; padding: 10px 0; }
        .ad-nav-item { flex: 1; text-align: center; color: #666; cursor: pointer; }
        .ad-nav-item.active { color: #007bff; }
        .ad-section { display: none; } .ad-section.active { display: block; }
    </style>
</head>
<body onclick="initAudioOnFirstClick()">

    <div id="auth-screen">
        <div class="auth-box glass">
            <h1 style="font-family: 'Orbitron'; color: var(--gold); font-size: 2.5rem;">PINUP</h1>
            <p style="color: #ccc; margin-bottom: 20px;">Elite Rewards</p>
            <input type="email" id="login-email" class="inp-field" placeholder="Enter Gmail...">
            <button class="btn-main" onclick="app.login()">START ENGINE</button>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <div class="app-header glass">
            <div class="user-info" onclick="app.nav('page-profile')">
                <img src="" id="head-img" class="u-img">
                <div><div id="head-name" style="font-weight: 600;">Player</div><div style="font-size: 0.7rem; color: var(--gold);">ELITE MEMBER</div></div>
            </div>
            <div class="balance-pill" onclick="app.openWithdraw()"><i class="fas fa-gem"></i><span id="head-bal">0</span></div>
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
                    <button class="tab-btn active" onclick="app.renderTopUp('regular', this)">Diamonds</button>
                    <button class="tab-btn" onclick="app.renderTopUp('special', this)">Special Packs</button>
                </div>
                <div id="topup-grid" class="topup-grid"></div>
            </div>

            <div id="page-rank" class="page-sec hidden">
                <h3 class="section-head"><i class="fas fa-trophy"></i> LEADERBOARD</h3>
                <div id="lb-list"></div>
            </div>

            <div id="page-profile" class="page-sec hidden">
                <div class="glass" style="padding: 30px; border-radius: 20px; text-align: center;">
                    <img src="" id="p-img" class="u-img" style="width: 100px; height: 100px; border: 4px solid var(--gold);">
                    <h2 id="p-name" style="margin-top: 15px;">Name</h2>
                    <p id="p-email" style="color: #777; font-size: 0.8rem;">email@gmail.com</p>
                    
                    <div onclick="tryAdminAccess()" style="margin-top: 15px; cursor: pointer;">
                        <i class="fas fa-shield-alt" style="color: #222; font-size: 1.2rem;"></i>
                    </div>

                    <div style="background: rgba(255,255,255,0.05); padding: 15px; border-radius: 12px; display: flex; justify-content: space-between; align-items: center; margin-top: 25px; border: 1px solid #444;">
                        <span style="font-size: 0.9rem;"><i class="fas fa-music" style="color: var(--gold); margin-right: 8px;"></i> Music</span>
                        <label class="switch">
                            <input type="checkbox" id="musicToggle" onchange="runMusic(this.checked)" checked>
                            <span class="slider"></span>
                        </label>
                    </div>
                </div>
            </div>
        </div>

        <div class="btm-nav">
            <i class="fas fa-home nav-icon active" onclick="app.nav('page-home', this)"></i>
            <i class="fas fa-shopping-cart nav-icon" onclick="app.nav('page-topup', this)"></i>
            <i class="fas fa-chart-bar nav-icon" onclick="app.nav('page-rank', this)"></i>
            <i class="fas fa-user nav-icon" onclick="app.nav('page-profile', this)"></i>
        </div>
    </div>

    <div id="admin-panel">
        <div class="ad-header"><h3>ADMIN PORTAL</h3><button class="btn btn-dark" onclick="closeAdmin()">EXIT</button></div>
        <div class="ad-container">
            <div id="ad-sec-home" class="ad-section active">
                <div class="ad-card"><h4>System Statistics</h4><p>Total Users: <span id="st-users">0</span></p></div>
                <div class="ad-card"><h4>Active Tasks</h4><div id="ad-task-list"></div></div>
            </div>
        </div>
        <div class="ad-nav">
            <div class="ad-nav-item active" onclick="adNav('ad-sec-home', this)"><i class="fas fa-cog"></i><br>Settings</div>
        </div>
    </div>

    <audio id="bgMusic" src="https://files.catbox.moe/4zr8ua" loop preload="auto"></audio>
    <audio id="claimSound" src="https://www.soundjay.com/buttons/sounds/button-3.mp3" preload="auto"></audio>

    <script>
        const DB = 'pinup_master_v1';
        let audioInited = false;

        // Initialize Audio on First Interaction (Browser Requirement)
        function initAudioOnFirstClick() {
            if(!audioInited) {
                const bgm = document.getElementById('bgMusic');
                bgm.play().catch(e => console.log("Auto-play blocked, waiting for login"));
                audioInited = true;
            }
        }

        function runMusic(isOn) {
            const bgm = document.getElementById('bgMusic');
            if (isOn) {
                bgm.volume = 0.5;
                bgm.play();
            } else {
                bgm.pause();
            }
        }

        // --- ADMIN SECRET LOGIC ---
        let secretClicks = 0;
        let clickTimer;
        function tryAdminAccess() {
            clearTimeout(clickTimer);
            secretClicks++;
            clickTimer = setTimeout(() => { secretClicks = 0; }, 2000);
            if(secretClicks >= 8) {
                secretClicks = 0;
                const pin = prompt("ENTER SYSTEM PIN:");
                if(pin === "41420") {
                    document.getElementById('main-app').classList.add('hidden');
                    document.getElementById('admin-panel').style.display = 'block';
                    renderAdmin();
                } else { alert("WRONG PIN"); }
            }
        }
        function closeAdmin() {
            document.getElementById('admin-panel').style.display = 'none';
            document.getElementById('main-app').classList.remove('hidden');
        }

        // --- CORE APP LOGIC ---
        const app = {
            user: null,
            init: () => {
                if(!localStorage.getItem(DB)) localStorage.setItem(DB, JSON.stringify({ users: [], tasks: [{id:1, title:'Join Telegram', link:'https://t.me/example', reward:50, code:'TG50'}] }));
                const sess = localStorage.getItem('pinup_sess');
                if(sess) {
                    app.user = JSON.parse(localStorage.getItem(DB)).users.find(u => u.email === sess);
                    if(app.user) app.load();
                }
            },
            login: () => {
                const e = document.getElementById('login-email').value.trim().toLowerCase();
                if(!e.endsWith('@gmail.com')) return alert("Enter valid Gmail");
                const db = JSON.parse(localStorage.getItem(DB));
                let u = db.users.find(x => x.email === e);
                if(!u) {
                    u = { email:e, name:e.split('@')[0], photo:'https://ui-avatars.com/api/?name='+e, diamonds:0, tasks:[] };
                    db.users.push(u); localStorage.setItem(DB, JSON.stringify(db));
                }
                app.user = u; localStorage.setItem('pinup_sess', e);
                runMusic(true); app.load();
            },
            load: () => {
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                app.refresh(); app.renderTasks();
            },
            refresh: () => {
                const db = JSON.parse(localStorage.getItem(DB));
                app.user = db.users.find(u => u.email === app.user.email);
                document.getElementById('head-name').innerText = app.user.name;
                document.getElementById('p-name').innerText = app.user.name;
                document.getElementById('head-bal').innerText = app.user.diamonds;
                document.getElementById('head-img').src = app.user.photo;
                document.getElementById('p-img').src = app.user.photo;
                document.getElementById('p-email').innerText = app.user.email;
            },
            nav: (pid, el) => {
                document.querySelectorAll('.page-sec').forEach(p => p.classList.add('hidden'));
                document.getElementById(pid).classList.remove('hidden');
                if(el) {
                    document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('active'));
                    el.classList.add('active');
                }
            },
            renderTasks: () => {
                const db = JSON.parse(localStorage.getItem(DB));
                const list = document.getElementById('task-list'); list.innerHTML = '';
                db.tasks.forEach(t => {
                    if(!app.user.tasks.includes(t.id)) {
                        list.innerHTML += `<div class="task-item"><h4 style="color:white;">${t.title}</h4><div style="display:flex;margin-top:10px;"><div class="task-link-box">${t.link}</div><button class="btn-copy" onclick="window.open('${t.link}')">OPEN</button></div><button class="btn-claim" onclick="app.claim(${t.id})">CLAIM ${t.reward} 💎</button></div>`;
                    }
                });
            },
            claim: (tid) => {
                const code = prompt("Enter Secret Code:");
                const db = JSON.parse(localStorage.getItem(DB));
                const t = db.tasks.find(x => x.id === tid);
                if(code === t.code) {
                    const u = db.users.find(x => x.email === app.user.email);
                    u.diamonds += t.reward; u.tasks.push(tid);
                    localStorage.setItem(DB, JSON.stringify(db));
                    document.getElementById('claimSound').play();
                    app.refresh(); app.renderTasks(); alert("Success!");
                } else { alert("Wrong Code!"); }
            },
            renderTopUp: (cat, btn) => {
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active')); btn.classList.add('active');
                const grid = document.getElementById('topup-grid'); grid.innerHTML = '';
                const items = [{n:'100 💎', p:'80'}, {n:'310 💎', p:'240'}, {n:'Weekly', p:'160'}];
                items.forEach(i => {
                    grid.innerHTML += `<div class="topup-card glass"><h4>${i.n}</h4><div class="topup-price">৳ ${i.p}</div><br><button class="btn-main" style="margin-top:10px;padding:5px;" onclick="alert('Contact Admin')">BUY</button></div>`;
                });
            }
        };

        function renderAdmin() {
            const db = JSON.parse(localStorage.getItem(DB));
            document.getElementById('st-users').innerText = db.users.length;
        }

        app.init();
    </script>
</body>
</html>
