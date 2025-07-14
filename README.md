<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบแปลภาษา (ไทย ↔ อังกฤษ) ด้วยเสียง (Gemini AI)</title>
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
        <h1>🎤 ระบบแปลภาษา (ไทย ↔ อังกฤษ)</h1>
        
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
            <h2><span class="icon">🇹🇭➡️🇺🇸</span> ไทย ➡️ อังกฤษ</h2>
            <div class="voice-controls">
                <button class="btn btn-primary" id="startThaiBtn" disabled>
                    <span>🎤</span> เริ่มพูด (ไทย)
                </button>
                <button class="btn btn-danger" id="stopThaiBtn" disabled>
                    <span>⏹️</span> หยุดบันทึก
                </button>
                <button class="btn btn-success" id="clearAllBtn">
                    <span>🗑️</span> ล้างข้อมูลทั้งหมด
                </button>
            </div>
            <div class="status" id="status">กรุณาใส่ Gemini API Key ก่อนใช้งาน</div>
            
            <h3>ข้อความภาษาไทย:</h3>
            <textarea id="thaiText" placeholder="พูดหรือพิมพ์ข้อความภาษาไทย..."></textarea>
            <button class="btn btn-primary translate-btn" id="translateThaiToEnglishBtn" disabled>
                <span>🔄</span> แปลเป็นภาษาอังกฤษ
            </button>
            
            <h3 style="margin-top: 20px;">ผลการแปล (ภาษาอังกฤษ):</h3>
            <textarea id="englishText" placeholder="ผลการแปลจะแสดงที่นี่..." readonly></textarea>
            <button class="btn btn-info translate-btn" id="listenEnglishBtn" disabled>
                <span>🔊</span> อ่านออกเสียง (อังกฤษ)
            </button>
        </div>

        <div class="section result-section">
            <h2><span class="icon">🇺🇸➡️🇹🇭</span> อังกฤษ ➡️ ไทย</h2>
            <div class="voice-controls">
                <button class="btn btn-info" id="startEnglishBtn" disabled>
                    <span>🎙️</span> เริ่มพูด (อังกฤษ)
                </button>
                <button class="btn btn-danger" id="stopEnglishBtn" disabled>
                    <span>⏹️</span> หยุดบันทึก
                </button>
            </div>
            
            <h3>ข้อความภาษาอังกฤษ:</h3>
            <textarea id="englishListenText" placeholder="พูดหรือพิมพ์ข้อความภาษาอังกฤษ..."></textarea>
            <button class="btn btn-primary translate-btn" id="translateEnglishToThaiBtn" disabled>
                <span>🔄</span> แปลเป็นภาษาไทย
            </button>
            
            <h3 style="margin-top: 20px;">ผลการแปล (ภาษาไทย):</h3>
            <textarea id="thaiTranslatedText" placeholder="ผลการแปลจะแสดงที่นี่..." readonly></textarea>
            <button class="btn btn-success translate-btn" id="listenThaiBtn" disabled>
                <span>🔊</span> อ่านออกเสียง (ไทย)
            </button>
        </div>
    </div>

    <script>
        class BiDirectionalVoiceTranslator {
            constructor() {
                this.recognitionThai = null;
                this.recognitionEnglish = null;
                this.isRecordingThai = false;
                this.isRecordingEnglish = false;
                this.geminiApiKey = localStorage.getItem('geminiApiKey') || '';
                this.speechSynthesisUtterance = null; // For en-US voice
                this.speechSynthesisUtteranceThai = null; // For th-TH voice

                this.initializeElements();
                this.setupSpeechRecognitions();
                this.setupEventListeners();
                this.checkApiKeyStatus();
            }

            initializeElements() {
                this.apiSetupSection = document.getElementById('apiSetupSection');
                this.apiKeyInput = document.getElementById('apiKeyInput');
                this.saveApiKeyBtn = document.getElementById('saveApiKeyBtn');
                this.removeApiKeyBtn = document.getElementById('removeApiKeyBtn');
                this.apiKeyStatusDisplay = document.getElementById('apiKeyStatusDisplay');

                // Thai to English elements
                this.startThaiBtn = document.getElementById('startThaiBtn');
                this.stopThaiBtn = document.getElementById('stopThaiBtn');
                this.clearAllBtn = document.getElementById('clearAllBtn');
                this.statusDiv = document.getElementById('status');
                this.thaiText = document.getElementById('thaiText');
                this.translateThaiToEnglishBtn = document.getElementById('translateThaiToEnglishBtn');
                this.englishText = document.getElementById('englishText');
                this.listenEnglishBtn = document.getElementById('listenEnglishBtn');

                // English to Thai elements
                this.startEnglishBtn = document.getElementById('startEnglishBtn');
                this.stopEnglishBtn = document.getElementById('stopEnglishBtn');
                this.englishListenText = document.getElementById('englishListenText');
                this.translateEnglishToThaiBtn = document.getElementById('translateEnglishToThaiBtn');
                this.thaiTranslatedText = document.getElementById('thaiTranslatedText');
                this.listenThaiBtn = document.getElementById('listenThaiBtn');
            }

            checkApiKeyStatus() {
                if (this.geminiApiKey) {
                    this.apiSetupSection.style.display = 'none';
                    this.apiKeyStatusDisplay.style.display = 'flex';
                    this.updateStatus('พร้อมใช้งาน! เลือกโหมดที่ต้องการ', 'success');
                    this.enableAllFeatures();
                } else {
                    this.apiSetupSection.style.display = 'block';
                    this.apiKeyInput.value = '';
                    this.apiKeyInput.disabled = false;
                    this.saveApiKeyBtn.style.display = 'inline-block';
                    this.removeApiKeyBtn.style.display = 'none';
                    this.apiKeyStatusDisplay.style.display = 'none';
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    this.disableAllFeatures();
                }
            }

            enableAllFeatures() {
                this.startThaiBtn.disabled = false;
                this.startEnglishBtn.disabled = false;
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            disableAllFeatures() {
                this.startThaiBtn.disabled = true;
                this.stopThaiBtn.disabled = true;
                this.translateThaiToEnglishBtn.disabled = true;
                this.listenEnglishBtn.disabled = true;

                this.startEnglishBtn.disabled = true;
                this.stopEnglishBtn.disabled = true;
                this.translateEnglishToThaiBtn.disabled = true;
                this.listenThaiBtn.disabled = true;
            }

            saveApiKey() {
                const inputKey = this.apiKeyInput.value.trim();
                if (!inputKey) {
                    alert('กรุณาใส่ Gemini API Key ก่อนบันทึก');
                    return;
                }
                if (inputKey.length < 20 || !inputKey.startsWith('AIza')) {
                    alert('API Key ดูเหมือนจะไม่ถูกต้อง กรุณาตรวจสอบอีกครั้ง (เช่น: AIzaSyC...)');
                    return;
                }

                this.geminiApiKey = inputKey;
                localStorage.setItem('geminiApiKey', this.geminiApiKey);
                this.checkApiKeyStatus();
                this.updateStatus('บันทึก API Key เรียบร้อย! พร้อมใช้งาน', 'success');
            }

            removeApiKey() {
                if (confirm('คุณแน่ใจหรือไม่ว่าต้องการลบ API Key?')) {
                    localStorage.removeItem('geminiApiKey');
                    this.geminiApiKey = '';
                    this.checkApiKeyStatus();
                    this.clearAll();
                    this.updateStatus('ลบ API Key เรียบร้อย กรุณาใส่ API Key ใหม่', 'info');
                }
            }

            setupSpeechRecognitions() {
                if (!('webkitSpeechRecognition' in window) && !('SpeechRecognition' in window)) {
                    this.updateStatus('เบราว์เซอร์ของคุณไม่รองรับการรู้จำเสียง โปรดใช้ Chrome หรือ Edge', 'error');
                    return;
                }

                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;

                // Thai Recognition
                this.recognitionThai = new SpeechRecognition();
                this.recognitionThai.continuous = true;
                this.recognitionThai.interimResults = true;
                this.recognitionThai.lang = 'th-TH';

                this.recognitionThai.onstart = () => {
                    this.isRecordingThai = true;
                    this.updateStatus('กำลังฟัง (ไทย)... <span class="wave-animation"></span>', 'listening');
                    this.startThaiBtn.disabled = true;
                    this.stopThaiBtn.disabled = false;
                    this.startThaiBtn.classList.add('recording');
                    this.thaiText.value = '';
                    this.englishText.value = '';
                    this.updateListenButtonStates();
                };
                this.recognitionThai.onresult = (event) => {
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
                        this.updateStatus('พบข้อความไทยแล้ว กำลังรอให้คุณพูดจบ...', 'success');
                    }
                    this.updateTranslateButtonStates();
                };
                this.recognitionThai.onerror = (event) => {
                    this.handleRecognitionError(event, 'ไทย');
                    this.stopRecordingThai();
                };
                this.recognitionThai.onend = () => {
                    this.stopRecordingThai();
                    if (this.thaiText.value.trim()) {
                        this.updateStatus('บันทึกเสียงไทยเสร็จสิ้น กำลังแปลภาษา...', 'processing');
                        this.translateThaiToEnglish();
                    } else {
                        this.updateStatus('กดปุ่ม "เริ่มพูด (ไทย)" เพื่อเริ่มต้น', 'info');
                    }
                };

                // English Recognition
                this.recognitionEnglish = new SpeechRecognition();
                this.recognitionEnglish.continuous = true;
                this.recognitionEnglish.interimResults = true;
                this.recognitionEnglish.lang = 'en-US';

                this.recognitionEnglish.onstart = () => {
                    this.isRecordingEnglish = true;
                    this.updateStatus('กำลังฟัง (อังกฤษ)... <span class="wave-animation"></span>', 'listening');
                    this.startEnglishBtn.disabled = true;
                    this.stopEnglishBtn.disabled = false;
                    this.startEnglishBtn.classList.add('recording');
                    this.englishListenText.value = '';
                    this.thaiTranslatedText.value = '';
                    this.updateListenButtonStates();
                };
                this.recognitionEnglish.onresult = (event) => {
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
                    this.englishListenText.value = finalTranscript + interimTranscript;
                    if (finalTranscript) {
                        this.updateStatus('พบข้อความอังกฤษแล้ว กำลังรอให้คุณพูดจบ...', 'success');
                    }
                    this.updateTranslateButtonStates();
                };
                this.recognitionEnglish.onerror = (event) => {
                    this.handleRecognitionError(event, 'อังกฤษ');
                    this.stopRecordingEnglish();
                };
                this.recognitionEnglish.onend = () => {
                    this.stopRecordingEnglish();
                    if (this.englishListenText.value.trim()) {
                        this.updateStatus('บันทึกเสียงอังกฤษเสร็จสิ้น กำลังแปลภาษา...', 'processing');
                        this.translateEnglishToThai();
                    } else {
                        this.updateStatus('กดปุ่ม "เริ่มพูด (อังกฤษ)" เพื่อเริ่มต้น', 'info');
                    }
                };
            }

            handleRecognitionError(event, lang) {
                let errorMessage = `เกิดข้อผิดพลาดในการรู้จำเสียง (${lang})`;
                if (event.error === 'no-speech') {
                    errorMessage = `ไม่พบเสียงพูด (${lang})`;
                } else if (event.error === 'not-allowed') {
                    errorMessage = `ไม่ได้รับอนุญาตให้ใช้ไมโครโฟน กรุณาอนุญาตในเบราว์เซอร์ (${lang})`;
                } else if (event.error === 'aborted') {
                    errorMessage = `การบันทึกเสียงถูกยกเลิก (${lang})`;
                }
                this.updateStatus(errorMessage, 'error');
            }

            setupEventListeners() {
                this.saveApiKeyBtn.addEventListener('click', () => this.saveApiKey());
                this.removeApiKeyBtn.addEventListener('click', () => this.removeApiKey());
                this.apiKeyInput.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter') this.saveApiKey();
                });
                this.apiKeyStatusDisplay.addEventListener('click', () => {
                    this.apiSetupSection.style.display = 'block';
                    this.apiKeyStatusDisplay.style.display = 'none';
                    this.apiKeyInput.value = this.geminiApiKey;
                    this.apiKeyInput.disabled = false;
                    this.saveApiKeyBtn.style.display = 'inline-block';
                    this.removeApiKeyBtn.style.display = 'inline-block';
                    this.apiKeyInput.focus();
                    this.updateStatus('คุณกำลังแก้ไข API Key', 'info');
                    this.disableAllFeatures();
                });
                
                // Thai to English events
                this.startThaiBtn.addEventListener('click', () => this.startRecordingThai());
                this.stopThaiBtn.addEventListener('click', () => this.stopRecordingThai());
                this.clearAllBtn.addEventListener('click', () => this.clearAll());
                this.translateThaiToEnglishBtn.addEventListener('click', () => this.translateThaiToEnglish());
                this.listenEnglishBtn.addEventListener('click', () => this.speakEnglishText());
                this.thaiText.addEventListener('input', () => this.updateTranslateButtonStates());
                this.englishText.addEventListener('input', () => this.updateListenButtonStates());

                // English to Thai events
                this.startEnglishBtn.addEventListener('click', () => this.startRecordingEnglish());
                this.stopEnglishBtn.addEventListener('click', () => this.stopRecordingEnglish());
                this.englishListenText.addEventListener('input', () => this.updateTranslateButtonStates());
                this.thaiTranslatedText.addEventListener('input', () => this.updateListenButtonStates());
                this.translateEnglishToThaiBtn.addEventListener('click', () => this.translateEnglishToThai());
                this.listenThaiBtn.addEventListener('click', () => this.speakThaiText());
            }

            updateStatus(message, type) {
                this.statusDiv.innerHTML = message;
                this.statusDiv.className = 'status';
                if (type) {
                    this.statusDiv.classList.add(type);
                }
            }

            updateTranslateButtonStates() {
                this.translateThaiToEnglishBtn.disabled = !this.thaiText.value.trim() || !this.geminiApiKey;
                this.translateEnglishToThaiBtn.disabled = !this.englishListenText.value.trim() || !this.geminiApiKey;
            }

            updateListenButtonStates() {
                this.listenEnglishBtn.disabled = !this.englishText.value.trim();
                this.listenThaiBtn.disabled = !this.thaiTranslatedText.value.trim();
            }

            startRecordingThai() {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return;
                }
                if (this.recognitionEnglish && this.isRecordingEnglish) { // Stop English recording if active
                    this.stopRecordingEnglish();
                }
                if (this.recognitionThai && !this.isRecordingThai) {
                    this.recognitionThai.start();
                }
            }

            stopRecordingThai() {
                if (this.recognitionThai && this.isRecordingThai) {
                    this.recognitionThai.stop();
                }
                this.isRecordingThai = false;
                this.startThaiBtn.disabled = !this.geminiApiKey;
                this.stopThaiBtn.disabled = true;
                this.startThaiBtn.classList.remove('recording');
            }

            startRecordingEnglish() {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return;
                }
                if (this.recognitionThai && this.isRecordingThai) { // Stop Thai recording if active
                    this.stopRecordingThai();
                }
                if (this.recognitionEnglish && !this.isRecordingEnglish) {
                    this.recognitionEnglish.start();
                }
            }

            stopRecordingEnglish() {
                if (this.recognitionEnglish && this.isRecordingEnglish) {
                    this.recognitionEnglish.stop();
                }
                this.isRecordingEnglish = false;
                this.startEnglishBtn.disabled = !this.geminiApiKey;
                this.stopEnglishBtn.disabled = true;
                this.startEnglishBtn.classList.remove('recording');
            }

            clearAll() {
                this.thaiText.value = '';
                this.englishText.value = '';
                this.englishListenText.value = '';
                this.thaiTranslatedText.value = '';

                if(this.geminiApiKey) {
                    this.updateStatus('ล้างข้อมูลเรียบร้อย', 'success');
                } else {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
                
                if (this.isRecordingThai) this.stopRecordingThai();
                if (this.isRecordingEnglish) this.stopRecordingEnglish();
                if (window.speechSynthesis.speaking) window.speechSynthesis.cancel();
            }

            async translateText(sourceText, sourceLang, targetLang) {
                if (!this.geminiApiKey) {
                    this.updateStatus('กรุณาใส่ Gemini API Key ก่อนใช้งาน', 'error');
                    return '';
                }
                if (!sourceText.trim()) {
                    this.updateStatus(`กรุณากรอกข้อความ ${sourceLang} ที่ต้องการแปล`, 'error');
                    return '';
                }

                const API_URL = `https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=${this.geminiApiKey}`;
                
                const prompt = `Translate the following ${sourceLang} text to ${targetLang}. Respond only with the ${targetLang} translation, without any additional comments, prefixes, or explanations, and avoid markdown if possible.
                
                ${sourceLang}: "${sourceText}"
                
                ${targetLang}:`;

                try {
                    const response = await fetch(API_URL, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify({
                            contents: [{ parts: [{ text: prompt }] }],
                            generationConfig: { 
                                temperature: 0.2,
                                maxOutputTokens: 200
                            }
                        })
                    });

                    if (!response.ok) {
                        const errorData = await response.json();
                        if (errorData.error && errorData.error.status === 'RESOURCE_EXHAUSTED') {
                             throw new Error('โควต้าการใช้งาน API หมด กรุณาลองใหม่ภายหลัง');
                        }
                        throw new Error(errorData.error.message || `HTTP error! status: ${response.status}`);
                    }

                    const data = await response.json();
                    
                    if (data.candidates && data.candidates[0] && data.candidates[0].content && data.candidates[0].content.parts[0]) {
                        let translated = data.candidates[0].content.parts[0].text.trim();
                        // Clean up potential prefixes from Gemini
                        if (translated.toLowerCase().startsWith(`${targetLang.toLowerCase()}:`)) {
                            translated = translated.substring(`${targetLang.toLowerCase()}:`.length).trim();
                        }
                        return translated;
                    } else {
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
                    } else {
                        errorMessage = `เกิดข้อผิดพลาด: ${error.message}`;
                    }
                    this.updateStatus(errorMessage, 'error');
                    return `Error: ${errorMessage}`;
                }
            }

            async translateThaiToEnglish() {
                this.updateStatus('กำลังแปลภาษาไทยเป็นอังกฤษ...', 'processing');
                this.translateThaiToEnglishBtn.disabled = true;
                this.englishText.value = 'Translating...';
                this.listenEnglishBtn.disabled = true;

                const result = await this.translateText(this.thaiText.value, 'Thai', 'English');
                this.englishText.value = result;

                if (result && !result.startsWith('Error:')) {
                    this.updateStatus('แปลภาษาไทยเป็นอังกฤษเสร็จสิ้น', 'success');
                    this.speakEnglishText(); // อ่านออกเสียงอัตโนมัติเมื่อแปลเสร็จ
                } else if (result.startsWith('Error:')) {
                    this.englishText.value = result; // แสดงข้อความ error
                } else {
                    this.updateStatus('ไม่มีข้อความให้แปล หรือเกิดข้อผิดพลาด', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            async translateEnglishToThai() {
                this.updateStatus('กำลังแปลภาษาอังกฤษเป็นไทย...', 'processing');
                this.translateEnglishToThaiBtn.disabled = true;
                this.thaiTranslatedText.value = 'Translating...';
                this.listenThaiBtn.disabled = true;

                const result = await this.translateText(this.englishListenText.value, 'English', 'Thai');
                this.thaiTranslatedText.value = result;

                if (result && !result.startsWith('Error:')) {
                    this.updateStatus('แปลภาษาอังกฤษเป็นไทยเสร็จสิ้น', 'success');
                    this.speakThaiText(); // อ่านออกเสียงอัตโนมัติเมื่อแปลเสร็จ
                } else if (result.startsWith('Error:')) {
                    this.thaiTranslatedText.value = result; // แสดงข้อความ error
                } else {
                    this.updateStatus('ไม่มีข้อความให้แปล หรือเกิดข้อผิดพลาด', 'error');
                }
                this.updateTranslateButtonStates();
                this.updateListenButtonStates();
            }

            speakEnglishText() {
                const text = this.englishText.value.trim();
                if (!text || text.startsWith('Error:')) {
                    this.updateStatus('ไม่มีข้อความภาษาอังกฤษให้อ่าน', 'info');
                    return;
                }

                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel();
                }

                this.speechSynthesisUtterance = new SpeechSynthesisUtterance(text);
                this.speechSynthesisUtterance.lang = 'en-US';
                
                this.speechSynthesisUtterance.onerror = (event) => {
                    console.error('Speech synthesis error (English):', event.error);
                    this.updateStatus(`ไม่สามารถอ่านออกเสียงภาษาอังกฤษได้: ${event.error}`, 'error');
                };
                this.speechSynthesisUtterance.onstart = () => {
                    this.updateStatus('กำลังอ่านออกเสียง (อังกฤษ)...', 'processing');
                    this.listenEnglishBtn.disabled = true;
                };
                this.speechSynthesisUtterance.onend = () => {
                    this.updateStatus('อ่านออกเสียง (อังกฤษ) เสร็จสิ้น', 'success');
                    this.listenEnglishBtn.disabled = false;
                };

                window.speechSynthesis.speak(this.speechSynthesisUtterance);
            }

            speakThaiText() {
                const text = this.thaiTranslatedText.value.trim();
                if (!text || text.startsWith('Error:')) {
                    this.updateStatus('ไม่มีข้อความภาษาไทยให้อ่าน', 'info');
                    return;
                }

                if (window.speechSynthesis.speaking) {
                    window.speechSynthesis.cancel();
                }

                this.speechSynthesisUtteranceThai = new SpeechSynthesisUtterance(text);
                this.speechSynthesisUtteranceThai.lang = 'th-TH';
                
                this.speechSynthesisUtteranceThai.onerror = (event) => {
                    console.error('Speech synthesis error (Thai):', event.error);
                    this.updateStatus(`ไม่สามารถอ่านออกเสียงภาษาไทยได้: ${event.error}`, 'error');
                };
                this.speechSynthesisUtteranceThai.onstart = () => {
                    this.updateStatus('กำลังอ่านออกเสียง (ไทย)...', 'processing');
                    this.listenThaiBtn.disabled = true;
                };
                this.speechSynthesisUtteranceThai.onend = () => {
                    this.updateStatus('อ่านออกเสียง (ไทย) เสร็จสิ้น', 'success');
                    this.listenThaiBtn.disabled = false;
                };

                window.speechSynthesis.speak(this.speechSynthesisUtteranceThai);
            }
        }

        document.addEventListener('DOMContentLoaded', () => {
            new BiDirectionalVoiceTranslator();
        });
    </script>
</body>
</html>
