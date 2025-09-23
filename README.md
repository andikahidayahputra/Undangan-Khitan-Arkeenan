<html lang="id">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Undangan — Sampul</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400..700&display=swap" rel="stylesheet">
    
    <style>
        :root{
            --overlay-rgba: rgba(0,0,0,0.45);
            --accent: rgba(255,255,255,0.12);
            --glass: rgba(255,255,255,0.06);
            --radius: 14px;
            --max-width: 900px;
        }
        html,body{
            height:100%;
            margin:0;
            font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
            -webkit-font-smoothing:antialiased;
            -moz-osx-font-smoothing:grayscale;
            color: #ffffff;
            background-image: url('foto kakang.jpeg');
            background-position: center center;
            background-size: cover;
            background-repeat: no-repeat;
        }
        .cover{position:relative;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:0;box-sizing:border-box;overflow:hidden;}
        .bg{position:absolute;inset:0;background-image: url('cover.jpg');background-size:cover;background-position:center center;filter:saturate(1.06) contrast(1.02);z-index:0;}
        .overlay{position:absolute;inset:0;background: linear-gradient(180deg, rgba(0,0,0,0.28) 0%, rgba(0,0,0,0.55) 100%), var(--overlay-rgba);z-index:1;backdrop-filter: blur(0%);}
        .content{position:relative;z-index:2;width:100%;max-width:var(--max-width);display:flex;gap:20px;align-items:center;justify-content:center;flex-direction:column;text-align:center;padding:28px;box-sizing:border-box;}
        .card{width:100%;background: linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius: var(--radius);padding:18px;box-sizing:border-box;box-shadow: 0 8px 30px rgba(0,0,0,0.45);backdrop-filter: blur(6px);border: 1px solid rgba(255,255,255,0.06);}
        h1{margin:6px 0 2px;font-size:clamp(20px,4.8vw,40px);letter-spacing:0.6px;font-weight:700;}
        /* CSS untuk font nama Arkeenan */
        .couple{
            font-family: 'Dancing Script', cursive; /* Menggunakan font Dancing Script */
            font-weight: 700; /* Font weight diubah ke 700 */
            font-size: clamp(28px, 6vw, 50px); /* Ukuran font diperbesar */
            opacity:0.98;
            margin:6px 0 12px;
            letter-spacing: 1.5px; /* Menambah spasi antar huruf agar lebih artistik */
        }
        .guest{font-size:clamp(14px,3.2vw,20px);opacity:0.95;margin-bottom:12px;}
        .meta{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;align-items:center;margin-bottom:14px;}
        .date{padding:8px 14px;border-radius:999px;background:var(--glass);font-weight:600;font-size:14px;}
        .countdown{display:flex;gap:10px;justify-content:center;margin-bottom:14px;flex-wrap:wrap;}
        .countdown .item{min-width:60px;padding:8px 10px;border-radius:10px;background: rgba(255,255,255,0.06);font-weight:700;font-size:14px;}
        .btn-row{display:flex;gap:12px;justify-content:center;margin-top:6px;flex-wrap:wrap;}
        .btn{-webkit-tap-highlight-color: transparent;cursor:pointer;border:0;padding:12px 18px;font-weight:700;border-radius:12px;background: linear-gradient(90deg, rgba(255,255,255,0.07), rgba(255,255,255,0.03));color:#fff;text-decoration:none;display:inline-flex;align-items:center;gap:10px;transition: transform .12s ease, box-shadow .12s ease, opacity .12s;box-shadow: 0 6px 18px rgba(0,0,0,0.45);}
        .btn:active{transform: translateY(1px) scale(.997);}
        .btn-primary{background: linear-gradient(90deg, rgba(255,255,255,0.12), rgba(255,255,255,0.06));border: 1px solid rgba(255,255,255,0.12);}
        .small{font-size:13px;opacity:0.9;}
        @media (max-width:480px){
            .card{ padding:16px; }
            .countdown .item{ min-width:48px; padding:6px 8px; font-size:13px;}
            .btn{ padding:10px 14px; }
        }
        .footer{margin-top:14px;font-size:12px;opacity:0.85;}
    </style>
</head>
<body>
    <div class="cover" role="main">
        <div class="bg" aria-hidden="true"></div>
        <div class="overlay" aria-hidden="true"></div>

        <div class="content">
            <div class="card" id="mainCard" role="region" aria-label="Sampul undangan">
                <h1 id="greeting">Undangan Khitanan</h1>
                <div class="couple" id="coupleNames">Arkeenan Putra Firmansyah</div>
                <div class="guest small" id="guestName">Untuk: Tamu Undangan</div>
                <div class="meta">
                    <div class="date" id="eventDateLabel">Sabtu, 18 Oktober 2025 — 18:00</div>
                </div>
                <div class="countdown" aria-live="polite" id="countdown">
                    <div class="item" id="cd-days">--<br><small>Hari</small></div>
                    <div class="item" id="cd-hours">--<br><small>Jam</small></div>
                    <div class="item" id="cd-mins">--<br><small>Menit</small></div>
                    <div class="item" id="cd-secs">--<br><small>Detik</small></div>
                </div>
                <div class="btn-row">
                    <button class="btn btn-primary" id="openBtn" aria-label="Buka Undangan">
                        Buka Undangan
                    </button>
                </div>
                <div class="footer">Musik akan otomatis diputar saat halaman diklik atau diketuk.</div>
            </div>
        </div>
    </div>

    <audio id="bgAudio" src="khitanan.mp3" preload="auto" autoplay loop></audio>

    <script>
        /**********************************************************************
         * CONFIG
         *********************************************************************/
        const coupleName = "Arkeenan Putra Firmansyah";
        const eventDate = "2025-10-18T08:00:00"; 
        const canvaLink = "https://undangan-khitanan-arkeenann.my.canva.site/undangan-khitan-arkeenan";

        // guest name dari parameter URL ?nama=
        function getQueryParam(name){
            try {
                const urlParams = new URLSearchParams(window.location.search);
                return urlParams.get(name);
            } catch(e){ return null; }
        }

        document.getElementById('coupleNames').textContent = coupleName;
        const eventDateObj = new Date(eventDate);
        if (!isNaN(eventDateObj)) {
            const dateOpts = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const timeOpts = { hour: '2-digit', minute: '2-digit' };
            document.getElementById('eventDateLabel').textContent =
                eventDateObj.toLocaleDateString('id-ID', dateOpts) + ' — ' + eventDateObj.toLocaleTimeString('id-ID', timeOpts);
        }
        const guestParam = getQueryParam('nama');
        document.getElementById('guestName').textContent = "Kepada: " + (guestParam ? decodeURIComponent(guestParam) : "Tamu Undangan");

        // countdown
        const cdDays = document.getElementById('cd-days');
        const cdHours = document.getElementById('cd-hours');
        const cdMins = document.getElementById('cd-mins');
        const cdSecs = document.getElementById('cd-secs');
        function updateCountdown(){
            const now = new Date();
            const diff = eventDateObj - now;
            if (isNaN(eventDateObj) || diff <= 0){
                cdDays.innerHTML = "0<br><small>Hari</small>";
                cdHours.innerHTML = "0<br><small>Jam</small>";
                cdMins.innerHTML = "0<br><small>Menit</small>";
                cdSecs.innerHTML = "0<br><small>Detik</small>";
                return;
            }
            const s = Math.floor(diff/1000);
            const days = Math.floor(s / (3600*24));
            const hours = Math.floor((s % (3600*24)) / 3600);
            const mins = Math.floor((s % 3600) / 60);
            const secs = s % 60;
            cdDays.innerHTML = days + '<br><small>Hari</small>';
            cdHours.innerHTML = hours + '<br><small>Jam</small>';
            cdMins.innerHTML = mins + '<br><small>Menit</small>';
            cdSecs.innerHTML = secs + '<br><small>Detik</small>';
        }
        updateCountdown();
        setInterval(updateCountdown, 1000);

        // buka canva
        document.getElementById('openBtn').addEventListener('click',()=>{
            window.open(canvaLink, '_blank');
        });

        // play music after user interaction (necessary for modern browsers)
        window.addEventListener('click', () => {
            const audio = document.getElementById('bgAudio');
            audio.play().catch(() => {});
        }, { once: true });

        window.addEventListener('touchend', () => {
            const audio = document.getElementById('bgAudio');
            audio.play().catch(() => {});
        }, { once: true });
    </script>
</body>
</html>
