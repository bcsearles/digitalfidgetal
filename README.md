<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My GitHub Page</title>

  <!-- Google Fonts: Space Grotesk -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300..700&display=swap" rel="stylesheet">

  <!-- Your CSS file -->
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Hello GitHub!</h1>
</body>
</html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Fidgetal</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: monospace;
            background: #f0f0f0;
            padding: 40px 20px;
        }

        .fidget-device {
            background: white;
            border: 3px solid #333;
            border-radius: 20px;
            padding: 20px;
            width: 450px;
            margin: 0 auto;
            max-width: calc(100vw - 40px);
        }

        .title {
            text-align: center;
            font-size: 30px;
            font-weight: bold;
            color: #333;
            padding: 10px;
            border: 2px solid #000;
            border-radius: 8px;
            margin-bottom: 20px;
            cursor: pointer;
        }

        .module {
            border: 2px solid #333;
            border-radius: 12px;
            margin: 10px 0;
            padding: 15px;
            text-align: center;
        }

        .btn {
            background: white;
            border: 2px solid #333;
            border-radius: 6px;
            width: 32px;
            height: 32px;
            font-size: 16px;
            cursor: pointer;
            margin: 5px;
        }

        .btn:hover {
            background: #f0f0f0;
        }

        .ball-track {
            width: 350px;
            height: 50px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 25px;
            position: relative;
            margin: 0 auto;
            cursor: pointer;
        }

        .ball {
            width: 28px;
            height: 28px;
            background: #f1c40f;
            border: 2px solid #000;
            border-radius: 50%;
            position: absolute;
            top: 10px;
            left: 188px;
            cursor: grab;
        }

        .wave-container {
            width: 240px;
            height: 100px;
            background: #000;
            border: 2px solid #000;
            border-radius: 8px;
            margin: 0 auto;
            cursor: pointer;
        }

        .wave-canvas {
            width: 100%;
            height: 100%;
            border-radius: 8px;
        }

        .hand-container {
            width: 100%;
            height: 70px;
            position: relative;
            cursor: pointer;
        }

        .triangle {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 20px;
            height: 20px;
            background: #e74c3c;
            border: 2px solid #000;
            border-radius: 50%;
            transition: all 0.4s;
        }

        .diamond {
            width: 40px;
            height: 40px;
            background: #2196f3;
            border: 3px solid #333;
            transform: rotate(45deg);
            cursor: pointer;
            margin: 0 auto;
            transition: all 0.3s;
        }

        .square {
            width: 40px;
            height: 40px;
            background: #27ae60;
            border: 3px solid #333;
            border-radius: 6px;
            position: absolute;
            top: 40px;
            left: 200px;
            cursor: move;
        }

        .label {
            font-size: 10px;
            color: #666;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="fidget-device">
        <div class="title" onclick="changeColor(this)">DIGITAL FIDGETAL</div>
        
        <div class="module">
            <div class="ball-track" onclick="clickTrack(event)">
                <div class="ball" id="ball"></div>
            </div>
            <div class="label">dibble me</div>
        </div>
        
        <div class="module">
            <div style="display: flex; align-items: center; gap: 15px; justify-content: center;">
                <div style="display: flex; flex-direction: column; gap: 5px;">
                    <button class="btn" onclick="changeWaveMode(-1)">•</button>
                    <button class="btn" onclick="changeWaveMode(1)">○</button>
                </div>
                <div class="wave-container" onclick="ripple(event)">
                    <canvas class="wave-canvas" id="canvas" width="240" height="100"></canvas>
                </div>
                <div style="display: flex; flex-direction: column; gap: 5px;">
                    <button class="btn" onclick="adjustWaves(1)">+</button>
                    <button class="btn" onclick="adjustWaves(-1)">-</button>
                </div>
            </div>
            <div class="label">tune me</div>
        </div>
        
        <div style="display: flex; gap: 10px;">
            <div class="module" style="flex: 3; cursor: pointer;" onclick="bounce(event)">
                <div class="hand-container">
                    <div class="triangle" id="triangle"></div>
                </div>
                <div class="label">boing me</div>
            </div>
            
            <div class="module" style="flex: 1;">
                <div class="diamond" onclick="spin(this)"></div>
                <div class="label">tumble me</div>
            </div>
        </div>
        
        <div class="module" id="squareModule" style="position: relative; height: 150px; padding: 15px;">
            <div style="position: absolute; left: 15px; top: 10px; display: flex; flex-direction: column; gap: 0px;">
                <button class="btn" onclick="addSquare()">+</button>
                <button class="btn" onclick="removeSquare()">-</button>
                <button class="btn" onclick="toggleBounce()">○</button>
            </div>
            <div class="square" id="square0"></div>
            <div class="label" style="position: absolute; bottom: 5px; left: 50%; transform: translateX(-50%); margin: 0;">wubba me</div>
        </div>
    </div>

    <script>
        let ballPos = 188;
        let ballVel = 0;
        let ballInterval = null;
        let waveMode = 5;
        let waveFreq = 5;
        let waveSpeed = 2;
        let waveColor = '#00ff00';
        let squares = [{x: 200, y: 40, vx: 3, vy: 2}];
        let nextId = 1;
        let bouncing = false;
        let colors = ['#333', '#e74c3c', '#3498db', '#2ecc71', '#f39c12'];
        let colorIndex = 0;

        // Ball physics
        let dragging = false;

        document.getElementById('ball').addEventListener('mousedown', (e) => {
            e.stopPropagation();
            dragging = true;
        });

        document.getElementById('ball').addEventListener('click', (e) => {
            e.stopPropagation();
            if (!dragging) {
                const ball = document.getElementById('ball');
                const rect = ball.getBoundingClientRect();
                const clickX = e.clientX - rect.left;
                const ballCenter = rect.width / 2;
                
                const direction = clickX > ballCenter ? 1 : -1;
                const strength = Math.abs(clickX - ballCenter) / ballCenter;
                ballVel = direction * (10 + strength * 20);
                
                startBallPhysics();
            }
        });

        document.addEventListener('mousemove', (e) => {
            if (dragging) {
                const track = document.querySelector('.ball-track');
                const rect = track.getBoundingClientRect();
                ballPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
                document.getElementById('ball').style.left = ballPos + 'px';
                ballVel = 0;
            }
        });

        document.addEventListener('mouseup', () => dragging = false);

        function startBallPhysics() {
            if (ballInterval) clearInterval(ballInterval);
            
            ballInterval = setInterval(() => {
                if (Math.abs(ballVel) < 0.3) {
                    clearInterval(ballInterval);
                    ballInterval = null;
                    ballVel = 0;
                    return;
                }
                
                ballPos += ballVel;
                ballPos = Math.max(14, Math.min(322, ballPos));
                
                if (ballPos <= 14 || ballPos >= 322) {
                    ballVel *= -0.8;
                }
                
                ballVel *= 0.97;
                document.getElementById('ball').style.left = ballPos + 'px';
            }, 16);
        }

        function changeColor(el) {
            colorIndex = (colorIndex + 1) % colors.length;
            el.style.color = colors[colorIndex];
        }

        function clickTrack(e) {
            if (dragging) return;
            const rect = e.currentTarget.getBoundingClientRect();
            ballPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
            document.getElementById('ball').style.left = ballPos + 'px';
        }

        function drawWaves() {
            const canvas = document.getElementById('canvas');
            const ctx = canvas.getContext('2d');
            const time = Date.now() * 0.01 * waveSpeed;
            
            ctx.clearRect(0, 0, 240, 100);
            ctx.strokeStyle = waveColor;
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            for (let x = 0; x < 240; x++) {
                const y = 50 + Math.sin((x * 0.02 * waveFreq) + time) * 25;
                if (x === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            ctx.stroke();
            requestAnimationFrame(drawWaves);
        }

        function adjustWaves(change) {
            waveSpeed = Math.max(0.5, Math.min(8, waveSpeed + change * 0.5));
        }

        function changeWaveMode(direction) {
            waveMode = Math.max(1, Math.min(10, waveMode + direction));
            updateWaveSettings(waveMode);
        }

        function updateWaveSettings(value) {
            waveFreq = value;
            const colors = ['#ff0000', '#ff8800', '#ffff00', '#88ff00', '#00ff00', '#00ff88', '#00ffff', '#0088ff', '#0000ff', '#8800ff'];
            waveColor = colors[value - 1] || '#00ff00';
        }

        function ripple(e) {
            const rect = e.currentTarget.getBoundingClientRect();
            const ripple = document.createElement('div');
            ripple.style.cssText = `
                position: absolute;
                left: ${e.clientX - rect.left}px;
                top: 50px;
                width: 4px;
                height: 4px;
                background: ${waveColor};
                border-radius: 50%;
                transform: translate(-50%, -50%);
                animation: ripple 1s ease-out forwards;
                pointer-events: none;
            `;
            e.currentTarget.appendChild(ripple);
            setTimeout(() => ripple.remove(), 1000);
        }

        function bounce(e) {
            const container = e.currentTarget;
            const triangle = document.getElementById('triangle');
            const rect = container.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            triangle.style.transform = `translate(${x - container.offsetWidth/2}px, ${y - container.offsetHeight/2}px) scale(1.5)`;
            setTimeout(() => triangle.style.transform = 'translate(-50%, -50%) scale(1)', 600);
        }

        function spin(el) {
            el.style.transform = 'rotate(405deg)';
            el.style.background = colors[Math.floor(Math.random() * colors.length)];
            setTimeout(() => el.style.transform = 'rotate(45deg)', 600);
        }

        function addSquare() {
            const container = document.getElementById('squareModule');
            const square = document.createElement('div');
            square.className = 'square';
            square.id = 'square' + nextId;
            
            const maxWidth = container.offsetWidth - 70;
            const maxHeight = container.offsetHeight - 60;
            const x = Math.random() * maxWidth;
            const y = Math.random() * maxHeight;
            square.style.left = x + 'px';
            square.style.top = y + 'px';
            
            container.appendChild(square);
            squares.push({x, y, vx: (Math.random() - 0.5) * 8, vy: (Math.random() - 0.5) * 8});
            nextId++;
            
            makeDraggable(square, squares.length - 1);
        }

        function removeSquare() {
            if (squares.length <= 1) return;
            squares.pop();
            const lastSquare = document.getElementById('square' + (nextId - 1));
            if (lastSquare) lastSquare.remove();
            nextId--;
        }

        function toggleBounce() {
            bouncing = !bouncing;
            if (bouncing) animate();
        }

        function animate() {
            if (!bouncing) return;
            
            squares.forEach((sq, i) => {
                const el = document.getElementById('square' + i);
                if (!el) return;
                
                const module = el.closest('.module');
                const maxWidth = module.offsetWidth - 70;
                const maxHeight = module.offsetHeight - 60;
                
                sq.x += sq.vx;
                sq.y += sq.vy;
                
                if (sq.x <= 0 || sq.x >= maxWidth) sq.vx = -sq.vx;
                if (sq.y <= 0 || sq.y >= maxHeight) sq.vy = -sq.vy;
                
                sq.x = Math.max(0, Math.min(maxWidth, sq.x));
                sq.y = Math.max(0, Math.min(maxHeight, sq.y));
                
                el.style.left = sq.x + 'px';
                el.style.top = sq.y + 'px';
            });
            
            requestAnimationFrame(animate);
        }

        function makeDraggable(el, index) {
            let isDragging = false;
            
            el.addEventListener('mousedown', (e) => {
                if (bouncing) return;
                isDragging = true;
                
                const moveHandler = (e) => {
                    if (!isDragging) return;
                    const container = document.getElementById('squareModule');
                    const rect = container.getBoundingClientRect();
                    const maxWidth = container.offsetWidth - 70;
                    const maxHeight = container.offsetHeight - 60;
                    const x = Math.max(0, Math.min(maxWidth, e.clientX - rect.left - 20));
                    const y = Math.max(0, Math.min(maxHeight, e.clientY - rect.top - 20));
                    
                    el.style.left = x + 'px';
                    el.style.top = y + 'px';
                    squares[index].x = x;
                    squares[index].y = y;
                };
                
                const upHandler = () => {
                    isDragging = false;
                    document.removeEventListener('mousemove', moveHandler);
                    document.removeEventListener('mouseup', upHandler);
                };
                
                document.addEventListener('mousemove', moveHandler);
                document.addEventListener('mouseup', upHandler);
            });
        }

        const style = document.createElement('style');
        style.textContent = `
            @keyframes ripple {
                0% { width: 4px; height: 4px; opacity: 1; }
                100% { width: 40px; height: 40px; opacity: 0; }
            }
        `;
        document.head.appendChild(style);

        drawWaves();
        makeDraggable(document.getElementById('square0'), 0);
    </script>
</body>
</html>
