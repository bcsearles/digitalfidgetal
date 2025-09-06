<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>8-Bit Fidgetal Arcade</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&display=swap');
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            image-rendering: pixelated;
            image-rendering: -moz-crisp-edges;
            image-rendering: crisp-edges;
        }

        body {
            font-family: 'Orbitron', monospace;
            background: 
                repeating-linear-gradient(
                    0deg,
                    #1a1a2e 0px,
                    #1a1a2e 2px,
                    #16213e 2px,
                    #16213e 4px
                ),
                linear-gradient(135deg, #0f3460, #533483);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #00ff41;
            overflow-x: hidden;
        }

        .fidget-container {
            background: 
                linear-gradient(45deg, #000000 25%, transparent 25%),
                linear-gradient(-45deg, #000000 25%, transparent 25%),
                linear-gradient(45deg, transparent 75%, #000000 75%),
                linear-gradient(-45deg, transparent 75%, #000000 75%),
                #1a1a2e;
            background-size: 8px 8px;
            background-position: 0 0, 0 4px, 4px -4px, -4px 0px;
            border: 4px solid #00ff41;
            border-radius: 0;
            padding: 30px;
            max-width: 900px;
            width: 100%;
            box-shadow: 
                0 0 20px #00ff41,
                inset 0 0 20px rgba(0, 255, 65, 0.1);
            position: relative;
        }

        .fidget-container::before {
            content: '';
            position: absolute;
            top: -2px;
            left: -2px;
            right: -2px;
            bottom: -2px;
            background: linear-gradient(45deg, #ff0080, #00ff41, #0080ff, #ff0080);
            z-index: -1;
            border-radius: 0;
            animation: borderGlow 2s linear infinite;
        }

        @keyframes borderGlow {
            0% { background-position: 0% 0%; }
            100% { background-position: 100% 100%; }
        }

        .title {
            text-align: center;
            font-size: 28px;
            font-weight: 900;
            margin-bottom: 30px;
            color: #00ff41;
            text-shadow: 
                2px 2px 0px #008f11,
                4px 4px 0px #005c0b,
                0 0 20px #00ff41;
            letter-spacing: 4px;
            font-family: 'Orbitron', monospace;
            text-transform: uppercase;
            animation: textGlow 1.5s ease-in-out infinite alternate;
        }

        @keyframes textGlow {
            from { text-shadow: 2px 2px 0px #008f11, 4px 4px 0px #005c0b, 0 0 20px #00ff41; }
            to { text-shadow: 2px 2px 0px #008f11, 4px 4px 0px #005c0b, 0 0 30px #00ff41, 0 0 40px #00ff41; }
        }

        .fidget-module {
            background: 
                linear-gradient(45deg, #333333 25%, transparent 25%),
                linear-gradient(-45deg, #333333 25%, transparent 25%),
                linear-gradient(45deg, transparent 75%, #333333 75%),
                linear-gradient(-45deg, transparent 75%, #333333 75%),
                #1a1a2e;
            background-size: 4px 4px;
            background-position: 0 0, 0 2px, 2px -2px, -2px 0px;
            border: 3px solid #00ff41;
            border-radius: 0;
            margin: 20px 0;
            padding: 25px;
            position: relative;
            box-shadow: 
                0 0 15px rgba(0, 255, 65, 0.3),
                inset 0 0 15px rgba(0, 255, 65, 0.1);
            transition: all 0.3s ease;
            cursor: move;
        }

        .fidget-module:hover {
            box-shadow: 
                0 0 25px rgba(0, 255, 65, 0.5),
                inset 0 0 25px rgba(0, 255, 65, 0.2);
            transform: translateY(-3px);
        }

        .module-title {
            color: #00ff41;
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
            text-transform: uppercase;
            letter-spacing: 2px;
            text-shadow: 2px 2px 0px #008f11;
        }

        .controls {
            display: flex;
            gap: 12px;
            align-items: center;
            margin: 15px 0;
            flex-wrap: wrap;
        }

        .btn {
            background: 
                linear-gradient(45deg, #666 25%, transparent 25%),
                linear-gradient(-45deg, #666 25%, transparent 25%),
                linear-gradient(45deg, transparent 75%, #666 75%),
                linear-gradient(-45deg, transparent 75%, #666 75%),
                #00ff41;
            background-size: 4px 4px;
            background-position: 0 0, 0 2px, 2px -2px, -2px 0px;
            border: 2px solid #008f11;
            border-radius: 0;
            width: 45px;
            height: 45px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
            color: #000;
            user-select: none;
            text-shadow: 1px 1px 0px rgba(255,255,255,0.5);
            font-family: 'Orbitron', monospace;
        }

        .btn:hover {
            background: 
                linear-gradient(45deg, #999 25%, transparent 25%),
                linear-gradient(-45deg, #999 25%, transparent 25%),
                linear-gradient(45deg, transparent 75%, #999 75%),
                linear-gradient(-45deg, transparent 75%, #999 75%),
                #41ff00;
            box-shadow: 0 0 15px rgba(65, 255, 0, 0.5);
            transform: translateY(-2px);
        }

        .btn:active {
            transform: translateY(1px);
            box-shadow: 0 0 10px rgba(65, 255, 0, 0.3);
        }

        /* 8-bit Ball */
        .ball-container {
            width: 350px;
            height: 80px;
            border: 3px solid #00ff41;
            border-radius: 0;
            position: relative;
            background: 
                repeating-linear-gradient(
                    90deg,
                    #0d1421 0px,
                    #0d1421 2px,
                    #1a1a2e 2px,
                    #1a1a2e 4px
                );
            margin: 20px auto;
            overflow: hidden;
            box-shadow: inset 0 0 20px rgba(0, 255, 65, 0.2);
        }

        .ball {
            width: 40px;
            height: 40px;
            border-radius: 0;
            position: absolute;
            top: 20px;
            left: 155px;
            transition: all 0.3s ease;
            box-shadow: 
                0 0 10px currentColor,
                inset -5px -5px 0px rgba(0,0,0,0.3);
            background: 
                linear-gradient(135deg, #ff0080 0%, #ff0080 25%, #ff4080 25%, #ff4080 50%, #ff0080 50%, #ff0080 75%, #ff4080 75%);
            background-size: 8px 8px;
            border: 2px solid #000;
        }

        .ball::before {
            content: '';
            position: absolute;
            top: 5px;
            left: 5px;
            width: 8px;
            height: 8px;
            background: rgba(255,255,255,0.8);
            border-radius: 0;
        }

        /* 8-bit Sliders */
        .custom-slider {
            width: 250px;
            height: 12px;
            background: 
                repeating-linear-gradient(
                    90deg,
                    #333 0px,
                    #333 4px,
                    #555 4px,
                    #555 8px
                );
            border: 2px solid #00ff41;
            border-radius: 0;
            margin: 15px auto;
            display: block;
            appearance: none;
            cursor: pointer;
            outline: none;
        }

        .custom-slider::-webkit-slider-thumb {
            appearance: none;
            width: 24px;
            height: 24px;
            background: 
                linear-gradient(135deg, #00ff41 0%, #00ff41 25%, #41ff00 25%, #41ff00 50%, #00ff41 50%, #00ff41 75%, #41ff00 75%);
            background-size: 4px 4px;
            border: 2px solid #008f11;
            border-radius: 0;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
        }

        .custom-slider::-moz-range-thumb {
            width: 24px;
            height: 24px;
            background: 
                linear-gradient(135deg, #00ff41 0%, #00ff41 25%, #41ff00 25%, #41ff00 50%, #00ff41 50%, #00ff41 75%, #41ff00 75%);
            background-size: 4px 4px;
            border: 2px solid #008f11;
            border-radius: 0;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 255, 65, 0.5);
        }

        /* 8-bit Wave Container */
        .wave-container {
            width: 320px;
            height: 100px;
            background: #000;
            border: 3px solid #00ff41;
            border-radius: 0;
            margin: 20px auto;
            position: relative;
            overflow: hidden;
            box-shadow: 
                0 0 15px rgba(0, 255, 65, 0.3),
                inset 0 0 15px rgba(0, 255, 65, 0.1);
        }

        .wave-canvas {
            width: 100%;
            height: 100%;
            border-radius: 0;
        }

        /* 8-bit Hand Container */
        .hand-container {
            width: 250px;
            height: 120px;
            border: 3px solid #00ff41;
            border-radius: 0;
            position: relative;
            margin: 20px auto;
            background: 
                repeating-linear-gradient(
                    45deg,
                    #1a1a2e 0px,
                    #1a1a2e 4px,
                    #2a2a3e 4px,
                    #2a2a3e 8px
                );
            cursor: crosshair;
            overflow: visible;
            box-shadow: inset 0 0 15px rgba(0, 255, 65, 0.2);
        }

        .stretchy-hand {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            transition: all 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            cursor: grab;
            font-size: 35px;
            filter: drop-shadow(2px 2px 0px #000);
            user-select: none;
        }

        /* 8-bit Bubbles */
        .bubble-container {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 8px;
            max-width: 300px;
            margin: 20px auto;
        }

        .bubble {
            width: 35px;
            height: 35px;
            border-radius: 0;
            background: 
                linear-gradient(135deg, #00ffff 0%, #00ffff 25%, #80ffff 25%, #80ffff 50%, #00ffff 50%, #00ffff 75%, #80ffff 75%);
            background-size: 4px 4px;
            border: 2px solid #008080;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
        }

        .bubble::before {
            content: '';
            position: absolute;
            top: 4px;
            left: 4px;
            width: 6px;
            height: 6px;
            background: rgba(255,255,255,0.8);
            border-radius: 0;
        }

        .bubble:hover {
            transform: scale(1.1);
            box-shadow: 0 0 10px rgba(0, 255, 255, 0.5);
        }

        .bubble.popped {
            transform: scale(0);
            opacity: 0;
        }

        /* 8-bit Shapes */
        .shapes-container {
            display: flex;
            justify-content: center;
            gap: 40px;
            margin: 20px 0;
            align-items: center;
        }

        .draggable-shape {
            width: 70px;
            height: 70px;
            cursor: move;
            transition: all 0.3s ease;
            position: relative;
            filter: drop-shadow(3px 3px 0px #000);
            user-select: none;
        }

        .draggable-shape:hover {
            transform: scale(1.1);
            filter: drop-shadow(5px 5px 0px #000);
        }

        .draggable-circle {
            border-radius: 0;
            background: 
                linear-gradient(135deg, #ff0080 0%, #ff0080 25%, #ff4080 25%, #ff4080 50%, #ff0080 50%, #ff0080 75%, #ff4080 75%);
            background-size: 8px 8px;
            border: 3px solid #800040;
        }

        .draggable-square {
            transform: rotate(45deg);
            background: 
                linear-gradient(135deg, #0080ff 0%, #0080ff 25%, #4080ff 25%, #4080ff 50%, #0080ff 50%, #0080ff 75%, #4080ff 75%);
            background-size: 8px 8px;
            border: 3px solid #004080;
        }

        /* 8-bit Spinners */
        .spinner-container {
            display: flex;
            justify-content: center;
            gap: 50px;
            margin: 30px 0;
            align-items: center;
        }

        .fidget-spinner {
            width: 90px;
            height: 90px;
            position: relative;
            cursor: pointer;
            transition: transform 0.1s;
            filter: drop-shadow(4px 4px 0px #000);
        }

        .spinner-center {
            width: 24px;
            height: 24px;
            background: 
                linear-gradient(135deg, #333 0%, #333 25%, #666 25%, #666 50%, #333 50%, #333 75%, #666 75%);
            background-size: 4px 4px;
            border-radius: 0;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 2;
            border: 2px solid #000;
        }

        .spinner-blade {
            width: 28px;
            height: 28px;
            border-radius: 0;
            position: absolute;
            border: 2px solid #000;
        }

        .blade1 { top: 5px; left: 50%; transform: translateX(-50%); }
        .blade2 { bottom: 5px; left: 8px; }
        .blade3 { bottom: 5px; right: 8px; }

        .spinning {
            animation: spin8bit 1s linear infinite;
        }

        @keyframes spin8bit {
            0% { transform: rotate(0deg); }
            25% { transform: rotate(90deg); }
            50% { transform: rotate(180deg); }
            75% { transform: rotate(270deg); }
            100% { transform: rotate(360deg); }
        }

        /* 8-bit Stress Ball */
        .stress-ball {
            width: 100px;
            height: 100px;
            border-radius: 0;
            background: 
                linear-gradient(135deg, #ff4080 0%, #ff4080 25%, #ff8080 25%, #ff8080 50%, #ff4080 50%, #ff4080 75%, #ff8080 75%);
            background-size: 8px 8px;
            border: 3px solid #800040;
            margin: 20px auto;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            user-select: none;
            filter: drop-shadow(4px 4px 0px #000);
        }

        .stress-ball:active {
            transform: scale(0.9);
            filter: drop-shadow(2px 2px 0px #000);
        }

        .stress-ball::before {
            content: '';
            position: absolute;
            top: 15px;
            left: 15px;
            width: 12px;
            height: 12px;
            background: rgba(255,255,255,0.6);
            border-radius: 0;
        }

        /* 8-bit Particle Container */
        .particle-container {
            width: 300px;
            height: 150px;
            border: 3px solid #00ff41;
            border-radius: 0;
            position: relative;
            margin: 20px auto;
            background: 
                repeating-linear-gradient(
                    0deg,
                    #000 0px,
                    #000 2px,
                    #111 2px,
                    #111 4px
                );
            overflow: hidden;
            cursor: crosshair;
            box-shadow: inset 0 0 20px rgba(0, 255, 65, 0.2);
        }

        .particle {
            position: absolute;
            border-radius: 0;
            pointer-events: none;
            animation: particle8bit 1.5s ease-out forwards;
            width: 8px !important;
            height: 8px !important;
            border: 1px solid rgba(255,255,255,0.5);
        }

        @keyframes particle8bit {
            0% {
                opacity: 1;
                transform: scale(1) translateY(0);
            }
            50% {
                opacity: 0.8;
                transform: scale(1.5) translateY(-20px);
            }
            100% {
                opacity: 0;
                transform: scale(0.5) translateY(-40px);
            }
        }

        /* 8-bit Sound Visualizer */
        .sound-container {
            display: flex;
            justify-content: center;
            align-items: end;
            gap: 2px;
            height: 80px;
            margin: 20px auto;
            width: 200px;
            padding: 5px;
            background: 
                repeating-linear-gradient(
                    90deg,
                    #000 0px,
                    #000 2px,
                    #111 2px,
                    #111 4px
                );
            border: 2px solid #00ff41;
        }

        .sound-bar {
            width: 8px;
            background: 
                linear-gradient(to top, 
                    #ff0080 0%, 
                    #ff0080 33%, 
                    #ffff00 33%, 
                    #ffff00 66%, 
                    #00ff41 66%, 
                    #00ff41 100%);
            border-radius: 0;
            transition: height 0.1s ease;
            height: 8px;
            border: 1px solid #000;
            border-bottom: none;
        }

        .description {
            color: #00ff41;
            font-size: 12px;
            margin-top: 10px;
            text-align: center;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-weight: 700;
            text-shadow: 1px 1px 0px #008f11;
        }

        .drag-hint {
            position: absolute;
            top: 8px;
            right: 12px;
            font-size: 10px;
            color: #00ff41;
            background: 
                linear-gradient(45deg, #000 25%, transparent 25%),
                linear-gradient(-45deg, #000 25%, transparent 25%),
                linear-gradient(45deg, transparent 75%, #000 75%),
                linear-gradient(-45deg, transparent 75%, #000 75%),
                #1a1a2e;
            background-size: 4px 4px;
            background-position: 0 0, 0 2px, 2px -2px, -2px 0px;
            padding: 4px 8px;
            border: 1px solid #008f11;
            border-radius: 0;
            text-transform: uppercase;
            font-weight: 700;
            letter-spacing: 1px;
        }

        /* 8-bit animations */
        @keyframes pulse8bit {
            0%, 100% { transform: scale(1); background-size: 8px 8px; }
            50% { transform: scale(1.2); background-size: 12px 12px; }
        }

        @keyframes glitch {
            0% { transform: translateX(0); }
            10% { transform: translateX(-2px); }
            20% { transform: translateX(2px); }
            30% { transform: translateX(-2px); }
            40% { transform: translateX(2px); }
            50% { transform: translateX(0); }
            100% { transform: translateX(0); }
        }

        /* Scanlines effect */
        .fidget-container::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                repeating-linear-gradient(
                    0deg,
                    transparent 0px,
                    transparent 2px,
                    rgba(0, 255, 65, 0.03) 2px,
                    rgba(0, 255, 65, 0.03) 4px
                );
            pointer-events: none;
            animation: scanlines 0.1s linear infinite;
        }

        @keyframes scanlines {
            0% { transform: translateY(0); }
            100% { transform: translateY(4px); }
        }

        /* Responsive 8-bit */
        @media (max-width: 768px) {
            .fidget-container {
                padding: 20px;
                margin: 10px;
            }
            
            .spinner-container {
                gap: 30px;
            }
            
            .shapes-container {
                gap: 20px;
            }
            
            .title {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="fidget-container">
        <div class="title">◤ 8-BIT FIDGETAL ARCADE ◥</div>
        
        <!-- Pixel Ball Balance -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">▲ PIXEL BALL BALANCE</div>
            <div class="controls">
                <button class="btn" onclick="changeBallColor()">■</button>
                <button class="btn" onclick="resetBall()">↻</button>
                <button class="btn" onclick="toggleBallSize()">▣</button>
            </div>
            <div class="ball-container">
                <div class="ball" id="ball"></div>
            </div>
            <input type="range" min="0" max="100" value="50" class="custom-slider" id="tiltSlider" oninput="adjustTilt(this.value)">
            <div class="description">◆ DRAG SLIDER TO CONTROL PIXEL BALL ◆</div>
        </div>

        <!-- Retro Particle System -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">✚ RETRO PARTICLE BLASTER</div>
            <div class="controls">
                <button class="btn" onclick="changeParticleMode()">✦</button>
                <button class="btn" onclick="clearParticles()">◊</button>
                <button class="btn" onclick="explodeParticles()">✸</button>
            </div>
            <div class="particle-container" id="particleContainer"></div>
            <div class="description">◆ CLICK TO SPAWN PIXEL PARTICLES ◆</div>
        </div>

        <!-- 8-bit Wave Generator -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">≋ RETRO WAVE SYNTHESIZER</div>
            <div class="controls">
                <button class="btn" onclick="toggleWaveType()">≈</button>
                <button class="btn" onclick="randomWave()">◉</button>
                <button class="btn" onclick="freezeWave()" id="freezeBtn">⏸</button>
            </div>
            <div class="wave-container">
                <canvas class="wave-canvas" id="waveCanvas" width="320" height="100"></canvas>
            </div>
            <input type="range" min="1" max="20" value="5" class="custom-slider" onchange="updateWaveSettings(this.value)">
            <div class="description">◆ CONTROL RETRO WAVEFORMS ◆</div>
        </div>

        <!-- Pixel Bubble Pop -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">◎ PIXEL BUBBLE POPPER</div>
            <div class="controls">
                <button class="btn" onclick="refillBubbles()">↺</button>
                <button class="btn" onclick="popAllBubbles()">✸</button>
                <button class="btn" onclick="changeBubbleColor()">▲</button>
            </div>
            <div class="bubble-container" id="bubbleContainer"></div>
            <div class="description">◆ POP THE PIXEL BUBBLES ◆</div>
        </div>

        <!-- 8-bit Hand -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">✋ RETRO STICKY HAND</div>
            <div class="controls">
                <button class="btn" onclick="changeHandColor()">♦</button>
                <button class="btn" onclick="changeHandSize()">▣</button>
                <button class="btn" onclick="autoThrow()">⚡</button>
            </div>
            <div class="hand-container" id="handContainer">
                <div class="stretchy-hand" id="stretchyHand">✋</div>
            </div>
            <div class="description">◆ CLICK TO LAUNCH PIXEL HAND ◆</div>
        </div>

        <!-- Pixel Stress Ball -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">● PIXEL STRESS CUBE</div>
            <div class="controls">
                <button class="btn" onclick="changeStressBallColor()">♦</button>
                <button class="btn" onclick="stressBallPulse()">♥</button>
                <button class="btn" onclick="resetStressBall()">↻</button>
            </div>
            <div class="stress-ball" id="stressBall"></div>
            <div class="description">◆ CLICK TO COMPRESS PIXEL CUBE ◆</div>
        </div>

        <!-- 8-bit Shapes -->
        <div class="fidget-module">
            <div class="drag-hint">◢◤ DRAG MODULE ◥◣</div>
            <div class="module-title">◆ RETRO GEOMETRY</div>
            <div class="controls">
                <button class="btn" onclick="morphShapes()">◊</button>
                <button class="btn" onclick="rainbowMode()">▲</button>
                <button class="btn" onclick="resetShapes()">↻</button>
            </div>
            <div class="shapes-container">
                <div class="draggable-shape draggable-circle" id="circle"></div>
