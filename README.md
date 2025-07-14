
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบแปลภาษาไทยเป็นอังกฤษด้วยเสียง (Gemini AI)</title>
    <link rel="icon" href="https://makubtrader.com/ccdc/Favicon.png" type="image/png" sizes="16x16">
    <link rel="icon" href="https://makubtrader.com/ccdc/Favicon.png" type="image/png" sizes="32x32">
    <link rel="apple-touch-icon" href="https://makubtrader.com/ccdc/Favicon.png">
    <link rel="shortcut icon" href="https://makubtrader.com/ccdc/Favicon.png">
    <link href="https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        /* General Styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Sarabun', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            color: #333;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            max-width: 800px;
            width: 100%;
            backdrop-filter: blur(10px);
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 2.8em;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            font-weight: 600;
        }

        .section {
            margin-bottom: 30px;
            padding: 25px;
            background: white;
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border: 1px solid rgba(102, 126, 234, 0.1);
        }

        .section h2 {
            color: #555;
            margin-bottom: 20px;
            font-size: 1.6em;
            display: flex;
            align-items: center;
            gap: 10px;
            font-weight: 500;
        }

        .icon {
            font-size: 1.2em;
            color: #764ba2;
        }

        /* API Key Section - ส่วนที่สำคัญ */
        .api-setup {
            margin-bottom: 30px;
            padding: 25px;
            background: linear-gradient(135deg, #f8f9ff 0%, #e8f2ff 100%);
            border-radius: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            border: 2px solid #667eea;
            position: relative;
            overflow: hidden;
        }

        .api-setup::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(45deg, #667eea, #764ba2);
        }

        .api-setup .warning {
            background: #fff3cd;
            border-left: 5px solid #ffc107;
            padding: 15px;
            margin-bottom: 20px;
            border-radius: 8px;
            font-size: 0.95em;
            color: #856404;
            line-height: 1.6;
        }

        .api-setup .warning a {
            color: #667eea;
            font-weight: bold;
            text-decoration: none;
            border-bottom: 1px dotted #667eea;
        }

        .api-setup .warning a:hover {
            text-decoration: underline;
            color: #5a67d8;
        }

        .api-input-group {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }

        .api-input {
            flex: 1;
            min-width: 250px;
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 1em;
            background: white;
            transition: all 0.3s ease;
            font-family: 'Courier New', monospace;
        }

        .api-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .api-input::placeholder {
            color: #a0aec0;
            font-style: italic;
        }

        .api-btn {
            padding: 15px 20px;
            border: none;
            border-radius: 10px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1em;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }

        .api-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }

        .api-btn.remove {
            background: linear-gradient(45deg, #ff6b6b, #ee5a6f);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .api-btn.remove:hover {
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
        }

        .api-btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        .api-status {
            margin-top: 15px;
            padding: 12px 15px;
            border-radius: 8px;
            font-size: 0.95em;
            font-weight: 600;
            text-align: center;
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            cursor: pointer; /* เพิ่ม cursor: pointer เพื่อบ่งบอกว่าคลิกได้ */
        }

        .api-status::before {
            content: '✅';
            font-size: 1.2em;
        }

        /* Voice Controls */
        .voice-controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .btn {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            display: flex;
            align-items: center;
            gap: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }

        .btn-primary {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }

        .btn-danger {
            background: linear-gradient(45deg, #ff6b6b, #ee4c77);
            color: white;
        }

        .btn-success {
            background: linear-gradient(45deg, #2ecc71, #27ae60);
            color: white;
        }

        .btn-info {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }

        .recording {
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); }
            50% { transform: scale(1.03); box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2); }
            100% { transform: scale(1); box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); }
        }

        textarea {
            width: 100%;
            min-height: 120px;
            padding: 15px;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            font-size: 1.1em;
            font-family: inherit;
            resize: vertical;
            transition: border-color 0.3s ease, background 0.3s ease;
            background: #fafafa;
        }

        textarea:focus {
            outline: none;
            border-color: #667eea;
            background: white;
        }

        .status {
            margin-top: 15px;
            padding: 12px;
            border-radius: 8px;
            font-weight: 500;
            text-align: center;
            transition: all 0.3s ease;
            font-size: 0.95em;
        }

        .status.listening {
            background: #e3f2fd;
            color: #1976d2;
            border: 1px solid #90caf9;
        }

        .status.processing {
            background: #fff3e0;
            color: #f57c00;
            border: 1px solid #ffcc02;
        }

        .status.error {
            background: #ffebee;
            color: #d32f2f;
            border: 1px solid #ffcdd2;
        }

        .status.success {
            background: #e8f5e8;
            color: #2e7d32;
            border: 1px solid #c8e6c9;
        }

        .status.info {
            background: #e3f2fd;
            color: #1976d2;
            border: 1px solid #90caf9;
        }

        .translate-btn {
            width: 100%;
            margin-top: 15px;
            padding: 15px;
            font-size: 18px;
        }

        .result-section {
            background: linear-gradient(135deg, #f5f7fa 0%, #e0e6f0 100%);
        }

        .wave-animation {
            display: inline-block;
            width: 20px;
            height: 20px;
            background: currentColor;
            border-radius: 50%;
            animation: wave 1.4s ease-in-out infinite both;
        }

        @keyframes wave {
            0%, 40%, 100% { transform: scaleY(0.4); }
            20% { transform: scaleY(1.0); }
        }

        /* Responsive Adjustments */
        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 2.2em;
            }
            
            .voice-controls {
                flex-direction: column;
                gap: 10px;
            }
            
            .btn {
                justify-content: center;
                width: 100%;
            }

            .api-input-group {
                flex-direction: column;
            }

            .api-input {
                min-width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎤 ระบบแปลภาษาไทยเป็นอังกฤษ</h1>
        
        <div class="api-setup" id="apiSetupSection">
            <h2><span class="icon">🔑</span> ตั้งค่า Gemini API Key</h2>
            <div class="warning">
                ⚠️ <strong>คำเตือนด้านความปลอดภัย:</strong> API Key ของคุณจะถูกเก็บในเบราว์เซอร์เท่านั้น และจะถูกล้างหากคุณล้างข้อมูลการเข้าชมเว็บไซต์<br>
                📝 หากยังไม่มี API Key สามารถสร้างได้ฟรีที่ 
                <a href="https://aistudio.google.com/app/apikey" target="_blank">Google AI Studio</a><br>
                💡 <strong>วิธีใช้:</strong> ใส่ API Key → กดบันทึก → เริ่มใช้งานได้เลย!
            </div>
            
            <div class="api-input-group">
                <input 
                    type="password" 
                    id="apiKeyInput" 
                    class="api-input" 
                    placeholder="ใส่ Gemini API Key ของคุณที่นี่... (เช่น: AIzaSyC...)" 
                    autocomplete="off"
                >
                <button class="api-btn" id="saveApiKeyBtn">
                    💾 บันทึก API Key
                </button>
            </div>
            
            <button class="api-btn remove" id="removeApiKeyBtn" style="display: none;">
                🗑️ ลบ API Key
            </button>
        </div>

        <div id="apiKeyStatusDisplay" class="api-status" style="display: none;">
            API Key ถูกตั้งค่าเรียบร้อยแล้ว! คลิกเพื่อแก้ไข.
        </div>

        <div class="section">
            <h2><span class="icon">🎙️</span> การบันทึกเสียง</h2>
            <div class="voice-controls">
                <button class="btn btn-primary" id="startBtn" disabled>
                    <span>🎤</span> เริ่มบันทึกเสียง
                </button>
                <button class="btn btn-danger" id="stopBtn" disabled>
                    <span>⏹️</span> หยุดบันทึก
                </button>
                <button class="btn btn-success" id="clearBtn">
                    <span>🗑️</span> ล้างข้อมูล
                </button>
            </div>
            <div class="status" id="status">กรุณาใส่ Gemini API Key ก่อนใช้งาน</div>
        </div>

        <div class="section">
            <h2><span class="icon">🇹🇭</span> ข้อความภาษาไทย</h2>
            <textarea id="thaiText" placeholder="พิมพ์ข้อความภาษาไทยหรือใช้การบันทึกเสียง..."></textarea>
            <button class="btn btn-primary translate-btn" id="translateBtn" disabled>
                <span>🔄</span> แปลเป็นภาษาอังกฤษ
            </button>
        </div>

        <div class="section result-section">
            <h2><span class="icon">🇺🇸</span> ผลการแปล (ภาษาอังกฤษ)</h2>
            <textarea id="englishText" placeholder="ผลการแปลจะแสดงที่นี่..." readonly></textarea>
            <button class="btn btn-info translate-btn" id="listenEnglishBtn" disabled>
                <span>🔊</span> อ่านออกเสียง (อังกฤษ)
            </button>
        </div>
    </div>

    <script>
        class ThaiVoiceTranslator {
            constructor() {
                this.recognition = null;
                this.isRecording = false;
                this.geminiApiKey = localStorage.getItem('geminiApiKey') || '';
                this.speechSynthesisUtterance = null;

                this.initializeElements();
                this.setupSpeechRecognition();
                this.setupEventListeners();
                this.checkApiKeyStatus();
            }

            initializeElements() {
                this.apiSetupSection = document.getElementById('apiSetupSection'); // ส่วน API Key ทั้งหมด
                this.apiKeyInput = document.getElementById('apiKeyInput');
                this.saveApiKeyBtn = document.getElementById('saveApiKeyBtn');
                this.removeApiKeyBtn = document.getElementById('removeApiKeyBtn');
                this.apiKeyStatusDisplay = document.getElementById('apiKeyStatusDisplay'); // สถานะที่แสดงแทนส่วน API Key

                this.startBtn = document.getElementById('startBtn');
                this.stopBtn = document.getElementById('stopBtn');
                this.clearBtn = document.getElementById('clearBtn');
                this.translateBtn = document.getElementById('translateBtn');
                this.listenEnglishBtn = document.getElementById('listenEnglishBtn');
                this.statusDiv = document.getElementById('status');
                this.thaiText = document.getElementById('thaiText');
                this.englishText = document.getElementById('englishText');
            }

            checkApiKeyStatus() {
                if (this.geminiApiKey) {
                    this.apiSetupSection.style.display = 'none'; // ซ่อนส่วน API Key
                    this.apiKeyStatusDisplay.style.display = 'flex'; // แสดงสถานะ API Key
                    this.updateStatus('พร้อมใช้งาน! กดปุ่ม "เริ่มบันทึกเสียง" เพื่อเริ่มต้น', 'success');
                    this.enableAllFeatures();
                } else {
                    this.apiSetupSection.style.display = 'block'; // แสดงส่วน API Key
                    this.apiKeyInput.value = '';
                    this.apiKeyInput.disabled = false;
                    this.saveApiKeyBtn.style.display = 'inline-block';
                    this.removeApiKeyBtn.style.display = 'none';
                    this.apiKeyStatusDisplay.style.display = 'none'; // ซ่อนสถานะ API Key
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    this.disableAllFeatures();
                }
            }

            enableAllFeatures() {
                this.startBtn.disabled = false;
                this.updateTranslateButtonState();
            }

            disableAllFeatures() {
                this.startBtn.disabled = true;
                this.translateBtn.disabled = true;
                this.stopBtn.disabled = true;
                this.listenEnglishBtn.disabled = true;
            }

            saveApiKey() {
                const inputKey = this.apiKeyInput.value.trim();
                if (!inputKey) {
                    alert('กรุณาใส่ Gemini API Key ก่อนบันทึก');
                    return;
                }
                
                // Basic validation for API key length
                if (inputKey.length < 20 || !inputKey.startsWith('AIza')) { // Common prefix for Google API keys
                    alert('API Key ดูเหมือนจะไม่ถูกต้อง กรุณาตรวจสอบอีกครั้ง (เช่น: AIzaSyC...)');
                    return;
                }

                this.geminiApiKey = inputKey;
                localStorage.setItem('geminiApiKey', this.geminiApiKey);
                this.checkApiKeyStatus(); // เรียกเพื่อซ่อนส่วน API Key
                this.updateStatus('บันทึก API Key เรียบร้อย! พร้อมใช้งาน', 'success');
            }

            removeApiKey() {
                if (confirm('คุณแน่ใจหรือไม่ว่าต้องการลบ API Key?')) {
                    localStorage.removeItem('geminiApiKey');
                    this.geminiApiKey = '';
                    this.checkApiKeyStatus(); // เรียกเพื่อแสดงส่วน API Key อีกครั้ง
                    this.clearAll();
                    this.updateStatus('ลบ API Key เรียบร้อย กรุณาใส่ API Key ใหม่', 'info');
                }
            }

            setupSpeechRecognition() {
                if (!('webkitSpeechRecognition' in window) && !('SpeechRecognition' in window)) {
                    this.updateStatus('เบราว์เซอร์ของคุณไม่รองรับการรู้จำเสียง โปรดใช้ Chrome หรือ Edge', 'error');
                    return;
                }

                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                this.recognition = new SpeechRecognition();
                
                this.recognition.continuous = true;
                this.recognition.interimResults = true;
                this.recognition.lang = 'th-TH'; // ตั้งค่าภาษาเป็นภาษาไทย

                this.recognition.onstart = () => {
                    this.isRecording = true;
                    this.updateStatus('กำลังฟัง... <span class="wave-animation"></span>', 'listening');
                    this.startBtn.disabled = true;
                    this.stopBtn.disabled = false;
                    this.startBtn.classList.add('recording');
                    this.thaiText.value = ''; // เคลียร์ข้อความเก่าเมื่อเริ่มบันทึกใหม่
                    this.englishText.value = ''; // เคลียร์ผลแปลเก่าด้วย
                    this.updateListenButtonState(); // อัปเดตสถานะปุ่มอ่านออกเสียง
                };

                this.recognition.onresult = (event) => {
                    let finalTranscript = '';
                    let interimTranscript = '';

                    for (let i = event.resultIndex; i < event.results.length; i++) {
                        const transcript = event.results[i][0].transcript;
                        if (event.results[i].isFinal) {
                            finalTranscript += transcript;
                        } else {
                            interimTranscript += transcript;
                        }
                    }

                    this.thaiText.value = finalTranscript + interimTranscript;
                    
                    if (finalTranscript) {
                        this.updateStatus('พบข้อความแล้ว กำลังรอให้คุณพูดจบ...', 'success');
                    }
                    this.updateTranslateButtonState();
                };

                this.recognition.onerror = (event) => {
                    let errorMessage = 'เกิดข้อผิดพลาดในการรู้จำเสียง';
                    if (event.error === 'no-speech') {
                        errorMessage = 'ไม่พบเสียงพูด';
                    } else if (event.error === 'not-allowed') {
                        errorMessage = 'ไม่ได้รับอนุญาตให้ใช้ไมโครโฟน กรุณาอนุญาตในเบราว์เซอร์';
                    } else if (event.error === 'aborted') {
                        errorMessage = 'การบันทึกเสียงถูกยกเลิก';
                    }
                    this.updateStatus(errorMessage, 'error');
                    this.stopRecording();
                };

                this.recognition.onend = () => {
                    this.stopRecording();
                    if (this.thaiText.value.trim()) {
                        this.updateStatus('บันทึกเสียงเสร็จสิ้น กำลังแปลภาษา...', 'processing'); // อัปเดตสถานะก่อนแปล
                        this.translateText(); // เรียกฟังก์ชันแปลภาษาอัตโนมัติ
                    } else { // หากไม่มีข้อความจากการบันทึกเสียง
                        this.updateStatus('กดปุ่ม "เริ่มบันทึกเสียง" เพื่อเริ่มต้น', 'info');
                    }
                };
            }

            setupEventListeners() {
                this.saveApiKeyBtn.addEventListener('click', () => this.saveApiKey());
                this.removeApiKeyBtn.addEventListener('click', () => this.removeApiKey());
                this.apiKeyInput.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') this.saveApiKey();
                });
                // เพิ่ม Event Listener สำหรับการคลิกที่สถานะ API Key
                this.apiKeyStatusDisplay.addEventListener('click', () => {
                    this.apiSetupSection.style.display = 'block'; // แสดงส่วน API Key
                    this.apiKeyStatusDisplay.style.display = 'none'; // ซ่อนสถานะ API Key
                    this.apiKeyInput.value = this.geminiApiKey; // แสดง key เต็มๆ ในช่อง input
                    this.apiKeyInput.disabled = false;
                    this.saveApiKeyBtn.style.display = 'inline-block';
                    this.removeApiKeyBtn.style.display = 'inline-block';
                    this.apiKeyInput.focus(); // ให้ cursor ไปที่ input เพื่อแก้ไขได้เลย
                    this.updateStatus('คุณกำลังแก้ไข API Key', 'info');
                    this.disableAllFeatures(); // ปิดการใช้งานอื่นๆ ชั่วคราว
                });
                
                this.startBtn.addEventListener('click', () => this.startRecording());
                this.stopBtn.addEventListener('click', () => this.stopRecording());
                this.clearBtn.addEventListener('click', () => this.clearAll());
                this.translateBtn.addEventListener('click', () => this.translateText());
                this.listenEnglishBtn.addEventListener('click', () => this.speakEnglishText());
                
                // ตรวจสอบการเปลี่ยนแปลงของ Thai text เพื่ออัปเดตสถานะปุ่มแปล
                this.thaiText.addEventListener('input', () => this.updateTranslateButtonState());
                // ตรวจสอบการเปลี่ยนแปลงของ English text เพื่ออัปเดตสถานะปุ่มอ่านออกเสียง
                this.englishText.addEventListener('input', () => this.updateListenButtonState());
            }

            updateStatus(message, type) {
                this.statusDiv.innerHTML = message;
                this.statusDiv.className = 'status'; // Reset classes
                if (type) {
                    this.statusDiv.classList.add(type);
                }
            }

            updateTranslateButtonState() {
                this.translateBtn.disabled = !this.thaiText.value.trim() || !this.geminiApiKey;
            }

            updateListenButtonState() {
                this.listenEnglishBtn.disabled = !this.englishText.value.trim();
            }

            startRecording() {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return;
                }
                if (this.recognition && !this.isRecording) {
                    this.recognition.start();
                }
            }

            stopRecording() {
                if (this.recognition && this.isRecording) {
                    this.recognition.stop();
                }
                this.isRecording = false;
                this.startBtn.disabled = !this.geminiApiKey; // ถ้าไม่มี API Key ปุ่มก็ยังปิดอยู่
                this.stopBtn.disabled = true;
                this.startBtn.classList.remove('recording');
            }

            clearAll() {
                this.thaiText.value = '';
                this.englishText.value = '';
                if(this.geminiApiKey) { // หากมี API Key อยู่แล้ว ค่อยแสดงสถานะว่าล้างข้อมูลสำเร็จ
                    this.updateStatus('ล้างข้อมูลเรียบร้อย', 'success');
                } else { // ถ้าไม่มี API Key ก็กลับไปสถานะให้ใส่ API Key
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                }
                this.updateTranslateButtonState();
                this.updateListenButtonState();
                
                if (this.isRecording) {
                    this.stopRecording();
                }
                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel();
                }
            }

            async translateText() {
                const text = this.thaiText.value.trim();
                if (!text) {
                    this.updateStatus('กรุณากรอกข้อความภาษาไทย', 'error');
                    this.englishText.value = '';
                    this.updateListenButtonState();
                    return;
                }
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    this.englishText.value = '';
                    this.updateListenButtonState();
                    return;
                }

                this.updateStatus('กำลังแปลภาษา...', 'processing');
                this.translateBtn.disabled = true;
                this.englishText.value = 'Translating...'; // แสดงข้อความกำลังแปล

                try {
                    // *** แก้ไขตรงนี้: เปลี่ยนโมเดลเป็น gemini-1.5-flash ***
                    const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${this.geminiApiKey}`;
                    
                    // ปรับ Prompt ให้ชัดเจนขึ้น
                    const prompt = `Translate the following Thai text to English. Respond only with the English translation, without any additional comments, prefixes, or explanations, and avoid markdown if possible.
                    
                    Thai: "${text}"
                    
                    English:`;

                    const response = await fetch(API_URL, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                        body: JSON.stringify({
                            contents: [{ parts: [{ text: prompt }] }],
                            generationConfig: { 
                                temperature: 0.2, // สามารถปรับค่านี้ได้ (0.0-1.0) เพื่อควบคุมความคิดสร้างสรรค์ (ต่ำ = ตรงตัว, สูง = สร้างสรรค์)
                                maxOutputTokens: 200 // จำกัดจำนวน token ของผลลัพธ์
                            }
                        })
                    });

                    if (!response.ok) {
                           const errorData = await response.json();
                           // ตรวจสอบ error code จาก Gemini API เพื่อให้ข้อความละเอียดขึ้น
                           if (errorData.error && errorData.error.status === 'RESOURCE_EXHAUSTED') {
                                throw new Error('โควต้าการใช้งาน API หมด กรุณาลองใหม่ภายหลัง หรือตรวจสอบการเรียกใช้งาน');
                           }
                           throw new Error(errorData.error.message || `HTTP error! status: ${response.status}`);
                    }

                    const data = await response.json();
                    
                    if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts[0]) {
                        let translatedText = data.candidates[0].content.parts[0].text.trim();
                        // บางครั้ง Gemini อาจจะเพิ่ม "English:" มาให้ ถึงแม้จะสั่งแล้วก็ตาม
                        if (translatedText.toLowerCase().startsWith('english:')) {
                            translatedText = translatedText.substring('english:'.length).trim();
                        }
                        this.englishText.value = translatedText;
                        this.updateStatus('แปลภาษาเสร็จสิ้น', 'success');
                        this.updateListenButtonState();
                        this.speakEnglishText(); // เรียกอ่านออกเสียงอัตโนมัติเมื่อแปลเสร็จ
                    } else {
                        // เพิ่มการตรวจสอบกรณีที่โมเดลอาจจะถูก blocked หรือไม่ให้ผลลัพธ์
                        if (data.promptFeedback && data.promptFeedback.blockReason) {
                            throw new Error(`คำร้องขอถูกบล็อก: ${data.promptFeedback.blockReason}. อาจเป็นเพราะเนื้อหาไม่เหมาะสม.`);
                        }
                        throw new Error('ไม่ได้รับการตอบสนองที่คาดหวังจาก Gemini API หรือผลลัพธ์ว่างเปล่า');
                    }
                } catch (error) {
                    console.error('Translation error with Gemini:', error);
                    let errorMessage = 'ไม่สามารถแปลภาษาได้';
                    if (error.message.includes('API key not valid')) {
                        errorMessage = 'API Key ไม่ถูกต้อง กรุณาตรวจสอบและใส่ใหม่';
                    } else if (error.message.includes('Quota') || error.message.includes('โควต้า')) {
                        errorMessage = 'โควต้าการใช้งาน API หมด กรุณาลองใหม่ภายหลัง';
                    } else if (error.message.includes('blocked')) {
                        errorMessage = `เกิดข้อผิดพลาด: ${error.message}`;
                    }
                    else {
                        errorMessage = `เกิดข้อผิดพลาด: ${error.message}`;
                    }
                    this.updateStatus(errorMessage, 'error');
                    this.englishText.value = `Error: ${errorMessage}`;
                } finally {
                    this.translateBtn.disabled = !this.thaiText.value.trim() || !this.geminiApiKey; // ให้ปุ่มกลับมาใช้งานได้ถ้ามีข้อความและ API Key
                }
            }

            speakEnglishText() {
                const text = this.englishText.value.trim();
                if (!text) {
                    this.updateStatus('ไม่มีข้อความภาษาอังกฤษให้อ่าน', 'info');
                    return;
                }

                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel(); // หยุดการอ่านเสียงที่กำลังดำเนินอยู่
                }

                this.speechSynthesisUtterance = new SpeechSynthesisUtterance(text);
                this.speechSynthesisUtterance.lang = 'en-US'; // ตั้งค่าภาษาเป็นภาษาอังกฤษ
                // สามารถเลือก voice ได้ถ้าต้องการ
                // const voices = window.speechSynthesis.getVoices();
                // this.speechSynthesisUtterance.voice = voices.find(voice => voice.lang === 'en-US');

                this.speechSynthesisUtterance.onerror = (event) => {
                    console.error('Speech synthesis error:', event.error);
                    this.updateStatus(`ไม่สามารถอ่านออกเสียงได้: ${event.error}`, 'error');
                };
                this.speechSynthesisUtterance.onstart = () => {
                    this.updateStatus('กำลังอ่านออกเสียง...', 'processing');
                    this.listenEnglishBtn.disabled = true; // ปิดปุ่มระหว่างอ่าน
                };
                this.speechSynthesisUtterance.onend = () => {
                    this.updateStatus('อ่านออกเสียงเสร็จสิ้น', 'success');
                    this.listenEnglishBtn.disabled = false; // เปิดปุ่มเมื่ออ่านจบ
                };

                window.speechSynthesis.speak(this.speechSynthesisUtterance);
            }
        }

        // เมื่อ DOM โหลดเสร็จ ให้เริ่มต้นการทำงานของ Translator
        document.addEventListener('DOMContentLoaded', () => {
            new ThaiVoiceTranslator();
        });
    </script>
</body>
</html>
