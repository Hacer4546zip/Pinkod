<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PIN Code Entry</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            min-height: 100vh;
            background: linear-gradient(to bottom right, #000000, #1a1a1a);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .container {
            position: relative;
            min-height: 100vh;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
            backdrop-filter: blur(8px);
        }
        .pin-pad {
            width: 100%;
            max-width: 400px;
            background-color: rgba(0, 0, 0, 0.7);
            backdrop-filter: blur(16px);
            border-radius: 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 25px -5px rgba(255, 0, 0, 0.1), 0 10px 10px -5px rgba(255, 0, 0, 0.04);
            padding: 2rem;
            padding-bottom: 3rem;
        }
        .pin-display {
            display: flex;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        .pin-digit {
            width: 3rem;
            height: 3rem;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
            background-color: rgba(255, 255, 255, 0.1);
            transition: all 0.3s ease;
        }
        .pin-digit.filled {
            background: linear-gradient(to right, #ff0000, #cc0000);
            transform: scale(1.05);
            box-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
        }
        .pin-digit.active {
            transform: scale(1.1);
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(255, 0, 0, 0.7); }
            70% { box-shadow: 0 0 0 10px rgba(255, 0, 0, 0); }
            100% { box-shadow: 0 0 0 0 rgba(255, 0, 0, 0); }
        }
        .number-pad {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 1rem;
            justify-content: center;
            max-width: 300px;
            margin: 0 auto;
        }
        .number-button {
            height: 4rem;
            width: 4rem;
            border-radius: 50%;
            font-size: 1.5rem;
            font-weight: 600;
            background: linear-gradient(to bottom right, rgba(255, 0, 0, 0.1), rgba(204, 0, 0, 0.1));
            border: none;
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px -1px rgba(255, 0, 0, 0.1), 0 2px 4px -1px rgba(255, 0, 0, 0.06);
        }
        .number-button:hover, .number-button:focus {
            background-color: rgba(255, 0, 0, 0.3);
            transform: translateY(-2px);
        }
        .number-button:active {
            transform: scale(0.95);
            box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.2);
        }
        .confirm-button {
            background: linear-gradient(to right, #ff0000, #cc0000);
            color: white;
            border: none;
            padding: 1rem 3rem;
            border-radius: 9999px;
            font-size: 1.25rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: block;
            margin: 2rem auto 0;
            box-shadow: 0 4px 15px rgba(255, 0, 0, 0.3);
        }
        .confirm-button:hover {
            background: linear-gradient(to right, #e60000, #b30000);
            transform: translateY(-2px);
        }
        .confirm-button:disabled {
            background: #4b5563;
            cursor: not-allowed;
            box-shadow: none;
        }
        .error-message {
            color: #ff0000;
            text-align: center;
            margin-top: 1rem;
            font-size: 1.125rem;
            font-weight: bold;
            opacity: 0;
            transform: translateY(-20px);
            transition: all 0.5s ease;
        }
        .error-message.show {
            opacity: 1;
            transform: translateY(0);
            animation: shake 0.5s;
        }
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            25% { transform: translateX(-5px); }
            75% { transform: translateX(5px); }
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            animation: fadeIn 0.3s ease;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .modal-content {
            background: #1a1a1a;
            color: white;
            padding: 2rem;
            border-radius: 0.5rem;
            box-shadow: 0 20px 25px -5px rgba(255, 0, 0, 0.2);
            max-width: 400px;
            width: 90%;
            transform: scale(0.9);
            animation: popUp 0.3s ease forwards;
        }
        @keyframes popUp {
            to { transform: scale(1); }
        }
        .modal-title {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 1rem;
            color: #ff0000;
            text-align: center;
        }
        .modal-message {
            margin-bottom: 1.5rem;
            font-size: 1rem;
            line-height: 1.5;
        }
        .modal-button {
            background: #00a8ff;
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 0.25rem;
            cursor: pointer;
            transition: all 0.3s ease;
            display: block;
            margin: 0 auto;
        }
        .modal-button:hover {
            background: #007acc;
            transform: translateY(-2px);
        }
        .additional-buttons {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-top: 2rem;
            max-width: 300px;
            margin-left: auto;
            margin-right: auto;
        }
        @media (min-width: 640px) {
            .additional-buttons {
                flex-direction: row;
            }
        }
        .additional-button {
            flex: 1;
            padding: 0.75rem 1.5rem;
            border-radius: 9999px;
            font-size: 1.125rem;
            font-weight: 500;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .additional-button.blue {
            background: #ff0000;
            color: white;
        }
        .additional-button.blue:hover {
            background: #cc0000;
        }
        .additional-button.green {
            background: #ffffff;
            color: #000000;
        }
        .additional-button.green:hover {
            background: #e6e6e6;
        }
        @media (max-width: 600px) {
            .pin-pad { padding: 1.5rem; }
            .pin-digit { width: 2.5rem; height: 2.5rem; font-size: 1.2rem; }
            .number-button { width: 3.5rem; height: 3.5rem; font-size: 1.2rem; }
            .confirm-button { font-size: 1rem; padding: 0.75rem 2rem; }
        }
    </style>
</head>
<body>
    <div id="welcomeModal" class="modal">
        <div class="modal-content">
            <h2 class="modal-title">🌟 Kelin Nomzod - Muhim Qoidalar 🌟</h2>
            <div class="modal-message">
                <p>📝 Hurmatli foydalanuvchi, quyidagi qoidalarga e'tibor bering:</p>
                <p>1. <strong>To'liq ma'lumot:</strong> Kelin nomzodga yozishda 3-4 ta sifatli rasm va batafsil ma'lumot taqdim eting.</p>
                <p>2. <strong>Samimiylik:</strong> Suhbatda samimiy va hurmatli bo'ling.</p>
            </div>
            <button class="modal-button" onclick="closeWelcomeModal()">Tanishdim va Roziman</button>
        </div>
    </div>

    <div id="pinEntryContainer" class="container" style="display: none;">
        <div class="pin-pad">
            <div style="text-align: center; margin-bottom: 1.5rem;">
                <h2 style="font-size: 1.5rem; font-weight: bold; margin-bottom: 0.5rem;">PIN Kodni Kiriting</h2>
                <p style="color: #9ca3af;">Kelin Nomzodga ulanish uchun PIN kodni kiriting...</p>
            </div>
            <div class="pin-display">
                <div class="pin-digit"></div>
                <div class="pin-digit"></div>
                <div class="pin-digit"></div>
                <div class="pin-digit"></div>
            </div>
            <div class="error-message" id="errorMessage"></div>
            <div class="number-pad">
                <button class="number-button">1</button>
                <button class="number-button">2</button>
                <button class="number-button">3</button>
                <button class="number-button">4</button>
                <button class="number-button">5</button>
                <button class="number-button">6</button>
                <button class="number-button">7</button>
                <button class="number-button">8</button>
                <button class="number-button">9</button>
                <button class="number-button">X</button>
                <button class="number-button">0</button>
                <button class="number-button">←</button>
            </div>
            <button class="confirm-button" id="confirmButton" disabled>Tasdiqlash</button>
            <div class="additional-buttons">
                <div class="additional-button blue" id="purchaseButton">PIN Qoidalari</div>
                <div class="additional-button green" id="advertiseButton">Elon Berish</div>
            </div>
        </div>
    </div>

    <script>
        const STORAGE_KEY = "pinCodeData";
        const maxLength = 4;
        const minLength = 2;
        const validPins = ["705", "769", "760", "6658", "6657", "750"];
        let pin = "";
        let attempts = 0;

        const pinDigits = document.querySelectorAll('.pin-digit');
        const numberButtons = document.querySelectorAll('.number-button');
        const confirmButton = document.getElementById('confirmButton');
        const errorMessage = document.getElementById('errorMessage');
        const purchaseButton = document.getElementById('purchaseButton');
        const advertiseButton = document.getElementById('advertiseButton');

        const randomMessages = [
            "Kichrasiz, hozir sizni ulash imkoni yo‘q, 2-3 daqiqadan so‘ng qayta urinib ko‘ring.",
            "Kelin nomzod cheklov qo‘ygan, 1-2 daqiqadan so‘ng qayta PIN kiriting.",
            "Nomzod band, birozdan so‘ng qayta urinib ko‘ring.",
            "Xato yuz berdi, kelin nomzod hozirda mavjud emas, keyinroq sinab ko‘ring."
        ];

        const randomUrls = [
            "https://t.me/Ajinauz",
"https://t.me/MoonBloom001",
"https://t.me/kdhebmd",
"https://t.me/Saida_Saiii",
"https://t.me/Umnitsa6554",
"https://t.me/erkinovna0226",
"https://t.me/MaM3015",
"https://t.me/kameta00l",
"https://t.me/myanonimaccaunt",
"https://t.me/asaal_002",
"https://t.me/Assalom_93",
"https://t.me/Nillyuushka007",
"https://t.me/Izzatullayevna02",
"https://t.me/alMusavvir14",
"https://t.me/ooo_drm",
"https://t.me/miirsaidovnaaa",
"https://t.me/Beautydollyy",
"https://t.me/La_xovla_vala_quvvata",
"https://t.me/faqatoldingah",
"https://t.me/da_ollov",
"https://t.me/dredd6",
"https://t.me/Alhamdulillahxi",
"https://t.me/D15_78",
"https://t.me/Munisa_5505",
"https://t.me/Shirina_770",
"https://t.me/uzbechka_0604",
"https://t.me/Nasstariin",
"https://t.me/Mursalina002",
"https://t.me/Uzbekistan4142",
"https://t.me/pamey77",
"https://t.me/Dunyo2503"
            // Qo‘shimcha URL’larni qisqartirdim, asl ro‘yxatni qoldirishingiz mumkin
        ];

        function updatePinDisplay() {
            pinDigits.forEach((digit, index) => {
                if (index < pin.length) {
                    digit.textContent = '•';
                    digit.classList.add('filled');
                } else {
                    digit.textContent = '';
                    digit.classList.remove('filled');
                }
                digit.classList.toggle('active', index === pin.length);
            });
            confirmButton.disabled = pin.length < minLength || pin.length > maxLength;
        }

        function handleNumberClick(number) {
            if (pin.length < maxLength) {
                pin += number;
                updatePinDisplay();
                vibrate(50); // Qo‘shimcha tebranish effekti
            }
        }

        function handleDelete() {
            pin = pin.slice(0, -1);
            updatePinDisplay();
            vibrate(50);
        }

        function handleClear() {
            pin = '';
            updatePinDisplay();
            vibrate(50);
        }

        function vibrate(duration) {
            if (navigator.vibrate) navigator.vibrate(duration);
        }

        function showErrorMessage(message) {
            errorMessage.textContent = message;
            errorMessage.classList.add('show');
            setTimeout(() => errorMessage.classList.remove('show'), 3000);
        }

        function showModal(title, message, buttonText, buttonAction) {
            const modal = document.createElement('div');
            modal.className = 'modal';
            modal.innerHTML = `
                <div class="modal-content">
                    <h3 class="modal-title">${title}</h3>
                    <p class="modal-message">${message}</p>
                    <button class="modal-button">${buttonText}</button>
                </div>
            `;
            document.body.appendChild(modal);
            const button = modal.querySelector('.modal-button');
            button.addEventListener('click', () => {
                buttonAction();
                document.body.removeChild(modal);
            });
        }

        function showBusyModal() {
            const modal = document.createElement('div');
            modal.className = 'modal';
            modal.innerHTML = `
                <div class="modal-content">
                    <h3 class="modal-title">⏳ Kuting...</h3>
                    <p class="modal-message" id="busyMessage">Qidirilmoqda...</p>
                </div>
            `;
            document.body.appendChild(modal);
            setTimeout(() => {
                const busyMessage = document.getElementById('busyMessage');
                busyMessage.textContent = randomMessages[Math.floor(Math.random() * randomMessages.length)];
            }, Math.random() * 2000 + 3000);
        }

        function handleConfirm() {
            if (validPins.includes(pin) && pin.length >= minLength && pin.length <= maxLength) {
                const storedData = localStorage.getItem(STORAGE_KEY);
                if (storedData) {
                    showBusyModal();
                    return;
                }

                const expirationMinutes = Math.random() < 0.5 ? 1 : 2;
                const expirationTime = new Date().getTime() + expirationMinutes * 60 * 1000;
                localStorage.setItem(STORAGE_KEY, JSON.stringify({ expirationTime }));

                setTimeout(() => localStorage.removeItem(STORAGE_KEY), expirationMinutes * 60 * 1000);

                showModal('✅ PIN Tasdiqlandi!', 'Siz bilan bog‘lanishga harakat qilinyapti...', 'OK', () => {
                    confirmButton.textContent = 'Ulanmoqda...';
                    confirmButton.disabled = true;
                    setTimeout(() => {
                        const randomUrl = randomUrls[Math.floor(Math.random() * randomUrls.length)];
                        window.location.href = randomUrl;
                    }, Math.random() * 3000 + 2000);
                });
            } else {
                attempts++;
                pin = '';
                updatePinDisplay();

                let errorMsg = attempts === 1 ? "⚠️ Xato PIN kiritildi!" :
                              attempts === 2 ? "⛔️ Yana xato!" :
                              attempts >= 3 ? "🚫 Juda ko‘p xato urinish!" : "";
                showErrorMessage(errorMsg);

                if (attempts >= 3) {
                    showModal('🚫 Cheklov!', 'Juda ko‘p xato urinish! PIN kod sotib oling (5 oylik - 50,000 so‘m)', 'Sotib olish', () => {
                        window.open('https://t.me/Munis_Admin', '_blank');
                    });
                }
            }
        }

        numberButtons.forEach(button => {
            button.addEventListener('click', () => {
                const value = button.textContent;
                if (value === 'X') handleClear();
                else if (value === '←') handleDelete();
                else handleNumberClick(value);
            });
        });

        confirmButton.addEventListener('click', handleConfirm);

        purchaseButton.addEventListener('click', () => {
            showModal('⚠️ Qoidalar', `
                🗨️ Agar spam olsangiz, ma’lumot va 3-4 rasm bilan yozing. Hurmatli bo‘ling va sabrli bo‘ling!
            `, 'Admin bilan bog‘lanish', () => {
                window.open('https://t.me/Munis_Admin', '_blank');
            });
        });

        advertiseButton.addEventListener('click', () => {
            window.open('https://t.me/Munis_Admin', '_blank');
        });

        window.addEventListener('load', () => {
            const storedData = localStorage.getItem(STORAGE_KEY);
            if (storedData) {
                const { expirationTime } = JSON.parse(storedData);
                if (new Date().getTime() < expirationTime) showBusyModal();
                else localStorage.removeItem(STORAGE_KEY);
            }
        });

        function closeWelcomeModal() {
            document.getElementById('welcomeModal').style.display = 'none';
            document.getElementById('pinEntryContainer').style.display = 'flex';
        }
    </script>
</body>
