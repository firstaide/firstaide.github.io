<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sprint Timer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: #2c2c2c;
            color: white;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 400px;
            text-align: center;
        }

        .app-title {
            font-size: 2.5rem;
            font-weight: bold;
            margin-bottom: 30px;
        }

        .settings-screen {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .how-to-use {
            margin-bottom: 25px;
            cursor: pointer;
            padding: 15px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.3s ease;
        }

        .how-to-use:hover {
            background: rgba(255, 255, 255, 0.15);
        }

        .how-to-title {
            font-size: 1.3rem;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #ffeb3b;
            margin-bottom: 5px;
        }

        .how-to-content {
            display: none;
            margin-top: 15px;
            line-height: 1.6;
            font-size: 1rem;
            color: rgba(255, 255, 255, 0.9);
            text-align: left;
        }

        .how-to-content.show {
            display: block;
        }

        .expand-icon {
            float: right;
            transition: transform 0.3s ease;
        }

        .expand-icon.expanded {
            transform: rotate(180deg);
        }

        .setting-group {
            margin-bottom: 25px;
        }

        .setting-label {
            display: block;
            font-size: 1.1rem;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .setting-control {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-top: 10px;
        }

        .setting-slider {
            flex: 1;
            -webkit-appearance: none;
            appearance: none;
            height: 8px;
            border-radius: 4px;
            background: rgba(255, 255, 255, 0.3);
            outline: none;
        }

        .setting-slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: white;
            cursor: pointer;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
        }

        .setting-slider::-moz-range-thumb {
            width: 24px;
            height: 24px;
            border-radius: 50%;
            background: white;
            cursor: pointer;
            border: none;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
        }

        .setting-value {
            min-width: 60px;
            padding: 10px 15px;
            font-size: 1.3rem;
            font-weight: bold;
            border: none;
            border-radius: 8px;
            background: rgba(255, 255, 255, 0.4);
            color: white;
            text-align: center;
            backdrop-filter: blur(5px);
        }

        .setting-value:focus {
            outline: none;
            background: rgba(255, 255, 255, 0.5);
            box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.3);
        }

        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
        }

        .btn {
            flex: 1;
            padding: 18px;
            font-size: 1.3rem;
            font-weight: bold;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-start {
            background: linear-gradient(135deg, #11998e 0%, #38ef7d 100%);
            color: white;
        }

        .btn-start:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(17, 153, 142, 0.4);
        }

        .btn-reset {
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            color: white;
        }

        .btn-reset:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(255, 107, 107, 0.4);
        }

        .feedback-btn {
            margin-top: 20px;
            padding: 12px 20px;
            background: rgba(255, 255, 255, 0.15);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 10px;
            color: white;
            text-decoration: none;
            display: inline-block;
            font-weight: 500;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .feedback-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-1px);
        }

        .training-screen {
            display: none;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 80vh;
        }

        .phase-indicator {
            font-size: 6rem;
            font-weight: bold;
            margin-bottom: 20px;
            text-transform: uppercase;
            letter-spacing: 2px;
        }

        .countdown {
            font-size: 12rem;
            font-weight: bold;
            margin-bottom: 20px;
            line-height: 0.8;
        }

        .session-info {
            font-size: 1.2rem;
            margin-bottom: 20px;
            opacity: 0.9;
        }

        .reset-btn-training {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            font-weight: bold;
            cursor: pointer;
            font-size: 1.1rem;
            transition: all 0.3s ease;
        }

        .reset-btn-training:hover {
            transform: translateX(-50%) scale(1.05);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.4);
        }

        .delay-screen {
            background: linear-gradient(135deg, #ffeaa7 0%, #fdcb6e 100%);
        }

        .sprint-screen {
            background: linear-gradient(135deg, #00b894 0%, #00cec9 100%);
        }

        .rest-screen {
            background: linear-gradient(135deg, #0984e3 0%, #74b9ff 100%);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="app-title">SPRINT TIMER</h1>
        
        <!-- Settings Screen -->
        <div id="settingsScreen" class="settings-screen">
            <div class="how-to-use" id="howToUse">
                <div class="how-to-title">
                    How to Use
                    <span class="expand-icon" id="expandIcon">▼</span>
                </div>
                <div class="how-to-content" id="howToContent">
                    Increase sprint stamina and leg spin speed.<br>
                    Put your bike on rollers with no or very low resistance.<br>
                    Put your phone where you can see it.<br>
                    "Delay start" gives you time to get on your bike and get ready.
                </div>
            </div>
            
            <div class="setting-group">
                <label class="setting-label" for="sprintTime">Sprint Time (seconds)</label>
                <div class="setting-control">
                    <input type="range" id="sprintTimeSlider" class="setting-slider" min="1" max="60" value="6">
                    <input type="number" id="sprintTime" class="setting-value" min="1" max="60" value="6">
                </div>
            </div>
            
            <div class="setting-group">
                <label class="setting-label" for="restTime">Rest Time (seconds)</label>
                <div class="setting-control">
                    <input type="range" id="restTimeSlider" class="setting-slider" min="1" max="120" value="14">
                    <input type="number" id="restTime" class="setting-value" min="1" max="120" value="14">
                </div>
            </div>
            
            <div class="setting-group">
                <label class="setting-label" for="sessionDuration">Session Duration (minutes)</label>
                <div class="setting-control">
                    <input type="range" id="sessionDurationSlider" class="setting-slider" min="1" max="30" value="6">
                    <input type="number" id="sessionDuration" class="setting-value" min="1" max="30" value="6">
                </div>
            </div>
            
            <div class="setting-group">
                <label class="setting-label" for="delayStart">Delay Start (seconds)</label>
                <div class="setting-control">
                    <input type="range" id="delayStartSlider" class="setting-slider" min="5" max="60" value="20">
                    <input type="number" id="delayStart" class="setting-value" min="5" max="60" value="20">
                </div>
            </div>
            
            <div class="button-group">
                <button id="startBtn" class="btn btn-start">Start</button>
                <button id="resetBtn" class="btn btn-reset">Reset</button>
            </div>
            
            <a href="https://docs.google.com/forms/d/e/1FAIpQLSfB4u9EnmK9VKoObIq4WDFGxPCLSXj4-1KGTPzelkvR7qtkQw/viewform?usp=header" target="_blank" class="feedback-btn">
                💬 Send Feedback
            </a>
        </div>
        
        <!-- Training Screen -->
        <div id="trainingScreen" class="training-screen">
            <button id="resetBtnTraining" class="reset-btn-training">RESET</button>
            <div id="phaseIndicator" class="phase-indicator">GET READY</div>
            <div id="countdown" class="countdown">20</div>
            <div id="sessionInfo" class="session-info">Session: Ready / 6:00</div>
        </div>
    </div>

    <script>
        class BMXTrainer {
            constructor() {
                this.settings = this.loadSettings();
                this.currentPhase = 'delay'; // delay, sprint, rest
                this.timeRemaining = 0;
                this.sessionTimeElapsed = 0;
                this.sessionDurationMs = 0;
                this.interval = null;
                this.sessionInterval = null;
                this.audioContext = null;
                this.bmxBeepSound = null;
                
                this.initializeElements();
                this.loadSettingsToUI();
                this.bindEvents();
                this.initializeAudio();
            }
            
            initializeElements() {
                this.settingsScreen = document.getElementById('settingsScreen');
                this.trainingScreen = document.getElementById('trainingScreen');
                this.phaseIndicator = document.getElementById('phaseIndicator');
                this.countdown = document.getElementById('countdown');
                this.sessionInfo = document.getElementById('sessionInfo');
                
                this.sprintTimeInput = document.getElementById('sprintTime');
                this.restTimeInput = document.getElementById('restTime');
                this.sessionDurationInput = document.getElementById('sessionDuration');
                this.delayStartInput = document.getElementById('delayStart');
                
                this.sprintTimeSlider = document.getElementById('sprintTimeSlider');
                this.restTimeSlider = document.getElementById('restTimeSlider');
                this.sessionDurationSlider = document.getElementById('sessionDurationSlider');
                this.delayStartSlider = document.getElementById('delayStartSlider');
                
                this.startBtn = document.getElementById('startBtn');
                this.resetBtn = document.getElementById('resetBtn');
                this.resetBtnTraining = document.getElementById('resetBtnTraining');
                
                this.howToUse = document.getElementById('howToUse');
                this.howToContent = document.getElementById('howToContent');
                this.expandIcon = document.getElementById('expandIcon');
            }
            
            loadSettings() {
                const defaults = {
                    sprintTime: 6,
                    restTime: 14,
                    sessionDuration: 6,
                    delayStart: 20
                };
                
                return { ...defaults };
            }
            
            saveSettings() {
                this.settings = {
                    sprintTime: parseInt(this.sprintTimeInput.value) || 6,
                    restTime: parseInt(this.restTimeInput.value) || 14,
                    sessionDuration: parseInt(this.sessionDurationInput.value) || 6,
                    delayStart: parseInt(this.delayStartInput.value) || 20
                };
            }
            
            loadSettingsToUI() {
                this.sprintTimeInput.value = this.settings.sprintTime;
                this.restTimeInput.value = this.settings.restTime;
                this.sessionDurationInput.value = this.settings.sessionDuration;
                this.delayStartInput.value = this.settings.delayStart;
                
                this.sprintTimeSlider.value = this.settings.sprintTime;
                this.restTimeSlider.value = this.settings.restTime;
                this.sessionDurationSlider.value = this.settings.sessionDuration;
                this.delayStartSlider.value = this.settings.delayStart;
            }
            
            bindEvents() {
                this.startBtn.addEventListener('click', () => this.startTraining());
                this.resetBtn.addEventListener('click', () => this.resetSettings());
                this.resetBtnTraining.addEventListener('click', () => this.stopTraining());
                
                // How to use toggle
                this.howToUse.addEventListener('click', () => this.toggleHowToUse());
                
                // Sync sliders with number inputs
                this.sprintTimeSlider.addEventListener('input', (e) => {
                    this.sprintTimeInput.value = e.target.value;
                });
                this.sprintTimeInput.addEventListener('input', (e) => {
                    this.sprintTimeSlider.value = e.target.value;
                });
                
                this.restTimeSlider.addEventListener('input', (e) => {
                    this.restTimeInput.value = e.target.value;
                });
                this.restTimeInput.addEventListener('input', (e) => {
                    this.restTimeSlider.value = e.target.value;
                });
                
                this.sessionDurationSlider.addEventListener('input', (e) => {
                    this.sessionDurationInput.value = e.target.value;
                });
                this.sessionDurationInput.addEventListener('input', (e) => {
                    this.sessionDurationSlider.value = e.target.value;
                });
                
                this.delayStartSlider.addEventListener('input', (e) => {
                    this.delayStartInput.value = e.target.value;
                });
                this.delayStartInput.addEventListener('input', (e) => {
                    this.delayStartSlider.value = e.target.value;
                });
            }
            
            initializeAudio() {
                try {
                    this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
                    this.createBMXBeepSound();
                } catch (e) {
                    console.log('Audio not supported');
                }
            }
            
            createBMXBeepSound() {
                this.bmxBeepSound = () => {
                    if (!this.audioContext) return;
                    
                    // Create 4 beeps with 0.1 second gaps
                    for (let i = 0; i < 4; i++) {
                        const startTime = this.audioContext.currentTime + (i * 0.2);
                        
                        const oscillator = this.audioContext.createOscillator();
                        const gainNode = this.audioContext.createGain();
                        
                        oscillator.connect(gainNode);
                        gainNode.connect(this.audioContext.destination);
                        
                        // 630Hz beep
                        oscillator.frequency.setValueAtTime(630, startTime);
                        oscillator.type = 'square';
                        
                        gainNode.gain.setValueAtTime(0, startTime);
                        gainNode.gain.setValueAtTime(0.3, startTime);
                        gainNode.gain.exponentialRampToValueAtTime(0.01, startTime + 0.1);
                        
                        oscillator.start(startTime);
                        oscillator.stop(startTime + 0.1);
                    }
                };
            }
            
            playBMXBeep() {
                if (this.bmxBeepSound) {
                    if (this.audioContext.state === 'suspended') {
                        this.audioContext.resume();
                    }
                    this.bmxBeepSound();
                }
            }
            
            toggleHowToUse() {
                const isVisible = this.howToContent.classList.contains('show');
                if (isVisible) {
                    this.howToContent.classList.remove('show');
                    this.expandIcon.classList.remove('expanded');
                } else {
                    this.howToContent.classList.add('show');
                    this.expandIcon.classList.add('expanded');
                }
            }
            
            startTraining() {
                this.saveSettings();
                this.sessionTimeElapsed = 0;
                this.sessionDurationMs = this.settings.sessionDuration * 60 * 1000;
                
                this.settingsScreen.style.display = 'none';
                this.trainingScreen.style.display = 'flex';
                
                this.startDelayPhase();
            }
            
            startSessionTimer() {
                this.sessionInterval = setInterval(() => {
                    this.sessionTimeElapsed += 100;
                    this.updateSessionInfo();
                    
                    if (this.sessionTimeElapsed >= this.sessionDurationMs) {
                        this.stopTraining();
                    }
                }, 100);
            }
            
            updateSessionInfo() {
                const elapsed = Math.floor(this.sessionTimeElapsed / 1000);
                const total = this.settings.sessionDuration * 60;
                const elapsedMin = Math.floor(elapsed / 60);
                const elapsedSec = elapsed % 60;
                const totalMin = Math.floor(total / 60);
                const totalSec = total % 60;
                
                if (this.currentPhase === 'delay') {
                    this.sessionInfo.textContent = 
                        `Session: Ready / ${totalMin}:${totalSec.toString().padStart(2, '0')}`;
                } else {
                    this.sessionInfo.textContent = 
                        `Session: ${elapsedMin}:${elapsedSec.toString().padStart(2, '0')} / ${totalMin}:${totalSec.toString().padStart(2, '0')}`;
                }
            }
            
            startDelayPhase() {
                this.currentPhase = 'delay';
                this.timeRemaining = this.settings.delayStart;
                this.phaseIndicator.textContent = 'GET READY';
                document.body.className = 'delay-screen';
                this.updateSessionInfo();
                this.startCountdown(() => {
                    this.startSessionTimer();
                    this.startSprintPhase();
                });
            }
            
            startSprintPhase() {
                this.currentPhase = 'sprint';
                this.timeRemaining = this.settings.sprintTime;
                this.phaseIndicator.textContent = 'SPRINT!';
                document.body.className = 'sprint-screen';
                this.playBMXBeep();
                this.startCountdown(() => this.startRestPhase());
            }
            
            startRestPhase() {
                this.currentPhase = 'rest';
                this.timeRemaining = this.settings.restTime;
                this.phaseIndicator.textContent = 'REST';
                document.body.className = 'rest-screen';
                this.startCountdown(() => {
                    if (this.sessionTimeElapsed < this.sessionDurationMs) {
                        this.startSprintPhase();
                    } else {
                        this.stopTraining();
                    }
                });
            }
            
            startCountdown(callback) {
                this.countdown.textContent = this.timeRemaining;
                
                this.interval = setInterval(() => {
                    this.timeRemaining--;
                    this.countdown.textContent = this.timeRemaining;
                    
                    if (this.timeRemaining <= 0) {
                        clearInterval(this.interval);
                        callback();
                    }
                }, 1000);
            }
            
            stopTraining() {
                if (this.interval) clearInterval(this.interval);
                if (this.sessionInterval) clearInterval(this.sessionInterval);
                
                document.body.className = '';
                this.trainingScreen.style.display = 'none';
                this.settingsScreen.style.display = 'block';
            }
            
            resetSettings() {
                this.sprintTimeInput.value = 6;
                this.restTimeInput.value = 14;
                this.sessionDurationInput.value = 6;
                this.delayStartInput.value = 20;
                
                this.sprintTimeSlider.value = 6;
                this.restTimeSlider.value = 14;
                this.sessionDurationSlider.value = 6;
                this.delayStartSlider.value = 20;
            }
        }
        
        document.addEventListener('DOMContentLoaded', () => {
            new BMXTrainer();
        });
    </script>
</body>
</html>
