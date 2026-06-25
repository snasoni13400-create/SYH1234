
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> 벽돌깨부수기 (Neon Brick Arcade)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Orbitron & Inter Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Tone.js for Retro Sound Effects -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tone/14.8.49/Tone.js"></script>

    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #03030c;
            background-image: 
                radial-gradient(at 50% 0%, rgba(31, 27, 85, 0.5) 0, transparent 50%),
                radial-gradient(at 0% 100%, rgba(14, 116, 144, 0.15) 0, transparent 50%),
                radial-gradient(at 100% 100%, rgba(168, 85, 247, 0.15) 0, transparent 50%);
            overflow-x: hidden;
        }
        .arcade-font {
            font-family: 'Orbitron', sans-serif;
        }
        .neon-glow {
            box-shadow: 0 0 15px rgba(168, 85, 247, 0.4);
        }
        .neon-border {
            border: 1px solid rgba(168, 85, 247, 0.3);
        }
        .neon-text-cyan {
            text-shadow: 0 0 10px rgba(6, 182, 212, 0.8);
        }
        .neon-text-pink {
            text-shadow: 0 0 10px rgba(236, 72, 153, 0.8);
        }
        .neon-text-purple {
            text-shadow: 0 0 10px rgba(168, 85, 247, 0.8);
        }
        canvas {
            image-rendering: pixelated;
        }
    </style>
