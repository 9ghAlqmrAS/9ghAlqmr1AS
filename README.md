<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>System Critical Alert</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background: #000;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            user-select: none;
        }

        canvas {
            display: block;
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
        }

        .overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(255, 0, 0, 0.03);
            pointer-events: none;
            z-index: 2;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { background: rgba(255, 0, 0, 0.02); }
            50% { background: rgba(255, 0, 0, 0.08); }
            100% { background: rgba(255, 0, 0, 0.02); }
        }

        /* أنيميشن اهتزاز الشاشة بالكامل */
        .shake-screen {
            animation: screenShake 0.5s ease-in-out infinite;
        }

        @keyframes screenShake {
            0% { transform: translate(2px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(0px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(2px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(2px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
        }

        /* نافذة الاختراق الرومانسية */
        .hacker-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0.9);
            width: 90%;
            max-width: 450px;
            background: rgba(10, 10, 10, 0.95);
            border: 2px solid #ff3344;
            box-shadow: 0 0 30px rgba(255, 51, 68, 0.6);
            border-radius: 12px;
            text-align: center;
            padding: 35px 25px;
            z-index: 1000;
            direction: rtl;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            opacity: 0;
        }

        .hacker-popup.show {
            display: block;
            transform: translate(-50%, -50%) scale(1);
            opacity: 1;
        }

        .heart-icon {
            font-size: 60px;
            color: #ff3344;
            animation: beat 0.8s infinite alternate;
            margin-bottom: 15px;
            display: inline-block;
            text-shadow: 0 0 15px #ff3344;
        }

        @keyframes beat {
            0% { transform: scale(1); }
            100% { transform: scale(1.18); }
        }

        .hacker-popup h2 {
            color: #ff3344;
            margin: 0 0 20px 0;
            font-size: 26px;
            letter-spacing: 1px;
            text-shadow: 0 0 10px rgba(255, 51, 68, 0.5);
        }

        .hacker-popup p {
            color: #ffffff;
            font-size: 19px;
            line-height: 1.6;
            margin: 0 0 30px 0;
            font-weight: 500;
        }

        .hacker-popup button {
            background: linear-gradient(45deg, #ff3344, #ff5566);
            color: white;
            border: none;
            padding: 12px 35px;
            font-size: 16px;
            font-weight: bold;
            border-radius: 25px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(255, 51, 68, 0.4);
            transition: 0.3s ease;
        }

        .hacker-popup button:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 51, 68, 0.7);
        }
    </style>
</head>
<body id="mainBody">

    <canvas id="matrix"></canvas>
    <div class="overlay"></div>

    <div id="hackerPopup" class="hacker-popup">
        <div class="heart-icon">❤️</div>
        <h2>⚠️ تنبيه اختراق أمني ⚠️</h2>
        <p>تم اختراق الجهاز .. رداً على اختراقك لقلبي يا وجه القمر</p>
        <button onclick="closePopup()">امتلاك النظام (إغلاق)</button>
    </div>

    <script>
        const canvas = document.getElementById('matrix');
        const ctx = canvas.getContext('2d');
        const body = document.getElementById('mainBody');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const chars = '01010101ABCDEFGHIJKLMNOPQRSTUVWXYZ☠️⚠️⚡';
        const charArr = chars.split('');
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const rainDrops = Array(Math.floor(columns)).fill(1);

        const draw = () => {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#00ff66'; 
            ctx.font = fontSize + 'px monospace';

            for (let i = 0; i < rainDrops.length; i++) {
                const text = charArr[Math.floor(Math.random() * charArr.length)];
                ctx.fillText(text, i * fontSize, rainDrops[i] * fontSize);

                if (rainDrops[i] * fontSize > canvas.height && Math.random() > 0.975) {
                    rainDrops[i] = 0;
                }
                rainDrops[i]++;
            }
        };

        const interval = setInterval(draw, 33);

        // توليد نغمة بيانو رومانسية نقية وآمنة برمجياً بدون ملفات خارجية
        function playRomanticMusic() {
            const AudioContext = window.AudioContext || window.webkitAudioContext;
            if (!AudioContext) return;
            const audioCtx = new AudioContext();
            
            // النوتات الموسيقية الهادئة (تتابع متناسق)
            const notes = [261.63, 329.63, 392.00, 523.25, 392.00, 329.63]; 
            let time = audioCtx.currentTime;

            // تكرار المعزوفة لتستمر في الخلفية هادئة
            function playChain() {
                notes.forEach((freq, index) => {
                    const osc = audioCtx.createOscillator();
                    const gainNode = audioCtx.createGain();
                    
                    osc.type = 'sine'; // صوت بيانو ناعم
                    osc.frequency.setValueAtTime(freq, time + index * 0.6);
                    
                    gainNode.gain.setValueAtTime(0.15, time + index * 0.6);
                    gainNode.gain.exponentialRampToValueAtTime(0.001, time + (index * 0.6) + 0.5);
                    
                    osc.connect(gainNode);
                    gainNode.connect(audioCtx.destination);
                    
                    osc.start(time + index * 0.6);
                    osc.stop(time + (index * 0.6) + 0.6);
                });
                time += notes.length * 0.6;
                setTimeout(playChain, notes.length * 600);
            }
            playChain();
        }

        // تسلسل الأحداث والمفاجأة
        setTimeout(() => {
            // 1. بدء اهتزاز الشاشة لعمل صدمة هكرز دقيقة واحدة
            body.classList.add('shake-screen');
            
            setTimeout(() => {
                // 2. إيقاف الاهتزاز بعد ثانية واحدة فوراً
                body.classList.remove('shake-screen');
                
                // 3. إظهار نافذة الحب والمفاجأة
                const popup = document.getElementById('hackerPopup');
                popup.style.display = 'block';
                setTimeout(() => popup.classList.add('show'), 10);
                
                // 4. تشغيل الموسيقى الهادئة تلقائياً للمتصفح
                playRomanticMusic();
            }, 1000);

        }, 3000); // تبدأ الإثارة بعد 3 ثوانٍ من فتح الصفحة

        function closePopup() {
            const popup = document.getElementById('hackerPopup');
            popup.classList.remove('show');
            setTimeout(() => popup.style.display = 'none', 300);
        }

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    </script>
</body>
</html>
