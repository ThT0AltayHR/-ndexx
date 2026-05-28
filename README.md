<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="referrer" content="no-referrer">
    
    <title>Hacked By TurkHackTeam | SYSTEM OVERRIDDEN</title>
    <link rel="icon" type="image/png" href="https://i.hizliresim.com/9x1hxd2.png">
    
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&display=swap" rel="stylesheet">

    <style>
        /* ==========================================================================
           1. TEMEL STİLLER VE SIFIRLAMA
           ========================================================================== */
        * { margin: 0; padding: 0; box-sizing: border-box; }

        body, html {
            height: 100%;
            background-color: #030000;
            color: #ffffff;
            font-family: 'Share Tech Mono', monospace;
            overflow: hidden;
            user-select: none;
            cursor: crosshair;
        }

        /* ==========================================================================
           2. EFEKT KATMANLARI (CRT & VIGNETTE)
           ========================================================================== */
        .scanlines {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: linear-gradient(rgba(18, 16, 16, 0) 50%, rgba(0, 0, 0, 0.25) 50%),
                        linear-gradient(90deg, rgba(255, 0, 0, 0.06), rgba(0, 255, 0, 0.02), rgba(0, 0, 255, 0.06));
            background-size: 100% 3px, 3px 100%;
            z-index: 10; pointer-events: none;
            animation: flicker 0.15s infinite;
        }
        @keyframes flicker { 0% { opacity: 0.95; } 50% { opacity: 0.85; } 100% { opacity: 0.95; } }

        .vignette {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at center, transparent 10%, #000000 95%);
            z-index: 8; pointer-events: none;
            box-shadow: inset 0 0 200px rgba(255,0,0,0.2);
        }

        canvas { position: absolute; top: 0; left: 0; width: 100%; height: 100%; }
        #matrixCanvas { z-index: 1; opacity: 0.5; }
        #networkCanvas { z-index: 2; }

        /* ==========================================================================
           3. ANA DÜZEN VE HUD (RADAR)
           ========================================================================== */
        .container {
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            height: 100vh; position: relative; z-index: 5; pointer-events: none;
            opacity: 0; transition: opacity 2s ease-in; /* Sayfa açılışında yavaşça belirmesi için */
        }

        .hud-wrapper {
            position: relative; display: flex; justify-content: center; align-items: center; margin-bottom: 40px;
        }

        .hud-circle { position: absolute; border-radius: 50%; border: 2px solid transparent; pointer-events: none; }
        .hud-1 { width: 320px; height: 320px; border-top: 3px solid rgba(255, 0, 60, 0.9); border-bottom: 3px solid rgba(255, 0, 60, 0.2); animation: spin 5s linear infinite; box-shadow: 0 0 20px rgba(255,0,0,0.5); }
        .hud-2 { width: 360px; height: 360px; border-left: 2px dashed rgba(255, 50, 50, 0.8); border-right: 2px dashed rgba(255, 50, 50, 0.8); animation: spin-reverse 8s linear infinite; }
        .hud-3 { width: 280px; height: 280px; border: 1px dotted rgba(255, 0, 0, 0.7); animation: pulse-ring 1.5s infinite alternate; }

        @keyframes spin { 100% { transform: rotate(360deg); } }
        @keyframes spin-reverse { 100% { transform: rotate(-360deg); } }
        @keyframes pulse-ring { 0% { transform: scale(0.95); opacity: 0.5; } 100% { transform: scale(1.05); opacity: 1; } }

        /* GLITCH EFEKTİ */
        .logo {
            width: 220px; z-index: 6; pointer-events: auto;
            filter: drop-shadow(0 0 15px rgba(255, 0, 0, 1));
            animation: intenseGlitch 4s infinite;
        }

        @keyframes intenseGlitch {
            0%, 90%, 100% { transform: translate(0, 0); filter: drop-shadow(0 0 15px rgba(255,0,0,1)); }
            92% { transform: translate(-5px, 5px); filter: drop-shadow(5px -5px 0 rgba(0,255,255,0.8)); }
            94% { transform: translate(5px, -5px); filter: drop-shadow(-5px 5px 0 rgba(255,0,255,0.8)); }
            96% { transform: translate(-2px, -2px) skewX(20deg); }
            98% { transform: translate(2px, 2px) skewX(-20deg); }
        }

        /* ==========================================================================
           4. ŞİFRE ÇÖZÜCÜ & TERMİNAL YAZILARI
           ========================================================================== */
        .terminal-box {
            width: 100%; max-width: 850px; text-align: center; padding: 30px;
            background: rgba(10, 0, 0, 0.7); border: 1px solid rgba(255, 0, 60, 0.5);
            border-radius: 5px; box-shadow: 0 0 40px rgba(255, 0, 0, 0.3), inset 0 0 20px rgba(255,0,0,0.2);
            position: relative; overflow: hidden; backdrop-filter: blur(5px);
        }

        .terminal-box::before {
            content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 3px;
            background: linear-gradient(90deg, transparent, #ff003c, transparent);
            animation: scan-line 1.5s linear infinite; box-shadow: 0 0 10px #ff003c;
        }

        @keyframes scan-line { 0% { transform: translateY(-10px); } 100% { transform: translateY(150px); } }

        .decrypt-text {
            font-family: 'Orbitron', sans-serif; font-size: 2.2rem; color: #fff;
            text-transform: uppercase; text-shadow: 0 0 10px rgba(255, 0, 0, 0.8);
            min-height: 90px; display: flex; align-items: center; justify-content: center; flex-direction: column;
        }

        .decrypt-text span {
            color: #ff003c; font-weight: 900; font-size: 3rem;
            text-shadow: 0 0 25px rgba(255, 0, 0, 1), 2px 2px 0px rgba(0,255,255,0.5);
            margin-top: 10px;
            animation: textGlitch 2s infinite;
        }

        @keyframes textGlitch {
            0%, 95%, 100% { transform: none; text-shadow: 0 0 25px rgba(255, 0, 0, 1), 2px 2px 0px rgba(0,255,255,0.5); }
            96% { transform: skewX(15deg); text-shadow: -3px 0 red, 3px 0 cyan; }
            98% { transform: skewX(-15deg); text-shadow: 3px 0 red, -3px 0 cyan; }
        }

        /* ==========================================================================
           5. CANLI HACK LOGLARI (SAĞ ALT KÖŞE)
           ========================================================================== */
        .live-logs {
            position: absolute; bottom: 20px; right: 20px; width: 300px; height: 200px;
            background: rgba(0,0,0,0.5); border-left: 2px solid #ff003c; padding: 10px;
            font-size: 0.8rem; color: #ff5555; overflow: hidden; z-index: 15;
            text-align: left; opacity: 0; transition: opacity 2s;
        }
        .log-line { margin-bottom: 5px; text-shadow: 0 0 5px red; }
        .log-success { color: #00ff00; text-shadow: 0 0 5px lime; }

        @media (max-width: 768px) {
            .hud-1 { width: 220px; height: 220px; } .hud-2 { width: 250px; height: 250px; } .hud-3 { width: 190px; height: 190px; }
            .logo { width: 150px; } .decrypt-text { font-size: 1.2rem; } .decrypt-text span { font-size: 1.8rem; }
            .live-logs { display: none; }
        }
    </style>
</head>
<body>

    <audio id="bg-audio" loop preload="auto">
        <source src="https://actions.google.com/sounds/v1/science_fiction/alien_spaceship_interior.ogg" type="audio/ogg">
    </audio>

    <div class="scanlines"></div>
    <div class="vignette"></div>

    <canvas id="matrixCanvas"></canvas>
    <canvas id="networkCanvas"></canvas>

    <div class="live-logs" id="live-logs"></div>

    <div class="container" id="main-content">
        
        <div class="hud-wrapper">
            <div class="hud-circle hud-1"></div>
            <div class="hud-circle hud-2"></div>
            <div class="hud-circle hud-3"></div>
            <a href="https://www.turkhackteam.org/" target="_blank" pointer-events="auto">
                <img src="https://i.hizliresim.com/9x1hxd2.png" alt="TurkHackTeam Logo" class="logo">
            </a>
        </div>
        
        <div class="terminal-box">
            <div class="decrypt-text" id="target-text"></div>
        </div>
    </div>

    <script>
        // --- 0. BAŞLANGIÇ SİKANSI ---
        window.onload = () => {
            // Müzik çalmayı deneriz, tarayıcı engellerse hata fırlatır ama kod çalışmaya devam eder
            const audio = document.getElementById('bg-audio');
            audio.volume = 0.5;
            audio.play().catch(err => console.log("Otomatik oynatma engellendi, etkileşim bekleniyor."));
            
            // Kullanıcı sayfada herhangi bir yere tıkladığında müziği başlat
            document.body.addEventListener('click', () => {
                if(audio.paused) audio.play();
            }, { once: true }); // Sadece ilk tıklamada çalışır

            // Elemanları yavaşça görünür yap
            setTimeout(() => {
                document.getElementById('main-content').style.opacity = '1';
                document.getElementById('live-logs').style.opacity = '1';
                startDecryptionLogic();
                startFakeLogs();
            }, 300);
        };

        // --- 1. MATRIX DİJİTAL YAĞMUR (KIRMIZI) ---
        const mCanvas = document.getElementById('matrixCanvas');
        const mCtx = mCanvas.getContext('2d');
        mCanvas.width = window.innerWidth; mCanvas.height = window.innerHeight;

        const alphabet = 'アァカサタナハマヤャラワガザダバパイィキシチニヒミリヰギジヂビピウゥクスツヌフムユュルグズブヅプエェケセテネヘメレゲゼデベペオォコソトノホモヨョロゴゾドボポヴッンABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789';
        const fontSize = 16; const columns = mCanvas.width / fontSize;
        const rainDrops = []; for (let x = 0; x < columns; x++) rainDrops[x] = 1;

        function drawMatrix() {
            mCtx.fillStyle = 'rgba(0, 0, 0, 0.05)'; mCtx.fillRect(0, 0, mCanvas.width, mCanvas.height);
            mCtx.font = fontSize + 'px monospace';
            for (let i = 0; i < rainDrops.length; i++) {
                const text = alphabet.charAt(Math.floor(Math.random() * alphabet.length));
                mCtx.fillStyle = Math.random() > 0.95 ? '#ffffff' : (Math.random() > 0.8 ? '#ff003c' : '#880000');
                mCtx.fillText(text, i * fontSize, rainDrops[i] * fontSize);
                if (rainDrops[i] * fontSize > mCanvas.height && Math.random() > 0.975) rainDrops[i] = 0;
                rainDrops[i]++;
            }
        }
        setInterval(drawMatrix, 35);

        // --- 2. AĞ (NETWORK) PARÇACIKLARI ---
        const nCanvas = document.getElementById('networkCanvas');
        const nCtx = nCanvas.getContext('2d');
        nCanvas.width = window.innerWidth; nCanvas.height = window.innerHeight;

        let particlesArray = [];
        let mouse = { x: null, y: null, radius: 250 };

        window.addEventListener('mousemove', (e) => {
            mouse.x = e.clientX; mouse.y = e.clientY;
            let xAxis = (window.innerWidth / 2 - e.clientX) / 30;
            let yAxis = (window.innerHeight / 2 - e.clientY) / 30;
            document.getElementById('main-content').style.transform = `translate(${-xAxis}px, ${-yAxis}px) perspective(1000px) rotateX(${yAxis/2}deg) rotateY(${xAxis/2}deg)`;
        });

        class Particle {
            constructor(x, y, directionX, directionY, size) {
                this.x = x; this.y = y; this.directionX = directionX; this.directionY = directionY; this.size = size;
            }
            draw() {
                nCtx.beginPath(); nCtx.arc(this.x, this.y, this.size, 0, Math.PI * 2, false);
                let dx = mouse.x - this.x; let dy = mouse.y - this.y;
                let distance = Math.sqrt(dx * dx + dy * dy);
                if (distance < mouse.radius) {
                    nCtx.fillStyle = '#ff003c'; nCtx.shadowBlur = 20; nCtx.shadowColor = '#ff0000';
                } else {
                    nCtx.fillStyle = 'rgba(255, 0, 0, 0.4)'; nCtx.shadowBlur = 0;
                }
                nCtx.fill();
            }
            update() {
                if (this.x > nCanvas.width || this.x < 0) this.directionX = -this.directionX;
                if (this.y > nCanvas.height || this.y < 0) this.directionY = -this.directionY;
                this.x += this.directionX; this.y += this.directionY;
                this.draw();
            }
        }

        function initNetwork() {
            particlesArray = [];
            let noOfParticles = Math.floor((nCanvas.width * nCanvas.height) / 8000);
            if(noOfParticles > 200) noOfParticles = 200;
            for (let i = 0; i < noOfParticles; i++) {
                let size = Math.random() * 2.5;
                let x = Math.random() * innerWidth; let y = Math.random() * innerHeight;
                let dirX = (Math.random() * 2) - 1; let dirY = (Math.random() * 2) - 1;
                particlesArray.push(new Particle(x, y, dirX, dirY, size));
            }
        }

        function animateNetwork() {
            requestAnimationFrame(animateNetwork);
            nCtx.clearRect(0, 0, innerWidth, innerHeight);
            for (let i = 0; i < particlesArray.length; i++) particlesArray[i].update();
            
            for (let a = 0; a < particlesArray.length; a++) {
                for (let b = a; b < particlesArray.length; b++) {
                    let distance = ((particlesArray[a].x - particlesArray[b].x) * (particlesArray[a].x - particlesArray[b].x))
                                 + ((particlesArray[a].y - particlesArray[b].y) * (particlesArray[a].y - particlesArray[b].y));
                    if (distance < 20000) {
                        let opacity = 1 - (distance / 20000);
                        let dx = mouse.x - particlesArray[a].x; let dy = mouse.y - particlesArray[a].y;
                        if (Math.sqrt(dx*dx + dy*dy) < mouse.radius) {
                            nCtx.strokeStyle = `rgba(255, 0, 60, ${opacity})`; nCtx.lineWidth = 2;
                        } else {
                            nCtx.strokeStyle = `rgba(150, 0, 0, ${opacity * 0.3})`; nCtx.lineWidth = 0.5;
                        }
                        nCtx.beginPath(); nCtx.moveTo(particlesArray[a].x, particlesArray[a].y); nCtx.lineTo(particlesArray[b].x, particlesArray[b].y); nCtx.stroke();
                    }
                }
            }
        }
        initNetwork(); animateNetwork();

        window.addEventListener('resize', () => {
            mCanvas.width = innerWidth; mCanvas.height = innerHeight;
            nCanvas.width = innerWidth; nCanvas.height = innerHeight;
            initNetwork();
        });

        // --- 3. ŞİFRE ÇÖZÜCÜ (DECRYPT) YAZI EFEKTİ ---
        const textElement = document.getElementById("target-text");
        const messages = [
            { top: "SİSTEM ELE GEÇİRİLDİ", bottom: "TURKHACKTEAM" },
            { top: "VETERAN7 - ZORROKİN - B0YNER", bottom: "HACKED!" },
            { top: "İSTEDİĞİMİZ ZAMAN", bottom: "İSTEDİĞİMİZ YERDE!" },
            { top: "GÜVENLİĞİNİZ BİR İLLÜZYON", bottom: "UYANDINIZ." }
        ];
        
        const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()_+><?/";
        let msgIndex = 0;

        function decryptText(targetStr, isBottom, callback) {
            let iteration = 0;
            const interval = setInterval(() => {
                let newText = targetStr.split("")
                    .map((letter, index) => {
                        if (index < iteration) return targetStr[index];
                        return letters[Math.floor(Math.random() * letters.length)];
                    }).join("");
                
                if(isBottom) {
                    textElement.innerHTML = textElement.innerHTML.split("<span>")[0] + "<span>" + newText + "</span>";
                } else {
                    let spanHTML = textElement.querySelector('span') ? "<span>" + textElement.querySelector('span').innerText + "</span>" : "";
                    textElement.innerHTML = newText + "<br>" + spanHTML;
                }

                if (iteration >= targetStr.length) {
                    clearInterval(interval); if(callback) callback();
                }
                iteration += 1 / 2;
            }, 30);
        }

        function startDecryptionLogic() {
            let currentMsg = messages[msgIndex];
            textElement.innerHTML = " INITIALIZING... <br><span> </span>";
            setTimeout(() => {
                decryptText(currentMsg.top, false, () => {
                    setTimeout(() => {
                        decryptText(currentMsg.bottom, true, () => {
                            setTimeout(() => {
                                msgIndex = (msgIndex + 1) % messages.length;
                                startDecryptionLogic();
                            }, 3500);
                        });
                    }, 200);
                });
            }, 500);
        }

        // --- 4. SAHTE CANLI LOG AKIŞI ---
        const logContainer = document.getElementById('live-logs');
        const fakeCommands = [
            "Bypassing firewall...", "SQL Injection successful.", "Extracting admin_hash...",
            "Decrypting MD5...", "Connecting to Root server...", "Overriding protocols...",
            "Downloading DB_DUMP.sql", "Clearing tracking logs...", "Planting backdoor.sh"
        ];
        
        function startFakeLogs() {
            setInterval(() => {
                const cmd = fakeCommands[Math.floor(Math.random() * fakeCommands.length)];
                const p = document.createElement('div');
                p.className = 'log-line';
                
                if(Math.random() > 0.7) {
                    p.innerHTML = `[+] ${cmd} <span class="log-success">OK</span>`;
                } else {
                    p.innerHTML = `[*] ${cmd}`;
                }
                
                logContainer.appendChild(p);
                if(logContainer.childElementCount > 8) {
                    logContainer.removeChild(logContainer.firstChild);
                }
            }, 800);
        }

        // --- 5. GÜVENLİK KORUMALARI ---
        document.addEventListener('contextmenu', e => { e.preventDefault(); alert("SYSTEM OVERRIDE | Erişim Engellendi."); });
        document.addEventListener('keydown', e => {
            if (e.keyCode === 123 || (e.ctrlKey && e.shiftKey && (e.keyCode === 73 || e.keyCode === 74)) || (e.ctrlKey && e.keyCode === 85)) {
                e.preventDefault(); return false;
            }
        });
        document.addEventListener('dragstart', e => e.preventDefault());

    </script>
</body>
</html>
