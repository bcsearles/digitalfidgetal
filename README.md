
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

        .shadow {
            box-shadow: 6px 6px 0px #000;
        }

        .light-shadow {
            box-shadow: 4px 4px 0px #666;
        }

        .fidget-device {
            background: white;
            border: 3px solid #333;
            border-radius: 20px;
            padding: 20px 20px 10px 20px;
            width: 450px;
            margin: 0 auto;
            max-width: calc(100vw - 40px);
            box-shadow: 8px 8px 0px #000;
        }

        .title {
            text-align: center;
            font-size: 30px;
            font-weight: bold;
            color: #333;
            padding: 20px 10px;
            border: 2px solid #000;
            border-radius: 8px;
            margin-bottom: 20px;
            cursor: pointer;
            width: 85%;
            margin-left: auto;
            margin-right: auto;
            box-shadow: 5px 5px 0px #000;
        }

        .module {
            border: 2px solid #333;
            border-radius: 12px;
            margin: 10px 0;
            padding: 15px;
            text-align: center;
            box-shadow: 5px 5px 0px #000;
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
            box-shadow: 3px 3px 0px #000;
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
            box-shadow: 4px 4px 0px #000;
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
            box-shadow: 3px 3px 0px #000;
        }

        .wave-container {
            width: 240px;
            height: 100px;
            background: #000;
            border: 2px solid #000;
            border-radius: 8px;
            margin: 0 auto;
            cursor: pointer;
            box-shadow: 4px 4px 0px #666;
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
            box-shadow: 3px 3px 0px #000;
        }

        .star {
            width: 50px;
            height: 50px;
            background: #f39c12;
            border: 3px solid #333;
            border-radius: 6px;
            margin: 0 auto;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            color: #fff;
            user-select: none;
            transition: transform 0.3s ease;
            box-shadow: 4px 4px 0px #000;
        }

        .square {
            width: 40px;
            height: 40px;
            background: #27ae60;
            border: 3px solid #333;
            border-radius: 6px;
            position: absolute;
            top: 20px;
            left: 200px;
            cursor: move;
            box-shadow: 3px 3px 0px #000;
        }

        .label {
            font-size: 10px;
            color: #666;
            margin-top: 20px;
        }

        @keyframes ripple {
            0% { width: 4px; height: 4px; opacity: 1; }
            100% { width: 40px; height: 40px; opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="fidget-device">
        <div class="title" onclick="changeColor(this)" style="margin-top: -5px;">
            DIGITAL FIDGETAL
            <div style="font-size: 12px; color: #666; font-weight: normal; margin-top: 5px;">the remedy for computertime restlessness</div>
        </div>
        
        <div class="module" style="margin-top: -5px; margin-bottom: 20px;">
            <div class="ball-track" onclick="clickTrack(event)">
                <div class="ball" id="ball"></div>
            </div>
            <div class="label">chuck me</div>
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
            
            <div class="module" style="flex: 1; position: relative; display: flex; flex-direction: column; justify-content: center; align-items: center;">
                <div class="star" onclick="spinStar(this)" style="margin-top: -25px;"></div>
                <div class="label" style="position: absolute; bottom: 15px; left: 50%; transform: translateX(-50%); margin: 0;">tumble me</div>
            </div>
        </div>
        
        <div class="module" id="squareModule" style="position: relative; height: 150px; padding: 15px; margin-top: 10px;">
            <div style="position: absolute; left: 15px; top: 10px; display: flex; flex-direction: column; gap: 0px;">
                <button class="btn" onclick="addSquare()">+</button>
                <button class="btn" onclick="removeSquare()">-</button>
                <button class="btn" onclick="toggleBounce()">○</button>
            </div>
            <div class="square" id="square0"></div>
            <div class="label" style="position: absolute; bottom: 15px; left: 50%; transform: translateX(-50%); margin: 0;">wubba me</div>
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
        let squares = [{x: 200, y: 20, vx: 3, vy: 2}];
        let nextId = 1;
        let bouncing = false;
        let starRotation = 0;
        let colors = ['#333', '#e74c3c', '#3498db', '#2ecc71', '#f39c12'];
        let colorIndex = 0;

        // Ball physics
        let dragging = false;

        function ensureShadow(element, shadow = '3px 3px 0px #000') {
            element.style.boxShadow = shadow;
        }

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
                
                ballVel = direction * (15 + strength * 25);
                startBallPhysics();
            }
        });

        document.addEventListener('mousemove', (e) => {
            if (dragging) {
                const track = document.querySelector('.ball-track');
                const rect = track.getBoundingClientRect();
                ballPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
                const ball = document.getElementById('ball');
                ball.style.left = ballPos + 'px';
                ensureShadow(ball);
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
                const ball = document.getElementById('ball');
                ball.style.left = ballPos + 'px';
                ensureShadow(ball);
            }, 16);
        }

        function changeColor(el) {
            colorIndex = (colorIndex + 1) % colors.length;
            el.style.color = colors[colorIndex];
            ensureShadow(el, '5px 5px 0px #000');
        }

        function clickTrack(e) {
            if (dragging) return;
            const rect = e.currentTarget.getBoundingClientRect();
            const clickPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
            
            const distance = clickPos - ballPos;
            const direction = distance > 0 ? 1 : -1;
            const clickDistance = Math.abs(distance);
            
            if (clickDistance > 20) {
                ballVel = direction * Math.min(18, 6 + (clickDistance * 0.08));
                startBallPhysics();
            } else {
                const ball = document.getElementById('ball');
                ball.style.transition = 'left 0.3s ease-out';
                ball.style.left = clickPos + 'px';
                ballPos = clickPos;
                ensureShadow(ball);
                
                if (ballInterval) {
                    clearInterval(ballInterval);
                    ballInterval = null;
                }
                ballVel = 0;
                
                setTimeout(() => {
                    ball.style.transition = '';
                    ensureShadow(ball);
                }, 300);
            }
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
            triangle.style.transition = 'all 0.3s ease-out';
            ensureShadow(triangle);
            
            setTimeout(() => {
                triangle.style.transition = 'all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55)';
                triangle.style.transform = 'translate(-50%, -50%) scale(1)';
                ensureShadow(triangle);
            }, 300);
            
            setTimeout(() => {
                triangle.style.transition = 'all 0.4s';
                ensureShadow(triangle);
            }, 700);
        }

        function spinStar(el) {
            const spins = 3 + Math.random() * 2;
            starRotation += spins * 360;
            
            el.style.transition = 'transform 2s ease-out';
            el.style.transform = `rotate(${starRotation}deg)`;
            el.style.background = colors[Math.floor(Math.random() * colors.length)];
            ensureShadow(el, '4px 4px 0px #000');
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
            
            const colorIndex = nextId % colors.length;
            square.style.background = colors[colorIndex];
            ensureShadow(square);
            
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
                ensureShadow(el, '2px 2px 0px #145a32');
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
                    ensureShadow(el);
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
            
            el.addEventListener('click', (e) => {
                if (bouncing || isDragging) return;
                e.stopPropagation();
                
                const container = document.getElementById('squareModule');
                const targetY = container.offsetHeight - 55;
                
                el.style.transition = 'top 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55)';
                el.style.top = targetY + 'px';
                ensureShadow(el);
                squares[index].y = targetY;
                
                setTimeout(() => {
                    el.style.transition = '';
                    ensureShadow(el);
                }, 600);
            });
        }

        // Initialize
        drawWaves();
        makeDraggable(document.getElementById('square0'), 0);
        
        // Force shadows on all elements
        setTimeout(() => {
            document.querySelectorAll('.ball, .triangle, .square, .btn, .module, .ball-track, .wave-container, .title, .fidget-device').forEach(el => {
                if (el.classList.contains('ball')) ensureShadow(el);
                else if (el.classList.contains('triangle')) ensureShadow(el);
                else if (el.classList.contains('square')) ensureShadow(el);
                else if (el.classList.contains('btn')) ensureShadow(el);
                else if (el.classList.contains('module')) ensureShadow(el, '5px 5px 0px #000');
                else if (el.classList.contains('ball-track')) ensureShadow(el, '4px 4px 0px #000');
                else if (el.classList.contains('wave-container')) ensureShadow(el, '4px 4px 0px #666');
                else if (el.classList.contains('title')) ensureShadow(el, '5px 5px 0px #000');
                else if (el.classList.contains('fidget-device')) ensureShadow(el, '8px 8px 0px #000');
            });
        }, 100);
    </script>
</body>
</html>
