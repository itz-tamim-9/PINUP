<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>PINUP | Ultimate Rewards</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <style>
        /* --- SHARED VARIABLES --- */
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
        
        /* --- USER APP STYLES (Dark Mode) --- */
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

        /* Auth & Layout */
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

        /* Tasks */
        .task-item { background: linear-gradient(90deg, #1a1a1a, #0d0d0d); border: 1px solid #333; padding: 15px; margin-bottom: 15px; border-radius: 12px; position: relative; overflow: hidden; }
        .task-link-box { background: #000; color: var(--neon); padding: 8px; border-radius: 4px; font-family: monospace; font-size: 0.8rem; border: 1px solid #333; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; flex: 1; }
        .btn-copy { background: #333; color: white; border: none; padding: 8px 15px; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 0.8rem; margin-left: 10px; }
        .btn-claim { width: 100%; padding: 12px; border: none; margin-top: 15px; background: linear-gradient(to bottom, var(--ff-yellow), var(--ff-orange)); color: black; font-weight: 800; font-family: var(--font-head); font-size: 1.1rem; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; border-radius: 6px; border-bottom: 4px solid #cc7a00; text-shadow: 0 1px 0 rgba(255,255,255,0.4); }
        .btn-claim:active { transform: translateY(2px); border-bottom-width: 2px; }

        /* Store */
        .topup-tabs { display: flex; gap: 10px; margin-bottom: 20px; overflow-x: auto; padding-bottom: 5px; }
        .tab-btn { background: #222; color: #aaa; padding: 8px 16px; border-radius: 20px; border: 1px solid #333; white-space: nowrap; font-size: 0.85rem; cursor: pointer; }
        .tab-btn.active { background: var(--gold); color: black; font-weight: bold; border-color: var(--gold); }
        .topup-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
        .topup-card { text-align: center; padding: 15px; border-radius: 15px; border: 1px solid rgba(255,255,255,0.1); position: relative; overflow: hidden; transition: 0.3s; }
        .topup-card:active { transform: scale(0.98); border-color: var(--gold); }
        .topup-price { background: var(--gold); color: black; display: inline-block; padding: 2px 10px; border-radius: 4px; font-weight: bold; font-size: 0.9rem; margin-top: 5px; }

        /* Others */
        .lb-row { display: flex; align-items: center; justify-content: space-between; padding: 12px; background: #161616; margin-bottom: 8px; border-radius: 8px; border-bottom: 2px solid transparent; }
        .lb-row:nth-child(-n+3) { border-color: var(--gold); background: linear-gradient(90deg, #161616, rgba(255, 215, 0, 0.05)); }
        .rank-badge { width: 35px; height: 35px; background: #333; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-weight: bold; color: #888; }
        .lb-row:nth-child(1) .rank-badge { background: var(--gold); color: black; }
        
        #chat-window { height: 65vh; display: flex; flex-direction: column; background: #000; border-radius: 20px; border: 1px solid #222; overflow: hidden; background-image: url('https://www.transparenttextures.com/patterns/carbon-fibre.png'); }
        #msg-container { flex: 1; overflow-y: auto; padding: 15px; display: flex; flex-direction: column; gap: 10px; }
        .chat-bubble { max-width: 75%; padding: 10px 14px; font-size: 0.9rem; border-radius: 15px; word-wrap: break-word; }
        .mine { align-self: flex-end; background: linear-gradient(135deg, var(--gold), #e6b800); color: black; border-bottom-right-radius: 2px; }
        .theirs { align-self: flex-start; background: #222; border: 1px solid #333; color: white; border-bottom-left-radius: 2px; }
        .chat-img { max-width: 100%; border-radius: 10px; margin-top: 5px; }
        
        .profile-head { text-align: center; margin-bottom: 25px; position: relative; }
        .lang-float { position: absolute; right: 0; top: 0; background: #222; border: 1px solid var(--gold); padding: 5px 12px; border-radius: 20px; font-size: 0.75rem; color: var(--gold); }
        .history-item { display: flex; justify-content: space-between; padding: 12px; background: rgba(255,255,255,0.03); margin-bottom: 8px; border-radius: 8px; font-size: 0.85rem; border-left: 2px solid #333; }

        /* Switch UI */
        .switch input:checked + .slider { background-color: var(--gold); border-color: var(--gold); }
        .slider:before { position: absolute; content: ""; height: 18px; width: 18px; left: 3px; bottom: 2px; background-color: white; transition: .4s; border-radius: 50%; }
        .switch input:checked + .slider:before { transform: translateX(21px); }

        /* Nav */
        .btm-nav { position: fixed; bottom: 20px; left: 20px; right: 20px; background: rgba(20, 20, 20, 0.95); backdrop-filter: blur(15px); border-radius: 25px; padding: 15px 30px; border: 1px solid rgba(255,215,0,0.2); display: flex; justify-content: space-between; box-shadow: 0 10px 30px rgba(0,0,0,0.5); z-index: 100; }
        .nav-icon { font-size: 1.4rem; color: #555; transition: 0.3s; position: relative; }
        .nav-icon.active { color: var(--gold); transform: translateY(-5px); }
        
        /* Modals */
        .modal-bg { position: fixed; inset: 0; background: rgba(0,0,0,0.9); z-index: 2000; display: flex; justify-content: center; align-items: center; opacity: 0; pointer-events: none; transition: 0.3s; }
        .modal-bg.active { opacity: 1; pointer-events: all; }
        .modal-content { background: #18181b; width: 90%; max-width: 350px; padding: 25px; border-radius: 20px; border: 1px solid var(--gold); text-align: center; transform: scale(0.8); transition: 0.3s; }
        .modal-bg.active .modal-content { transform: scale(1); }

        /* --- ADMIN PANEL STYLES (Light Mode Override) --- */
        #admin-panel {
            background: #f4f6f9; color: #333; position: fixed; inset: 0; z-index: 5000; overflow-y: auto; font-family: sans-serif;
        }
        #admin-panel .ad-header { background: #1e1e2d; color: #fff; padding: 15px; display: flex; justify-content: space-between; align-items: center; position: sticky; top: 0; z-index: 10; }
        #admin-panel .ad-container { padding: 15px; }
        #admin-panel .ad-card { background: white; padding: 15px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); margin-bottom: 15px; }
        #admin-panel .btn { padding: 6px 12px; border: none; border-radius: 4px; cursor: pointer; color: white; font-size: 0.8rem; margin-right: 5px; }
        #admin-panel .btn-blue { background: #007bff; } 
        #admin-panel .btn-green { background: #28a745; } 
        #admin-panel .btn-red { background: #dc3545; } 
        #admin-panel .btn-dark { background: #343a40; }
        #admin-panel .user-row { display: flex; align-items: center; gap: 10px; border-bottom: 1px solid #eee; padding: 10px 0; }
        #admin-panel input, #admin-panel select { width: 100%; padding: 10px; margin-bottom: 10px; border: 1px solid #ddd; box-sizing: border-box; background: #fff; color: #333; }
        #admin-panel .ad-nav { position: fixed; bottom: 0; width: 100%; background: white; display: flex; border-top: 1px solid #ddd; padding-bottom: 10px;}
        #admin-panel .ad-nav-item { flex: 1; text-align: center; padding: 12px; color: #666; cursor: pointer; }
        #admin-panel .ad-nav-item.active { color: #007bff; background: #f0f8ff; }
        .ad-section { display: none; } .ad-section.active { display: block; }
    </style>
</head>
<body>

    <div id="auth-screen">
        <div class="auth-box glass">
            <h1 style="font-family: 'Orbitron'; color: var(--gold); font-size: 2.5rem;">PINUP</h1>
            <p style="color: #ccc; margin-bottom: 20px;">Elite Rewards</p>
            <input type="email" id="login-email" class="inp-field" placeholder="Enter Valid Gmail...">
            <button class="btn-main" onclick="app.login()" data-sound="confirm">START ENGINE</button>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <div class="app-header glass">
            <div class="user-info" onclick="app.nav('page-profile')" data-sound="nav">
                <img src="" id="head-img" class="u-img">
                <div><div id="head-name" style="font-weight: 600; font-size: 0.9rem;">Player</div><div style="font-size: 0.7rem; color: var(--gold);">ELITE MEMBER</div></div>
            </div>
            <div class="balance-pill" onclick="app.openWithdraw()" data-sound="open"><i class="fas fa-gem" style="color: var(--gold);"></i><span id="head-bal" style="font-weight: 700;">0</span></div>
        </div>

        <div class="content-area">
            <div id="page-home" class="page-sec">
                <div style="width: 100%; margin-bottom: 25px; border-radius: 15px; overflow: hidden; border: 1px solid #333; background: #000; line-height: 0;">
                    <iframe width="100%" height="200" src="https://www.youtube.com/embed/MeamyO9UxPk?si=0&modestbranding=1" frameborder="0" allowfullscreen></iframe>
                </div>
                <h3 class="section-head"><i class="fas fa-crosshairs"></i> MISSIONS</h3>
                <div id="task-list"></div>
            </div>

            <div id="page-topup" class="page-sec hidden">
                <h3 class="section-head"><i class="fas fa-bolt"></i> STORE</h3>
                <div class="topup-tabs">
                    <button class="tab-btn active" onclick="app.renderTopUp('regular', this)" data-sound="tab">Diamonds</button>
                    <button class="tab-btn" onclick="app.renderTopUp('special', this)" data-sound="tab">Special Packs</button>
                    <button class="tab-btn" onclick="app.renderTopUp('member', this)" data-sound="tab">Memberships</button>
                </div>
                <div id="topup-grid" class="topup-grid"></div>
            </div>

            <div id="page-rank" class="page-sec hidden">
                <div class="glass" style="padding: 20px; border-radius: 15px; text-align: center; margin-bottom: 20px;">
                    <p style="color: #888; font-size: 0.8rem;">TOTAL ACTIVE PLAYERS</p>
                    <h1 style="color: var(--neon); font-family: 'Orbitron';"><i class="fas fa-users"></i> 24,891</h1>
                </div>
                <h3 class="section-head"><i class="fas fa-trophy"></i> Top 50</h3>
                <div id="lb-list"></div>
            </div>

            <div id="page-chat" class="page-sec hidden" style="height: 100%;">
                <h3 class="section-head"><i class="fas fa-headset"></i> Support</h3>
                <div id="chat-window">
                    <div id="msg-container"></div>
                    <div style="padding: 10px; background: #111; display: flex; gap: 10px; align-items: center; border-top: 1px solid #333;">
                        <label for="chat-file" style="color: var(--gold); cursor: pointer; padding: 10px;" data-sound="open"><i class="fas fa-paperclip"></i></label>
                        <input type="file" id="chat-file" accept="image/*" class="hidden" onchange="app.handleChatImg(this)">
                        <input id="chat-inp" class="inp-field" style="margin:0; border-radius: 50px; padding: 10px 20px;" placeholder="Type here...">
                        <button onclick="app.sendMsg()" style="background: var(--gold); width: 40px; height: 40px; border-radius: 50%; border: none;" data-sound="send"><i class="fas fa-paper-plane"></i></button>
                    </div>
                </div>
            </div>

            <div id="page-profile" class="page-sec hidden">
                <div class="glass" style="padding: 30px; border-radius: 20px; position: relative;">
                    <div class="lang-float" onclick="app.toggleLang()" data-sound="nav"><i class="fas fa-globe"></i> <span id="lang-disp">EN</span></div>
                    
                    <div class="profile-head">
                        <img src="" id="p-img" class="u-img" style="width: 100px; height: 100px; border: 4px solid var(--gold);">
                        <label for="p-up" style="position: absolute; bottom: 0; right: 35%; background: var(--gold); color: black; width: 30px; height: 30px; border-radius: 50%; display: grid; place-items: center; cursor: pointer;" data-sound="open"><i class="fas fa-camera"></i></label>
                        <input type="file" id="p-up" class="hidden" accept="image/*" onchange="app.uploadProfile(this)">
                        <h2 id="p-name" style="margin-top: 15px; color: white;">Name</h2>
                        <p id="p-email" style="color: #777; font-size: 0.8rem;">email@gmail.com</p>
                        
                        <div onclick="tryAdminAccess()" style="margin-top: 10px; cursor: pointer; display: inline-block;" data-sound="nav">
                            <i class="fas fa-shield-alt" style="color: #444; font-size: 1.2rem;"></i>
                        </div>
                    </div>

                    <div style="background: rgba(255,255,255,0.05); padding: 15px; border-radius: 12px; display: flex; justify-content: space-between; align-items: center; margin-top: 20px; border: 1px solid #444;">
                        <div style="display: flex; align-items: center; gap: 10px;">
                            <i class="fas fa-music" style="color: var(--gold);"></i>
                            <span style="color: #fff; font-size: 0.9rem; font-weight: 500;">Background Music</span>
                        </div>
                        <label class="switch" style="position: relative; display: inline-block; width: 46px; height: 24px;">
                            <input type="checkbox" id="musicToggle" onchange="runMusic(this.checked)" style="opacity: 0; width: 0; height: 0;" checked>
                            <span class="slider" style="position: absolute; cursor: pointer; inset: 0; background-color: #333; border-radius: 34px; transition: .4s; border: 1px solid #555;"></span>
                        </label>
                    </div>

                </div>
                <h3 class="section-head" style="margin-top: 30px;"><i class="fas fa-history"></i> History</h3>
                <div id="history-list"></div>
            </div>
        </div>

        <div class="btm-nav">
            <i class="fas fa-home nav-icon active" onclick="app.nav('page-home', this)" data-sound="nav"></i>
            <i class="fas fa-shopping-cart nav-icon" onclick="app.nav('page-topup', this)" data-sound="nav"></i>
            <i class="fas fa-chart-bar nav-icon" onclick="app.nav('page-rank', this)" data-sound="nav"></i>
            <i class="fas fa-comments nav-icon" onclick="app.nav('page-chat', this)" data-sound="nav"></i>
            <i class="fas fa-user nav-icon" onclick="app.nav('page-profile', this)" data-sound="nav"></i>
        </div>
    </div>

    <div id="admin-panel" class="hidden">
        <div class="ad-header"><h3>PINUP ADMIN</h3><button class="btn btn-dark" onclick="closeAdmin()" data-sound="close">EXIT ADMIN</button></div>

        <div id="sec-dash" class="ad-container ad-section active">
            <div class="ad-card"><h4>Total Users: <span id="st-users" style="color:blue">0</span></h4><button class="btn btn-red" style="margin-top:10px" onclick="if(confirm('Reset All Data?')){localStorage.removeItem('pinup_ult_v4');location.reload();}" data-sound="danger">RESET DB</button></div>
            <div class="ad-card"><h4>Pending Requests</h4><div id="req-list"></div></div>
        </div>

        <div id="sec-users" class="ad-container ad-section">
            <div class="ad-card" id="user-list"></div>
        </div>

        <div id="sec-tasks" class="ad-container ad-section">
            <div class="ad-card"><h4>Add Task</h4><input id="t-tit" placeholder="Title"><input id="t-lnk" placeholder="Link"><input id="t-cod" placeholder="Secret Code" style="background:#e3f2fd"><input id="t-rew" type="number" placeholder="Reward"><button class="btn btn-blue" style="width:100%" onclick="adm.addTask()" data-sound="confirm">PUBLISH</button></div>
            <div id="active-tasks"></div>
        </div>

        <div class="ad-nav"><div class="ad-nav-item active" onclick="adNav('sec-dash',this)" data-sound="nav"><i class="fas fa-home"></i> Home</div><div class="ad-nav-item" onclick="adNav('sec-users',this)" data-sound="nav"><i class="fas fa-users"></i> Users</div><div class="ad-nav-item" onclick="adNav('sec-tasks',this)" data-sound="nav"><i class="fas fa-tasks"></i> Tasks</div></div>
    </div>

    <div id="edit-modal" class="modal-bg" style="z-index: 6000;"><div class="modal-content" style="background:white; color:black;"><h4 style="color:black">Edit User: <span id="e-email"></span></h4><input id="e-name" placeholder="Name"><input id="e-bal" type="number" placeholder="Diamonds"><input id="e-img" placeholder="Img URL"><div style="display:flex;gap:10px;margin-top:10px"><button class="btn btn-green" style="flex:1" onclick="adm.saveUser()" data-sound="confirm">SAVE</button><button id="btn-ban" class="btn btn-red" style="flex:1" onclick="adm.toggleBan()" data-sound="danger">BAN</button></div><button class="btn btn-dark" style="width:100%;margin-top:10px" onclick="document.getElementById('edit-modal').classList.remove('active')" data-sound="close">CLOSE</button></div></div>
    <div id="chat-modal-adm" class="modal-bg" style="z-index: 6000;"><div class="modal-content" style="background:white; height:80vh; display:flex; flex-direction:column; color:black;"><div style="display:flex;justify-content:space-between;"><b>Chat: <span id="c-user"></span></b><button onclick="document.getElementById('chat-modal-adm').classList.remove('active')" data-sound="close">X</button></div><div class="chat-area" id="c-msgs-adm" style="flex:1; overflow-y:auto; background:#f9f9f9; border:1px solid #eee; padding:10px; margin:10px 0;"></div><div style="display:flex;gap:5px;"><input type="file" id="c-file-adm" style="width:50px"><input id="c-inp-adm" style="flex:1" placeholder="Reply..."><button class="btn btn-blue" onclick="adm.sendMsg()" data-sound="send">Send</button></div></div></div>

    <div id="modal-wd" class="modal-bg"><div class="modal-content glass"><h2 style="color:var(--gold);font-family:'Orbitron'">WITHDRAW</h2><input id="wd-uid" class="inp-field" placeholder="Enter Player UID" style="text-align:center"><div style="display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:20px"><button class="tab-btn" onclick="app.selWd(100,this)" data-sound="tab">100 💎</button><button class="tab-btn" onclick="app.selWd(300,this)" data-sound="tab">300 💎</button><button class="tab-btn" onclick="app.selWd(500,this)" data-sound="tab">500 💎</button><button class="tab-btn" onclick="app.selWd(1000,this)" data-sound="tab">1000 💎</button></div><button class="btn-main" onclick="app.submitWd()" data-sound="confirm">CONFIRM</button><button onclick="document.getElementById('modal-wd').classList.remove('active')" style="background:none;color:#777;border:none;margin-top:15px" data-sound="close">Cancel</button></div></div>
    <div id="modal-pay" class="modal-bg"><div class="modal-content glass"><h3 style="color:white">Confirm Payment</h3><p style="margin:10px 0;color:#ccc">Send <b style="color:var(--gold)" id="pay-amt">0</b> to <span style="color:var(--neon)">01965613742</span></p><div style="display:flex;gap:15px;justify-content:center;margin:15px 0"><div class="pay-opt" onclick="app.payM='bkash';this.style.borderColor='var(--gold)'" style="border:1px solid #333;padding:5px;border-radius:5px" data-sound="open"><img src="https://freelogopng.com/s/all_img/1656234745bkash-app-logo-png.png" width="50"></div><div class="pay-opt" onclick="app.payM='nogad';this.style.borderColor='var(--gold)'" style="border:1px solid #333;padding:5px;border-radius:5px" data-sound="open"><img src="https://freelogopng.com/images/all_img/1679248787nagad-logo.png" width="50"></div></div><input id="pay-trx" class="inp-field" placeholder="Last 4 Digits / TrxID"><button class="btn-main" onclick="app.doPay()" data-sound="confirm">I HAVE PAID</button><button onclick="document.getElementById('modal-pay').classList.remove('active')" style="background:none;border:none;color:#555;margin-top:10px" data-sound="close">Close</button></div></div>
    <div id="modal-claim" class="modal-bg"><div class="modal-content glass"><h3 style="color:var(--gold)">Secret Code</h3><input id="claim-inp" class="inp-field" placeholder="Enter Code..."><button class="btn-main" onclick="app.doClaim()" data-sound="confirm">CLAIM REWARD</button><button onclick="document.getElementById('modal-claim').classList.remove('active')" style="background:none;border:none;color:#555;margin-top:10px" data-sound="close">Close</button></div></div>

    <script>
        const DB = 'pinup_ult_v4';

        /* --------------------------
           SOUND & BGM MANAGEMENT
           - Robust centralized SoundManager
           - All clickable elements attempt to play a context-aware sound
           - Specific events (claim success/fail, typing, send, close, nav, open, confirm...) use dedicated sounds
           -------------------------- */

        const SoundManager = {
            audios: {},
            enabled: true,
            unlocked: false, // unlock after first user gesture
            // Predefined sound sources (publicly-hosted stable files). 
            // NOTE: You can replace bgMusic.src with your preferred Phonk mp3 (most viewed phonk) URL.
            sources: {
                bg: "https://file-examples.com/wp-content/uploads/2017/11/file_example_MP3_700KB.mp3", // placeholder BGM (replace with phonk mp3 URL)
                click: "https://www.soundjay.com/button/sounds/button-16.mp3",
                claimInit: "https://www.soundjay.com/button/sounds/button-3.mp3", // used previously
                typing: "https://www.soundjay.com/button/sounds/button-09.mp3",
                success: "https://www.soundjay.com/misc/sounds/bell-ringing-05.mp3",
                error: "https://www.soundjay.com/button/sounds/beep-07.mp3",
                close: "https://www.soundjay.com/button/sounds/button-10.mp3",
                send: "https://www.soundjay.com/button/sounds/button-4.mp3",
                pay: "https://www.soundjay.com/misc/sounds/cash-register-1.mp3",
                danger: "https://www.soundjay.com/button/sounds/button-6.mp3",
                tab: "https://www.soundjay.com/button/sounds/button-11.mp3",
                nav: "https://www.soundjay.com/button/sounds/button-12.mp3"
            },
            load: function() {
                // create audio elements, with muted autoplay disabled initially
                for (const [k, src] of Object.entries(this.sources)) {
                    const a = new Audio(src);
                    a.preload = "auto";
                    a.volume = (k === 'bg') ? 0.35 : 0.9;
                    a.loop = (k === 'bg');
                    this.audios[k] = a;
                }

                // Expose main bgMusic element for other code (keeps API backward-compatible)
                const existing = document.getElementById('bgMusic');
                if (existing) {
                    existing.src = this.sources.bg;
                    existing.loop = true;
                    existing.volume = 0.35;
                    this.audios.bg = existing;
                } else {
                    const bg = document.createElement('audio');
                    bg.id = 'bgMusic';
                    bg.src = this.sources.bg;
                    bg.loop = true;
                    bg.preload = 'auto';
                    bg.volume = 0.35;
                    document.body.appendChild(bg);
                    this.audios.bg = bg;
                }

                // claimSound id kept for compatibility, but tied to SoundManager
                let cs = document.getElementById('claimSound');
                if (!cs) {
                    cs = document.createElement('audio');
                    cs.id = 'claimSound';
                    document.body.appendChild(cs);
                }
                cs.src = this.sources.claimInit;
                cs.preload = 'auto';
                this.audios.claimInit = cs;
            },
            unlockAudio: function() {
                if (this.unlocked) return;
                // Play a very short silent/resolved sound by playing and immediately pausing
                try {
                    // Try to play a short click to unlock
                    this.play('click', {volume: 0.001});
                    // Also resume bg audio if musicToggle is checked
                    const musicToggle = document.getElementById('musicToggle');
                    if (musicToggle && musicToggle.checked) {
                        const bg = this.audios.bg;
                        if (bg && typeof bg.play === 'function') {
                            bg.play().catch(()=>{/* will play on next interaction */});
                        }
                    }
                } catch (e) { /* ignore */ }
                this.unlocked = true;
            },
            play: function(name, opts = {}) {
                if (!this.enabled) return;
                const a = this.audios[name];
                if (!a) return;
                try {
                    const inst = a.cloneNode(true); // clone to allow overlapping
                    inst.volume = (typeof opts.volume === 'number') ? opts.volume : a.volume;
                    if (opts.loop) inst.loop = true;
                    inst.play().catch(err=>{ /* autoplay blocked until user gesture */ });
                    return inst;
                } catch (e) {
                    // fallback: try to play original audio instance
                    try { a.currentTime = 0; a.play().catch(()=>{});} catch(e) {}
                }
            },
            pauseBg: function() {
                const bg = this.audios.bg;
                if (bg && !bg.paused) try { bg.pause(); } catch(e) {}
            },
            resumeBg: function() {
                const bg = this.audios.bg;
                if (bg && bg.paused) try { bg.play().catch(()=>{}); } catch(e) {}
            },
            setBgSrc: function(url) {
                if (!url) return;
                const bg = this.audios.bg;
                bg.src = url;
                bg.load();
            }
        };

        // Initialize SoundManager
        SoundManager.load();

        // Ensure audio unlocked on first user gesture (click/touch)
        function unlockOnGesture() {
            SoundManager.unlockAudio();
            document.removeEventListener('click', unlockOnGesture);
            document.removeEventListener('touchstart', unlockOnGesture);
        }
        document.addEventListener('click', unlockOnGesture);
        document.addEventListener('touchstart', unlockOnGesture);

        // Global click-to-sound mapping using event delegation
        document.addEventListener('click', (ev) => {
            const el = ev.target.closest && ev.target.closest('*');
            if (!el) return;

            // If element or its ancestor has data-sound attribute, play that
            let node = el;
            while (node && node !== document.body) {
                const ds = node.getAttribute && node.getAttribute('data-sound');
                if (ds) {
                    // play the requested sound (if exists), else default click
                    if (SoundManager.audios[ds]) SoundManager.play(ds);
                    else SoundManager.play('click');
                    return;
                }
                node = node.parentElement;
            }

            // Heuristics for common controls
            if (el.matches('button, .btn, .tab-btn, .nav-icon, .pay-opt, .balance-pill, label')) {
                // Distinguish context by classes or innerText
                const txt = (el.innerText || "").toLowerCase();
                if (txt.includes('claim') || el.classList.contains('btn-claim')) {
                    SoundManager.play('claimInit');
                } else if (txt.includes('close') || txt === 'x' || txt.includes('cancel') || txt.includes('exit')) {
                    SoundManager.play('close');
                } else if (txt.includes('send') || el.getAttribute('aria-label') === 'send' || el.querySelector('.fa-paper-plane')) {
                    SoundManager.play('send');
                } else if (el.classList.contains('tab-btn') || txt.includes('diamond') || txt.includes('100') || el.closest('#topup-grid')) {
                    SoundManager.play('tab');
                } else if (el.classList.contains('nav-icon') || el.closest('.ad-nav-item')) {
                    SoundManager.play('nav');
                } else if (txt.includes('reset') || txt.includes('reject') || txt.includes('ban') || el.classList.contains('btn-red')) {
                    SoundManager.play('danger');
                } else {
                    SoundManager.play('click');
                }
            }
        }, {capture: true});

        // Typing sound in claim input (per-character vibe)
        (function attachTypingVibe() {
            const claimInp = () => document.getElementById('claim-inp');
            function playType() {
                // play a very subtle typing sound (not intrusive)
                SoundManager.play('typing', {volume: 0.45});
            }
            document.addEventListener('input', (e) => {
                if (e.target === claimInp()) {
                    // debounce slight to avoid spamming; but provide per-character vibe
                    playType();
                }
            });
        })();

        // --------------------------
        // BGM control (runMusic used in app)
        function runMusic(isOn) {
            // Ensure user gesture unlocked
            SoundManager.unlockAudio();
            if (isOn) {
                SoundManager.resumeBg();
            } else {
                SoundManager.pauseBg();
            }
        }

        // --- SECRET ADMIN LOGIC ---
        let secretClicks = 0;
        let clickTimer;
        
        function tryAdminAccess() {
            clearTimeout(clickTimer);
            secretClicks++;
            
            // Reset count if no click for 2 seconds
            clickTimer = setTimeout(() => { secretClicks = 0; }, 2000);

            if(secretClicks >= 8) {
                secretClicks = 0;
                const pin = prompt("ENTER SYSTEM PIN:");
                if(pin === "41420") {
                    openAdmin();
                    SoundManager.play('confirm');
                } else {
                    alert("ACCESS DENIED");
                    SoundManager.play('error');
                }
            }
        }

        function openAdmin() {
            document.getElementById('main-app').classList.add('hidden');
            document.getElementById('admin-panel').classList.remove('hidden');
            adm.init();
        }

        function closeAdmin() {
            document.getElementById('admin-panel').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            SoundManager.play('close');
        }

        function adNav(id, el) { 
            document.querySelectorAll('.ad-section').forEach(s => s.classList.remove('active')); 
            document.getElementById(id).classList.add('active'); 
            document.querySelectorAll('.ad-nav-item').forEach(i => i.classList.remove('active')); 
            el.classList.add('active'); 
            SoundManager.play('nav');
            if(id === 'sec-users') adm.renderUsers(); 
            if(id === 'sec-tasks') adm.renderTasks(); 
        }

        // --- USER APP LOGIC ---
        const app = {
            user: null, lang: 'en', wdVal: 0, payItem: null, payCost: null, payM: null, claimTemp: null, chatImg: null,
            init: () => {
                if(!localStorage.getItem(DB)) localStorage.setItem(DB, JSON.stringify({ users: [], tasks: [], withdrawals: [], msgs: [] }));
                const sess = localStorage.getItem('pinup_sess');
                if(sess) {
                    const u = JSON.parse(localStorage.getItem(DB)).users.find(x => x.email === sess);
                    if(u && !u.blocked) { app.user = u; app.load(); }
                }
            },
            login: () => {
                const e = document.getElementById('login-email').value.trim().toLowerCase();
                if(!e.endsWith('@gmail.com')) { SoundManager.play('error'); return alert("❌ Only @gmail.com allowed!"); }
                const dbData = JSON.parse(localStorage.getItem(DB));
                let u = dbData.users.find(x => x.email === e);
                if(!u) {
                    u = { email: e, name: e.split('@')[0], photo: 'https://cdn-icons-png.flaticon.com/512/149/149071.png', diamonds: 0, history: [], tasks: [], blocked: false };
                    dbData.users.push(u); localStorage.setItem(DB, JSON.stringify(dbData));
                }
                if(u.blocked) { SoundManager.play('danger'); return alert("⛔ Account Suspended!"); }
                app.user = u; localStorage.setItem('pinup_sess', e); 
                // On login (user gesture) unlock audio & start BGM
                SoundManager.unlockAudio();
                runMusic(true);
                SoundManager.play('confirm');
                app.load();
            },
            load: () => {
                document.getElementById('auth-screen').classList.add('hidden');
                document.getElementById('main-app').classList.remove('hidden');
                app.refresh(); app.renderTasks(); app.renderTopUp('regular', document.querySelector('.tab-btn')); app.renderRank(); app.renderChat();
            },
            refresh: () => {
                const dbData = JSON.parse(localStorage.getItem(DB));
                app.user = dbData.users.find(x => x.email === app.user.email);
                document.getElementById('head-name').innerText = app.user.name;
                document.getElementById('head-img').src = app.user.photo;
                document.getElementById('head-bal').innerText = app.user.diamonds;
                document.getElementById('p-name').innerText = app.user.name;
                document.getElementById('p-email').innerText = app.user.email;
                document.getElementById('p-img').src = app.user.photo;
                const hl = document.getElementById('history-list'); hl.innerHTML = '';
                [...app.user.history].reverse().forEach(h => {
                    hl.innerHTML += `<div class="history-item"><span>${h.desc}</span><span style="color:${h.type==='in'?'#00ff00':'#ff4757'}">${h.type==='in'?'+':'-'}${h.amt}</span></div>`;
                });
            },
            nav: (pid, el) => {
                document.querySelectorAll('.page-sec').forEach(p => p.classList.add('hidden'));
                document.getElementById(pid).classList.remove('hidden');
                document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('active'));
                if(el) el.classList.add('active');
                SoundManager.play('nav');
            },
            renderTasks: () => {
                const dbData = JSON.parse(localStorage.getItem(DB));
                const list = document.getElementById('task-list'); list.innerHTML = '';
                dbData.tasks.forEach(t => {
                    if(!app.user.tasks.includes(t.id)) {
                        // attach data-sound attributes to actionable buttons inside HTML for precise sounds
                        list.innerHTML += `<div class="task-item"><div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;"><h4 style="color:white;">${t.title}</h4><span style="color:var(--gold); font-weight:bold;">+${t.reward} 💎</span></div><div style="display:flex; align-items:center;"><div class="task-link-box">${t.link}</div><button class="btn-copy" onclick="navigator.clipboard.writeText('${t.link}');alert('Link Copied!');SoundManager.play('click')">COPY</button></div><button class="btn-claim" data-sound="claimInit" onclick="app.initClaim(${t.id}, '${t.code}', ${t.reward})">CLAIM</button></div>`;
                    }
                });
            },
            initClaim: (id, code, rew) => {
                // Play claim-init vibe
                SoundManager.play('claimInit');
                app.claimTemp = {id, code, rew}; document.getElementById('claim-inp').value=''; document.getElementById('modal-claim').classList.add('active'); 
            },
            doClaim: () => {
                const provided = document.getElementById('claim-inp').value;
                if(provided !== app.claimTemp.code) { 
                    SoundManager.play('error'); 
                    // give a distinct wrong-code vibe, and notify
                    alert("Wrong Code!");
                    return;
                }
                const dbData = JSON.parse(localStorage.getItem(DB));
                const u = dbData.users.find(x => x.email === app.user.email);
                u.diamonds += app.claimTemp.rew; u.tasks.push(app.claimTemp.id);
                u.history.push({ desc:'Mission Complete', amt:`${app.claimTemp.rew}💎`, type:'in' });
                localStorage.setItem(DB, JSON.stringify(dbData));
                SoundManager.play('success');
                app.refresh(); app.renderTasks(); document.getElementById('modal-claim').classList.remove('active'); alert("💎 Reward Claimed!");
            },
            renderTopUp: (cat, btn) => {
                document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active')); if(btn) btn.classList.add('active');
                const grid = document.getElementById('topup-grid'); grid.innerHTML = '';
                let data = cat === 'regular' ? [{n:'25💎',p:'25'},{n:'50💎',p:'40'},{n:'115💎',p:'80'},{n:'240💎',p:'160'},{n:'355💎',p:'240'},{n:'480💎',p:'320'},{n:'505💎',p:'340'},{n:'610💎',p:'405'},{n:'725💎',p:'485'},{n:'1240💎',p:'810'},{n:'2530💎',p:'1620'},{n:'5060💎',p:'3240'},{n:'7590💎',p:'4865'},{n:'10120💎',p:'6490'},{n:'12650💎',p:'8100'}] : (cat === 'special' ? [{n:'Level Up Pass',p:'160'}, {n:'Evo 3 Days',p:'75'},{n:'Evo 7 Days',p:'110'},{n:'Evo 30 Days',p:'340'}] : [{n:'Weekly Lite',p:'45'},{n:'Weekly Mem',p:'160'},{n:'Monthly Mem',p:'795'},{n:'4X Weekly Lite',p:'180'}]);
                data.forEach(d => { grid.innerHTML += `<div class="topup-card glass" data-sound="open" onclick="app.initPay('${d.n}','${d.p}')"><img src="https://cdn-icons-png.flaticon.com/512/3752/3752843.png" width="40"><div style="font-weight:bold;color:white;margin:5px 0;">${d.n}</div><div class="topup-price">৳ ${d.p}</div></div>`; });
            },
            initPay: (n, p) => { app.payItem=n; app.payCost=p; document.getElementById('pay-amt').innerText=p+'৳'; document.getElementById('modal-pay').classList.add('active'); SoundManager.play('open'); },
            doPay: () => {
                const tr = document.getElementById('pay-trx').value; if(!tr || !app.payM) { SoundManager.play('error'); return alert("Missing Info"); }
                const dbData = JSON.parse(localStorage.getItem(DB));
                dbData.withdrawals.push({ user:app.user.email, type:'TopUp', item:app.payItem, price:app.payCost, method:app.payM, trx:tr, status:'Pending' });
                localStorage.setItem(DB, JSON.stringify(dbData)); document.getElementById('modal-pay').classList.remove('active'); SoundManager.play('pay'); alert("Payment Submitted!");
            },
            openWithdraw: () => { document.getElementById('modal-wd').classList.add('active'); app.wdVal = 0; SoundManager.play('open'); },
            selWd: (amt, el) => { app.wdVal = amt; document.querySelectorAll('#modal-wd .tab-btn').forEach(b => b.style.background='#222'); el.style.background = 'var(--gold)'; SoundManager.play('tab'); },
            submitWd: () => {
                const uid = document.getElementById('wd-uid').value; if(!uid || app.wdVal === 0) { SoundManager.play('error'); return alert("Enter UID & Amount"); } if(app.user.diamonds < app.wdVal) { SoundManager.play('error'); return alert("Insufficient Diamonds!"); }
                const dbData = JSON.parse(localStorage.getItem(DB)); const idx = dbData.users.findIndex(u => u.email === app.user.email);
                dbData.users[idx].diamonds -= app.wdVal; dbData.users[idx].history.push({ desc: `Withdraw (UID:${uid})`, amt: `${app.wdVal}💎`, type: 'out' });
                dbData.withdrawals.push({ user: app.user.email, type: 'Withdraw', item: `${app.wdVal} 💎`, price: 0, trx: uid, method: 'GAME', status: 'Pending' });
                localStorage.setItem(DB, JSON.stringify(dbData)); app.refresh(); document.getElementById('modal-wd').classList.remove('active'); SoundManager.play('confirm'); alert("Request Sent!");
            },
            handleChatImg: (inp) => { if(inp.files[0]){ const r = new FileReader(); r.onload = (e) => { app.chatImg = e.target.result; document.getElementById('chat-inp').placeholder = "Image Attached..."; SoundManager.play('open'); }; r.readAsDataURL(inp.files[0]); }},
            sendMsg: () => {
                const txt = document.getElementById('chat-inp').value; if(!txt && !app.chatImg) { SoundManager.play('error'); return; }
                const dbData = JSON.parse(localStorage.getItem(DB)); dbData.msgs.push({ user: app.user.email, txt: txt, img: app.chatImg, from: 'user', time: new Date().toLocaleTimeString() });
                localStorage.setItem(DB, JSON.stringify(dbData)); document.getElementById('chat-inp').value = ''; app.chatImg = null; document.getElementById('chat-inp').placeholder = "Type here..."; SoundManager.play('send'); app.renderChat();
            },
            renderChat: () => {
                const dbData = JSON.parse(localStorage.getItem(DB)); const box = document.getElementById('msg-container'); box.innerHTML = '';
                dbData.msgs.filter(m => m.user === app.user.email).forEach(m => {
                    const cls = m.from === 'user' ? 'mine' : 'theirs'; const imgHtml = m.img ? `<img src="${m.img}" class="chat-img">` : '';
                    box.innerHTML += `<div class="chat-bubble ${cls}">${m.txt} ${imgHtml}</div>`;
                }); box.scrollTop = box.scrollHeight;
            },
            uploadProfile: (inp) => { if(inp.files[0]){const r=new FileReader();r.onload=e=>{const dbData=JSON.parse(localStorage.getItem(DB));dbData.users.find(u=>u.email===app.user.email).photo=e.target.result;localStorage.setItem(DB,JSON.stringify(dbData));app.refresh();SoundManager.play('confirm');};r.readAsDataURL(inp.files[0]);}},
            renderRank: () => { const l=document.getElementById('lb-list');let arr=[{n:app.user.name,d:app.user.diamonds,img:app.user.photo}];for(let i=0;i<50;i++){const nm="Player"+Math.floor(Math.random()*999);arr.push({n:nm,d:Math.floor(Math.random()*8000)+100,img:`https://ui-avatars.com/api/?name=${nm}&background=random`});}arr.sort((a,b)=>b.d-a.d);l.innerHTML='';arr.slice(0,50).forEach((p,i)=>{let b=i<3?`color:var(--gold);font-size:1.2rem;`:`color:#777`;let icn=i===0?'👑':i+1;l.innerHTML+=`<div class="lb-row"><div style="display:flex;align-items:center;gap:10px;"><div class="rank-badge" style="${b}">${icn}</div><img src="${p.img}" style="width:35px;height:35px;border-radius:50%;border:1px solid #333;"><div>${p.n}</div></div><div style="color:var(--gold);font-weight:bold;">${p.d}💎</div></div>`;});},
            toggleLang: () => { app.lang = app.lang==='en'?'bn':'en'; document.getElementById('lang-disp').innerText = app.lang.toUpperCase(); SoundManager.play('nav'); }
        };

        // --- ADMIN APP LOGIC ---
        let chatUser = null, editUserIdx = null;
        const adm = {
            init: () => { adm.renderDash(); },
            getDB: () => JSON.parse(localStorage.getItem(DB)),
            saveDB: (d) => localStorage.setItem(DB, JSON.stringify(d)),
            renderDash: () => {
                const db = adm.getDB(); document.getElementById('st-users').innerText = db.users.length;
                const l = document.getElementById('req-list'); l.innerHTML = '';
                db.withdrawals.forEach((w, i) => {
                    if(w.status === 'Pending') {
                        l.innerHTML += `<div style="border-bottom:1px solid #eee; padding:10px 0;"><div style="font-weight:bold;color:${w.type==='TopUp'?'blue':'orange'}">${w.type} | ${w.user}</div><div style="font-size:0.9rem">${w.item} (${w.price}৳) | Trx/UID: <b>${w.trx}</b></div><div style="margin-top:5px"><button class="btn btn-green" onclick="adm.act(${i},'Success')" data-sound="confirm">Approve</button><button class="btn btn-red" onclick="adm.act(${i},'Rejected')" data-sound="danger">Reject</button></div></div>`;
                    }
                });
            },
            act: (i, st) => { const db = adm.getDB(); db.withdrawals[i].status = st; adm.saveDB(db); SoundManager.play(st==='Success'?'success':'danger'); adm.renderDash(); },
            renderUsers: () => {
                const db = adm.getDB(); const l = document.getElementById('user-list'); l.innerHTML = '';
                db.users.forEach((u, i) => {
                    l.innerHTML += `<div class="user-row"><img src="${u.photo}" style="width:40px;height:40px;border-radius:50%"><div style="flex:1"><b>${u.name}</b><br><small>${u.email}</small><br><span style="color:blue">${u.diamonds} 💎</span></div><div><button class="btn btn-blue" onclick="adm.openChat('${u.email}')" data-sound="open"><i class="fas fa-comment"></i></button><button class="btn btn-dark" onclick="adm.openEdit(${i})" data-sound="open">EDIT</button></div></div>`;
                });
            },
            openEdit: (i) => {
                editUserIdx = i; const u = adm.getDB().users[i];
                document.getElementById('e-email').innerText = u.email; document.getElementById('e-name').value = u.name;
                document.getElementById('e-bal').value = u.diamonds; document.getElementById('e-img').value = u.photo;
                document.getElementById('btn-ban').innerText = u.blocked ? "UNBAN" : "BAN";
                document.getElementById('edit-modal').classList.add('active'); SoundManager.play('open');
            },
            saveUser: () => {
                const db = adm.getDB(); db.users[editUserIdx].name = document.getElementById('e-name').value;
                db.users[editUserIdx].diamonds = parseInt(document.getElementById('e-bal').value);
                db.users[editUserIdx].photo = document.getElementById('e-img').value;
                adm.saveDB(db); document.getElementById('edit-modal').classList.remove('active'); adm.renderUsers(); SoundManager.play('confirm');
            },
            toggleBan: () => { const db = adm.getDB(); db.users[editUserIdx].blocked = !db.users[editUserIdx].blocked; adm.saveDB(db); document.getElementById('edit-modal').classList.remove('active'); adm.renderUsers(); SoundManager.play('danger'); },
            openChat: (e) => { chatUser = e; document.getElementById('chat-modal-adm').classList.add('active'); document.getElementById('c-user').innerText = e; adm.renderChat(); SoundManager.play('open'); },
            renderChat: () => { const db = adm.getDB(); const box = document.getElementById('c-msgs-adm'); box.innerHTML = ''; db.msgs.filter(m => m.user === chatUser).forEach(m => { const cls = m.from==='admin'?'msg-adm':'msg-usr'; const img = m.img ? `<img src="${m.img}" class="c-img">` : ''; box.innerHTML += `<div style="clear:both; margin-bottom:5px;"><div class="msg" style="background:${m.from==='admin'?'#007bff':'#e9ecef'}; color:${m.from==='admin'?'white':'black'}; padding:5px 10px; border-radius:10px; float:${m.from==='admin'?'right':'left'}">${m.txt} ${img}</div></div>`; }); box.scrollTop = box.scrollHeight; },
            sendMsg: () => {
                const txt = document.getElementById('c-inp-adm').value; const file = document.getElementById('c-file-adm').files[0];
                if(file) { const r = new FileReader(); r.onload = (e) => { adm.pushMsg(txt, e.target.result); }; r.readAsDataURL(file); } else { if(!txt) { SoundManager.play('error'); return; } adm.pushMsg(txt, null); }
            },
            pushMsg: (t, i) => { const db = adm.getDB(); db.msgs.push({ user:chatUser, txt:t, img:i, from:'admin', time:new Date().toLocaleTimeString() }); adm.saveDB(db); document.getElementById('c-inp-adm').value=''; document.getElementById('c-file-adm').value=''; adm.renderChat(); SoundManager.play('send'); },
            addTask: () => { const t = { id:Date.now(), title:document.getElementById('t-tit').value, link:document.getElementById('t-lnk').value, code:document.getElementById('t-cod').value, reward:parseInt(document.getElementById('t-rew').value) }; if(!t.code) { SoundManager.play('error'); return alert("Code required"); } const db = adm.getDB(); db.tasks.push(t); adm.saveDB(db); adm.renderTasks(); SoundManager.play('confirm'); },
            renderTasks: () => { const db = adm.getDB(); document.getElementById('active-tasks').innerHTML = db.tasks.map((t,i) => `<div style="background:#eee;padding:10px;margin-bottom:5px"><b>${t.title}</b> (${t.reward}💎) Code:${t.code} <button style="float:right;color:red;border:none" onclick="adm.delTask(${i})" data-sound="danger">X</button></div>`).join(''); },
            delTask: (i) => { const db = adm.getDB(); db.tasks.splice(i, 1); adm.saveDB(db); adm.renderTasks(); SoundManager.play('danger'); }
        };

        // Keep storage reload reactive for session changes
        window.addEventListener('storage', () => app.refresh());
        app.init();
    </script>

    <!-- Audio elements (some created by SoundManager but we keep these for compatibility) -->
    <audio id="claimSound" src="https://www.soundjay.com/buttons/sounds/button-3.mp3" preload="auto"></audio>
    <!-- BG Music: placeholder. Replace src with an actual PHONK mp3 (most-viewed phonk) if you want a real phonk track. -->
    <audio id="bgMusic" src="https://file-examples.com/wp-content/uploads/2017/11/file_example_MP3_700KB.mp3" loop preload="auto"></audio>

</body>
</html>
