<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <title>Integrated Flow Neon Bar</title>
    <style>
        :root {
            --pink-neon: #ff007f;
            --cyan-neon: #00f2ff;
            --bar-bg: #08080c;
            --trace-speed: 12s; /* Çok yavaş ve kaliteli bir akış için */
        }

        body {
            background-color: #020202;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        /* --- ANA KONTEYNER --- */
        .main-container {
            position: relative;
            width: 850px;
            height: 52px;
            padding: 2px;
            background: rgba(255, 255, 255, 0.03);
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        /* DIŞ ÇERÇEVE NEON HATTI */
        .main-container::before {
            content: '';
            position: absolute;
            width: 150%;
            height: 400%;
            background: conic-gradient(from 0deg, transparent 75%, var(--pink-neon), #fff, var(--cyan-neon), transparent 100%);
            animation: rotate var(--trace-speed) infinite linear;
        }

        .bar-body {
            position: relative;
            width: 100%;
            height: 100%;
            background: var(--bar-bg);
            border-radius: 6px;
            display: flex;
            align-items: center;
            overflow: hidden;
            z-index: 2;
        }

        /* --- SOL PEMBE ÜNİTE (Hat ile Çevrelenmiş) --- */
        .neon-box-left {
            position: absolute;
            left: 0;
            width: 242px;
            height: 100%;
            padding: 1.5px; /* Hattın geçeceği ince kanal */
            clip-path: polygon(0 0, 100% 0, 80% 100%, 0 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        /* PEMBE BLOĞUN ÇEVRESİNDE DÖNEN HAT */
        .neon-box-left::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            background: conic-gradient(from 0deg, transparent 80%, var(--pink-neon), #fff, transparent 100%);
            animation: rotate var(--trace-speed) infinite linear;
        }

        .pink-inner {
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, #ff0055, #ff00aa);
            clip-path: polygon(0 0, 100% 0, 80% 100%, 0 100%);
            z-index: 3;
            /* İçerisi sade, sadece hafif parlıyor */
            animation: gentlePulse 5s infinite alternate ease-in-out;
        }

        /* --- SAĞ MAVİ ÜNİTE (Hat ile Çevrelenmiş) --- */
        .neon-box-right {
            position: absolute;
            right: 0;
            width: 242px;
            height: 100%;
            padding: 1.5px;
            clip-path: polygon(20% 0, 100% 0, 100% 100%, 0 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        /* MAVİ BLOĞUN ÇEVRESİNDE DÖNEN HAT */
        .neon-box-right::before {
            content: '';
            position: absolute;
            width: 200%;
            height: 200%;
            background: conic-gradient(from 0deg, transparent 80%, var(--cyan-neon), #fff, transparent 100%);
            /* Ters yöne dönerek simetri yaratır */
            animation: rotate var(--trace-speed) infinite linear reverse;
        }

        .cyan-inner {
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, #00d2ff, #3a7bd5);
            clip-path: polygon(20% 0, 100% 0, 100% 100%, 0 100%);
            z-index: 3;
            /* İçerisi sade, sadece hafif parlıyor */
            animation: gentlePulse 5s infinite alternate ease-in-out 1s;
        }

        /* --- ORTA ALAN --- */
        .center-space {
            flex: 1;
            height: 100%;
            z-index: 1;
        }

        /* --- ANİMASYONLAR --- */

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Blokların minimalist parlama efekti */
        @keyframes gentlePulse {
            0% { filter: brightness(0.9) saturate(0.95); }
            100% { filter: brightness(1.1) saturate(1.1); }
        }

        /* Opsiyonel: Çok yavaş cam süzülmesi */
        .glass-shine {
            position: absolute;
            top: 0;
            left: -150%;
            width: 40%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.04), transparent);
            transform: skewX(-20deg);
            animation: sweep 15s infinite linear;
            z-index: 10;
        }

        @keyframes sweep {
            0% { left: -150%; }
            30% { left: 150%; }
            100% { left: 150%; }
        }

    </style>
</head>
<body>

    <div class="main-container">
        <div class="bar-body">
            <div class="glass-shine"></div>

            <div class="neon-box-left">
                <div class="pink-inner"></div>
            </div>

            <div class="center-space"></div>

            <div class="neon-box-right">
                <div class="cyan-inner"></div>
            </div>
        </div>
    </div>

</body>
</html>
