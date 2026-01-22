<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PINUP PREMIUM | PHONK EDITION</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-dark: #09090b;
            --card-glass: rgba(30, 30, 35, 0.7);
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
            background: var(--card-glass); backdrop-filter: blur(15px); -webkit-backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
        }

        /* UI Enhancements */
        #auth-screen { position: fixed; inset: 0; z-index: 9999; background: url('https://wallpapers.com/s/hd/free-fire-cool-background-1920-x-1080-3l3k6p5w5z5w5z5w.jpg') no-repeat center center/cover; }
        .auth-box { width: 90%; max-width: 350px; padding: 30px; border-radius: 20px; text-align: center; border: 1px solid var(--gold); background: rgba(0,0,0,0.85); position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
        .inp-field { width: 100%; background: rgba(255,255,255,0.08); border: 1px solid #444; padding: 15px; border-radius: 12px; color: white; margin: 15px 0; transition: 0.3s; }
        .inp-field:focus { border-color: var(--neon); box-shadow: 0 0 10px var(--neon); }
        .btn-main { width: 100%; padding: 14px; background: linear-gradient(135deg, var(--gold), #ffa500); color: #000; border: none; border-radius: 10px; font-weight: 700; font-family: var(--font-head); cursor: pointer; clip-path: polygon(10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%, 0 10px); }
        
        #main-app { height: 100%; display: flex; flex-direction: column; }
        .app-header { padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid rgba(255,255,255,0.05); }
        .u-img { width: 45px; height: 45px; border-radius: 50%; border: 2px solid var(--gold); object-fit: cover; }
        .balance-pill { background: rgba(0,0,0,0.6); border: 1px solid var(--gold); padding: 8px 16px; border-radius: 50px; display: flex; align-items: center; gap: 8px; cursor: pointer; }
        .content-area { flex: 1; overflow-y: auto; padding: 20px; padding-bottom: 100px; }
        .section-head { font-family: var(--font-head); font-size: 1.2rem; color: var(--gold); margin-bottom: 20px; border-left: 4px solid var(--neon); padding-left: 12px; }

        /* Tasks Style */
        .task-item { background: linear-gradient(90deg, #1a1a1a, #0d0d0d); border: 1px solid #333; padding: 15px; margin-bottom: 15px; border-radius: 15px; }
        .btn-claim { width: 100%; padding: 12px; border: none; margin-top: 15px; background: linear-gradient(to bottom, var(--ff-yellow), var(--ff-orange)); color: black; font-weight: 800; font-family: var(--font-head); border-radius: 8px; cursor: pointer; }

        /* Navigation */
        .btm-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; background: rgba(15, 15, 15, 0.95); backdrop-filter: blur(20px); border-radius: 25px; padding: 15px 30px; border: 1px solid rgba(255,215,0,0.2); display: flex; justify-content: space-between; z-index: 100; }
        .nav-icon { font-size: 1.4rem; color: #555; transition: 0.3s; }
        .nav-icon.active { color: var(--gold); transform: translateY(-5px); text-shadow: 0 0 10px var(--gold); }
        
        /* Modals */
        .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 2000; display: flex; justify-content: center; align-items: center; opacity: 0; pointer-events: none; transition: 0.3s; }
        .modal-bg.active { opacity: 1; pointer-events: all; }
        .modal-content { background: #121214; width: 90%; max-width: 350px; padding: 25px; border-radius: 20px; border: 1px solid var(--gold); text-align: center; }

        /* Admin UI */
        #admin-panel { background: #f4f6f9; color: #333; position: fixed; inset: 0; z-index: 5000; overflow-y: auto; display: none; }
        .ad-header { background: #1e1e2d; color: #fff; padding: 15px; display: flex; justify-content: space-between; align-items: center; }
        
        .switch { position: relative; display: inline-block; width: 46px; height: 24px; }
        .slider { position: absolute; cursor: pointer; inset: 0; background-color: #333; border-radius: 34px; transition: .4s; border: 1px solid #555; }
        .slider:before { position: absolute; content: ""; height: 18px; width: 18px; left: 3px; bottom: 2px; background-color: white; border-radius: 50%; transition: .4s; }
        input:checked + .slider { background-color: var(--gold); }
        input:checked + .slider:before { transform: translateX(21px); }
    </style>
</head>
<body onclick="startBGM()">

    <audio id="bgMusic" src="https://files.catbox.moe/p9r1m0.mp3" loop preload="auto"></audio> <audio id="snd-tap" src="https://www.soundjay.com/buttons/sounds/button-16.mp3" preload="auto"></audio>
    <audio id="snd-success" src="https://www.myinstants.com/media/sounds/success-fanfare-trumpets.mp3" preload="auto"></audio>
    <audio id="snd-error" src="https://www.soundjay.com/buttons/sounds/button-10.mp3" preload="auto"></audio>
    <audio id="snd-close" src="https://www.soundjay.com/buttons/sounds/button-50.mp3" preload="auto"></audio>
    <audio id="snd-key" src="https://www.soundjay.com/buttons/sounds/button-37.mp3" preload="auto"></audio>

    <div id="auth-screen">
        <div class="auth-box glass">
            <h1 style="font-family: 'Orbitron'; color: var(--gold); font-size: 2.2rem;">PINUP</h1>
            <p style="color: #888; margin-bottom: 20px; font-size: 0.8rem; letter-spacing: 2px;">PREMIUM REWARDS</p>
            <input type="email" id="login-email" class="inp-field" placeholder="Enter Gmail...">
            <button class="btn-main" onclick="playSnd('tap'); app.login()">LOGIN ENGINE</button>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <div class="app-header glass">
            <div class="user-info" onclick="playSnd('tap'); app.nav('page-profile')">
                <img src="" id="head-img" class="u-img">
                <div>
                    <div id="head-name" style="font-weight: 600; font-size: 0.9rem;">Player</div>
                    <div style="font-size: 0.6rem; color: var(--gold);">LEVEL: PRO</div>
                </div>
            </div>
            <div class="balance-pill" onclick="playSnd('tap'); app.openWithdraw()">
                <i class="fas fa-gem" style="color: var(--gold);"></i>
                <span id="head-bal">0</span>
            </div>
        </div>

        <div class="content-area">
            <div id="page-home" class="page-sec">
                <h3 class="section-head"><i class="fas fa-bolt"></i> MISSIONS</h3>
                <div id="task-list"></div>
            </div>

            <div id="page-topup" class="page-sec hidden">
                <h3 class="section-head"><i class="fas fa-shopping-cart"></i> STORE</h3>
                <div id="topup-grid" style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;"></div>
            </div>

            <div id="page-rank" class="page-sec hidden">
                <h3 class="section-head"><i class="fas fa-trophy"></i> TOP PLAYERS</h3>
                <div id="lb-list"></div>
            </div>

            <div id="page-profile" class="page-sec hidden">
                <div class="glass" style="padding: 30px; border-radius: 20px; text-align: center;">
                    <img src="" id="p-img" class="u-img" style="width: 100px; height: 100px; border: 4px solid var(--gold); margin-bottom: 15px;">
                    <h2 id="p-name">Username</h2>
                    <p id="p-email" style="color: #777; margin-bottom: 20px;">email@gmail.com</p>
                    
                    <div onclick="playSnd('tap'); tryAdminAccess()" style="cursor: pointer; display: inline-block;">
                        <i class="fas fa-shield-alt" style="color: #1a1a1a; font-size: 1.1rem;"></i>
                    </div>

                    <div style="background: rgba(255,255,255,0.05); padding: 15px; border-radius: 12px; display: flex; justify-content: space-between; align-items: center; margin-top: 30px; border: 1px solid #333;">
                        <span><i class="fas fa-music" style="color: var(--gold);"></i> Music Vibe</span>
                        <label class="switch">
                            <input type="checkbox" id="musicToggle" onchange="playSnd('tap'); toggleBGM(this.checked)" checked>
                            <span class="slider"></span>
                        </label>
                    </div>
                </div>
            </div>
        </div>

        <div class="btm-nav">
            <i class="fas fa-home nav-icon active" onclick="playSnd('tap'); app.nav('page-home', this)"></i>
            <i class="fas fa-shopping-bag nav-icon" onclick="playSnd('tap'); app.nav('page-topup', this)"></i>
            <i class="fas fa-chart-line nav-icon" onclick="playSnd('tap'); app.nav('page-rank', this)"></i>
            <i class="fas fa-user-circle nav-icon" onclick="playSnd('tap'); app.nav('page-profile', this)"></i>
        </div>
    </div>

    <div id="modal-claim" class="modal-bg">
        <div class="modal-content glass">
            <h3 style="color: var(--gold); font-family: 'Orbitron';">VERIFY MISSION</h3>
            <input id="claim-inp" class="inp-field" placeholder="Type Secret Code..." onkeypress="playSnd('key')" style="text-align: center;">
            <button class="btn-main" onclick="app.doClaim()">SUBMIT CODE</button>
            <button onclick="playSnd('close'); document.getElementById('modal-claim').classList.remove('active')" style="background:none; border:none; color:#555; margin-top:15px; cursor:pointer;">CLOSE</button>
        </div>
    </div>

    <div id="admin-panel">
        <div class="ad-header">
            <h3>SECRET ADMIN</h3>
            <button onclick="playSnd('close'); closeAdmin()" style="padding: 8px 15px; background: red; color: white; border: none; border-radius: 5px;">EXIT</button>
        </div>
        <div style="padding: 20px;">
            <div class="ad-card" style="background: white; padding: 15px; border-radius: 10px;">
                <h4>Settings & Control</h4>
                <p>Total Users: <span id="st-users">0</span></p>
                <hr style="margin: 15px 0;">
                <button class="btn-main" style="background: #222; color: gold;" onclick="playSnd('tap'); alert('Reset Done')">Clear Cache</button>
            </div>
        </div>
    </div>

    <script>
        const DB_NAME = 'pinup_phonk_v5';
        let bgmStarted = false;

        // --- SOUND ENGINE ---
        function playSnd(type) {
            const sounds = {
                tap: document.getElementById('snd-tap'),
                success: document.getElementById('snd-success'),
                error: document.getElementById('snd-error'),
                close: document.getElementById('snd-close'),
                key: document.getElementById('snd-key')
            };
            if(sounds[type]) {
                sounds[type].currentTime = 0;
                sounds[type].play().catch(e => {});
            }
        }

        function startBGM() {
            if(!bgmStarted) {
                const bgm = document.getElementById('bgMusic');
                bgm.volume = 0.4;
                bgm.play().then(() => { bgmStarted = true; }).catch(e => {});
            }
        }

        function toggleBGM(isOn) {
            const bgm = document.getElementById('bgMusic');
            isOn ? bgm.play() : bgm.pause();
        }

        // --- SECRET LOGIC ---
        let secretClicks = 0, clickTimer;
        function tryAdminAccess() {
            clearTimeout(clickTimer);
            secretClicks++;
            clickTimer = setTimeout(() => { secretClicks = 0; }, 2000);
            if(secretClicks >= 8) {
                secretClicks = 0;
                playSnd('key');
                const pin = prompt("ENTER SYSTEM PIN:");
                if(pin === "41420") {
                    playSnd('success');
                    document.getElementById('main-app').classList.add('hidden');
                    document.getElementById('admin-panel').style.display = 'block';
                    document.getElementById('st-users').innerText = JSON.parse(localStorage.getItem(DB_NAME)).users.length;
                } else { playSnd('error'); alert("ACCESS DENIED"); }
            }
        }
        function closeAdmin() {
            document.getElementById('admin-panel').style.display = 'none';
            document.getElementById('main-app').classList.remove('hidden');
        }

        // --- APP ENGINE ---
        const app = {
            user: null,
            tempTask: null,
            init: () => {
                if(!localStorage.getItem(DB_NAME)) {
                    localStorage.setItem(DB_NAME, JSON.stringify({
                        users: [],
                        tasks: [
                            {id: 1, title: 'Subscribe Channel', reward: 50, link: 'https://youtube.com', code: 'PRO77'},
                            {id: 2, title: 'Join Telegram', reward: 100, link: 'https://t.me', code: 'PHONK'},
                            {id: 3, title: 'Follow Instagram', reward: 30, link: 'https://instagram.com', code: 'GOLD'}
                        ]
                    }));
                }
                const sess = localStorage.getItem('pinup_active');
                if(sess) {
                    app.user = JSON.parse(localStorage.getItem(DB_NAME)).users.find(u => u.email === sess);
                    if(app.user) app.load();
                }
            },
            login: () => {
                const e = document.getElementById('login-email').value.trim().toLowerCase();
                if(!e.endsWith('@gmail.com')) { playSnd('error'); return alert("Use valid Gmail!"); }
                const db = JSON.parse(localStorage.getItem(DB_NAME));
                let u = db.users.find(x => x.email === e);
                if(!u) {
                    u = { email: e, name: e.split('@')[0], photo: 'https://ui-avatars.com/api/?name='+e+'&background=FFD700&color=000', diamonds: 0, done: [] };
                    db.users.push(u); localStorage.setItem(DB_NAME, JSON.stringify(db));
                }
                app.user = u;
                localStorage.setItem('pinup_active', e);
                app.load();
            },
            load: () => {
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                app.refresh();
                app.renderTasks();
                app.renderStore();
                app.renderRank();
            },
            refresh: () => {
                const db = JSON.parse(localStorage.getItem(DB_NAME));
                app.user = db.users.find(u => u.email === app.user.email);
                document.getElementById('head-name').innerText = app.user.name;
                document.getElementById('head-bal').innerText = app.user.diamonds;
                document.getElementById('head-img').src = app.user.photo;
                document.getElementById('p-img').src = app.user.photo;
                document.getElementById('p-name').innerText = app.user.name;
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
                const db = JSON.parse(localStorage.getItem(DB_NAME));
                const box = document.getElementById('task-list'); box.innerHTML = '';
                db.tasks.forEach(t => {
                    if(!app.user.done.includes(t.id)) {
                        box.innerHTML += `
                        <div class="task-item">
                            <div style="display:flex; justify-content:space-between;">
                                <b>${t.title}</b>
                                <span style="color:var(--gold);">+${t.reward} 💎</span>
                            </div>
                            <button class="btn-claim" onclick="playSnd('tap'); window.open('${t.link}'); app.openClaim(${t.id})">VERIFY & CLAIM</button>
                        </div>`;
                    }
                });
            },
            openClaim: (tid) => {
                app.tempTask = tid;
                document.getElementById('claim-inp').value = '';
                document.getElementById('modal-claim').classList.add('active');
            },
            doClaim: () => {
                const codeInp = document.getElementById('claim-inp').value.trim();
                const db = JSON.parse(localStorage.getItem(DB_NAME));
                const task = db.tasks.find(x => x.id === app.tempTask);
                
                if(codeInp === task.code) {
                    playSnd('success');
                    const u = db.users.find(x => x.email === app.user.email);
                    u.diamonds += task.reward;
                    u.done.push(task.id);
                    localStorage.setItem(DB_NAME, JSON.stringify(db));
                    document.getElementById('modal-claim').classList.remove('active');
                    app.refresh(); app.renderTasks();
                    alert("Reward Claimed!");
                } else {
                    playSnd('error');
                    alert("Invalid Code!");
                }
            },
            renderStore: () => {
                const grid = document.getElementById('topup-grid');
                const items = [{n:'100 💎',p:'85'}, {n:'310 💎',p:'250'}, {n:'520 💎',p:'410'}, {n:'Weekly',p:'165'}];
                items.forEach(i => {
                    grid.innerHTML += `<div class="glass" style="padding:15px; border-radius:15px; text-align:center;">
                        <img src="https://cdn-icons-png.flaticon.com/512/3752/3752843.png" width="35">
                        <div style="font-size:0.8rem; margin:10px 0;">${i.n}</div>
                        <button class="btn-main" style="padding:5px; font-size:0.7rem;" onclick="playSnd('tap'); alert('Contact Admin')">৳${i.p}</button>
                    </div>`;
                });
            },
            renderRank: () => {
                const list = document.getElementById('lb-list');
                for(let i=1; i<=5; i++) {
                    list.innerHTML += `<div class="glass" style="padding:12px; margin-bottom:10px; border-radius:10px; display:flex; justify-content:space-between;">
                        <span>#${i} Top Player_${i}</span>
                        <span style="color:var(--gold);">${1000-(i*100)} 💎</span>
                    </div>`;
                }
            },
            openWithdraw: () => {
                playSnd('tap');
                alert("Withdraw section available for Pro levels only.");
            }
        };

        app.init();
    </script>
</body>
</html>
