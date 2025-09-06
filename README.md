<!DOCTYPE html>
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
            font-family: 'Space Grotesk', sans-serif;
            background: #f0f0f0;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .main-container {
            display: flex;
            gap: 30px;
            align-items: flex-start;
            max-width: 1200px;
        }

        .fidget-device {
            background: white;
            border: 3px solid #333;
            border-radius: 25px;
            padding: 25px;
            width: 400px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .title {
            text-align: center;
            font-size: 26px;
            font-weight: bold;
            letter-spacing: 2px;
            color: #333;
            margin-bottom: 0px;
            padding: 15px 20px 8px 20px;
            background: white;
            border: 2px solid #000;
            border-radius: 10px 10px 0 0;
        }

        .subtitle {
            text-align: center;
            font-size: 12px;
            color: #666;
            margin-bottom: 20px;
            font-style: italic;
            padding: 2px 20px 15px 20px;
            background: white;
            border: 2px solid #000;
            border-top: none;
            border-radius: 0 0 10px 10px;
            margin-top: -2px;
        }

        .module {
            background: white;
            border: 2px solid #333;
            border-radius: 15px;
            margin: 15px 0;
            padding: 20px;
            position: relative;
        }

        .module-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }

        .controls {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .btn {
            background: white;
            border: 2px solid #333;
            border-radius: 8px;
            width: 40px;
            height: 40px;
            font-size: 20px;
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

        /* Ball Balance Module */
        .ball-track {
            width: 280px;
            height: 60px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 30px;
            position: relative;
            overflow: hidden;
            margin: 10px 0;
            cursor: pointer;
        }

        .ball {
            width: 30px;
            height: 30px;
            background: #2196f3;
            border: 2px solid #000;
            border-radius: 50%;
            position: absolute;
            top: 15px;
            left: 125px;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
            cursor: pointer;
        }

        .tilt-controls {
            display: flex;
            flex-direction: row;
            align-items: center;
            gap: 15px;
            justify-content: center;
        }

        /* Wave Generator */
        .wave-container {
            width: 200px;
            height: 80px;
            background: #000;
            border: 2px solid #000;
            border-radius: 10px;
            position: relative;
            margin: 10px 0;
            cursor: pointer;
        }

        .wave-canvas {
            width: 100%;
            height: 100%;
            border-radius: 10px;
        }

        .wave-controls {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .slider-container {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .custom-slider {
            width: 120px;
            height: 6px;
            background: #ddd;
            border-radius: 3px;
            appearance: none;
            cursor: pointer;
        }

        .custom-slider::-webkit-slider-thumb {
            appearance: none;
            width: 18px;
            height: 18px;
            background: white;
            border: 2px solid #333;
            border-radius: 50%;
            cursor: pointer;
        }

        /* Stretchy Hand */
        .hand-container {
            width: 100%;
            height: 100px;
            background: transparent;
            border: none;
            border-radius: 15px;
            position: relative;
            cursor: pointer;
            overflow: visible;
            margin: 10px 0;
        }

        .hand-container:hover {
            background: rgba(240, 240, 240, 0.3);
        }

        .stretchy-hand {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 40px;
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            cursor: grab;
        }

        /* Shapes Module */
        .shapes-area {
            width: 280px;
            height: 100px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 15px;
            position: relative;
            margin: 10px 0;
        }

        .shape {
            position: absolute;
            cursor: move;
            transition: all 0.3s ease;
            user-select: none;
        }

        .circle {
            width: 50px;
            height: 50px;
            background: #2196f3;
            border: 3px solid #333;
            border-radius: 8px;
            top: 25px;
            left: 50px;
        }

        /* Spinning Diamonds */
        .diamond-container {
            display: flex;
            justify-content: space-around;
            align-items: center;
            width: 280px;
            height: 90px;
            margin: 10px 0;
        }

        .diamond {
            width: 60px;
            height: 60px;
            background: #2196f3;
            border: 3px solid #333;
            transform: rotate(45deg);
            cursor: pointer;
            transition: all 0.3s ease;
            border-radius: 8px;
            flex-shrink: 0;
        }

        .diamond:hover {
            transform: rotate(45deg) scale(1.05);
        }

        .diamond.spinning {
            animation: diamondSpin 2s ease-in-out;
        }

        @keyframes diamondSpin {
            0% { transform: rotate(45deg); }
            25% { transform: rotate(135deg); }
            50% { transform: rotate(225deg); }
            75% { transform: rotate(315deg); }
            100% { transform: rotate(405deg); }
        }

        @keyframes ripple {
            0% {
                width: 4px;
                height: 4px;
                opacity: 1;
            }
            100% {
                width: 40px;
                height: 40px;
                opacity: 0;
            }
        }

        /* Responsive */
        @media (max-width: 768px) {
            .main-container {
                flex-direction: column;
                gap: 20px;
            }
            
            .fidget-device {
                width: 100%;
                max-width: 400px;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <div class="fidget-device">
            <div class="title">DIGITAL FIDGETAL</div>
            <div class="subtitle">the remedy for conference call restlessness</div>
            
            <!-- Ball Balance Module -->
            <div class="module">
                <div class="module-content">
                    <div class="ball-track">
                        <div class="ball" id="ball"></div>
                    </div>
                    
                    <div class="tilt-controls">
                        <input type="range" min="0" max="100" value="50" class="custom-slider" 
                               id="ballSlider" oninput="moveBallFromSlider(this.value)" style="width: 200px;">
                    </div>
                    
                    <div style="font-size: 12px; color: #666; text-align: center; margin-top: 10px;">
                        wibble me
                    </div>
                </div>
            </div>
            
            <!-- Wave Generator Module -->
            <div class="module">
                <div class="module-content">
                    <div class="wave-controls">
                        <button class="btn" onclick="adjustWaves(1)">+</button>
                        <button class="btn" onclick="adjustWaves(-1)">-</button>
                    </div>
                    
                    <div class="wave-container">
                        <canvas class="wave-canvas" id="waveCanvas" width="160" height="60"></canvas>
                    </div>
                    
                    <div class="slider-container">
                        <input type="range" min="1" max="10" value="5" class="custom-slider" 
                               onchange="updateWaveSettings(this.value)">
                    </div>
                    
                    <div style="font-size: 12px; color: #666; text-align: center; margin-top: 10px;">
                        tune me
                    </div>
                </div>
            </div>
            
            <!-- Stretchy Hand Module -->
            <div class="module">
                <div class="module-content">
                    <div class="hand-container" onclick="throwHand(event)">
                        <div class="stretchy-hand" id="stretchyHand">▲</div>
                    </div>
                    
                    <div style="font-size: 12px; color: #666; text-align: center; margin-top: 10px;">
                        dap me
                    </div>
                </div>
            </div>
            
            <!-- Shapes Module -->
            <div class="module">
                <div class="module-content">
                    <div class="controls">
                        <button class="btn" onclick="addCircle()">+</button>
                        <button class="btn" onclick="removeCircle()">-</button>
                        <button class="btn" onclick="toggleShapeBouncing()" style="width: 40px; height: 40px; font-size: 20px; display: flex; align-items: center; justify-content: center;">○</button>
                    </div>
                    
                    <div class="shapes-area">
                        <div class="shape circle" id="circle" style="background: #f44336;"></div>
                    </div>
                    
                    <div style="font-size: 12px; color: #666; text-align: center; margin-top: 10px;">
                        boing me
                    </div>
                </div>
            </div>

            <!-- Spinning Diamonds Module -->
            <div class="module">
                <div class="module-content">
                    <div class="diamond-container">
                        <div class="diamond" id="diamond1" onclick="spinDiamond(this)"></div>
                        <div class="diamond" id="diamond2" onclick="spinDiamond(this)"></div>
                        <div class="diamond" id="diamond3" onclick="spinDiamond(this)"></div>
                    </div>
                    
                    <div style="font-size: 12px; color: #666; text-align: center; margin-top: 10px;">
                        tumble me
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // State management
        let state = {
            ballColors: ['#f44336'], // Only red
            ballColorIndex: 0,
            ballPosition: 125,
            ballVelocity: 0,
            ballMomentum: null,
            handColors: ['▲'],
            handColorIndex: 0,
            waveSettings: { frequency: 5, amplitude: 20, speed: 2, color: '#00ff41' },
            shapeColors: ['#f44336'], // Only red
            shapeColorIndex: 0,
            circles: [{id: 'circle', x: 50, y: 25, vx: 0, vy: 0, size: 50}],
            nextCircleId: 1,
            shapeAnimation: { x: 150, y: 32, size: 35, isAnimating: false },
            diamondColors: ['#2196f3', '#e91e63', '#4caf50', '#ff9800', '#9c27b0'],
            diamondColorIndices: [0, 0, 0] // Track color state for each diamond
        };

        // Ball functions
        function changeBallColor(reverse = false) {
            if (reverse) {
                state.ballColorIndex = (state.ballColorIndex - 1 + state.ballColors.length) % state.ballColors.length;
            } else {
                state.ballColorIndex = (state.ballColorIndex + 1) % state.ballColors.length;
            }
            document.getElementById('ball').style.background = state.ballColors[state.ballColorIndex];
        }

        function updateSliderFromBall() {
            const slider = document.getElementById('ballSlider');
            if (slider) {
                const sliderValue = ((state.ballPosition - 15) / 220) * 100;
                slider.value = Math.max(0, Math.min(100, sliderValue));
            }
        }

        function moveBallFromSlider(sliderValue) {
            state.ballPosition = 15 + (sliderValue / 100) * 220;
            state.ballPosition = Math.max(15, Math.min(235, state.ballPosition));
            document.getElementById('ball').style.left = state.ballPosition + 'px';
        }

        function updateBallMomentum() {
            if (Math.abs(state.ballVelocity) < 0.5) {
                clearInterval(state.ballMomentum);
                state.ballMomentum = null;
                state.ballVelocity = 0;
                return;
            }
            
            state.ballPosition += state.ballVelocity;
            state.ballPosition = Math.max(15, Math.min(235, state.ballPosition));
            
            // Bounce off walls
            if (state.ballPosition <= 15 || state.ballPosition >= 235) {
                state.ballVelocity *= -0.7;
            }
            
            // Apply friction
            state.ballVelocity *= 0.95;
            
            document.getElementById('ball').style.left = state.ballPosition + 'px';
            updateSliderFromBall();
        }

        // Wave functions
        function drawWaves() {
            const canvas = document.getElementById('waveCanvas');
            if (!canvas) return;
            const ctx = canvas.getContext('2d');
            const time = Date.now() * 0.01 * state.waveSettings.speed;
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.strokeStyle = state.waveSettings.color;
            ctx.lineWidth = 2;
            ctx.beginPath();
            
            for (let x = 0; x < canvas.width; x++) {
                const y = canvas.height/2 + Math.sin((x * 0.02 * state.waveSettings.frequency) + time) * state.waveSettings.amplitude;
                if (x === 0) ctx.moveTo(x, y);
                else ctx.lineTo(x, y);
            }
            ctx.stroke();
            
            requestAnimationFrame(drawWaves);
        }

        function adjustWaves(change) {
            state.waveSettings.frequency = Math.max(1, Math.min(15, state.waveSettings.frequency + change));
            state.waveSettings.amplitude = Math.max(5, Math.min(35, state.waveSettings.amplitude + change * 3));
        }

        function updateWaveSettings(value) {
            state.waveSettings.speed = value / 2;
            const colors = ['#ff0000', '#ff8800', '#ffff00', '#88ff00', '#00ff00', '#00ff88', '#00ffff', '#0088ff', '#0000ff', '#8800ff'];
            state.waveSettings.color = colors[Math.floor(value) - 1] || '#00ff00';
        }

        // Hand functions
        function throwHand(event) {
            const container = event.currentTarget;
            const hand = document.getElementById('stretchyHand');
            const rect = container.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;
            
            hand.style.transform = `translate(${x - container.offsetWidth/2}px, ${y - container.offsetHeight/2}px) rotate(45deg) scale(1.5)`;
            
            setTimeout(() => {
                hand.style.transform = 'translate(-50%, -50%) rotate(45deg) scale(1)';
            }, 600);
        }

        // Shape functions
        function addCircle() {
            const container = document.querySelector('.shapes-area');
            const newCircle = document.createElement('div');
            const circleId = 'circle' + state.nextCircleId++;
            
            newCircle.className = 'shape circle';
            newCircle.id = circleId;
            newCircle.style.background = '#f44336'; // Always red
            
            // Random position within container bounds
            const x = Math.random() * (container.offsetWidth - 50);
            const y = Math.random() * (container.offsetHeight - 50);
            newCircle.style.left = x + 'px';
            newCircle.style.top = y + 'px';
            
            container.appendChild(newCircle);
            
            // Add to state
            state.circles.push({
                id: circleId,
                x: x,
                y: y,
                vx: (Math.random() - 0.5) * 8,
                vy: (Math.random() - 0.5) * 8,
                size: 50,
                color: '#f44336'
            });
            
            // Make it draggable
            makeCircleDraggable(newCircle);
        }

        function removeCircle() {
            if (state.circles.length <= 1) return; // Keep at least one circle
            
            const lastCircle = state.circles.pop();
            const element = document.getElementById(lastCircle.id);
            if (element) {
                element.remove();
            }
        }

        function toggleShapeBouncing() {
            const container = document.querySelector('.shapes-area');
            
            if (state.shapeAnimation.isAnimating) {
                state.shapeAnimation.isAnimating = false;
                // Reset transitions for all circles
                state.circles.forEach(circle => {
                    const element = document.getElementById(circle.id);
                    if (element) {
                        element.style.transition = 'all 0.3s ease';
                    }
                });
                return;
            }
            
            state.shapeAnimation.isAnimating = true;
            
            // Initialize velocities for all circles and remove transitions
            state.circles.forEach(circle => {
                const element = document.getElementById(circle.id);
                if (element) {
                    element.style.transition = 'none';
                    circle.x = parseInt(element.style.left) || circle.x;
                    circle.y = parseInt(element.style.top) || circle.y;
                    if (circle.vx === 0 && circle.vy === 0) {
                        circle.vx = (Math.random() - 0.5) * 8;
                        circle.vy = (Math.random() - 0.5) * 8;
                    }
                }
            });
            
            function bounceAll() {
                if (!state.shapeAnimation.isAnimating) return;
                
                const containerWidth = container.offsetWidth;
                const containerHeight = container.offsetHeight;
                
                state.circles.forEach(circle => {
                    const element = document.getElementById(circle.id);
                    if (!element) return;
                    
                    circle.x += circle.vx;
                    circle.y += circle.vy;
                    
                    // Bounce off walls
                    if (circle.x <= 0 || circle.x >= containerWidth - circle.size) {
                        circle.vx = -circle.vx;
                        circle.x = Math.max(0, Math.min(containerWidth - circle.size, circle.x));
                    }
                    
                    if (circle.y <= 0 || circle.y >= containerHeight - circle.size) {
                        circle.vy = -circle.vy;
                        circle.y = Math.max(0, Math.min(containerHeight - circle.size, circle.y));
                    }
                    
                    element.style.left = circle.x + 'px';
                    element.style.top = circle.y + 'px';
                });
                
                requestAnimationFrame(bounceAll);
            }
            
            bounceAll();
        }

        // Diamond functions
        function spinDiamond(diamondElement) {
            diamondElement.classList.add('spinning');
            
            // Get diamond index from ID (diamond1, diamond2, diamond3)
            const diamondIndex = parseInt(diamondElement.id.slice(-1)) - 1;
            
            // Change color for this specific diamond
            state.diamondColorIndices[diamondIndex] = (state.diamondColorIndices[diamondIndex] + 1) % state.diamondColors.length;
            
            setTimeout(() => {
                diamondElement.style.background = state.diamondColors[state.diamondColorIndices[diamondIndex]];
                diamondElement.classList.remove('spinning');
            }, 1000);
        }

        // Shape dragging
        function makeCircleDraggable(shape) {
            let isDragging = false;
            
            shape.addEventListener('mousedown', (e) => {
                if (state.shapeAnimation.isAnimating) return;
                
                isDragging = true;
                const shapeRect = shape.getBoundingClientRect();
                const startX = e.clientX - shapeRect.left - shape.offsetWidth/2;
                const startY = e.clientY - shapeRect.top - shape.offsetHeight/2;
                
                function moveShape(e) {
                    if (isDragging) {
                        const container = shape.parentNode;
                        const rect = container.getBoundingClientRect();
                        const x = Math.max(0, Math.min(container.offsetWidth - shape.offsetWidth, e.clientX - rect.left - startX));
                        const y = Math.max(0, Math.min(container.offsetHeight - shape.offsetHeight, e.clientY - rect.top - startY));
                        
                        shape.style.left = x + 'px';
                        shape.style.top = y + 'px';
                        
                        // Update state
                        const circleData = state.circles.find(c => c.id === shape.id);
                        if (circleData) {
                            circleData.x = x;
                            circleData.y = y;
                        }
                    }
                }
                
                function stopDragging() {
                    isDragging = false;
                    document.removeEventListener('mousemove', moveShape);
                    document.removeEventListener('mouseup', stopDragging);
                }
                
                document.addEventListener('mousemove', moveShape);
                document.addEventListener('mouseup', stopDragging);
            });
            
            shape.addEventListener('wheel', (e) => {
                e.preventDefault();
                const currentSize = parseInt(shape.style.width) || 50;
                const delta = e.deltaY > 0 ? -5 : 5;
                const newSize = Math.max(20, Math.min(80, currentSize + delta));
                shape.style.width = newSize + 'px';
                shape.style.height = newSize + 'px';
                
                // Update state
                const circleData = state.circles.find(c => c.id === shape.id);
                if (circleData) {
                    circleData.size = newSize;
                }
            });
        }

        function makeShapesDraggable() {
            // Make all existing circles draggable
            state.circles.forEach(circle => {
                const element = document.getElementById(circle.id);
                if (element) {
                    makeCircleDraggable(element);
                }
            });
        }

        // Initialize everything
        function init() {
            drawWaves();
            makeShapesDraggable();
            updateSliderFromBall();
            
            // Set initial colors
            const ball = document.getElementById('ball');
            if (ball) {
                ball.style.background = '#2196f3';
            }
            
            const initialCircle = document.getElementById('circle');
            if (initialCircle) {
                initialCircle.style.background = '#2196f3';
            }

            // Set initial diamond colors
            for (let i = 1; i <= 3; i++) {
                const diamond = document.getElementById(`diamond${i}`);
                if (diamond) {
                    diamond.style.background = state.diamondColors[state.diamondColorIndices[i-1]];
                }
            }
            
            document.querySelectorAll('.btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    btn.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        btn.style.transform = 'scale(1)';
                    }, 100);
                });
            });
            
            document.querySelector('.ball-track').addEventListener('click', (e) => {
                const rect = e.currentTarget.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const targetPosition = Math.max(15, Math.min(235, x - 15));
                
                const direction = targetPosition - state.ballPosition;
                state.ballVelocity = direction * 0.4;
                
                if (!state.ballMomentum) {
                    state.ballMomentum = setInterval(updateBallMomentum, 16);
                }
            });
            
            document.getElementById('waveCanvas').addEventListener('click', (e) => {
                const rect = e.currentTarget.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const ripple = document.createElement('div');
                ripple.style.position = 'absolute';
                ripple.style.left = x + 'px';
                ripple.style.top = '50%';
                ripple.style.width = '4px';
                ripple.style.height = '4px';
                ripple.style.background = state.waveSettings.color;
                ripple.style.borderRadius = '50%';
                ripple.style.transform = 'translate(-50%, -50%)';
                ripple.style.animation = 'ripple 1s ease-out forwards';
                ripple.style.pointerEvents = 'none';
                e.currentTarget.parentNode.appendChild(ripple);
                
                setTimeout(() => ripple.remove(), 1000);
            });
        }

        window.addEventListener('load', init);
    </script>
</body>
</html>
