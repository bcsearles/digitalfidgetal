<script>
if (location.protocol !== 'https:') {
    location.replace(`https:${location.href.substring(location.protocol.length)}`);
}
</script>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Digital Fidgetal</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        body {
            font-family: 'Space Grotesk', sans-serif;
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
            box-shadow: 12px 12px 0px #333;
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
            box-shadow: 6px 6px 0px #333;
        }

        .module {
            border: 2px solid #333;
            border-radius: 12px;
            margin: 10px 0;
            padding: 15px;
            text-align: center;
            box-shadow: 6px 6px 0px #333;
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
            transition: all 0.1s ease;
        }

        .btn:hover { background: #f0f0f0; }
        .btn:active {
            box-shadow: 1px 1px 0px #000;
            transform: translate(2px, 2px);
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
            box-shadow: 4px 4px 0px #bbb;
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
            box-shadow: 4px 4px 0px #000;
        }

        .wave-container {
            width: 240px;
            height: 100px;
            background: #000;
            border: 2px solid #000;
            border-radius: 8px;
            margin: 0 auto;
            cursor: pointer;
            box-shadow: 4px 4px 0px #333;
        }

        .wave-canvas { width: 100%; height: 100%; border-radius: 8px; }

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
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            color: #fff;
            user-select: none;
            transition: transform 0.3s ease;
            position: relative;
            z-index: 2;
        }

        .star-shadow {
            position: absolute;
            top: 6px;
            left: 6px;
            width: 50px;
            height: 50px;
            background: #000;
            border-radius: 6px;
            z-index: 1;
            pointer-events: none;
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
            box-shadow: 4px 4px 0px #000;
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
        <div class="title" onclick="changeColor(this)">
            DIGITAL FIDGETAL
            <div style="font-size: 12px; color: #666; font-weight: normal; margin-top: 5px;">the remedy for computertime restlessness</div>
        </div>
        
        <div class="module" style="margin-bottom: 22px;">
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
        
        <div style="display: flex; gap: 15px;">
            <div class="module" style="flex: 3; cursor: pointer;" onclick="bounce(event)">
                <div class="hand-container">
                    <div class="triangle" id="triangle"></div>
                </div>
                <div class="label">boing me</div>
            </div>
            
            <div class="module" style="flex: 1; position: relative; display: flex; flex-direction: column; justify-content: center; align-items: center;">
                <div style="position: relative; margin-top: -25px;">
                    <div class="star-shadow"></div>
                    <div class="star" onclick="spinStar(this)"></div>
                </div>
                <div class="label" style="position: absolute; bottom: 15px; left: 50%; transform: translateX(-50%); margin: 0;">tumble me</div>
            </div>
        </div>
        
        <div class="module" id="squareModule" style="position: relative; height: 150px; padding: 15px;">
            <div style="position: absolute; left: 15px; top: 10px; display: flex; flex-direction: column;">
                <button class="btn" onclick="addSquare()">+</button>
                <button class="btn" onclick="removeSquare()">-</button>
                <button class="btn" onclick="toggleBounce()">○</button>
            </div>
            <div class="square" id="square0"></div>
            <div class="label" style="position: absolute; bottom: 15px; left: 50%; transform: translateX(-50%); margin: 0;">wubba me</div>
        </div>
    </div>

    <script>
        let ballPos = 188, ballVel = 0, ballInterval = null, dragging = false;
        let waveFreq = 5, waveSpeed = 2, waveColor = '#00ff00';
        let squares = [{x: 200, y: 40, vx: 3, vy: 2}];
        let nextId = 1, bouncing = false, starRotation = 0;
        let colors = ['#333', '#e74c3c', '#3498db', '#2ecc71', '#f39c12'];
        let colorIndex = 0;

        function updateBallShadow() {
            const ball = document.getElementById('ball');
            const displacement = (ballPos - 175) / 100;
            ball.style.boxShadow = `${4 + displacement * 2}px ${4 + Math.abs(displacement) * 0.5}px 0px #000`;
        }

        function updateTriangleShadow(x, y, container) {
            const triangle = document.getElementById('triangle');
            const dispX = (x - container.offsetWidth / 2) / (container.offsetWidth / 2);
            const dispY = (y - container.offsetHeight / 2) / (container.offsetHeight / 2);
            triangle.style.boxShadow = `${3 + dispX * 8}px ${3 + dispY * 8}px 0px #000`;
        }

        function updateSquareShadow(el, x, y, maxW, maxH) {
            const dispX = (x - maxW / 2) / (maxW / 2);
            const dispY = (y - maxH / 2) / (maxH / 2);
            el.style.boxShadow = `${4 + dispX * 2}px ${4 + dispY * 2}px 0px #000`;
        }

        document.getElementById('ball').addEventListener('mousedown', e => {
            e.stopPropagation();
            dragging = true;
        });

        document.addEventListener('mousemove', e => {
            if (dragging) {
                const rect = document.querySelector('.ball-track').getBoundingClientRect();
                ballPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
                document.getElementById('ball').style.left = ballPos + 'px';
                updateBallShadow();
            }
        });

        document.addEventListener('mouseup', () => dragging = false);

        function startBallPhysics() {
            if (ballInterval) clearInterval(ballInterval);
            ballInterval = setInterval(() => {
                if (Math.abs(ballVel) < 0.3) {
                    clearInterval(ballInterval);
                    ballInterval = null;
                    return;
                }
                ballPos += ballVel;
                ballPos = Math.max(14, Math.min(322, ballPos));
                if (ballPos <= 14 || ballPos >= 322) ballVel *= -0.8;
                ballVel *= 0.97;
                document.getElementById('ball').style.left = ballPos + 'px';
                updateBallShadow();
            }, 16);
        }

        function changeColor(el) {
            colorIndex = (colorIndex + 1) % colors.length;
            el.style.color = colors[colorIndex];
        }

        function clickTrack(e) {
            if (dragging) return;
            const rect = e.currentTarget.getBoundingClientRect();
            const clickPos = Math.max(14, Math.min(322, e.clientX - rect.left - 14));
            const distance = Math.abs(clickPos - ballPos);
            
            if (distance > 20) {
                ballVel = (clickPos > ballPos ? 1 : -1) * Math.min(18, 6 + distance * 0.08);
                startBallPhysics();
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
            waveFreq = Math.max(1, Math.min(10, waveFreq + direction));
            const waveColors = ['#ff0000', '#ff8800', '#ffff00', '#88ff00', '#00ff00', '#00ff88', '#00ffff', '#0088ff', '#0000ff', '#8800ff'];
            waveColor = waveColors[waveFreq - 1] || '#00ff00';
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
            updateTriangleShadow(x, y, container);
            
            setTimeout(() => {
                triangle.style.transform = 'translate(-50%, -50%) scale(1)';
                triangle.style.boxShadow = '3px 3px 0px #000';
            }, 300);
        }

        function spinStar(el) {
            const spins = 3 + Math.random() * 2;
            starRotation += spins * 360;
            
            // Apply transition and rotation to the star
            el.style.transition = 'transform 2s ease-out';
            el.style.transform = `rotate(${starRotation}deg)`;
            el.style.background = colors[Math.floor(Math.random() * colors.length)];
            
            // Apply same transition and rotation to the shadow
            const shadow = el.parentElement.querySelector('.star-shadow');
            if (shadow) {
                shadow.style.transition = 'transform 2s ease-out';
                shadow.style.transform = `rotate(${starRotation}deg)`;
            }
        }

        function addSquare() {
            const container = document.getElementById('squareModule');
            const square = document.createElement('div');
            square.className = 'square';
            square.id = 'square' + nextId;
            
            const maxW = container.offsetWidth - 70;
            const maxH = container.offsetHeight - 60;
            const x = Math.random() * maxW;
            const y = Math.random() * maxH;
            
            square.style.left = x + 'px';
            square.style.top = y + 'px';
            square.style.background = colors[nextId % colors.length];
            
            container.appendChild(square);
            squares.push({x, y, vx: (Math.random() - 0.5) * 8, vy: (Math.random() - 0.5) * 8});
            updateSquareShadow(square, x, y, maxW, maxH);
            makeDraggable(square, squares.length - 1);
            nextId++;
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
                const maxW = module.offsetWidth - 70;
                const maxH = module.offsetHeight - 60;
                
                sq.x += sq.vx;
                sq.y += sq.vy;
                
                if (sq.x <= 0 || sq.x >= maxW) sq.vx = -sq.vx;
                if (sq.y <= 0 || sq.y >= maxH) sq.vy = -sq.vy;
                
                sq.x = Math.max(0, Math.min(maxW, sq.x));
                sq.y = Math.max(0, Math.min(maxH, sq.y));
                
                el.style.left = sq.x + 'px';
                el.style.top = sq.y + 'px';
                updateSquareShadow(el, sq.x, sq.y, maxW, maxH);
            });
            requestAnimationFrame(animate);
        }

        function makeDraggable(el, index) {
            let isDragging = false;
            
            el.addEventListener('mousedown', e => {
                if (bouncing) return;
                isDragging = true;
                
                const moveHandler = e => {
                    if (!isDragging) return;
                    const container = document.getElementById('squareModule');
                    const rect = container.getBoundingClientRect();
                    const maxW = container.offsetWidth - 70;
                    const maxH = container.offsetHeight - 60;
                    const x = Math.max(0, Math.min(maxW, e.clientX - rect.left - 20));
                    const y = Math.max(0, Math.min(maxH, e.clientY - rect.top - 20));
                    
                    el.style.left = x + 'px';
                    el.style.top = y + 'px';
                    squares[index].x = x;
                    squares[index].y = y;
                    updateSquareShadow(el, x, y, maxW, maxH);
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

        // Initialize
        drawWaves();
        makeDraggable(document.getElementById('square0'), 0);
        updateBallShadow();
        setTimeout(() => {
            const container = document.getElementById('squareModule');
            updateSquareShadow(document.getElementById('square0'), squares[0].x, squares[0].y, container.offsetWidth - 70, container.offsetHeight - 60);
        }, 100);
    </script>
</body>
</html>
