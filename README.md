<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beni Kızdırdın mı? 💕</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        .container {
            text-align: center;
            background: rgba(255, 255, 255, 0.95);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            max-width: 600px;
            width: 90%;
            position: relative;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }

        h1 {
            color: #333;
            margin-bottom: 30px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .gif-container {
            width: 100%;
            height: 300px;
            margin-bottom: 30px;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            background: #f0f0f0;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .gif-container img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            flex-wrap: wrap;
            position: relative;
        }

        button {
            padding: 15px 40px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        #evetBtn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a6f);
            color: white;
            box-shadow: 0 4px 15px rgba(238, 90, 111, 0.4);
        }

        #evetBtn:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(238, 90, 111, 0.6);
        }

        #hayirBtn {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            box-shadow: 0 4px 15px rgba(68, 160, 141, 0.4);
            position: relative;
        }

        #hayirBtn:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(68, 160, 141, 0.6);
        }

        .counter {
            margin-top: 20px;
            font-size: 1.1em;
            color: #666;
        }

        .hearts {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 1000;
        }

        .heart {
            position: absolute;
            font-size: 20px;
            animation: fall linear forwards;
            opacity: 0.8;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .final-message {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.9);
            z-index: 2000;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            animation: fadeIn 1s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .final-message img {
            max-width: 80%;
            max-height: 60vh;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(255,255,255,0.2);
        }

        .final-message h2 {
            color: white;
            font-size: 3em;
            margin-top: 30px;
            text-align: center;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        .close-btn {
            position: absolute;
            top: 20px;
            right: 30px;
            color: white;
            font-size: 2em;
            cursor: pointer;
            background: none;
            border: none;
        }

        .emoji {
            font-size: 2em;
            margin: 0 10px;
        }

        @media (max-width: 600px) {
            h1 { font-size: 1.8em; }
            button { padding: 12px 30px; font-size: 1em; }
        }
    </style>
</head>
<body>
    <div class="hearts" id="hearts"></div>
    
    <div class="container">
        <h1>Beni Kızdırdın mı? <span class="emoji">😤</span></h1>
        
        <div class="gif-container" id="gifContainer">
            <img id="mainGif" src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/3o7TKSjRrfIPjeiVyM/giphy.gif" alt="Cute angry gif">
        </div>
        
        <div class="buttons">
            <button id="evetBtn" onclick="evetTikla()">Evet</button>
            <button id="hayirBtn" onclick="hayirTikla()">Hayır</button>
        </div>
        
        <div class="counter" id="counter"></div>
    </div>

    <div class="final-message" id="finalMessage">
        <button class="close-btn" onclick="kapat()">×</button>
        <img id="finalGif" src="" alt="Final gif">
        <h2>Seni Çok Seviyorum! <span class="emoji">💖</span></h2>
    </div>

    <script>
        let evetBoyut = 1;
        let hayirBoyut = 1;
        let tiklamaSayisi = 0;
        
        const gifs = [
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/3o7TKSjRrfIPjeiVyM/giphy.gif", // Başlangıç - şüpheli
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/l0HlNQ03J5JxX6lva/giphy.gif", // Hafif sinirli
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/26gscSDIglL2prSH6/giphy.gif", // Daha sinirli
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/L95W4wv8nnb9K/giphy.gif", // Kızgın kedi
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/9Y5BbDSkSTiY8/giphy.gif", // Çok sinirli
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/6nWhy3ulBL7G/giphy.gif"  // Final öncesi
        ];

        const finalGifs = [
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/l0HlNQ03J5JxX6lva/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/3oriO0OEd9QIDdllqo/giphy.gif",
            "https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExYW10dWJ1Z3JvdW5kPTEmY3Q9Zw/mIZ9rPeMKefm0/giphy.gif"
        ];

        function hayirTikla() {
            tiklamaSayisi++;
            
            // Evet büyür, hayır küçülür
            evetBoyut += 0.3;
            hayirBoyut -= 0.1;
            
            if (hayirBoyut < 0.3) hayirBoyut = 0.3;
            
            const evetBtn = document.getElementById('evetBtn');
            const hayirBtn = document.getElementById('hayirBtn');
            const mainGif = document.getElementById('mainGif');
            const counter = document.getElementById('counter');
            
            evetBtn.style.transform = `scale(${evetBoyut})`;
            hayirBtn.style.transform = `scale(${hayirBoyut})`;
            
            // GIF değiştir
            if (tiklamaSayisi < gifs.length) {
                mainGif.src = gifs[tiklamaSayisi];
            }
            
            // Buton konumunu rastgele değiştir (kaçış efekti)
            if (tiklamaSayisi > 2) {
                const x = (Math.random() - 0.5) * 100;
                const y = (Math.random() - 0.5) * 50;
                hayirBtn.style.transform = `scale(${hayirBoyut}) translate(${x}px, ${y}px)`;
            }
            
            counter.innerHTML = `Hayır denemesi: ${tiklamaSayisi} 😏<br>Evet butonu büyüyor...`;
            
            // Kalp efekti
            createHeart();
        }

        function evetTikla() {
            const finalMsg = document.getElementById('finalMessage');
            const finalGif = document.getElementById('finalGif');
            
            // Rastgele final gif
            finalGif.src = finalGifs[Math.floor(Math.random() * finalGifs.length)];
            
            finalMsg.style.display = 'flex';
            
            // Kalp yağmuru
            for(let i = 0; i < 50; i++) {
                setTimeout(() => createHeart(), i * 100);
            }
        }

        function kapat() {
            document.getElementById('finalMessage').style.display = 'none';
        }

        function createHeart() {
            const hearts = document.getElementById('hearts');
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.innerHTML = ['❤️', '💖', '💕', '💗', '💓', '💝'][Math.floor(Math.random() * 6)];
            heart.style.left = Math.random() * 100 + '%';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            heart.style.fontSize = (Math.random() * 20 + 10) + 'px';
            hearts.appendChild(heart);
            
            setTimeout(() => heart.remove(), 5000);
        }

        // Başlangıçta kalp efekti
        setInterval(() => createHeart(), 2000);
    </script>
</body>
</html>
