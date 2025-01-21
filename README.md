<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PIN Code Entry</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            min-height: 100vh;
            background: linear-gradient(to bottom right, #1a202c, #4a1d96, #4c1d95);
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
            background-color: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(16px);
            border-radius: 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 20px 25px -5px rgba(139, 92, 246, 0.1), 0 10px 10px -5px rgba(139, 92, 246, 0.04);
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
            background: linear-gradient(to right, #8b5cf6, #6d28d9);
            box-shadow: 0 4px 6px -1px rgba(139, 92, 246, 0.1), 0 2px 4px -1px rgba(139, 92, 246, 0.06);
        }
        .pin-digit.active {
            transform: scale(1.1);
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% {
                box-shadow: 0 0 0 0 rgba(139, 92, 246, 0.7);
            }
            70% {
                box-shadow: 0 0 0 10px rgba(139, 92, 246, 0);
            }
            100% {
                box-shadow: 0 0 0 0 rgba(139, 92, 246, 0);
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
            background: linear-gradient(to bottom right, rgba(139, 92, 246, 0.1), rgba(124, 58, 237, 0.1));
            border: none;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 6px -1px rgba(139, 92, 246, 0.1), 0 2px 4px -1px rgba(139, 92, 246, 0.06);
        }
        .number-button:hover, .number-button:focus {
            background-color: rgba(139, 92, 246, 0.2);
            transform: translateY(-2px);
        }
        .number-button:active {
            transform: scale(0.95);
            box-shadow: inset 0 2px 4px 0 rgba(0, 0, 0, 0.06);
        }
        .confirm-button {
            background-color: #8b5cf6;
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
            box-shadow: 0 4px 6px -1px rgba(139, 92, 246, 0.1), 0 2px 4px -1px rgba(139, 92, 246, 0.06);
        }
        .confirm-button:hover {
            background-color: #7c3aed;
            transform: translateY(-2px);
        }
        .confirm-button:disabled {
            background-color: #4b5563;
            cursor: not-allowed;
        }
        .error-message {
            color: #ef4444;
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
            background-color: rgba(0, 0, 0, 0.5);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
        }
        .modal-content {
            background-color: white;
            color: black;
            padding: 2rem;
            border-radius: 0.5rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
            max-width: 400px;
            width: 100%;
        }
        .modal-title {
            font-size: 1.25rem;
            font-weight: bold;
            margin-bottom: 1rem;
        }
        .modal-message {
            margin-bottom: 1.5rem;
        }
        .modal-button {
            background-color: #3b82f6;
            color: white;
            border: none;
            padding: 0.5rem 1rem;
            border-radius: 0.25rem;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .modal-button:hover {
            background-color: #2563eb;
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
            background-color: #3b82f6;
            color: white;
        }
        .additional-button.blue:hover {
            background-color: #2563eb;
        }
        .additional-button.green {
            background-color: #10b981;
            color: white;
        }
        .additional-button.green:hover {
            background-color: #059669;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="pin-pad">
            <div style="text-align: center; margin-bottom: 1.5rem;">
                <h2 style="font-size: 1.5rem; font-weight: bold; margin-bottom: 0.5rem;">PIN Kodni kiriting</h2>
                <p style="color: #9ca3af;">Дикаат Келин Номзодга Уланиш Учун Пин Код Тиринг ва мен сизни килин номзод билан боглайман</p>
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
                <div class="additional-button blue" id="purchaseButton">Pin Kod Xarid Qilish</div>
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
            "https://t.me/Muhammadalieva_001",
"https://t.me/Sirimmeni",
"https://t.me/AllahuMMaSolli",
"https://t.me/Dilnoz_4848",
"https://t.me/Maryam300110",
"https://t.me/hasratimm09",
"https://t.me/maksudova1991",
"https://t.me/aysha8880",
"https://t.me/ALLOHIMDANBOSHQAILOHYUQ",
"https://t.me/shokirovna_707",
"https://t.me/HHamida_al",
"https://t.me/sabinafey",
"https://t.me/Beautydollyy",
"https://t.me/Sabrligim0009",
"https://t.me/Kabatullohn",
"https://t.me/Durjan99",
"https://t.me/Amerikanka_Ayko",
"https://t.me/Kilaram",
"https://t.me/Qaysar7778",
"https://t.me/Mingshukralhamdulilloh",
"https://t.me/Sabrligim9716",
"https://t.me/ismailovam1006",
"https://t.me/Allox1985",
"https://t.me/Inshaolloh85",
"https://t.me/Allohning_uyi_mominni_qalbi",
"https://t.me/hghgf65hg",
"https://t.me/Feruza_205",
"https://t.me/farishtamsabr",
"https://t.me/farm0783",
"https://t.me/qizologim999",
"https://t.me/bonu220788",
"https://t.me/abcd01_1",
"https://t.me/abcd01_1",
"https://t.me/hulkar6665",
"https://t.me/szszsz_11",
"https://t.me/Raxmat_hayott",
"https://t.me/alhamdulillah_robbil_alam",
"https://t.me/kamilaa_a7",
"https://t.me/deo_0102",
"https://t.me/Hasbunalloh1907",
"https://t.me/Azizaaammm",
"https://t.me/svetokmira8877",
"https://t.me/SSHS1985",
"https://t.me/madam2904",
"https://t.me/Gjjjjjjjkd",
"https://t.me/hgftfdfff",
"https://t.me/Ofiyat7777",
"https://t.me/Lolaxon87",
"https://t.me/avvut",
"https://t.me/ralff77",
"https://t.me/Ne_Zvezditee",
"https://t.me/Rustamovnaaaa9",
"https://t.me/MX1994_77",
"https://t.me/sakinatunni",
"https://t.me/Sabriya_4441",
"https://t.me/kamilaa_a7",
"https://t.me/nurnoma29",
"https://t.me/Insanmutlu0",
"https://t.me/Zarina0777",
"https://t.me/Muhibbi_000",
"https://t.me/Jonim92",
"https://t.me/Adu_zarr",
"https://t.me/avvut",
"https://t.me/Pok_insonlar_poklar_uchundir",
"https://t.me/safiy_122",
"https://t.me/Asilxumadan",
"https://t.me/Love9820l",
"https://t.me/Noozaaniinn",
"https://t.me/Maysara0808",
"https://t.me/Dil6367",
"https://t.me/gizlisevdam1991",
"https://t.me/Madina_998",
"https://t.me/inshaallah_1_1",
"https://t.me/ShadowMonlight",
"https://t.me/m8617",
"https://t.me/habibi_771",
"https://t.me/maya_polavina",
"https://t.me/asrorovna_o1",
"https://t.me/Sonya5511",
"https://t.me/abdulaz1zovaa7",
"https://t.me/Quvonchim66",
"https://t.me/D_inkal",
"https://t.me/Love9820l",
"https://t.me/kamilaa_a7",
"https://t.me/Ixlas_1",
"https://t.me/ALLOHIMDANBOSHQAILOHYUQ",
"https://t.me/shokirovna_707",
"https://t.me/HHamida_al",
"https://t.me/sabinafey",
"https://t.me/Beautydollyy",
"https://t.me/Sabrligim0009",
"https://t.me/Durjan99",
"https://t.me/Amerikanka_Ayko",
"https://t.me/Kilaram",
"https://t.me/Qaysar7778",
"https://t.me/Mingshukralhamdulilloh",
"https://t.me/Sabrligim9716",
"https://t.me/ismailovam1006",
"https://t.me/Allox1985",
"https://t.me/Beautydollyy",
"https://t.me/Hazzzzooooon",
"https://t.me/Inshaolloh85",
"https://t.me/Allohning_uyi_mominni_qalbi",
"https://t.me/As_mo0909",
"https://t.me/hghgf65hg",
"https://t.me/Feruza_205",
"https://t.me/farishtamsabr",
"https://t.me/farm0783",
"https://t.me/qizologim999",
"https://t.me/zeb_uzar"
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
                        window.open('https://t.me/Munisa_Admen', '_blank');
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
            showModal('⚠️Qoidalar Qullanma', `
                ‍🗨️ Агар сиз хабар ёзганда СПАМ берса, Гарантия ю! 😔 Сиз эркак киши момлангизни тугирланг, чунки у
                келининомзод аётган талаби бор. Демак, сиз элонни тушунмасдан ёзаябсиз. 🧐 Шунга кўра, сиз 3-4 та расм
                ва маълумот билан ёзищингиз керак эди. Сиз бу ишни қилмагансиз ва сизни спам келган! ❗️ 💔 Бир аёлни
                кунглини ололиш эркакнинг вазифаси.🫵 Унутманг, агар кунглини ололмасангиз, ёзиб овора бўлманг, чунки
                аёлнинг кунглини олиш сизга боғлиқ. 🤝 Биз сиз учун қўлдан келгунича ҳаракат қилиб, шу жойгача сизни
                олиб келдик. Сизга шу ерда марокли сухбат тилаб қоламан! 🥰👇
            `, 'Qoidalarga Rivoya qiling ⚠️', () => {
                window.open('https://t.me/Munisa_Admen', '_blank');
            });
        });

        advertiseButton.addEventListener('click', () => {
            window.open('https://t.me/Munisa_Admen', '_blank');
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
    </script>
</body>
</html>