</head>
<body class="min-h-screen text-slate-100 flex flex-col items-center justify-between p-4 md:p-6">

    <!-- Game Container -->
    <div class="w-full max-w-4xl flex flex-col gap-4 z-10">
        
        <!-- Header Panel with Scoreboard -->
        <header class="w-full bg-slate-950/70 backdrop-blur-md rounded-2xl p-4 flex flex-wrap justify-between items-center gap-4 neon-border shadow-2xl">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-purple-600 to-pink-500 flex items-center justify-center shadow-lg shadow-purple-500/30">
                    <i class="fa-solid fa-gamepad text-lg text-white animate-pulse"></i>
                </div>
                <div>
                    <h1 class="arcade-font text-xl font-black tracking-widest bg-gradient-to-r from-cyan-400 via-purple-400 to-pink-400 bg-clip-text text-transparent">
                        NEON BRICKS
                    </h1>
                    <p class="text-[10px] uppercase tracking-widest text-slate-400">Retro Pulse v2.0</p>
                </div>
            </div>

            <!-- Stats Bar -->
            <div class="flex items-center gap-6 text-sm">
                <!-- Score -->
                <div class="text-center">
                    <span class="block text-[10px] uppercase tracking-wider text-slate-400 font-semibold">SCORE</span>
                    <span id="score-val" class="arcade-font text-lg font-bold text-cyan-400 neon-text-cyan">00000</span>
                </div>
                <!-- High Score -->
                <div class="text-center hidden sm:block border-l border-slate-800 pl-6">
                    <span class="block text-[10px] uppercase tracking-wider text-slate-400 font-semibold">HIGH SCORE</span>
                    <span id="high-score-val" class="arcade-font text-lg font-bold text-purple-400 neon-text-purple">00000</span>
                </div>
                <!-- Level -->
                <div class="text-center border-l border-slate-800 pl-6">
                    <span class="block text-[10px] uppercase tracking-wider text-slate-400 font-semibold">LEVEL</span>
                    <span id="level-val" class="arcade-font text-lg font-bold text-pink-400 neon-text-pink">1 / 4</span>
                </div>
                <!-- Lives -->
                <div class="text-center border-l border-slate-800 pl-6">
                    <span class="block text-[10px] uppercase tracking-wider text-slate-400 font-semibold">LIVES</span>
                    <div id="lives-container" class="flex gap-1 mt-1 text-pink-500">
                        <i class="fa-solid fa-heart animate-bounce"></i>
                        <i class="fa-solid fa-heart animate-bounce" style="animation-delay: 0.1s"></i>
                        <i class="fa-solid fa-heart animate-bounce" style="animation-delay: 0.2s"></i>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Body: Screen Canvas + Left/Right Control Aids -->
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-4 items-stretch">
            
            <!-- Side Panel Left (Game Rules & Info) -->
            <div class="lg:col-span-1 bg-slate-950/50 backdrop-blur-md rounded-2xl p-4 neon-border flex flex-col justify-between gap-4 order-2 lg:order-1">
                <div>
                    <h3 class="arcade-font text-xs font-bold text-purple-400 tracking-wider mb-3 flex items-center gap-2">
                        <i class="fa-solid fa-circle-info"></i> 게임 조작법
                    </h3>
                    <ul class="text-xs space-y-2 text-slate-400">
                        <li class="flex items-start gap-2">
                            <span class="text-cyan-400 font-bold">PC:</span>
                            <span>마우스 좌우 이동 또는 <kbd class="px-1 bg-slate-800 rounded text-slate-200">←</kbd> <kbd class="px-1 bg-slate-800 rounded text-slate-200">→</kbd> 방향키 (or A / D 키)</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <span class="text-pink-400 font-bold">모바일:</span>
                            <span>화면 하단 터치 드래그로 슬라이드</span>
                        </li>
                        <li class="flex items-start gap-2">
                            <span class="text-purple-400 font-bold">일시정지:</span>
                            <span><kbd class="px-1 bg-slate-800 rounded text-slate-200">Space</kbd> 키 입력</span>
                        </li>
                    </ul>
                </div>

                <!-- Active Powerup Display -->
                <div class="border-t border-slate-800/80 pt-3">
                    <h3 class="arcade-font text-xs font-bold text-pink-400 tracking-wider mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-bolt"></i> 현재 파워업
                    </h3>
                    <div id="active-powerups-list" class="space-y-1.5">
                        <div class="text-[11px] text-slate-500 italic">적용된 특수 효과 없음</div>
                    </div>
                </div>

                <div class="text-[10px] text-slate-500 border-t border-slate-800/80 pt-3 text-center lg:text-left">
                    <p>© 2026 Neon Retro Systems.</p>
                    <p>Powered by Tone.js & Canvas.</p>
                </div>
            </div>

            <!-- Center Canvas Area -->
            <div class="lg:col-span-3 relative bg-slate-950 rounded-2xl overflow-hidden neon-border shadow-2xl flex flex-col order-1 lg:order-2">
                
                <!-- Screen Shake wrapper -->
                <div id="screen-shake-wrapper" class="w-full h-full relative flex items-center justify-center">
                    <canvas id="gameCanvas" width="800" height="500" class="w-full h-auto max-h-[500px] block bg-[#04040d] cursor-none"></canvas>
                </div>

                <!-- Custom Overlay Modals inside Game Arena -->
                <!-- 1. Start Menu Overlay -->
                <div id="start-overlay" class="absolute inset-0 bg-slate-950/90 flex flex-col items-center justify-center p-6 text-center z-20 transition-all duration-300">
                    <div class="max-w-md space-y-6">
                        <div class="space-y-2">
                            <span class="px-3 py-1 bg-purple-500/20 text-purple-400 rounded-full text-xs font-bold tracking-widest uppercase border border-purple-500/30">
                                Retro Sci-Fi Breakout
                            </span>
                            <h2 class="arcade-font text-4xl md:text-5xl font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-cyan-400 via-pink-400 to-purple-500 tracking-widest">
                                NEON ARCADE
                            </h2>
                            <p class="text-slate-400 text-xs max-w-sm mx-auto">
                                화려하게 펼쳐지는 네온 벽돌들을 격파하세요! 아이템을 획득하고 레트로 음악과 함께 한계를 극복하세요.
                            </p>
                        </div>

                        <!-- Difficulty Selector -->
                        <div class="space-y-2">
                            <span class="text-xs text-slate-400 uppercase tracking-widest font-bold">난이도 선택</span>
                            <div class="grid grid-cols-3 gap-2 p-1 bg-slate-900 rounded-xl border border-slate-800">
                                <button onclick="setDifficulty('easy')" id="btn-diff-easy" class="py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-slate-800 text-slate-400 hover:text-white">쉬움</button>
                                <button onclick="setDifficulty('normal')" id="btn-diff-normal" class="py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-purple-600 text-white neon-glow">보통</button>
                                <button onclick="setDifficulty('hard')" id="btn-diff-hard" class="py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-slate-800 text-slate-400 hover:text-white">어려움</button>
                            </div>
                        </div>

                        <button id="btn-start" class="w-full py-4 bg-gradient-to-r from-red-600 to-rose-600 rounded-xl font-bold uppercase tracking-widest text-sm hover:from-red-500 hover:to-rose-500 active:scale-95 transition-all shadow-lg shadow-red-500/30 flex items-center justify-center gap-2">
                            <i class="fa-solid fa-play"></i> 스타트
                        </button>

                        <div class="text-[10px] text-slate-500 flex justify-center gap-6">
                            <span><i class="fa-solid fa-volume-high text-cyan-400 mr-1"></i> Tone.js 사운드 켜짐</span>
                            <span><i class="fa-solid fa-keyboard text-pink-400 mr-1"></i> 키보드/마우스 완벽지원</span>
                        </div>
                    </div>
                </div>

                <!-- 2. Pause Overlay -->
                <div id="pause-overlay" class="absolute inset-0 bg-slate-950/80 backdrop-blur-sm hidden flex-col items-center justify-center p-6 text-center z-20">
                    <div class="space-y-4">
                        <i class="fa-solid fa-circle-pause text-5xl text-purple-400 animate-pulse"></i>
                        <h2 class="arcade-font text-3xl font-bold tracking-widest text-slate-100">일시정지됨</h2>
                        <p class="text-xs text-slate-400">계속하려면 <span class="px-2 py-0.5 bg-slate-800 rounded font-semibold text-white">Space</span> 키 또는 아래 버튼을 누르세요.</p>
                        <button onclick="togglePause()" class="px-6 py-2.5 bg-purple-600 hover:bg-purple-500 text-xs font-bold uppercase tracking-widest rounded-xl shadow-lg transition-all">
                            게임 재개
                        </button>
                    </div>
                </div>

                <!-- 3. Game Over Overlay -->
                <div id="gameover-overlay" class="absolute inset-0 bg-red-950/90 backdrop-blur-md hidden flex-col items-center justify-center p-6 text-center z-20">
                    <div class="space-y-6 max-w-sm">
                        <div class="space-y-1">
                            <span class="text-xs font-black tracking-widest text-red-500 uppercase">MISSION FAILED</span>
                            <h2 class="arcade-font text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-r from-red-500 to-pink-500 tracking-wider">
                                GAME OVER
                            </h2>
                        </div>
                        <div class="bg-black/40 p-4 rounded-xl border border-red-500/20 space-y-2">
                            <div class="flex justify-between text-xs text-slate-400">
                                <span>최종 획득 점수:</span>
                                <span id="final-score" class="font-bold text-cyan-400 arcade-font">0</span>
                            </div>
                            <div class="flex justify-between text-xs text-slate-400">
                                <span>진행한 마지막 레벨:</span>
                                <span id="final-level" class="font-bold text-pink-400 arcade-font">Level 1</span>
                            </div>
                        </div>
                        <button onclick="restartGame()" class="w-full py-3.5 bg-gradient-to-r from-red-600 to-pink-600 hover:from-red-500 hover:to-pink-500 active:scale-95 text-xs font-bold uppercase tracking-widest rounded-xl shadow-lg shadow-red-500/20 transition-all flex items-center justify-center gap-2">
                            <i class="fa-solid fa-rotate-left"></i> 재도전 하기
                        </button>
                    </div>
                </div>

                <!-- 4. Level Clear Overlay -->
                <div id="clear-overlay" class="absolute inset-0 bg-emerald-950/90 backdrop-blur-md hidden flex-col items-center justify-center p-6 text-center z-20">
                    <div class="space-y-6 max-w-sm">
                        <div class="space-y-1">
                            <span class="text-xs font-black tracking-widest text-emerald-400 uppercase">EXCELLENT PLAY</span>
                            <h2 class="arcade-font text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-r from-emerald-400 to-teal-400 tracking-wider">
                                LEVEL CLEAR
                            </h2>
                        </div>
                        <div class="bg-black/40 p-4 rounded-xl border border-emerald-500/20 space-y-2">
                            <p class="text-xs text-slate-300">스테이지를 정복하셨습니다! 한 단계 더 강력해진 도전을 받아들이세요.</p>
                        </div>
                        <button onclick="loadNextLevel()" class="w-full py-3.5 bg-gradient-to-r from-emerald-500 to-teal-600 hover:from-emerald-400 hover:to-teal-500 active:scale-95 text-xs font-bold uppercase tracking-widest rounded-xl shadow-lg shadow-emerald-500/20 transition-all flex items-center justify-center gap-2">
                            다음 레벨 진입 <i class="fa-solid fa-arrow-right animate-bounce-horizontal"></i>
                        </button>
                    </div>
                </div>

                <!-- 5. All Clear (Victory) Overlay -->
                <div id="victory-overlay" class="absolute inset-0 bg-yellow-950/90 backdrop-blur-md hidden flex-col items-center justify-center p-6 text-center z-20">
                    <div class="space-y-6 max-w-sm">
                        <div class="space-y-1">
                            <span class="text-xs font-black tracking-widest text-yellow-400 uppercase animate-pulse">SUPREME CHAMPION</span>
                            <h2 class="arcade-font text-4xl md:text-5xl font-black text-transparent bg-clip-text bg-gradient-to-r from-yellow-400 via-amber-400 to-orange-500 tracking-wider">
                                ALL CLEAR!
                            </h2>
                        </div>
                        <p class="text-xs text-slate-300">
                            모든 네온 은하계의 벽돌을 산산조각 내셨습니다! 진정한 브릭 브레이커 아케이드 마스터의 명예를 얻으셨습니다.
                        </p>
                        <div class="bg-black/40 p-4 rounded-xl border border-yellow-500/20 space-y-2">
                            <div class="flex justify-between text-xs text-slate-400">
                                <span>최종 명예 점수:</span>
                                <span id="victory-score" class="font-bold text-yellow-400 arcade-font">0</span>
                            </div>
                        </div>
                        <button onclick="restartGame()" class="w-full py-3.5 bg-gradient-to-r from-yellow-500 to-amber-600 hover:from-yellow-400 hover:to-amber-500 active:scale-95 text-xs font-bold uppercase tracking-widest rounded-xl shadow-lg shadow-yellow-500/20 transition-all flex items-center justify-center gap-2">
                            처음부터 다시 즐기기 <i class="fa-solid fa-rotate-left"></i>
                        </button>
                    </div>
                </div>

            </div>

        </div>

        <!-- Sound Activation Toast Hint -->
        <div class="flex flex-wrap items-center justify-between gap-4 p-4 bg-slate-900/50 backdrop-blur rounded-2xl border border-slate-800/80 text-xs">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-lg bg-cyan-950/80 text-cyan-400 border border-cyan-800 flex items-center justify-center text-sm">
                    <i class="fa-solid fa-music"></i>
                </div>
                <div>
                    <p class="font-bold text-slate-300">8-Bit 아케이드 사운드 활성화</p>
                    <p class="text-[10px] text-slate-500">Tone.js 신디사이저가 직접 연주하는 복고풍 무드의 효과음입니다.</p>
                </div>
            </div>
            <div class="flex items-center gap-2">
                <button onclick="muteAudio()" id="btn-sound" class="px-3 py-1.5 bg-slate-800 text-slate-300 hover:text-white rounded-lg font-semibold flex items-center gap-1.5 transition-colors">
                    <i class="fa-solid fa-volume-up"></i> <span>사운드: ON</span>
                </button>
            </div>
        </div>

    </div>

    <script>
        // --- 1. Audio System Setup (Tone.js wrapper) ---
        let audioMuted = false;
        let audioInitialized = false;

        // Custom Sound FX Synths
        let synthPaddle, synthBrick, synthPowerup, synthLose, synthLaser;

        function initAudio() {
            if (audioInitialized) return;
            try {
                // Main Beep/Paddle synth
                synthPaddle = new Tone.PolySynth(Tone.Synth, {
                    oscillator: { type: "triangle" },
                    envelope: { attack: 0.01, decay: 0.1, sustain: 0.1, release: 0.1 }
                }).toDestination();
                synthPaddle.volume.value = -8;

                // Explosion/Brick synth
                synthBrick = new Tone.NoiseSynth({
                    noise: { type: "white" },
                    envelope: { attack: 0.005, decay: 0.1, sustain: 0, release: 0.1 }
                }).toDestination();
                synthBrick.volume.value = -12;

                // Powerup/Laser sound effects
                synthPowerup = new Tone.MonoSynth({
                    oscillator: { type: "sawtooth" },
                    filter: { Q: 2, type: "lowpass", frequency: 2000 },
                    envelope: { attack: 0.02, decay: 0.2, sustain: 0.2, release: 0.2 }
                }).toDestination();
                synthPowerup.volume.value = -10;

                synthLaser = new Tone.Synth({
                    oscillator: { type: "square" },
                    envelope: { attack: 0.005, decay: 0.08, sustain: 0, release: 0.05 }
                }).toDestination();
                synthLaser.volume.value = -14;

                // Start Tone.js Context
                Tone.start();
                audioInitialized = true;
                console.log("Tone.js Synthesizers initialized successfully.");
            } catch (e) {
                console.error("Audio initialization failed. Using silent mode.", e);
            }
        }

        function playSound(type, pitch = "C4") {
            if (audioMuted || !audioInitialized) return;
            try {
                if (type === 'paddle') {
                    synthPaddle.triggerAttackRelease(pitch, "16n");
                } else if (type === 'brick') {
                    synthBrick.triggerAttackRelease("16n");
                } else if (type === 'powerup') {
                    synthPowerup.triggerAttackRelease("E5", "8n");
                    setTimeout(() => synthPowerup.triggerAttackRelease("G5", "8n"), 80);
                } else if (type === 'laser') {
                    synthLaser.triggerAttackRelease("C6", "16n");
                } else if (type === 'lose') {
                    synthPaddle.triggerAttackRelease("G3", "8n");
                    setTimeout(() => synthPaddle.triggerAttackRelease("E3", "4n"), 150);
                } else if (type === 'win') {
                    synthPaddle.triggerAttackRelease("C5", "8n");
                    setTimeout(() => synthPaddle.triggerAttackRelease("E5", "8n"), 100);
                    setTimeout(() => synthPaddle.triggerAttackRelease("G5", "8n"), 200);
                    setTimeout(() => synthPaddle.triggerAttackRelease("C6", "4n"), 300);
                }
            } catch (err) {
                // Silent catch for browser blocking or active node issues
            }
        }

        function muteAudio() {
            audioMuted = !audioMuted;
            const btn = document.getElementById('btn-sound');
            if (audioMuted) {
                btn.innerHTML = `<i class="fa-solid fa-volume-mute"></i> <span>사운드: OFF</span>`;
                btn.classList.add('bg-red-950/40', 'text-red-400');
                btn.classList.remove('bg-slate-800', 'text-slate-300');
            } else {
                if (!audioInitialized) initAudio();
                btn.innerHTML = `<i class="fa-solid fa-volume-up"></i> <span>사운드: ON</span>`;
                btn.classList.remove('bg-red-950/40', 'text-red-400');
                btn.classList.add('bg-slate-800', 'text-slate-300');
            }
        }

        // --- 2. Canvas & Core Settings ---
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // High Score storage keys
        const LOCAL_STORAGE_KEY = "neon_bricks_highscore";

        // Global Difficulty variables
        let difficulty = 'normal'; 
        let speedMultiplier = 1.0;

        function setDifficulty(diff) {
            difficulty = diff;
            const btns = {
                easy: document.getElementById('btn-diff-easy'),
                normal: document.getElementById('btn-diff-normal'),
                hard: document.getElementById('btn-diff-hard')
            };

            // Reset classes
            Object.keys(btns).forEach(k => {
                btns[k].className = "py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-slate-800 text-slate-400 hover:text-white";
            });

            // Activate chosen one
            if (diff === 'easy') {
                btns.easy.className = "py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-cyan-600 text-white neon-glow";
                speedMultiplier = 0.8;
            } else if (diff === 'normal') {
                btns.normal.className = "py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-purple-600 text-white neon-glow";
                speedMultiplier = 1.0;
            } else if (diff === 'hard') {
                btns.hard.className = "py-2 text-xs font-bold rounded-lg transition-all duration-200 bg-pink-600 text-white neon-glow";
                speedMultiplier = 1.25;
            }
        }

        // --- 3. Game State Models & Definitions ---
        let score = 0;
        let highScore = localStorage.getItem(LOCAL_STORAGE_KEY) ? parseInt(localStorage.getItem(LOCAL_STORAGE_KEY)) : 0;
        let currentLevel = 1;
        const totalLevels = 4;
        let lives = 3;
        let isPaused = false;
        let isPlaying = false;
        let screenShakeAmount = 0;

        // Display High Score immediately
        document.getElementById("high-score-val").innerText = String(highScore).padStart(5, '0');

        // Paddle Configuration
        const paddleConfig = {
            baseWidth: 120,
            height: 16,
            radius: 8,
            speed: 8,
            color: '#10b981' // emerald
        };

        let paddle = {
            x: canvas.width / 2 - paddleConfig.baseWidth / 2,
            y: canvas.height - 35,
            width: paddleConfig.baseWidth,
            height: paddleConfig.height,
            targetWidth: paddleConfig.baseWidth
        };

        // Ball Setup
        let balls = []; // supports multiball
        const baseBallSpeed = 5;

        // Powerups Configuration
        const powerupTypes = {
            WIDE: { name: '패들 확장', color: '#10b981', symbol: '↔', desc: '패들 길이가 넓어집니다.' },
            MULTIBALL: { name: '멀티 볼', color: '#3b82f6', symbol: '●●', desc: '공이 3개로 분리됩니다.' },
            LASER: { name: '레이저 캐논', color: '#f43f5e', symbol: '▲', desc: '패들에서 레이저 탄환을 발사합니다.' },
            SLOW: { name: '타임 슬로우', color: '#eab308', symbol: '▼', desc: '공의 속도가 느려집니다.' },
            SHIELD: { name: '안전 보강막', color: '#8b5cf6', symbol: '▬', desc: '바닥을 막는 안전 보호막이 생깁니다.' }
        };

        let activePowerups = {
            WIDE: { duration: 0, max: 600 },    // frame count
            LASER: { duration: 0, max: 500, lastShot: 0 },
            SLOW: { duration: 0, max: 400 },
            SHIELD: { duration: 0, max: 800 }
        };

        let fallingPowerups = [];
        let lasers = [];

        // Particles System
        let particles = [];

        // Bricks Storage
        let bricks = [];

        // Key states
        let keys = {
            ArrowLeft: false,
            ArrowRight: false,
            KeyA: false,
            KeyD: false
        };

        // Touch Input variables
        let isTouchDragging = false;
        let touchStartX = 0;

        // --- 4. Brick Layout Generation for Levels ---
        function createBricks(level) {
            bricks = [];
            const cols = 10;
            const brickWidth = 68;
            const brickHeight = 22;
            const padding = 8;
            const offsetTop = 45;
            const offsetLeft = (canvas.width - (cols * (brickWidth + padding) - padding)) / 2;

            // Define Brick Colors & Strengths
            // strength 1 = neon green, 2 = neon cyan, 3 = neon pink, -1 = golden indestructible, 99 = explosive
            const colorsByStrength = {
                1: '#22c55e', // green
                2: '#06b6d4', // cyan
                3: '#ec4899', // pink
                4: '#a855f7', // purple
                99: '#f97316' // orange explosive
            };

            if (level === 1) {
                // Simple Grid
                const rows = 4;
                for (let r = 0; r < rows; r++) {
                    for (let c = 0; c < cols; c++) {
                        // Strength 1 and 2
                        let strength = (r < 1) ? 2 : 1;
                        // 15% chance to be powerup container
                        let isPowerupHolder = Math.random() < 0.2;
                        bricks.push({
                            x: offsetLeft + c * (brickWidth + padding),
                            y: offsetTop + r * (brickHeight + padding),
                            w: brickWidth,
                            h: brickHeight,
                            strength: strength,
                            maxStrength: strength,
                            color: colorsByStrength[strength],
                            isPowerup: isPowerupHolder,
                            type: 'normal'
                        });
                    }
                }
            } 
            else if (level === 2) {
                // Zig-Zag Structure with multi-hit bricks & Exploding blocks
                const rows = 5;
                for (let r = 0; r < rows; r++) {
                    for (let c = 0; c < cols; c++) {
                        // checkerboard layout or space empty
                        if ((r + c) % 2 === 0) {
                            let isExplosive = (r === 2 && (c === 3 || c === 6));
                            let strength = isExplosive ? 99 : (r === 0 ? 3 : 2);
                            let type = isExplosive ? 'explosive' : 'normal';
                            bricks.push({
                                x: offsetLeft + c * (brickWidth + padding),
                                y: offsetTop + r * (brickHeight + padding),
                                w: brickWidth,
                                h: brickHeight,
                                strength: strength,
                                maxStrength: strength,
                                color: colorsByStrength[strength],
                                isPowerup: Math.random() < 0.25,
                                type: type
                            });
                        }
                    }
                }
            }
            else if (level === 3) {
                // Pyramids / Concentric wall structure
                for (let r = 0; r < 6; r++) {
                    for (let c = r; c < cols - r; c++) {
                        let strength = (r === 0) ? 4 : (r < 3 ? 3 : 1);
                        bricks.push({
                            x: offsetLeft + c * (brickWidth + padding),
                            y: offsetTop + r * (brickHeight + padding),
                            w: brickWidth,
                            h: brickHeight,
                            strength: strength,
                            maxStrength: strength,
                            color: colorsByStrength[strength],
                            isPowerup: Math.random() < 0.3,
                            type: 'normal'
                        });
                    }
                }
            }
            else if (level === 4) {
                // Space Invader shape + moving feature simulation
                // Let's draw a space invader icon
                const invader = [
                    [0,0,1,0,0,0,0,1,0,0],
                    [0,0,0,1,0,0,1,0,0,0],
                    [0,0,1,1,1,1,1,1,0,0],
                    [0,1,1,0,1,1,0,1,1,0],
                    [1,1,1,1,1,1,1,1,1,1],
                    [1,0,1,1,1,1,1,1,0,1],
                ];

                for (let r = 0; r < invader.length; r++) {
                    for (let c = 0; c < invader[r].length; c++) {
                        if (invader[r][c] === 1) {
                            // High tier level
                            let isExplosive = (r === 3 && (c === 2 || c === 7));
                            let strength = isExplosive ? 99 : (r === 4 ? 4 : 2);
                            let type = isExplosive ? 'explosive' : 'normal';

                            bricks.push({
                                x: offsetLeft + c * (brickWidth + padding),
                                y: offsetTop + r * (brickHeight + padding),
                                w: brickWidth,
                                h: brickHeight,
                                strength: strength,
                                maxStrength: strength,
                                color: colorsByStrength[strength],
                                isPowerup: Math.random() < 0.35,
                                type: type,
                                direction: Math.random() < 0.5 ? 1 : -1, // moving bricks parameter
                                initialX: offsetLeft + c * (brickWidth + padding)
                            });
                        }
                    }
                }
            }
        }

        // --- 5. Spawn Handlers ---
        function spawnBall(x, y, dx = 0, dy = -baseBallSpeed) {
            balls.push({
                x: x,
                y: y,
                radius: 7,
                dx: dx,
                dy: dy,
                color: '#22d3ee', // bright neon cyan
                glowColor: 'rgba(6, 182, 212, 0.8)'
            });
        }

        function spawnPowerup(x, y) {
            const keys = Object.keys(powerupTypes);
            const randomType = keys[Math.floor(Math.random() * keys.length)];
            fallingPowerups.push({
                x: x,
                y: y,
                w: 18,
                h: 18,
                type: randomType,
                dy: 2,
                angle: 0
            });
        }

        function createExplosion(x, y, color, count = 12) {
            for (let i = 0; i < count; i++) {
                const angle = Math.random() * Math.PI * 2;
                const speed = 1.5 + Math.random() * 3.5;
                particles.push({
                    x: x,
                    y: y,
                    dx: Math.cos(angle) * speed,
                    dy: Math.sin(angle) * speed,
                    radius: 1 + Math.random() * 3,
                    color: color,
                    alpha: 1,
                    decay: 0.02 + Math.random() * 0.03
                });
            }
        }

        // Initialize / Start Level Function
        function startLevel(levelNum) {
            currentLevel = levelNum;
            document.getElementById("level-val").innerText = `${currentLevel} / ${totalLevels}`;
            
            // Clean arrays
            balls = [];
            fallingPowerups = [];
            lasers = [];
            particles = [];

            // Reset paddle properties
            paddle.width = paddleConfig.baseWidth;
            paddle.targetWidth = paddleConfig.baseWidth;
            paddle.x = canvas.width / 2 - paddle.width / 2;

            // Reset active powerup durations
            Object.keys(activePowerups).forEach(k => activePowerups[k].duration = 0);
            updatePowerupsUI();

            // Setup level bricks
            createBricks(currentLevel);

            // Spawn original starting ball slightly above the paddle center
            const finalMult = (difficulty === 'hard') ? speedMultiplier : 1.0;
            spawnBall(
                paddle.x + paddle.width / 2, 
                paddle.y - 15, 
                (Math.random() - 0.5) * 3, 
                -baseBallSpeed * speedMultiplier
            );

            playSound('win');
        }

        // --- 6. Controls & Input Handling ---
        window.addEventListener('keydown', e => {
            if (e.code === 'ArrowLeft' || e.code === 'KeyA') keys.ArrowLeft = true;
            if (e.code === 'ArrowRight' || e.code === 'KeyD') keys.ArrowRight = true;
            
            // Toggle pause with Space
            if (e.code === 'Space' && isPlaying) {
                e.preventDefault();
                togglePause();
            }
        });

        window.addEventListener('keyup', e => {
            if (e.code === 'ArrowLeft' || e.code === 'KeyA') keys.ArrowLeft = false;
            if (e.code === 'ArrowRight' || e.code === 'KeyD') keys.ArrowRight = false;
        });

        // Mouse Controls
        canvas.addEventListener('mousemove', e => {
            if (!isPlaying || isPaused) return;
            const rect = canvas.getBoundingClientRect();
            // Scale mouse coordinates to match canvas real resolution
            const scaleX = canvas.width / rect.width;
            const mouseX = (e.clientX - rect.left) * scaleX;
            
            // Center of paddle follows mouse
            paddle.x = mouseX - paddle.width / 2;
            
            // Bound inside canvas
            if (paddle.x < 0) paddle.x = 0;
            if (paddle.x + paddle.width > canvas.width) paddle.x = canvas.width - paddle.width;
        });

        // Touch Controls
        canvas.addEventListener('touchstart', e => {
            if (!isPlaying || isPaused) return;
            initAudio(); // Warm up Tone.js context in iOS/Android safely
            isTouchDragging = true;
            const rect = canvas.getBoundingClientRect();
            const scaleX = canvas.width / rect.width;
            touchStartX = (e.touches[0].clientX - rect.left) * scaleX;
            e.preventDefault();
        }, { passive: false });

        canvas.addEventListener('touchmove', e => {
            if (!isTouchDragging || !isPlaying || isPaused) return;
            const rect = canvas.getBoundingClientRect();
            const scaleX = canvas.width / rect.width;
            const touchX = (e.touches[0].clientX - rect.left) * scaleX;
            
            // Dynamic absolute positioning
            paddle.x = touchX - paddle.width / 2;

            if (paddle.x < 0) paddle.x = 0;
            if (paddle.x + paddle.width > canvas.width) paddle.x = canvas.width - paddle.width;
            e.preventDefault();
        }, { passive: false });

        canvas.addEventListener('touchend', e => {
            isTouchDragging = false;
        });

        // Start & Restart Core Actions
        document.getElementById('btn-start').addEventListener('click', () => {
            initAudio();
            document.getElementById('start-overlay').classList.add('opacity-0', 'pointer-events-none');
            setTimeout(() => {
                document.getElementById('start-overlay').classList.add('hidden');
            }, 300);
            
            resetGameSystem();
            isPlaying = true;
        });

        function resetGameSystem() {
            score = 0;
            lives = 3;
            currentLevel = 1;
            document.getElementById('score-val').innerText = String(score).padStart(5, '0');
            updateLivesUI();
            startLevel(currentLevel);
        }

        function restartGame() {
            document.getElementById('gameover-overlay').classList.add('hidden');
            document.getElementById('victory-overlay').classList.add('hidden');
            resetGameSystem();
            isPaused = false;
            isPlaying = true;
        }

        function togglePause() {
            if (!isPlaying) return;
            isPaused = !isPaused;
            const pauseOverlay = document.getElementById('pause-overlay');
            if (isPaused) {
                pauseOverlay.classList.remove('hidden');
                pauseOverlay.classList.add('flex');
            } else {
                pauseOverlay.classList.add('hidden');
                pauseOverlay.classList.remove('flex');
                if (audioInitialized) Tone.start();
            }
        }

        // --- 7. Core Physics and Collision Updates ---
        function updatePhysics() {
            if (!isPlaying || isPaused) return;

            // Shake mitigation
            if (screenShakeAmount > 0) {
                screenShakeAmount -= 0.5;
            }

            // Keyboard paddle movement (smoothed)
            if (keys.ArrowLeft) {
                paddle.x -= paddleConfig.speed;
                if (paddle.x < 0) paddle.x = 0;
            }
            if (keys.ArrowRight) {
                paddle.x += paddleConfig.speed;
                if (paddle.x + paddle.width > canvas.width) paddle.x = canvas.width - paddle.width;
            }

            // Smooth width transitions for Wide Powerup
            if (paddle.width !== paddle.targetWidth) {
                paddle.width += (paddle.targetWidth - paddle.width) * 0.1;
            }

            // A. Update Active Powerups timer
            updatePowerupTimers();

            // B. Laser Firing mechanism
            if (activePowerups.LASER.duration > 0) {
                const now = Date.now();
                if (now - activePowerups.LASER.lastShot > 400) { // shot interval
                    lasers.push(
                        { x: paddle.x + 10, y: paddle.y - 4, dy: -6 },
                        { x: paddle.x + paddle.width - 10, y: paddle.y - 4, dy: -6 }
                    );
                    playSound('laser');
                    activePowerups.LASER.lastShot = now;
                }
            }

            // Move Lasers
            for (let i = lasers.length - 1; i >= 0; i--) {
                const l = lasers[i];
                l.y += l.dy;
                // remove out of bounds
                if (l.y < 0) {
                    lasers.splice(i, 1);
                    continue;
                }

                // Laser-Brick collision
                for (let j = bricks.length - 1; j >= 0; j--) {
                    const b = bricks[j];
                    if (l.x > b.x && l.x < b.x + b.w && l.y > b.y && l.y < b.y + b.h) {
                        // hit!
                        lasers.splice(i, 1);
                        hitBrick(j, b);
                        break;
                    }
                }
            }

            // C. Move Falling Items
            for (let i = fallingPowerups.length - 1; i >= 0; i--) {
                const p = fallingPowerups[i];
                p.y += p.dy;
                p.angle += 0.03;

                // Out of screen
                if (p.y > canvas.height) {
                    fallingPowerups.splice(i, 1);
                    continue;
                }

                // Collect Powerup Collision (Paddle)
                if (p.x + p.w > paddle.x && p.x < paddle.x + paddle.width &&
                    p.y + p.h > paddle.y && p.y < paddle.y + paddle.height) {
                    // Activate powerup!
                    activatePowerup(p.type);
                    fallingPowerups.splice(i, 1);
                    playSound('powerup');
                    continue;
                }
            }

            // D. Ball physics and Wall/Paddle Collisions
            for (let i = balls.length - 1; i >= 0; i--) {
                const b = balls[i];

                // Slow-mo items effect
                const currentSpeedMult = activePowerups.SLOW.duration > 0 ? 0.6 : 1.0;
                b.x += b.dx * currentSpeedMult;
                b.y += b.dy * currentSpeedMult;

                // Wall bounce Left & Right
                if (b.x - b.radius < 0) {
                    b.x = b.radius;
                    b.dx = -b.dx;
                    playSound('paddle', 'G4');
                } else if (b.x + b.radius > canvas.width) {
                    b.x = canvas.width - b.radius;
                    b.dx = -b.dx;
                    playSound('paddle', 'G4');
                }

                // Ceiling bounce
                if (b.y - b.radius < 0) {
                    b.y = b.radius;
                    b.dy = -b.dy;
                    playSound('paddle', 'D4');
                }

                // Base Bottom loss OR Active Shield bounce
                if (b.y + b.radius > canvas.height) {
                    if (activePowerups.SHIELD.duration > 0) {
                        // Shield acts as temporary ceiling bounce
                        b.y = canvas.height - b.radius - 5;
                        b.dy = -b.dy;
                        screenShakeAmount = 5;
                        playSound('paddle', 'B4');
                        createExplosion(b.x, canvas.height - 2, '#8b5cf6', 8);
                    } else {
                        // Lose current ball
                        balls.splice(i, 1);
                        createExplosion(b.x, canvas.height - 5, '#ef4444', 15);
                        continue;
                    }
                }

                // Paddle Collision bounce
                if (b.y + b.radius >= paddle.y && b.y - b.radius <= paddle.y + paddle.height &&
                    b.x + b.radius >= paddle.x && b.x - b.radius <= paddle.x + paddle.width) {
                    
                    // Bounce & calculate hit deflection angle based on hit position
                    const hitPos = (b.x - paddle.x) / paddle.width; // 0 (left edge) to 1 (right edge)
                    const angle = (hitPos - 0.5) * (Math.PI / 2.5); // max 72 deg deflection
                    
                    const speed = Math.sqrt(b.dx * b.dx + b.dy * b.dy);
                    b.dx = speed * Math.sin(angle);
                    b.dy = -speed * Math.cos(angle);
                    
                    // Cap horizontal speed slightly to prevent infinite horizontal bouncing
                    if (Math.abs(b.dx) < 1) b.dx = b.dx < 0 ? -1.5 : 1.5;

                    b.y = paddle.y - b.radius; // push out
                    playSound('paddle', 'C5');
                    
                    // Visual feedback
                    createExplosion(b.x, paddle.y, '#10b981', 4);
                }

                // Brick Collisions
                for (let j = bricks.length - 1; j >= 0; j--) {
                    const br = bricks[j];
                    if (b.x + b.radius > br.x && b.x - b.radius < br.x + br.w &&
                        b.y + b.radius > br.y && b.y - b.radius < br.y + br.h) {
                        
                        // Collision direction determination
                        const overlapX = Math.min(b.x + b.radius - br.x, br.x + br.w - (b.x - b.radius));
                        const overlapY = Math.min(b.y + b.radius - br.y, br.y + br.h - (b.y - b.radius));

                        if (overlapX < overlapY) {
                            b.dx = -b.dx;
                            if (b.x < br.x) b.x -= overlapX;
                            else b.x += overlapX;
                        } else {
                            b.dy = -b.dy;
                            if (b.y < br.y) b.y -= overlapY;
                            else b.y += overlapY;
                        }

                        hitBrick(j, br);
                        break; // Process one collision at a time per ball
                    }
                }
            }

            // Check Game Over (No balls left)
            if (balls.length === 0) {
                loseLife();
            }

            // Check Win condition (No breakable bricks left)
            const breakables = bricks.filter(b => b.strength > 0);
            if (breakables.length === 0 && bricks.length > 0) {
                levelComplete();
            }

            // Moving brick animation logic for Stage 4
            if (currentLevel === 4) {
                bricks.forEach(b => {
                    b.x += b.direction * 0.4;
                    // wiggle area limits
                    if (Math.abs(b.x - b.initialX) > 20) {
                        b.direction *= -1;
                    }
                });
            }

            // Particles Update
            for (let i = particles.length - 1; i >= 0; i--) {
                const pt = particles[i];
                pt.x += pt.dx;
                pt.y += pt.dy;
                pt.alpha -= pt.decay;
                if (pt.alpha <= 0) {
                    particles.splice(i, 1);
                }
            }
        }

        // --- 8. Brick Hitting Logic ---
        function hitBrick(index, br) {
            playSound('brick');
            screenShakeAmount = 3;

            // Damage Brick
            if (br.type === 'explosive') {
                bricks.splice(index, 1);
                createExplosion(br.x + br.w/2, br.y + br.h/2, '#f97316', 30);
                triggerChainExplosion(br.x + br.w/2, br.y + br.h/2);
                addScore(250);
            } else {
                br.strength--;
                if (br.strength <= 0) {
                    bricks.splice(index, 1);
                    createExplosion(br.x + br.w/2, br.y + br.h/2, br.color, 16);
                    addScore(100 * currentLevel);

                    // Chance to drop powerup
                    if (br.isPowerup) {
                        spawnPowerup(br.x + br.w/2, br.y + br.h);
                    }
                } else {
                    // Dim/Update Color on hit
                    createExplosion(br.x + br.w/2, br.y + br.h/2, br.color, 4);
                    addScore(20);
                }
            }
        }

        // Explosive brick chain blast radius
        function triggerChainExplosion(centerX, centerY) {
            const range = 95; // pixels range
            screenShakeAmount = 15;
            
            for (let i = bricks.length - 1; i >= 0; i--) {
                const br = bricks[i];
                const bCenterX = br.x + br.w / 2;
                const bCenterY = br.y + br.h / 2;
                const dist = Math.hypot(bCenterX - centerX, bCenterY - centerY);

                if (dist <= range) {
                    // Detonate immediately
                    bricks.splice(i, 1);
                    createExplosion(bCenterX, bCenterY, br.color, 14);
                    addScore(120);
                }
            }
        }

        // --- 9. Power-up Activators ---
        function activatePowerup(type) {
            if (type === 'MULTIBALL') {
                // Duplicate all currently active balls
                const currentBalls = [...balls];
                currentBalls.forEach(b => {
                    // Spawn 2 new balls with slight velocity alterations
                    spawnBall(b.x, b.y, b.dx - 1.5, b.dy + 0.5);
                    spawnBall(b.x, b.y, b.dx + 1.5, b.dy - 0.5);
                });
                // ensure at least some balls exist
                if (balls.length === 0) {
                    spawnBall(canvas.width / 2, canvas.height - 50, 0, -baseBallSpeed);
                }
            } else if (type === 'WIDE') {
                paddle.targetWidth = paddleConfig.baseWidth * 1.6;
                activePowerups.WIDE.duration = activePowerups.WIDE.max;
            } else if (type === 'LASER') {
                activePowerups.LASER.duration = activePowerups.LASER.max;
            } else if (type === 'SLOW') {
                activePowerups.SLOW.duration = activePowerups.SLOW.max;
            } else if (type === 'SHIELD') {
                activePowerups.SHIELD.duration = activePowerups.SHIELD.max;
            }

            updatePowerupsUI();
        }

        function updatePowerupTimers() {
            Object.keys(activePowerups).forEach(key => {
                if (activePowerups[key].duration > 0) {
                    activePowerups[key].duration--;
                    if (activePowerups[key].duration === 0) {
                        // Deactivate effect
                        if (key === 'WIDE') {
                            paddle.targetWidth = paddleConfig.baseWidth;
                        }
                        updatePowerupsUI();
                    }
                }
            });
        }

        // Render Applied Powerup labels to Left Side Panel
        function updatePowerupsUI() {
            const list = document.getElementById('active-powerups-list');
            list.innerHTML = '';
            let activeCount = 0;

            Object.keys(activePowerups).forEach(k => {
                const act = activePowerups[k];
                if (act.duration > 0) {
                    activeCount++;
                    const percent = Math.floor((act.duration / act.max) * 100);
                    const item = powerupTypes[k];

                    list.innerHTML += `
                        <div class="space-y-1 bg-slate-900/60 p-2 rounded-lg border border-slate-800">
                            <div class="flex justify-between items-center text-xs">
                                <span class="font-bold" style="color: ${item.color}">${item.symbol} ${item.name}</span>
                                <span class="text-[10px] text-slate-400 font-mono">${percent}%</span>
                            </div>
                            <div class="w-full bg-slate-950 h-1.5 rounded-full overflow-hidden">
                                <div class="h-full rounded-full transition-all duration-100" style="width: ${percent}%; background-color: ${item.color}"></div>
                            </div>
                        </div>
                    `;
                }
            });

            if (activeCount === 0) {
                list.innerHTML = `<div class="text-[11px] text-slate-500 italic">적용된 특수 효과 없음</div>`;
            }
        }

        // --- 10. Scoring and Life Systems ---
        function addScore(amount) {
            score += amount;
            document.getElementById('score-val').innerText = String(score).padStart(5, '0');
            
            if (score > highScore) {
                highScore = score;
                localStorage.setItem(LOCAL_STORAGE_KEY, highScore);
                document.getElementById('high-score-val').innerText = String(highScore).padStart(5, '0');
            }
        }

        function updateLivesUI() {
            const container = document.getElementById('lives-container');
            container.innerHTML = '';
            for (let i = 0; i < lives; i++) {
                container.innerHTML += `<i class="fa-solid fa-heart animate-bounce" style="animation-delay: ${i * 0.1}s"></i>`;
            }
        }

        function loseLife() {
            playSound('lose');
            lives--;
            updateLivesUI();

            if (lives <= 0) {
                // End game completely
                isPlaying = false;
                document.getElementById('final-score').innerText = score;
                document.getElementById('final-level').innerText = `Level ${currentLevel}`;
                document.getElementById('gameover-overlay').classList.remove('hidden');
                document.getElementById('gameover-overlay').classList.add('flex');
            } else {
                // Respawn single starting ball
                spawnBall(
                    paddle.x + paddle.width / 2, 
                    paddle.y - 15, 
                    (Math.random() - 0.5) * 3, 
                    -baseBallSpeed * speedMultiplier
                );
            }
        }

        function levelComplete() {
            isPlaying = false;
            playSound('win');
            
            if (currentLevel < totalLevels) {
                document.getElementById('clear-overlay').classList.remove('hidden');
                document.getElementById('clear-overlay').classList.add('flex');
            } else {
                // All Game Clear Victory
                document.getElementById('victory-score').innerText = score;
                document.getElementById('victory-overlay').classList.remove('hidden');
                document.getElementById('victory-overlay').classList.add('flex');
            }
        }

        function loadNextLevel() {
            document.getElementById('clear-overlay').classList.add('hidden');
            document.getElementById('clear-overlay').classList.remove('flex');
            currentLevel++;
            startLevel(currentLevel);
            isPlaying = true;
        }

        // --- 11. Canvas Drawing Methods ---
        function draw() {
            // Apply Screen Shake Transformation offset
            ctx.save();
            if (screenShakeAmount > 0) {
                const dx = (Math.random() - 0.5) * screenShakeAmount;
                const dy = (Math.random() - 0.5) * screenShakeAmount;
                ctx.translate(dx, dy);
            }

            // Clear Scene
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw Subtle Grid Pattern Background
            ctx.strokeStyle = '#1e1b4b/30';
            ctx.lineWidth = 1;
            const gridSize = 40;
            ctx.beginPath();
            for (let x = 0; x < canvas.width; x += gridSize) {
                ctx.moveTo(x, 0);
                ctx.lineTo(x, canvas.height);
            }
            for (let y = 0; y < canvas.height; y += gridSize) {
                ctx.moveTo(0, y);
                ctx.lineTo(canvas.width, y);
            }
            ctx.strokeStyle = 'rgba(30, 27, 75, 0.4)';
            ctx.stroke();

            // A. Draw Bricks
            bricks.forEach(b => {
                ctx.shadowBlur = 10;
                ctx.shadowColor = b.color;
                
                // Exploding bricks have special gradient
                if (b.type === 'explosive') {
                    const grad = ctx.createRadialGradient(b.x+b.w/2, b.y+b.h/2, 2, b.x+b.w/2, b.y+b.h/2, b.w/2);
                    grad.addColorStop(0, '#f97316');
                    grad.addColorStop(1, '#ea580c');
                    ctx.fillStyle = grad;
                } else {
                    ctx.fillStyle = b.color;
                }

                // Draw rounded rectangle for slick modern style
                ctx.beginPath();
                ctx.roundRect(b.x, b.y, b.w, b.h, 4);
                ctx.fill();

                // Draw brick neon gloss border/inner highlight
                ctx.strokeStyle = 'rgba(255, 255, 255, 0.4)';
                ctx.lineWidth = 1;
                ctx.stroke();

                // Extra visual decoration for multi-hit bricks (show durability lines)
                if (b.strength > 1 && b.type !== 'explosive') {
                    ctx.fillStyle = 'rgba(0, 0, 0, 0.35)';
                    ctx.font = '10px "Orbitron"';
                    ctx.shadowBlur = 0; // remove shadow for text performance
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText(b.strength, b.x + b.w / 2, b.y + b.h / 2);
                }
            });

            // B. Draw Shield Floor
            if (activePowerups.SHIELD.duration > 0) {
                ctx.shadowBlur = 18;
                ctx.shadowColor = '#8b5cf6';
                ctx.strokeStyle = '#8b5cf6';
                ctx.lineWidth = 6;
                ctx.beginPath();
                ctx.moveTo(0, canvas.height - 3);
                ctx.lineTo(canvas.width, canvas.height - 3);
                ctx.stroke();
            }

            // C. Draw Paddle
            ctx.shadowBlur = 15;
            ctx.shadowColor = paddleConfig.color;
            ctx.fillStyle = paddleConfig.color;
            ctx.beginPath();
            ctx.roundRect(paddle.x, paddle.y, paddle.width, paddle.height, paddleConfig.radius);
            ctx.fill();

            // Draw laser canons if active
            if (activePowerups.LASER.duration > 0) {
                ctx.fillStyle = '#ef4444';
                ctx.shadowColor = '#ef4444';
                // Left nozzle
                ctx.fillRect(paddle.x + 5, paddle.y - 6, 8, 8);
                // Right nozzle
                ctx.fillRect(paddle.x + paddle.width - 13, paddle.y - 6, 8, 8);
            }

            // D. Draw Lasers
            lasers.forEach(l => {
                ctx.shadowBlur = 8;
                ctx.shadowColor = '#ef4444';
                ctx.fillStyle = '#f87171';
                ctx.fillRect(l.x - 2, l.y, 4, 10);
            });

            // E. Draw Balls
            balls.forEach(b => {
                ctx.shadowBlur = 12;
                ctx.shadowColor = b.glowColor;
                ctx.fillStyle = b.color;
                ctx.beginPath();
                ctx.arc(b.x, b.y, b.radius, 0, Math.PI * 2);
                ctx.fill();

                // Core inner shine
                ctx.fillStyle = '#ffffff';
                ctx.beginPath();
                ctx.arc(b.x - 2, b.y - 2, b.radius * 0.4, 0, Math.PI * 2);
                ctx.fill();
            });

            // F. Draw Falling Powerups
            fallingPowerups.forEach(p => {
                const item = powerupTypes[p.type];
                ctx.shadowBlur = 12;
                ctx.shadowColor = item.color;
                
                // Draw rotating square capsule
                ctx.save();
                ctx.translate(p.x + p.w / 2, p.y + p.h / 2);
                ctx.rotate(p.angle);
                
                ctx.fillStyle = 'rgba(15, 23, 42, 0.85)';
                ctx.strokeStyle = item.color;
                ctx.lineWidth = 1.5;
                
                ctx.beginPath();
                ctx.roundRect(-p.w / 2, -p.h / 2, p.w, p.h, 4);
                ctx.fill();
                ctx.stroke();

                // Draw Powerup Symbol
                ctx.shadowBlur = 0;
                ctx.fillStyle = item.color;
                ctx.font = '10px "Orbitron", sans-serif';
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                ctx.fillText(item.symbol, 0, 0);

                ctx.restore();
            });

            // G. Draw Particles
            particles.forEach(pt => {
                ctx.shadowBlur = 0;
                ctx.fillStyle = pt.color;
                ctx.globalAlpha = pt.alpha;
                ctx.beginPath();
                ctx.arc(pt.x, pt.y, pt.radius, 0, Math.PI * 2);
                ctx.fill();
            });
            ctx.globalAlpha = 1.0; // Reset transparency completely

            ctx.restore(); // Restore shake matrix transform
        }

        // --- 12. Main Game Loop ---
        function loop() {
            updatePhysics();
            draw();
            requestAnimationFrame(loop);
        }

        // Initialize On Load
        window.onload = function() {
            setDifficulty('normal');
            // Populate simple inactive canvas view initially
            createBricks(1);
            draw();
            requestAnimationFrame(loop);
        };
    </script>
</body>
</html>
