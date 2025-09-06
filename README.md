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

        .browser-bar {
            display: none;
        }

        .browser-dots {
            display: flex;
            gap: 6px;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #ddd;
        }

        .title {
            text-align: center;
            font-size: 16px;
            font-weight: bold;
            letter-spacing: 2px;
            color: #333;
            margin-bottom: 20px;
            padding: 0 20px;
            border-top: 2px dashed #333;
            border-bottom: 2px dashed #333;
            padding-top: 8px;
            padding-bottom: 8px;
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
        }

        .ball {
            width: 30px;
            height: 30px;
            background: #ff4444;
            border-radius: 50%;
            position: absolute;
            top: 15px;
            left: 125px;
            transition: all 0.3s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.2);
        }

        .tilt-controls {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 8px;
        }

        .tilt-arrows {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }

        .arrow {
            font-size: 24px;
            color: #666;
            cursor: pointer;
            user-select: none;
            transition: color 0.2s;
        }

        .arrow:hover {
            color: #333;
        }

        .triangle {
            width: 0;
            height: 0;
            border-left: 8px solid transparent;
            border-right: 8px solid transparent;
            border-bottom: 12px solid #999;
        }

        /* Wave Generator */
        .wave-container {
            width: 200px;
            height: 80px;
            background: #000;
            border-radius: 10px;
            position: relative;
            margin: 10px 0;
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
            width: 200px;
            height: 100px;
            background: #f8f8f8;
            border: 2px solid #ddd;
            border-radius: 15px;
            position: relative;
            cursor: pointer;
            overflow: visible;
            margin: 10px 0;
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

        .hand-trail {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 2px;
            background: #4CAF50;
            transform-origin: top;
            opacity: 0.6;
            border-radius: 1px;
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
            background: white;
            border: 3px solid #333;
            border-radius: 50%;
            top: 25px;
            left: 50px;
        }

        .square {
            width: 35px;
            height: 35px;
            background: white;
            border: 3px solid #333;
            transform: rotate(45deg);
            top: 32px;
            left: 150px;
        }

        .color-slider {
            width: 200px;
            margin: 10px 0;
        }

        .color-dot {
            width: 30px;
            height: 30px;
            background: #8B5CF6;
            border-radius: 50%;
            position: absolute;
            right: 40px;
            top: 50%;
            transform: translateY(-50%);
            border: 2px solid #333;
        }

        /* Fidget Spinners */
        .spinners-container {
            display: flex;
            gap: 30px;
            justify-content: center;
            margin: 10px 0;
        }

        .fidget-spinner {
            width: 70px;
            height: 70px;
            position: relative;
            cursor: pointer;
        }

        .spinner-center {
            width: 20px;
            height: 20px;
            background: #333;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 2;
            border: 2px solid white;
        }

        .spinner-blade {
            width: 25px;
            height: 25px;
            background: #4A90E2;
            border: 3px solid #333;
            border-radius: 50%;
            position: absolute;
        }

        .blade1 { 
            top: 2px; 
            left: 50%; 
            transform: translateX(-50%); 
        }
        .blade2 { 
            bottom: 2px; 
            left: 9px; 
        }
        .blade3 { 
            bottom: 2px; 
            right: 9px; 
        }

        .spinning .fidget-spinner {
            animation: spin 2s linear infinite;
        }

        @keyframes spin {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        .spinner-controls {
            display: flex;
            justify-content: center;
            margin-top: 15px;
            gap: 10px;
        }

        /* Info Panel */
        .info-panel {
            background: #2E86AB;
            color: white;
            padding: 20px;
            border-radius: 10px;
            width: 300px;
            font-size: 14px;
            line-height: 1.6;
        }

        .info-section {
            margin-bottom: 15px;
            padding: 10px;
            background: rgba(255,255,255,0.1);
            border-radius: 8px;
        }

        .bonus-note {
            background: #1B4F72;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 20px;
            position: relative;
        }

        .bonus-note::before {
            content: '*';
            font-size: 20px;
            font-weight: bold;
            color: #F39C12;
        }

        .arrow-indicator {
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 40px;
            color: #333;
        }

        /* Dragging states */
        .dragging {
            opacity: 0.7;
            transform: rotate(5deg);
            z-index: 1000;
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
            
            .info-panel {
                width: 100%;
                max-width: 400px;
            }
        }
    </style>
</head>
<body>
    <div class="main-container">
        <!-- Main Fidget Device -->
        <div class="fidget-device">
            <div class="browser-bar">
                <div class="browser-dots">
                    <div class="dot"></div>
                    <div class="dot"></div>
                    <div class="dot"></div>
                </div>
            </div>
            
            <div class="title">DIGITAL FIDGETAL</div>
            
            <!-- Ball Balance Module -->
            <div class="module">
                <div class="module-content">
                    <div class="controls">
                        <button class="btn" onclick="changeBallColor()">+</button>
                        <button class="btn" onclick="changeBallColor(true)">-</button>
                    </div>
                    
                    <div class="ball-track">
                        <div class="ball" id="ball"></div>
                    </div>
                    
                    <div class="tilt-controls">
                        <div class="arrow" onclick="tiltBall(-10)">↑</div>
                        <div class="triangle"></div>
                        <div class="arrow" onclick="tiltBall(10)">↓</div>
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
                        <canvas class="wave-canvas" id="waveCanvas" width="200" height="80"></canvas>
                    </div>
                    
                    <div class="slider-container">
                        <input type="range" min="1" max="10" value="5" class="custom-slider" 
                               onchange="updateWaveSettings(this.value)">
                    </div>
                </div>
            </div>
            
            <!-- Stretchy Hand Module -->
            <div class="module">
                <div class="module-content">
                    <div class="controls">
                        <button class="btn" onclick="changeHandColor()">+</button>
                        <button class="btn" onclick="changeHandColor(true)">-</button>
                    </div>
                    
                    <div class="hand-container" onclick="throwHand(event)">
                        <div class="stretchy-hand" id="stretchyHand">🖐️</div>
                    </div>
                </div>
            </div>
            
            <!-- Shapes Module -->
            <div class="module">
                <div class="module-content">
                    <div class="controls">
                        <button class="btn" onclick="changeShapeColor()">+</button>
                        <button class="btn" onclick="changeShapeColor(true)">-</button>
                    </div>
                    
                    <div class="shapes-area">
                        <div class="shape circle" id="circle"></div>
                        <div class="shape square" id="square"></div>
                        <div class="color-dot" id="colorDot"></div>
                    </div>
                    
                    <input type="range" min="0" max="360" value="180" class="color-slider" 
                           onchange="updateShapeColors(this.value)">
                </div>
            </div>
            
            <!-- Fidget Spinner Module -->
            <div class="module">
                <div class="module-content">
                    <div class="spinner-controls">
                        <button class="btn" onclick="changeSpinnerColor()">+</button>
                        <button class="btn" onclick="changeSpinnerColor(true)">-</button>
                        <button class="btn" onclick="changeSpinnerColor()">+</button>
                    </div>
                    
                    <div class="spinners-container">
                        <div class="fidget-spinner" onclick="spinSpinner(this)">
                            <div class="spinner-center"></div>
                            <div class="spinner-blade blade1"></div>
                            <div class="spinner-blade blade2"></div>
                            <div class="spinner-blade blade3"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // State management
        let state = {
            ballColors: ['#ff4444', '#44ff44', '#4444ff', '#ffff44', '#ff44ff', '#44ffff'],
            ballColorIndex: 0,
            ballPosition: 125,
            handColors: ['🖐️', '✋', '👋', '🤚', '✊', '👊', '🙌', '👐'],
            handColorIndex: 0,
            waveSettings: { frequency: 5, amplitude: 20, speed: 2, color: '#00ff41' },
            shapeColors: ['#ffeb3b', '#e91e63', '#2196f3', '#4caf50', '#ff9800', '#9c27b0'],
            shapeColorIndex: 0,
            spinnerColors: [['#4A90E2', '#4A90E2'], ['#E74C3C', '#E74C3C'], ['#2ECC71', '#2ECC71'], ['#F39C12', '#F39C12']],
            spinnerColorIndex: 0
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

        function tiltBall(direction) {
            state.ballPosition = Math.max(15, Math.min(355, state.ballPosition + direction));
            document.getElementById('ball').style.left = state.ballPosition + 'px';
        }

        // Wave functions
        function drawWaves() {
            const canvas = document.getElementById('waveCanvas');
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
        function changeHandColor(reverse = false) {
            if (reverse) {
                state.handColorIndex = (state.handColorIndex - 1 + state.handColors.length) % state.handColors.length;
            } else {
                state.handColorIndex = (state.handColorIndex + 1) % state.handColors.length;
            }
            document.getElementById('stretchyHand').textContent = state.handColors[state.handColorIndex];
        }

        function throwHand(event) {
            const container = event.currentTarget;
            const hand = document.getElementById('stretchyHand');
            const rect = container.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;
            
            // Create trail effect
            const trail = document.createElement('div');
            trail.className = 'hand-trail';
            trail.style.left = '50%';
            trail.style.transform = `translate(-50%, -50%) rotate(${Math.atan2(y - 50, x - 100) * 180 / Math.PI + 90}deg)`;
            trail.style.height = Math.sqrt((x - 100) ** 2 + (y - 50) ** 2) + 'px';
            container.appendChild(trail);
            
            hand.style.transform = `translate(${x - 100}px, ${y - 50}px) scale(1.5)`;
            
            setTimeout(() => {
                hand.style.transform = 'translate(-50%, -50%) scale(1)';
                if (trail.parentNode) trail.remove();
            }, 600);
        }

        // Shape functions
        function changeShapeColor(reverse = false) {
            if (reverse) {
                state.shapeColorIndex = (state.shapeColorIndex - 1 + state.shapeColors.length) % state.shapeColors.length;
            } else {
                state.shapeColorIndex = (state.shapeColorIndex + 1) % state.shapeColors.length;
            }
            document.getElementById('circle').style.background = state.shapeColors[state.shapeColorIndex];
            document.getElementById('square').style.background = state.shapeColors[(state.shapeColorIndex + 1) % state.shapeColors.length];
        }

        function updateShapeColors(value) {
            const hue = value;
            document.getElementById('circle').style.background = `hsl(${hue}, 70%, 60%)`;
            document.getElementById('colorDot').style.background = `hsl(${hue}, 70%, 60%)`;
        }

        // Spinner functions
        function changeSpinnerColor(reverse = false) {
            if (reverse) {
                state.spinnerColorIndex = (state.spinnerColorIndex - 1 + state.spinnerColors.length) % state.spinnerColors.length;
            } else {
                state.spinnerColorIndex = (state.spinnerColorIndex + 1) % state.spinnerColors.length;
            }
            
            const colors = state.spinnerColors[state.spinnerColorIndex];
            document.querySelectorAll('.spinner-blade').forEach(blade => {
                blade.style.background = colors[0];
            });
        }

        function spinSpinner(spinner) {
            spinner.classList.add('spinning');
            setTimeout(() => {
                spinner.classList.remove('spinning');
            }, 2000);
        }

        // Shape dragging
        function makeShapesDraggable() {
            ['circle', 'square'].forEach(id => {
                const shape = document.getElementById(id);
                let isDragging = false;
                
                shape.addEventListener('mousedown', (e) => {
                    isDragging = true;
                    const startX = e.clientX - shape.offsetLeft;
                    const startY = e.clientY - shape.offsetTop;
                    
                    function moveShape(e) {
                        if (isDragging) {
                            const container = shape.parentNode;
                            const rect = container.getBoundingClientRect();
                            const x = Math.max(0, Math.min(container.offsetWidth - shape.offsetWidth, e.clientX - rect.left - startX));
                            const y = Math.max(0, Math.min(container.offsetHeight - shape.offsetHeight, e.clientY - rect.top - startY));
                            
                            shape.style.left = x + 'px';
                            shape.style.top = y + 'px';
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
                
                // Mouse wheel to resize
                shape.addEventListener('wheel', (e) => {
                    e.preventDefault();
                    const currentSize = parseInt(shape.style.width) || (id === 'circle' ? 50 : 35);
                    const delta = e.deltaY > 0 ? -5 : 5;
                    const newSize = Math.max(20, Math.min(80, currentSize + delta));
                    shape.style.width = newSize + 'px';
                    shape.style.height = newSize + 'px';
                });
            });
        }

        // Module dragging
        function makeModulesDraggable() {
            const modules = document.querySelectorAll('.module');
            modules.forEach(module => {
                let isDragging = false;
                
                module.addEventListener('dragstart', (e) => {
                    isDragging = true;
                    module.classList.add('dragging');
                    e.dataTransfer.effectAllowed = 'move';
                    e.dataTransfer.setData('text/html', module.outerHTML);
                });
                
                module.addEventListener('dragend', () => {
                    isDragging = false;
                    module.classList.remove('dragging');
                });
                
                module.addEventListener('dragover', (e) => {
                    e.preventDefault();
                    e.dataTransfer.dropEffect = 'move';
                });
                
                module.addEventListener('drop', (e) => {
                    e.preventDefault();
                    if (e.target !== module) {
                        const container = module.parentNode;
                        const allModules = [...container.querySelectorAll('.module')];
                        const draggedIndex = allModules.indexOf(document.querySelector('.dragging'));
                        const targetIndex = allModules.indexOf(module);
                        
                        if (draggedIndex > targetIndex) {
                            container.insertBefore(document.querySelector('.dragging'), module);
                        } else {
                            container.insertBefore(document.querySelector('.dragging'), module.nextSibling);
                        }
                    }
                });
            });
        }

        // Initialize everything
        function init() {
            // Start wave animation
            drawWaves();
            
            // Make shapes draggable
            makeShapesDraggable();
            
            // Add click feedback to all buttons
            document.querySelectorAll('.btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    btn.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        btn.style.transform = 'scale(1)';
                    }, 100);
                });
            });
            
            // Add interactive feedback to ball track
            document.querySelector('.ball-track').addEventListener('click', (e) => {
                const rect = e.currentTarget.getBoundingClientRect();
                const x = e.clientX - rect.left;
                const ballPosition = Math.max(15, Math.min(355, x - 15));
                state.ballPosition = ballPosition;
                document.getElementById('ball').style.left = ballPosition + 'px';
            });
            
            // Add wave canvas click interaction
            document.getElementById('waveCanvas').addEventListener('click', (e) => {
                const rect = e.currentTarget.getBoundingClientRect();
                const x = e.clientX - rect.left;
                // Create wave ripple effect at click point
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
                e.currentTarget.parentNode.appendChild(ripple);
                
                setTimeout(() => ripple.remove(), 1000);
            });
        }

        // Start when page loads
        window.addEventListener('load', init);
    </script>
</body>
</html>
