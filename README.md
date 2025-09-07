
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
            font-family: 'Space Grotesk', monospace, sans-serif;
            background: #f0f0f0;
            margin: 0;
            padding: 40px 20px;
            position: relative;
            overflow-x: hidden;
            /* Ensure no extra space at top */
            padding-top: 40px;
            margin-top: 0;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0.2;
            background: 
                radial-gradient(circle, transparent 1px, #666 1px),
                radial-gradient(circle, transparent 1px, #999 1px),
                radial-gradient(circle, transparent 1px, #333 1px);
            background-size: 4px 4px, 7px 7px, 11px 11px;
            background-position: 0 0, 3px 3px, 6px 6px;
            animation: staticNoise 0.5s infinite linear;
            z-index: -1;
        }

        @keyframes staticNoise {
            0% { 
                transform: translate(0, 0);
                filter: hue-rotate(0deg);
            }
            25% { 
                transform: translate(-1px, 1px);
                filter: hue-rotate(0deg);
            }
            50% { 
                transform: translate(1px, -1px);
                filter: hue-rotate(0deg);
            }
            75% { 
                transform: translate(-1px, -1px);
                filter: hue-rotate(0deg);
            }
            100% { 
                transform: translate(1px, 1px);
                filter: hue-rotate(0deg);
            }
        }

        .loading-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: white;
            color: #333;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            font-family: 'Space Grotesk', monospace, sans-serif;
        }

        .loading-text {
            font-size: 32px;
            font-weight: bold;
            letter-spacing: 2px;
            text-align: center;
        }

        .fidget-device {
            background: white;
            border: 3px solid #333;
            border-radius: 20px;
            padding: 20px;
            width: 450px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            margin: 0 auto;
            max-width: calc(100vw - 40px);
        }

        .title {
            text-align: center;
            font-size: 30px;
            font-weight: bold;
            letter-spacing: 1px;
            color: #333;
            padding: 10px 15px 6px 15px;
            background: white;
            border: 2px solid #000;
            border-radius: 8px 8px 0 0;
            max-width: 340px;
            margin: 0 auto;
        }

        .subtitle {
            text-align: center;
            font-size: 12px;
            color: #666;
            margin-bottom: 15px;
            padding: 2px 15px 10px 15px;
            background: white;
            border: 2px solid #000;
            border-top: none;
            border-radius: 0 0 8px 8px;
            margin-top: -6px;
            max-width: 340px;
            margin-left: auto;
            margin-right: auto;
        }

        .module {
            background: white;
            border: 2px solid #333;
            border-radius: 12px;
            margin: 10px 0;
            padding: 15px;
        }

        .module-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 10px;
        }

        .controls {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .btn {
            background: white;
            border: 2px solid #333;
            border-radius: 6px;
            width: 32px;
            height: 32px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
        }

        .btn:hover {
            background: #f0f0f0;
            transform: translateY(-2px);
        }

        .btn:active {
            transform: translateY(0);
        }

        .tilt-controls {
            display: flex;
            align-items: center;
            gap: 15px;
            width: 100%;
            justify-content: center;
            padding-right: 15px;
        }

        .ball-track {
            width: 350px;
            height: 50px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 25px;
            position: relative;
            overflow: hidden;
            cursor: pointer;
        }

        .ball {
            width: 24px;
            height: 24px;
            background: #f1c40f;
            border: 2px solid #000;
            border-radius: 50%;
            position: absolute;
            top: 12px;
            left: 190px;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }

        .custom-vertical-slider {
            width: 20px;
            height: 60px;
            position: relative;
            margin-left: 20px;
            cursor: pointer;
        }

        .slider-track {
            width: 5px;
            height: 60px;
            background: #888;
            border-radius: 3px;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
        }

        .slider-thumb {
            width: 16px;
            height: 16px;
            background: white;
            border: 2px solid #000;
            border-radius: 50%;
            position: absolute;
            left: 50%;
            top: 34%;
            transform: translate(-50%, -50%);
            cursor: pointer;
            transition: top 0.1s ease;
        }

        .wave-container {
            width: 240px;
            height: 60px;
            background: #000;
            border: 2px solid #000;
            border-radius: 8px;
            position: relative;
            cursor: pointer;
        }

        .wave-canvas {
            width: 100%;
            height: 100%;
            border-radius: 8px;
        }

        .slider {
            width: 100px;
            height: 5px;
            background: #888 !important;
            border-radius: 3px;
            appearance: none;
            cursor: pointer;
            -webkit-appearance: none;
            outline: none;
        }

        .slider::-webkit-slider-thumb {
            appearance: none;
            -webkit-appearance: none;
            width: 16px;
            height: 16px;
            background: white !important;
            border: 2px solid #000 !important;
            border-radius: 50%;
            cursor: pointer;
        }

        .slider::-moz-range-thumb {
            width: 16px;
            height: 16px;
            background: white !important;
            border: 2px solid #000 !important;
            border-radius: 50%;
            cursor: pointer;
        }

        .hand-container {
            width: 100%;
            height: 70px;
            background: transparent;
            border-radius: 12px;
            position: relative;
            cursor: pointer;
            overflow: visible;
        }

        .hand-container:hover {
            background: rgba(240, 240, 240, 0.3);
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
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            cursor: grab;
            border-radius: 50%;
        }

        .shapes-area {
            width: 300px;
            height: 120px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 12px;
            position: relative;
        }

        .shape {
            position: absolute;
            cursor: move;
            transition: all 0.3s ease;
            user-select: none;
        }

        .square {
            width: 40px;
            height: 40px;
            background: #27ae60;
            border: 3px solid #333;
            border-radius: 6px;
            top: 40px;
            left: 130px;
        }

        .diamond-container {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            height: 60px;
        }

        .diamond {
            width: 40px;
            height: 40px;
            background: #2196f3;
            border: 3px solid #333;
            transform: rotate(45deg);
            cursor: pointer;
            transition: all 0.3s ease;
            border-radius: 6px;
        }

        .diamond:hover {
            transform: rotate(45deg) scale(1.05);
        }

        .diamond.spinning {
            animation: spin 0.6s ease-in-out;
        }

        @keyframes spin {
            0% { transform: rotate(45deg); }
            25% { transform: rotate(135deg); }
            50% { transform: rotate(225deg); }
            75% { transform: rotate(315deg); }
            100% { transform: rotate(405deg); }
        }

        .label {
            font-size: 10px;
            color: #666;
            text-align: center;
            margin-top: 8px;
        }

        @media (max-width: 768px) {
            .fidget-device {
                width: 100%;
                max-width: 450px;
            }
        }
    </style>
</head>
<body>
    <div class="loading-screen" id="loadingScreen">
        <div class="loading-text">WELCOME TO<br>DIGITAL FIDGETAL</div>
    </div>
    
    <div class="fidget-device">
        <div class="title">DIGITAL FIDGETAL</div>
        <div class="subtitle">the remedy for computertime restlessness</div>
        
        <div class="module">
            <div class="module-content">
                <div class="tilt-controls">
                    <div class="ball-track" onclick="clickBallTrack(event)">
                        <div class="ball" id="ball"></div>
                    </div>
                    <div class="custom-vertical-slider" id="customSlider" onclick="handleSliderClick(event)">
                        <div class="slider-track"></div>
                        <div class="slider-thumb" id="sliderThumb"></div>
                    </div>
                </div>
                <div class="label">dibble me</div>
            </div>
        </div>
        
        <div class="module">
            <div class="module-content">
                <div style="display: flex; align-items: flex-start; gap: 15px;">
                    <div style="display: flex; flex-direction: column; align-items: center; gap: 10px; margin-top: 10px;">
                        <div class="controls">
                            <button class="btn" onclick="adjustWaves(1)">+</button>
                            <button class="btn" onclick="adjustWaves(-1)">-</button>
                        </div>
                        <input type="range" min="1" max="10" value="5" class="slider" onchange="updateWaveSpeed(this.value)" style="width: 74px;">
                    </div>
                    <div class="wave-container" onclick="ripple(event)">
                        <canvas class="wave-canvas" id="waveCanvas" width="240" height="60"></canvas>
                    </div>
                </div>
                <div class="label">tune me</div>
            </div>
        </div>
        
        <div style="display: flex; gap: 10px;">
            <div class="module" style="flex: 3;">
                <div class="module-content">
                    <div class="hand-container" onclick="throwTriangle(event)">
                        <div class="triangle" id="triangle"></div>
                    </div>
                    <div class="label">boing me</div>
                </div>
            </div>
            
            <div class="module" style="flex: 0.7;">
                <div class="module-content">
                    <div class="diamond-container">
                        <div class="diamond" onclick="spinDiamond(this, 0)"></div>
                    </div>
                    <div class="label" style="margin-top: 12px;">tumble me</div>
                </div>
            </div>
        </div>
        
        <div class="module">
            <div class="module-content">
                <div style="display: flex; align-items: center; gap: 15px;">
                    <div class="shapes-area" id="shapesArea">
                        <div class="shape square" id="square0"></div>
                    </div>
                    <div style="display: flex; flex-direction: column; gap: 10px;">
                        <button class="btn" onclick="addSquare()">+</button>
                        <button class="btn" onclick="removeSquare()">-</button>
                        <button class="btn" onclick="toggleBouncing()">○</button>
                    </div>
                </div>
                <div class="label">wubba me</div>
            </div>
        </div>
    </div>

    <script>
        let ballPos = 190;
        let ballVel = 0;
        let ballInterval = null;
        let waveFreq = 5;
        let waveAmp = 15;
        let waveSpeed = 2;
        let waveColor = '#00ff41';
        let squares = [{x: 130, y: 40, vx: 3, vy: 2}];
        let nextSquareId = 1;
        let bouncing = false;
        let colors = ['#2196f3', '#e91e63', '#4caf50', '#ff9800', '#9c27b0'];
        let diamondColors = [0];

        function showLoadingDemo() {
            const loadingScreen = document.getElementById('loadingScreen');
            loadingScreen.style.display = 'flex';
            setTimeout(() => {
                loadingScreen.style.display = 'none';
            }, 3000);
        }

        function handleSliderClick(e) {
            const slider = e.currentTarget;
            const rect = slider.getBoundingClientRect();
            const y = e.clientY - rect.top;
            const percentage = Math.max(0, Math.min(100, ((60 - y) / 60) * 100));
            
            updateSliderPosition(percentage);
            moveBall(percentage);
        }

        function updateSliderPosition(percentage) {
            const thumb = document.getElementById('sliderThumb');
            const topPosition = 100 - percentage;
            thumb.style.top = topPosition + '%';
        }

        function moveBall(value) {
            ballPos = 12 + (value / 100) * 314;
            document.getElementById('ball').style.left = ballPos + 'px';
        }

        function updateBallSlider() {
            const percentage = ((ballPos - 12) / 314) * 100;
            updateSliderPosition(percentage);
        }

        // Make slider draggable
        let isDraggingSlider = false;
        document.getElementById('customSlider').addEventListener('mousedown', function(e) {
            isDraggingSlider = true;
            handleSliderClick(e);
        });

        document.addEventListener('mousemove', function(e) {
            if (isDraggingSlider) {
                const slider = document.getElementById('customSlider');
                const rect = slider.getBoundingClientRect();
                const y = e.clientY - rect.top;
                const percentage = Math.max(0, Math.min(100, ((60 - y) / 60) * 100));
                
                updateSliderPosition(percentage);
                moveBall(percentage);
            }
        });

        document.addEventListener('mouseup', function() {
            isDraggingSlider = false;
        });

        function clickBallTrack(e) {
            const rect = e.currentTarget.getBoundingClientRect();
            const targetPos = Math.max(12, Math.min(326, e.clientX - rect.left - 12));
            ballVel = (targetPos - ballPos) * 0.4;
            
            if (!ballInterval) {
                ballInterval = setInterval(() => {
                    if (Math.abs(ballVel) < 0.5) {
                        clearInterval(ballInterval);
                        ballInterval = null;
                        ballVel = 0;
                        return;
                    }
                    
                    ballPos += ballVel;
                    ballPos = Math.max(12, Math.min(326, ballPos));
                    
                    if (ballPos <= 12 || ballPos >= 326) {
                        ballVel *= -0.7;
                    }
                    
                    ballVel *= 0.95;
                    document.getElementById('ball').style.left = ballPos + 'px';
                    updateBallSlider();
                }, 16);
            }
        }

        function drawWaves() {
            const canvas = document.getElementById('waveCanvas');
            const ctx = canvas.getContext('2d');
            const time = Date.now() * 0.01 * waveSpeed;
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.strokeStyle = waveColor;
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            for (let x = 0; x < canvas.width; x++) {
                const y = canvas.height/2 + Math.sin((x * 0.02 * waveFreq) + time) * waveAmp;
                if (x === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            ctx.stroke();
            requestAnimationFrame(drawWaves);
        }

        function adjustWaves(change) {
            waveFreq = Math.max(1, Math.min(15, waveFreq + change));
            waveAmp = Math.max(5, Math.min(25, waveAmp + change * 3));
        }

        function updateWaveSpeed(value) {
            waveSpeed = value / 2;
            const colors = ['#ff0000', '#ff8800', '#ffff00', '#88ff00', '#00ff00', '#00ff88', '#00ffff', '#0088ff', '#0000ff', '#8800ff'];
            waveColor = colors[Math.floor(value) - 1] || '#00ff00';
        }

        function ripple(e) {
            const rect = e.currentTarget.getBoundingClientRect();
            const ripple = document.createElement('div');
            ripple.style.cssText = `
                position: absolute;
                left: ${e.clientX - rect.left}px;
                top: 50%;
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

        function throwTriangle(e) {
            const container = e.currentTarget;
            const triangle = document.getElementById('triangle');
            const rect = container.getBoundingClientRect();
            const x = e.clientX - rect.left;
            const y = e.clientY - rect.top;
            
            triangle.style.transform = `translate(${x - container.offsetWidth/2}px, ${y - container.offsetHeight/2}px) scale(1.5)`;
            
            setTimeout(() => {
                triangle.style.transform = 'translate(-50%, -50%) scale(1)';
            }, 600);
        }

        function addSquare() {
            const container = document.getElementById('shapesArea');
            const square = document.createElement('div');
            square.className = 'shape square';
            square.id = 'square' + nextSquareId;
            
            const x = Math.random() * 260;
            const y = Math.random() * 80;
            square.style.left = x + 'px';
            square.style.top = y + 'px';
            
            container.appendChild(square);
            squares.push({x, y, vx: (Math.random() - 0.5) * 8, vy: (Math.random() - 0.5) * 8});
            nextSquareId++;
            
            makeDraggable(square, squares.length - 1);
        }

        function removeSquare() {
            if (squares.length <= 1) return;
            
            squares.pop();
            const lastSquare = document.getElementById('square' + (nextSquareId - 1));
            if (lastSquare) lastSquare.remove();
            nextSquareId--;
        }

        function toggleBouncing() {
            bouncing = !bouncing;
            
            if (bouncing) {
                squares.forEach(sq => {
                    if (sq.vx === 0 && sq.vy === 0) {
                        sq.vx = (Math.random() - 0.5) * 6;
                        sq.vy = (Math.random() - 0.5) * 6;
                    }
                });
                
                const container = document.getElementById('shapesArea');
                
                function animate() {
                    if (!bouncing) return;
                    
                    squares.forEach((sq, i) => {
                        const element = document.getElementById('square' + i);
                        if (!element) return;
                        
                        sq.x += sq.vx;
                        sq.y += sq.vy;
                        
                        if (sq.x <= 0 || sq.x >= container.offsetWidth - 40) {
                            sq.vx = -sq.vx;
                            sq.x = Math.max(0, Math.min(container.offsetWidth - 40, sq.x));
                        }
                        
                        if (sq.y <= 0 || sq.y >= container.offsetHeight - 40) {
                            sq.vy = -sq.vy;
                            sq.y = Math.max(0, Math.min(container.offsetHeight - 40, sq.y));
                        }
                        
                        element.style.left = sq.x + 'px';
                        element.style.top = sq.y + 'px';
                        element.style.transition = 'none';
                    });
                    
                    requestAnimationFrame(animate);
                }
                animate();
            } else {
                document.querySelectorAll('.square').forEach(el => {
                    el.style.transition = 'all 0.3s ease';
                });
            }
        }

        function spinDiamond(element, index) {
            element.classList.add('spinning');
            diamondColors[index] = (diamondColors[index] + 1) % colors.length;
            element.style.background = colors[diamondColors[index]];
            
            setTimeout(() => {
                element.classList.remove('spinning');
            }, 600);
        }

        function makeDraggable(element, index) {
            let isDragging = false;
            
            element.addEventListener('mousedown', (e) => {
                if (bouncing) return;
                isDragging = true;
                
                const moveHandler = (e) => {
                    if (!isDragging) return;
                    const container = element.parentNode;
                    const rect = container.getBoundingClientRect();
                    const x = Math.max(0, Math.min(container.offsetWidth - 28, e.clientX - rect.left - 14));
                    const y = Math.max(0, Math.min(container.offsetHeight - 28, e.clientY - rect.top - 14));
                    
                    element.style.left = x + 'px';
                    element.style.top = y + 'px';
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

        // Initialize loading screen and page
        document.addEventListener('DOMContentLoaded', function() {
            // Ensure loading screen is visible on page load
            const loadingScreen = document.getElementById('loadingScreen');
            loadingScreen.style.display = 'flex';
            
            // Hide loading screen after 3 seconds
            setTimeout(() => {
                loadingScreen.style.display = 'none';
            }, 3000);
            
            // Initialize other components
            drawWaves();
            makeDraggable(document.getElementById('square0'), 0);
        });

        const style = document.createElement('style');
        style.textContent = `
            @keyframes ripple {
                0% { width: 4px; height: 4px; opacity: 1; }
                100% { width: 40px; height: 40px; opacity: 0; }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
