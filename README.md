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
            transition: all 0.3s;
        }
        .pin-digit.filled {
            background: linear-gradient(to right, #ff0000, #cc0000);
            box-shadow: 0 4px 6px -1px rgba(255, 0, 0, 0.1), 0 2px 4px -1px rgba(255, 0, 0, 0.06);
        }
        .pin-digit.active {
            transform: scale(1.1);
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% {
                box-shadow: 0 0 0 0 rgba(255, 0, 0, 0.7);
            }
            70% {
                box-shadow: 0 0 0 10px rgba(255, 0, 0, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(255, 0, 0, 0);
            }
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
            transition: all 0.3s;
            box-shadow: 0 4px 6px -1px rgba(255, 0, 0, 0.1), 0 2px 4px -1px rgba(255, 0, 0, 0.06);
        }
        .number-button:hover, .number-button:focus {
            background-color: rgba(255, 0, 0, 0.2);
            transform: translateY(-2px);
        }
        .number-button:active {
            transform: scale(0.95);
            box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.06);
        }
        .confirm-button {
            background-color: #ff0000;
            color: white;
            border: none;
            padding: 1rem 3rem;
            border-radius: 9999px;
            font-size: 1.25rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            display: block;
            margin: 2rem auto 0;
            box-shadow: 0 4px 6px -1px rgba(255, 0, 0, 0.1), 0 2px 4px -1px rgba(255, 0, 0, 0.06);
        }
        .confirm-button:hover {
            background-color: #cc0000;
            transform: translateY(-2px);
        }
        .confirm-button:disabled {
            background-color: #4b5563;
            cursor: not-allowed;
        }
        .error-message {
            color: #ff0000;
            text-align: center;
            margin-top: 1rem;
            font-size: 1.125rem;
            font-weight: bold;
            opacity: 0;
            transform: translateY(-20px);
            transition: all 0.5s;
        }
        .error-message.show {
            opacity: 1;
            transform: translateY(0);
        }
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        .modal-content {
            background-color: #1a1a1a;
            color: white;
            padding: 2rem;
            border-radius: 0.5rem;
            box-shadow: 0 20px 25px -5px rgba(255, 0, 0, 0.1), 0 10px 10px -5px rgba(255, 0, 0, 0.04);
            max-width: 400px;
            width: 100%;
        }
        .modal-title {
            font-size: 1.25rem;
            font-weight: bold;
            margin-bottom: 1rem;
            color: #ff0000;
        }
        .modal-message {
            margin-bottom: 1.5rem;
        }
        .modal-button {
            background-color: #ff0000;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            cursor: pointer;
            transition: background-color 0.3s;
            display: block;
            margin: 0 auto;
        }
        .modal-button:hover {
            background-color: #cc0000;
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
            transition: all 0.3s;
        }
        .additional-button.blue {
            background-color: #ff0000;
            color: white;
        }
        .additional-button.blue:hover {
            background-color: #cc0000;
        }
        .additional-button.green {
            background-color: #ffffff;
            color: #000000;
        }
        .additional-button.green:hover {
            background-color: #e6e6e6;
        }
    </style>
</head>
<body>
    <div id="welcomeModal" class="modal">
        <div class="modal-content">
            <h2 class="modal-title">🌟 Kelin Nomzod - Muhim Qoidalar 🌟</h2>
            <div class="modal-message">
                <p>📝 Hurmatli foydalanuvchi, iltimos quyidagi qoidalarga e'tibor bering:</p>
                
                <p>1. <strong>To'liq ma'lumot:</strong> Kelin nomzodga yozishda 3-4 ta sifatli rasm va batafsil ma'lumot taqdim eting.</p>
                
                <p>2. <strong>Samimiylik:</strong> Suhbatda samimiy va hurmatli bo'ling. Kelin nomzodning his-tuyg'ularini hurmat qiling.</p>
                
                <p>3. <strong>Sabr-toqat:</strong> Agar darhol javob ololmasangiz, sabr qiling.</p>
                
                <p>4. <strong>Spam qilmang:</strong> Takroriy yoki keraksiz xabarlar yuborish taqiqlanadi.</p>
                
                <p>5. <strong>Hurmat:</strong> Har doim hurmat va odob doirasida muloqot qiling.</p>
                
                <p>🤝 Biz sizga eng yaxshi tajribani taqdim etish uchun harakat qilamiz.</p>
                
                <p>💖 Sizga omad va baxt tilaymiz! Umid qilamizki, siz o'z juftingizni topasiz.</p>
            </div>
            <button class="modal-button" onclick="closeWelcomeModal()">Tanishdim va Roziman</button>
        </div>
    </div>

    <div id="pinEntryContainer" class="container" style="display: none;">
        <div class="pin-pad">
            <div style="text-align: center; margin-bottom: 1.5rem;">
                <h2 style="font-size: 1.5rem; font-weight: bold; margin-bottom: 0.5rem;">PIN Kodni kiriting</h2>
                <p style="color: #9ca3af;">Дикаат Келин Номзодга Уланиш Учун Пин Кодни Тиринг....?</p>
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
            <button class="confirm-button" id="confirmButton" disabled>PIN Kodni Tasdiqlash</button>
            <div class="additional-buttons">
                <div class="additional-button blue" id="purchaseButton">Pin Kod Qoidalari....</div>
                <div class="additional-button green" id="advertiseButton">Elon Berish</div>
            </div>
        </div>
    </div>

    <script>
        const STORAGE_KEY = "pinCodeData";
        const maxLength = 4;
        const minLength = 2;
        const validPins = ["705", "769", "760", "6688", "6687", "750"];
        let pin = "";
        let attempts = 0;

        const pinDigits = document.querySelectorAll('.pin-digit');
        const numberButtons = document.querySelectorAll('.number-button');
        const confirmButton = document.getElementById('confirmButton');
        const errorMessage = document.getElementById('errorMessage');
        const purchaseButton = document.getElementById('purchaseButton');
        const advertiseButton = document.getElementById('advertiseButton');

        const randomMessages = [
            "Kichrasiz siz so'ragan qizga hozir sizni ulay olmayman sababi qiz lichkasiga chiklov o'rnatgan bunday holda siz 2 yoki 3 daqiqadan so'ng qayta kirib pin kodni tiring",
            "uzur sizni qiz bilan ulashgan urundim biroq kelin nomzod tomonidan chiklov chiqdi 1 yoki 2 daqiqidan so'ng qayta pin kod tering",
            "Men sizni tushunaman men xarakat qildim sizni kelin nomzod bilan ulashga ammo ulanishlar befoyda hozircha siz boshqa nomzod kanaldan ko'ring bu kelin nomzod cheklov doirasidan ko'p odamlar yozgan va uning telegramdagi xabarlarga to'lganini ko'rdim",
            "Voy meng bor uzur xurmatli foydalanuvchi sizni kelin nomzod bilan ulashda xato bo'ldi sababi Kelin nomzod xozirda zaynet biroz vaxtdan so'ng qayta o'rinib ko'ring",
            "Kelin nomzod xabar yozishni vaxtincha chiklagan 1 nicha daqiqadan so'ng qayta tering kodingizni",
            "Noqulayliklar uchun sizdan o'zur surayman kelin nomzodga xabar junatishni hozirda imkoni yoq sababi oddiy kelin nomzod band bo'lishi mumkun yoki u hozirda kim bilandur gaplashayabdi 1 yoki 2 dadqiqadan so'ng harakat qiling",
            "Siz hozirda vaxtincha cheklov qo'yilgan Nomzodni so'radingiz bu kelinga xozir yoza olmaysiz birozdan so'ng xarakat qiling",
            "Qizning o'zi xabar yozishni cheklagan bu vaxtincha bo'lishi mumkun qayta o'runiny 5 6 daqiqadan so'ng",
        ];

        const randomUrls = [
            "https://t.me/Onam_2020",
            "https://t.me/Nargiza1122334455",
            "https://t.me/xxxoo11122",
            "https://t.me/huzunnnn",
            "https://t.me/Zebo_12_28",
            "https://t.me/Musulmonlar7778",
            "https://t.me/az25901",
            "https://t.me/rumayso_002",
            "https://t.me/Allohimsangaishonaman",
            "https://t.me/sinamataqdir",
            "https://t.me/VATANIM81",
            "https://t.me/hghg6yt56yt54r",
            "https://t.me/isakova1",
            "https://t.me/hggf6bvgh65t",
            "https://t.me/Taqdirlar123",
            "https://t.me/hghg6yter",
            "https://t.me/Sjsjshzhsnsns",
            "https://t.me/M_4_58",
            "https://t.me/Asiraaman",
            "https://t.me/xggc67ug5",
            "https://t.me/Sheykxa_202",
            "https://t.me/Hazon0101",
            "https://t.me/anne_annecim",
            "https://t.me/Armonim1725",
            "https://t.me/+79040219058",
            "https://t.me/Muallima786",
            "https://t.me/Qs1914",
            "https://t.me/Baxtizlab77",
            "https://t.me/Bineslady",
            "https://t.me/Qulmatovanigora",
            "https://t.me/Habibin_11111",
            "https://t.me/Bineslady",
            "https://t.me/Xayot1311",
            "https://t.me/beheppy_55",
            "https://t.me/Mexrimsen",
            "https://t.me/Ahmadjonn01",
            "https://t.me/Maxmud1713",
            "https://t.me/WWSH_999999",
            "https://t.me/Maxmud1713",
            "https://t.me/BDUTSh",
            "https://t.me/L917M",
            "https://t.me/Tarix0199",
            "https://t.me/OORZULAR",
            "https://t.me/Sazooooooooo",
            "https://t.me/Sazooooooooo",
            "https://t.me/dilozorbolmang",
            "https://t.me/dunyooo571",
            "https://t.me/Allhamdulloh888",
            "https://t.me/parizoddddd",
            "https://t.me/mmaddiinnamm",
            "https://t.me/Guliruxso",
            "https://t.me/mubicaaa",
            "https://t.me/gipsofilyaa",
            "https://t.me/ustozdst",
            "https://t.me/Sabina9111",
            "https://t.me/Farishtamcha",
            "https://t.me/Lave0000",
            "https://t.me/DILIIM10",
            "https://t.me/amor_fati_1_7",
            "https://t.me/mubicaaa",
            "https://t.me/shaxrustamovnaoo1",
            "https://t.me/SHAIK_244",
            "https://t.me/Zeboijahon",
            "https://t.me/Zilola_36_37",
            "https://t.me/s135789",
            "https://t.me/Nazli240",
            "https://t.me/Qaysar7778",
            "https://t.me/MNBasall",
            "https://t.me/mlkm100",
            "https://t.me/Lifelongdestination",
            "https://t.me/Talabaaaaaaaaaaaaaaaa",
            "https://t.me/tmmadin",
            "https://t.me/Zilola96_96",
            "https://t.me/aklonnn",
            "https://t.me/BKAUZ",
            "https://t.me/Qaysar7778",
            "https://t.me/deo_0102",
            "https://t.me/Dilbarim_28",
            "https://t.me/allohim_ozinga_shukurrr",
            "https://t.me/Dildoram_86",
            "https://t.me/LYOMM444555666777888999",
            "https://t.me/sevinchka96",
            "https://t.me/Uzoqroo_Yur",
            "https://t.me/Dilbarim_28",
            "https://t.me/black_rose_fn",
            "https://t.me/Qaysar7778",
            "https://t.me/shaxrustamovnaoo1",
            "https://t.me/HGM2804",
            "https://t.me/Hasbuhu3",
            "https://t.me/black_rose_fn",
            "https://t.me/laylo013",
            "https://t.me/Muchi_SamarkanskayaN1",
            "https://t.me/Janatimsan2016",
            "https://t.me/Vvvhffghkkl",
            "https://t.me/laylo013",
            "https://t.me/Gozal7899",
            "https://t.me/nastarim77",
            "https://t.me/Jisoo089",
            "https://t.me/mubicaaa",
            "https://t.me/deo_0102",
            "https://t.me/Gozal7899"
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
            }
        }

        function handleDelete() {
            pin = pin.slice(0, -1);
            updatePinDisplay();
        }

        function handleClear() {
            pin = '';
            updatePinDisplay();
        }

        function showErrorMessage(message) {
            errorMessage.textContent = message;
            errorMessage.classList.add('show');
            setTimeout(() => {
                errorMessage.classList.remove('show');
            }, 3000);
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
                    <h3 class="modal-title">Kichrasiz</h3>
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

                setTimeout(() => {
                    localStorage.removeItem(STORAGE_KEY);
                }, expirationMinutes * 60 * 1000);

                showModal('PIN tasdiqlandi!', 'Siz bilan bog\'lanishga harakat qilinyapti...', 'OK', () => {
                    setTimeout(() => {
                        const randomUrl = randomUrls[Math.floor(Math.random() * randomUrls.length)];
                        window.location.href = randomUrl;
                    }, Math.random() * 3000 + 2000);
                });
            } else {
                attempts++;
                pin = '';
                updatePinDisplay();

                let errorMessage = '';
                if (attempts === 1) {
                    errorMessage = "⚠️ Kichrasiz Xato Pin Kod Kiritilgan";
                } else if (attempts === 2) {
                    errorMessage = "⛔️ Siz Xato Tirdingiz";
                } else if (attempts === 3) {
                    errorMessage = "🚫 Siz Xali Xam Pin Kod ni Xato Tirish Bilan Band Siz";
                } else {
                    errorMessage = "⚠️ Siz Xato Qildingiz Foydasi Yoq To'g'ri Pin Kod Kititing 🔐";
                }

                showErrorMessage(errorMessage);

                if (attempts >= 3) {
                    showModal('Kichrasiz siz juda ko\'p xato qildingiz', 'Pin kod sotib oling 5 oylik 50.000 ming so\'m', 'Sotib olish', () => {
                        window.open('https://t.me/Munis_Admin', '_blank');
                    });
                }
            }
        }

        numberButtons.forEach(button => {
            button.addEventListener('click', () => {
                const value = button.textContent;
                if (value === 'X') {
                    handleClear();
                } else if (value === '←') {
                    handleDelete();
                } else {
                    handleNumberClick(value);
                }
            });
        });

        confirmButton.addEventListener('click', handleConfirm);

        purchaseButton.addEventListener('click', () => {
            showModal('⚠️ Admin Shaxshiy Savollarga Javob bermaydi shaxsiy Savollar Bermang ..!', `
                ‍🗨️ Агар сиз хабар ёзганда СПАМ берса, Гарантия ю! 😔 Сиз эркак киши момлангизни тугирланг, чунки у
                келининомзод аётган талаби бор. Демак, сиз элонни тушунмасдан ёзаябсиз. 🧐 Шунга кўра, сиз 3-4 та расм
                ва маълумот билан ёзищингиз керак эди. Сиз бу ишни қилмагансиз ва сизни спам келган! ❗️ 💔 Бир аёлни
                кунглини ололиш эркакнинг вазифаси.🫵 Унутманг, агар кунглини ололмасангиз, ёзиб овора бўлманг, чунки
                аёлнинг кунглини олиш сизга боғлиқ. 🤝 Биз сиз учун қўлдан келгунича ҳаракат қилиб, шу жойгача сизни
                олиб келдик. Сизга шу ерда марокли сухбат тилаб қоламан! 🥰👇
            `, 'Qoidalarga Rivoya qiling ⚠️', () => {
                window.open('https://t.me/Munis_Admin', '_blank');
            });
        });

        advertiseButton.addEventListener('click', () => {
            window.open('https://t.me/Munis_Admin', '_blank');
        });

        // Check for stored data on load
        window.addEventListener('load', () => {
            const storedData = localStorage.getItem(STORAGE_KEY);
            if (storedData) {
                const { expirationTime } = JSON.parse(storedData);
                if (new Date().getTime() < expirationTime) {
                    showBusyModal();
                } else {
                    localStorage.removeItem(STORAGE_KEY);
                }
            }
        });

        function closeWelcomeModal() {
            document.getElementById('welcomeModal').style.display = 'none';
            document.getElementById('pinEntryContainer').style.display = 'flex';
        }
    </script>
</body>
