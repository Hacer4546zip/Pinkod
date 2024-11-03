<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pinkod Terib Kirish & Chat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #a1a1a; /* Qora fon */
            color: white; /* Oq matn */
            display: flex;
            flex-direction: column;
            justify-content: center; /* Vertikal markazlash */
            align-items: center; /* Gorizontal markazlash */
            height: 100vh; /* Butun balandlikni egallash */
            margin: 0;
        }

        .container {
            display: flex;
            flex-direction: column;
            align-items: center; /* Elementlarni gorizontal markazlash */
            width: 70%; /* Mobil ekran uchun kenglik */
            max-width: 600px; /* Maksimal kenglik */
        }

        .greetings {
    color: black; /* Qora rang */
    font-size: 8vw; /* Ekran o'lchamiga mos kenglikdan kelib chiqadigan hajm */
    font-weight: bold; /* Qalin harflar */
    margin-bottom: 20px; /* Pastga bo'shliq */
    text-align: center; /* Markazdan joylash */
}

@media (max-width: 600px) {
    greetings {
        font-size: 4vw; /* Kichik ekranlar uchun yana ham kichikroq hajm */
    }
}

@media (max-width: 200px) {
    greetings {
        font-size: 3vw; /* Juda kichik ekranlar uchun yana ham kichikroq hajm */
    }
}

        .pin-container, .chat-container {
            background-color: #262626;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.5);
            margin: 10px 0;
            width: 100%;
        }

        .chat-container {
            max-height: 400px; /* Chat oyna balandligi */
            display: flex;
            flex-direction: column; /* Vertikal joylashuv */
        }

        h2 {
            margin-bottom: 20px;
            color: #00ff00;
            text-align: center;
        }

        input[type="password"], input[type="text"] {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #00ff00;
            border-radius: 13px;
            background-color: #333;
            color: white;
        }

        button {
            padding: 10px 20px; /* Tugma ichidagi bo'shliqlar */
            background-color: #00ff00;
            color: black;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            width: auto; /* Tugmalarning kengligi avtomatik bo'ladi */
            margin: 5px; /* Tugmalar orasidagi bo'shliq */
        }

        button:hover {
            background-color: #005600;
        }

        .error-message {
            color: red;
            margin-top: 10px;
            display: none;
        }

        .chat-box {
            max-height: 300px; /* Chat oyna balandligi */
            overflow-y: auto; /* Oqim kerak bo'lsa, skroll qiladi */
            background-color: #1c1c1c;
            padding: 10px;
            border-radius: 2px;
            margin-bottom: 10px;
            flex: 1; /* Chat-box bo'sh joyni egallaydi */
        }

        .chat-message {
            margin: 5px 0;
            opacity: 0; /* Dastlab ko'rinmas */
            animation: fadeIn 0.5s forwards, slideIn 0.5s forwards; /* Animatsiya qo'shildi */
        }

        .bot-message {
            text-align: left; /* Bot xabarlari chap tomonda */
            color: white; /* Bot xabarlari oq rangda */
        }

        .user-message {
            text-align: right; /* Foydalanuvchi xabarlari o'ng tomonda */
            color: #00ff00; /* Foydalanuvchi xabarlari yashil rangda */
        }

        .bot-name {
            color: red; /* Bot nomini qizil rangda ko'rsatish */
        }

        .chat-input {
            display: flex; /* Flex qoidasi yordamida joylash */
            width: 100%;
            justify-content: center; /* Tugmalarni markazlashtirish */
            margin-top: 10px; /* Yuqori tomondan bo'shliq */
        }

        .chat-input input {
            flex: 1; /* Xabar kiritish maydoni kengligi */
            margin-right: 10px; /* O'ng tarafda bo'shliq */
            height: 50px; /* Xabar kiritish joyi balandligi */
            font-size: 16px; /* O'lcham o'zgarishi */
            padding: 10px; /* Ichkaridan bo'sh joy */
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        @keyframes slideIn {
            from {
                transform: translateY(10px); /* Pastdan yuqoriga ko'chirish */
            }
            to {
                transform: translateY(0); /* Dastur bo'yondan o'z holatiga o'tish */
            }
        }
    </style>
</head>
<body>
    <div class="greetings">Qizlarga Xabar Yozish Uchun Sizda Maxsus Kod Bo'lishi Lozim </div>
    
    <div class="container">
        <div class="pin-container">
            <h2>Pinkod Tering Qizga Xabar Yozish Uchun..!</h2>
            <form id="pinForm" onsubmit="return verifyPin(event);">
                <input type="password" id="pin" placeholder="Pinkodni kiriting" required maxlength="3" pattern="\d{3}">
                <div class="error-message" id="error-message">Noto'g'ri pin kod! Iltimos, qayta urinib ko'ring.</div>
                <button type="submit">Pin Kodni Tasdiqlash</button>
            </form>
        </div>

        <div class="chat-container">
            <h2>Online Chat 7/24</h2>
            <div class="chat-box" id="chatBox"></div>
            <div class="chat-input">
                <input type="text" id="chatMessage" placeholder="Xabar yozing..." required>
                <button onclick="sendMessage()">Yuborish</button>
                <button onclick="window.location.href='https://t.me/m/ODj4SY-yNzg6'">Kod Sotib olish</button>
            </div>
        </div>
    </div>

    <script>
        const botMessages = [
            "Kicha Mazza Qildim, telfonda gaplashdim 🥰",
            "Vay iflos xaromi ekan, lichkamga mani sukib qochib kitibdi",
            "Manga Poxxuy ☺️",
            "Usha erkakni topsam, tashog'ini ayiraman 😏",
            "Kicha Paynet qilgandim, tugab qoldi 😪",
            "Tanishamizmi, jon?",
            "Raxmat, shart mas umuman keragi yo'q",
            "Telfon raqamimizni bering, manga",
            "Tel raqamimni bersam, telfon qilib bezor qilasilar, shu uchun bermayman",
            "Nima hohlaysiz mandan, uzi siz?",
            "Bugun bir qiz bilan uchrashdim, juda qiziqarli boʻldi 😘",
            "Men hech qachon shunday his qilmagan edim, juda yoqimli 😍",
            "Asabni Buzmayla iltimos",
            "zaybal qildinglar qizlar bormi uzi",
            "erkaklar nomer qoldiringlar",
            "rosa zirikib kittim",
            "musofirda juda zirikarli hayot",
            "ha",
            "nega",
            "sababi bormi",
            "qanday siz aka",
            "salom",
            "assalom",
            "kim bor",
            "man keldim",
            "xormayla",
            "manam keldim",
            "xammaga salom",
            "lichga yozvoring gapim bor",
            "mani gapim bor lichkaga qarang",
            "aloo lichkaga qaravoriyla",
            "silar botmisilar nima",
            "asta sekin yoziyla bolla",
            "o'qishga uspit qilolmayab man",
            "aka lichkamga yozmang shu chatta yozing",
            "rasm yuboringlar manga",
            "salom qandaysizlar",
            "va aliykum salom",
            "xush kilib siz",
            "xush kurdik",
            "nichamiz bugun",
            "chatda bugun odam kop",
            "bugun odam rosa kopku",
            "xa xa xa yana nima",
            "usha yegit yoqib qoluvdi",
            "aka elon berganmidiz",
            "mashu elon kimni eloni",
            "sizam elon berganmisiz",
            "xa man elon bergandim",
            "ha",
            "ha 🤣",
            "ustimdan kulyabsizmi",
            "Anashu erkak borku elon bergan usha mashinik ekan 😪",
            "extiot buliyla oramizda mashinik qizlaram bor",
            "kimni mashinik divossan jinni",
            "mani aytyabsizmi",
            "xudodan qurqiyla",
            "yolg'on gapirmayla",
            "tuxmat qilmayma endi",
            "zaybal aka sekvordizku",
            "bunchakop gapirasan shaxlo",
            "laylo san yegiting keldi",
            "erimni kim qushdi chatga",
            "voy kim manga bugun paynet qiladi 😄",
            "manga ham paynet qiladigon erkak bormikan",
            "Bla usha kuni bir yegit yozdi manga yoqib qoluvdi chornilabdi",
            "kim manga spam berdi aytvoriyla",
            "telegramga yozolmayab man",
            "elon bergan manga yozganlarga yozolmayab man",
            "эй хормайла опалар",
            "салом хуш келиб сиз",
            "сиз кайдан сиз",
            "ман элон бергандим кизлар безор килди телфон килиб",
            "ростан ака мани узим сизга 2 марта адашиб телфон килдим",
            "🤣 Томим киттиб колди",
            "салом",
            "ман янги ман чатда",
            "men xozir qushildim chatga",
            "xammaga omad",
            "опа сиз ерга теголмангиз",
            "бир умр ерсиз утасиз шекилли",
            "ака сиз уйлган аёл йук ботта",
            "сиз излаган қиз хали кирмаган",
            "ох жонум",
            "laylo opa baxtizni topdizmi",
            "baxt nima uzi",
            "dalbayoblar bir gapa",
            "nima dimoqchisiz",
            "ochig'ini ayting",
            "telfon nomer tashanglar ey",
            "odam zerikib kitti tel qiling",
            "manga kim tel qilishni hohlaydi",
            "sekaman naxxuy og'zingni yum",
            "nima",
            "hichnima",
            "jonga tegar odam ekan siz",
            "siz gapga tushunmaysiz",
            "kim aytgan busa qutog'ni yebdi",
            "shu erkak mashinik",
            "xa xa xa ulib qolaman hozir",
            "qani siz aka",
            "alooo",
            "kim tanishishni hohlaydi",
            "man bilan tanishing",
            "nichi marta elon berdiz",
            "mani elonimni kim uchirdi",
            "yana elon beraman u yegit manga yoqmadi",
            "to'g'ri manoda elon bergandim",
            "bittasi mani sekmoqchi buldi",
            "bitta odam manga seks taklif qildi",
            "elon berganlar realni uzimi",
            "ha uzimni rasmim",
            "ha man rasmim bilan elon joylagandim",
            "albatta uzimni rasmim",
            "elonidagi qiz sizmisiz",
            "opa rasmda chiroyli ekansiz",
            "nichi yoshda siz",
            "man 21 yosh man",
            "man 19",
            "men 17",
            "Man 22",
            "Ман 50 ёш",
            "Манга хотин кирак",
            "мани хотиним йок",
            "хатиним улган",
            "эриз борми",
            "манга уйланасизми",
            "Менга эр кирак 30 40 ёшли",
            "Салом манга эр кирак 45 ёшларда",
            "Salom man 17 yoshman",
            "assalom man 17 yosh",
            "mani yoshim 17 da",
            "man 32 yosh",
            "man ayol kishi man",
            "o'iz gey siz man ayol kishi",
            "siz erkakmi",
            "geymisiz aka man ayol kishi",
            "voy tovba",
            "voy man ayolman",
            "man qiz bola man",
            "rosatan qizmisiz",
            "selkani kim olib kitti",
            "borishga joyim yoq kuchada qoldim",
            "xa xa battar boling",
            "edi naxxuy",
            "sukinmayla",
            "barashangizga amim",
            "омимни йибсан шу гапинга",
            "Омимни йибсиз",
            "пашон урот",
            "сизга нима",
            "сукинмайла кизла",
            "bolla bormi uzi",
            "birorta terik jon bormi",
            "salom aka",
            "salom",
            "assalom",
            "Menku bu",
            "tanmay qoldizmi aka",
            "lichkamga u kuni yozgandizku",
            "xa tanidim aka",
            "elonimni uchirmayla",
            "mani elonimni o'chirmang",
            "nima hohlaysiz",
            "quchoqlashib yotardim oldizda busam",
            "oh mazza aka",
            "manam maskvada man",
            "kim bor rassiada",
            "rassiada yurgan yegitla qani sila",
            "musofirda yurganla bormi",
            "salam ismim dildora rassiada man xozir",
            "Шахло ман Россияда ман",
            "дилороб ман рассиада ман",
            "Малика исмим бухородан",
            "Азиза ман рассиада ман хозир",
            "Шахкат ман",
            "Манга поххуй кимсиз",
            "Dam olaman ey",
            "Ertaga chat kirasizmi",
            "Eshittiylami yaqinda admen shu chatta telfonda gaplashish imkonini qushar ekan",
            "Voy rastanmi",
            "Juda zo'r bulardi",
            "Kachon ekan shu kun",
            "Ko'rishishni juda hohlayab man",
            "ersiz odam qiynaladi",
            "odamnin bahkti yörümta bulmasin ekan",
            "Baxqlik yashashga hakim bor",
            "man Санкт-Петербургда ман",
            "petirda man",
            "1998 йил ман",
            "96 йил ман",
            "Москвада сан 2004 йил ман",
            "2006 йил ман рассиадаман хозир",
            "ман якинда келдим питирга",
            "ман танишаман",
            "мен танишмокчиман",
            "смаркандан ман",
            "Мафтуна",
            "Барно",
            "Бухоролик ман",
            "Андижон",
            "Фаргона",
            "наманган",
            "шахрисабиз",
            "navoi",
            "samarqandan man",
            "yaxshi raxmat",
            "Aka baxtizni topdizmi",
            "opa baxtizni topdizmi",
            "shu odamga ishonish qiyinda telfon qilgandim malumoti yolg'on",
            "nima aldayab siz qizlarni",
            "aka siz o'yin kulgu uchun elon bergan ekan",
            "maxsadiz yoq",
            "sovchilarizni junating qarshidan man",
            "qashqadaryodan man 2007 yil",
            "men 2008 yil",
            "gulnoza man 2005 yil",
            "1988 yil man",
            "88 yillar bormi",
            "92 lar bormi",
            "97 topiladimi",
            "qariz berib turiyla oyni oxiri beraman",
            "kimda pul bor",
            "dugonajon ishonamng anvarga",
            "dugosh Sherzod aka aldayabdi",
            "o'sha erkak manga ham tel qilgandi",
            "laylo manga tel qildi",
            "Farangiz 2003 man",
            "Toshkent",
            "Jizzaxdan man 2006 yil",
            "jizzaz",
            "sirdaryodan man",
            "ha",
            "hm",
            "😏",
            "😄",
            "aldamayman rosti",
            "rosti 2004 yil man",
            "menda usha",
            "man tanishaman",
            "manga ham yozvoriyla",
            "ha ha mashka",
            "birrasi mandan pul suratabdi",
            "bermang opa ularga pul",
            "odamlaram jinni",
            "hozir bu chatda jinni bulaman",
            "man jinni bulib qolay diyab man",
            "ichki kuyov kirak",
            "Salom ichki kuyov bulaman digan bormi",
            "salam men uz baxtimni izlab kirdim",
            "manam baxtimni izlab kirdim",
            "hop",
            "ha tushundim",
            "lich qarang",
            "spam man",
            "sizam spamdamisiz",
            "spamm bergan quling sinsin",
            "sukmayla",
            "sukinmang",
            "манга хам эр борми",
            "бахтимни излаб киргандим",
            "ёлгончилар манга телфон килманглар",
            "безор киламан телфон килиб",
            "ertaga tel qiling",
            "nomer bering",
            "nima qilasiz",
            "niga gapla",
            "kimga qanaqa yangilik bor",
            "elon natijasi qanday ekan",
            "elon bergandim 100 tacha ayol qiz tel qildi",
            "Ayollar telfon qilib bezor qilarkan elondan berganimga",
            "Elon bersa buladimi",
            "Admenga yozasiz elon qabul qiladi",
            "кимга элон берамиз",
            "ким билади адмен лечкасини",
            "Ким бор",
            "Салом хаммага",
            "Элон бераман",
            "Элонимни учиринг адмен",
            "Элтимос телфон килиб безор килманглар мани",
            "Ака элонимни яхшилаб укинг",
            "Мани элонимни укимасдан личкамга ёзманглар",
            "бугун ким нечта ёл билан танишди",
            "манга 7 та ёл тел килди бугун",
            "Охири телфонимни синдираман 1000 та ёл телфон килди",
            "элон бергандим бугун 8 та ёл килди телфон",
            "манга хам тел килди ёллар",
            "мазза",
            "кича битт ёл билан куришдим",
            "ертага учрашувибюм бор",
            "manga kim tel qilishni hohlaydi",
            "tugmani bosganingda admen bo'ladi",
            "Xa elon berdim qizlar yozdi",
            "Zor natija munisa opa raxmat",
            "Natijaga gap yoq raxmat",
            "Raxmat Munisa man kutmagandim natija bomba",
            "Aka natija zur ekan",
            "Xullar bu chatta yozganni foydasi yoq elon berib ko'ring qizlarni uzlari sizga yozishadi",
            "Xa qizlarni uzi sizga telfon qiladi elon bering",
         "Привет как дела",
        "Всему миру привет",
        "Самандар исмим",
        "мен лола бухорадан 1987 йил",
        "Элон бириб куринг курасиз ака",
        "ростан элонларга ишонсам буладими",
        "ха ака",
        "мани узим элон жойлаб курдим пулига арзийди",
        "манам элон бирсамми диб уйладим",
        "хама муниса опани махтади бир элон бераман",
        "куёвликка номзод бор хоразимдан 96 йил",
        "ман хоразимдан 98 йил анора",
        "Кашкадарёдан ман 2003",
        "ismim lobar 2004 yil man ajrashgan",
        "Gulmira",
        "Ismiz nima",
        "otiz nima",
        "kimga beramiz elon",
        "siz admenmi",
        "elon bering ishonchli aka",
        "Elon birib ko'ring ishonchli ekan",
        "ertaga elon beraman hop",
        "Qizlar manga telfon qilib bezor qilib tashadi zirikkanimdan kirdim chatga",
        "man yangi man hozir kirdim chatga",
        "Kim biladi elon berish nichpul ekan",
        "Shu kanalda elon birish 50 ming ekan",
        "Juda arzon ekan bosha kanalda 50 ming oladi hichkim telfon qilmaydi",
        "bu kanalga 50 meng tashlashga arziydi o'zim sinab ko'rdim",
        "Guli tanishamizmi",
        "voy buncha qimmat 50.000 meng",
        "Киммат маску хозир 50 минга хич нарса бермайди",
        "Ха 50 минг ташлаган ман зор натижа",
        "кимни канали бу узи",
        "канака чат бу узи ман тушунмай колдим",
        "хуш келиб сиз ака",
        "Салом хаммага",
        "Ман янги ман исмим Гулбахор",
        "Орамизда тулов килиб кизлар блан гаплашганлар борми",
        "ха гаплашганлар бор ака ишончли",
        "ман элон бериб синаб курдим ростан кизлар телфон килишаркан",
        "ман шу ёр ёрда элон бериб битта киз блан танишдим манга ёкмади у киз",
        "манам элон бериб биттаси блан учрашдим расмда чиройли киз экан",
        "Сардор яхшимисиз телфонизни кутаринг гапим бор",
        "Шайдо отим ещим 32 да бахтимни излаб кирдим буйирга",
        "Камола ман 42 еш",
        "менам рассиада туриб элон жойладим рассиада биттаси блан куришдим еши катта опа экан мехмон килиб жунатвордим уйига",
        "элон бирийла курасила натижа курсатади муниса",
        "manga poxxuy elon bermasam ham shu chatta tobvolaman sevgilimni",
        "🤐 Man aytmagandim",
        "🤣 jinni xona",
        "Qizla lich yozvoriyla gapim bor",
        "😪 Xafa man sizdan",
        "Qachon kartamga pul tashab berasiz Masurjon aka",
        "Bolam och kartamga pul tashang aka",
        "Xammasi pul surashdan boshqa narsaga utmaydi qizla",
        "Shu yor yor kanalida elon bergandim yegitlar yozdi bittasi yoqib qolgandi qochib kitti rasmimni ko'rib 🤣",
        "yuragiz tosh ekan",
        "yozvoring",
        "hamma jamul jam bitta man kam chatda",
        "elon berganlar biz nechtamiz chatda",
        "Xa aka ishonchli elon bergan man",
        "manga telfon qildi qizlar",
        "Salom Munisa opa raxmat baxtimni topdim",
        "Eriz bor ekanku telfon qilgandim eriz sukib kitti mani 🤣",
        "eri borlaram elon joylab quyganmi",
        "ajrashmasdan elon berganlar bor ekan",
        "Aka siz oldin ajrashib oling ayoliz bilan kiyin manga yozasiz",
        "Qonuniy ajrashgan man ko'rsataymi dakumentlarimni ajrim qog'oz",
        "ishondim",
        "Qizlar silar gadoymi buncha pul suraysilar",
        "Mani pul zavodim yoq",
        "Raxmat opa 2 ruzg'orga baxtimni topdim",
        "Рахмат Муниса синглим 2 рузгор учун бахтимни топдим",
        "Муниса хармат бахтимни топдим",
        "Бахтимни топдим хоразимга эрга тегябман",
        "Бухорога тегябман эрга",
        "Андижонга тегадигон аёллар борми",
        "Бирага яшагани киз кирак ман 27 ёщ",
        "Салом танишамизми",
        "Сиз кадан сиз ака",
        "Ман жиззахдан",
        "Саломга алик беринг",
        "Алик",
        "Азиз ака нечи ёщ",
        "Лола сиз нечи ёщ",
        "Ман 22 ёш",
        "61 ёщда ман болам",
        "61 ёщ",
        "34 ёщ",
        "35 yosh man",
        "28 da yoshim",
        "aka dib ayting",
        "Xozir sizga dada dib aytadi🤣",
        "Bolam bir past jim o'tir",
        "So'kmang",
        "⚠️Диккат Диккат Элон Кабул Бошланди 🟢 Ким Элон Беришни Хохласа Адменга ёзинг https://t.me/Vovo_Admen",
        "Элон Кабули Бошланди https://t.me/Vovo_Admen Хаволани Босинг Адменга ёзинг Муниса исми",
        "Менга эр керак 21 ёш ман гулустондан ман битта фарзандим хам бор",
        "Ёш киз ман 23 фарзандим бор ойла кураман диганла борми",
        "30 ёщ ман Муниса исмим эрга тегмаган ман киз боламан",
        "Дилдораман Самаркандан 20 ёш турмуш курмаган ман",
        "17 yosh man aldanib qolgan man kim mani to'y qilib olishga qurbi yetadi kuyov uchun yosh chegarasi 30 yoshgacha tegaman",
        "18 yosh man yegitim aldab ketgan erga tegaman",
        "Man 21 yosh aldanib qolgan man ota onam mani haydob chiqarib yuborgan 1 yil buldi ijarada yashayman",
        "mani bitta 3 oyliq farzandim bor 24 yosh man ajrashganman uzim ijarada yashayman",
        "Ko'chada qoldim bugunga kimni uyida joy bor",
        "tanishamiz lich yozganga surpriz bor",
        "tez lich yoziyla",
        "Tel yozing aka",
        "telfon raqamizni yozing",
        "Kichrasiz Foydalanuvchi chatda Telfon raqam Yozish taqiqlangan⚠️",
        "🗨Haqoratli So'zlarni ishlatmang",
        "So'kinmang blok bo'lasiz",
        "Xuyyet Qilib Qoldim Buncha Tez Tez Yozasilar 😃",
        "😀",
        "😄",
        "Yoqib Qoldiz😇",
        "Elon berdim hozir",
        "Ertalab elon bergandim yaxshi qizlar tel qildi munisa opa raxmat",
        "opa manga qizlar tel qilishni boshladi raxmat",
        "opa tel qilyabdi qizlar raxma",
        "quling singur qaysing spam urding manga",
        "yana spam man",
        "spam bo'ldim",
        "spamga soldi jalab",
        "jalab spam berma manga",
        "spam keldi",
        "spam qildi",
        "elon berdim telfon qilishayabdi qizlar manga",
        "Raxmat opa qizlar endi telfon qilyabdi",
        "kicha elon joylagandim bugun telfon qilishni boshladi",
        "aldamang",
        "sizni aldamadimku",
        "ha tel qildi qizlar",
        "😁 Raxmat Qizlar Telfon qilishayabdi opa",
        "Andijonli qizla tel qilyabdi opa",
        "Mani elonimga yozib qo'ying opa bekorchi qizlar telfon qilmasin",
        "Hop yozdim",
        "Elon bergandim rostini aytsam ha telfon qildi manga faqat yoshi katta opalar qildi",
        "man uzi buydoq man elon bergandim yoshim 21 da 45 50 yoshli opalar tel qilishayabdi 🤣",
        "Man 19 yosh man ko'zi yumi opalar man qiz bolaman",
        "man qiz bolaman ayollar niga telfon qilishayabdi manga",
        "lezbi opam tel qildi manga",
        "xa xa xa opa",
        "opa zor siz",
        "elon bersam momolaram tel qildi ey oxiri baxtimni topdim",
        "erga tegaman 18 yosh man",
        "21 yoshda man Aziza ismim erga tegaman",
        "18 yosh Angerindanman",
        "Quqonlik man 20 yosh",
        "ha ayol kishi man",
        "man qiz bola",
        "elon berdim",
        "Elon birdim yegitlar yozdi raxmat opa",
        "Elon joylagandim boboylar yozishdi telfon qildi",
        "2 ruzg'orga erga tegaman 23 yosh man",
        "2 рузгорга тегаман сурхондарёдан ман",
        "🚫 Телфон ракам ёзиш такикланган⛔️",
        "♻️ Элон Кабул Бошланди куёвлар адменга ёзинг",
        "Элон нархи 50 минг",
        "500 рубл тулаб элон бериб бахтимни топдим рахмат",
        "менам эрга тегсам буладими",
        "Бахтини топиб ойла курганла борми",
        "ман шу каналда уйланим",
        "ман шу муниса оркали эрга тегдим",
        "эрга тегдим яна ажрашдим",
        "ажрашган ман",
        "Мен ажрашган ёлман",
        "ажрашган ман",
        "ха ажримга берган ман",
        "эрим йок",
        "2 марта эрга тегиб чиккан ман",
        "3 марта бахтим ухшамади мани",
        "ажрашим хозир ота онам уйида ман",
        "ота онамникида яшайман",
        "Элон бердим хаммага рахмат тел килишни бошлади кизлар",
        "рахмат тел килишди кизлар",
        "тел келди манга кизлар",
        "телфон килябди манга кизлар",
        "кизлар блан гаплашдим",
        "код сотиб олдим 5 ойлик кизлар блан гаплашдим",
        "ха бахтимни топдим",
        "Код олдим рахмат",
        "Кодни кимга ёзамиз",
        "Код олганлар код ёзиш жойи бор пастта уша жойга кодни ёщинг кизни хаволаси чикади",
        "Келин номзодни хаволасига кириб булмаса бошка кизни курасиз у зацнет булиши мумкун",
        "шу киз борми чатда",
        "сизам чатдамисиз ака",
        "Код олдим рахмат Муниса опа",
        "Кодни тердим ишлади рахмат",
        "Код тириб кизни лечкасини олдим рахмат",
        "Бу код 5 ой ишлайдими",
        "Вогзалда 1998-йилда туғилган, турмушга чиқмаган, ўрта, оппоқ, хушбичим келишган истарали қиз бола бор. Олий маълумотли мактабда ишлашади узларига ухшаган укимишли йигитка беришади.",
        "Тукизбулок кучасида 1999йил жувон борлар 1та кизчалари бор эпчил чаккон.",
        "Авгонбогда 2000йил жувон борлар 1та фарзандлари бор богчада ишлашади яхши оила.",
        "2006йил уйда утиредигон кизимиз борлар урта буй истаралик.",
        "Навоийда 1993йил жувон борлар 1та фарзандлари бор бамани одобли кизимиз.",
        "Фаробий кучасида 1988йил жувон борлар 1та фарзандлари бор яхши жой буса чикаришади.",
        "Дангарада 2003йил олий малумотли кизимиз борлар оила бамани.",
        "2003йил АДМИда укидигон кизимиз борлар камгап ширингина яхши жой буса чикаришади.",
        "2003йил жувонча борлар такволи хонадон кизлари кизимиз чиройли келишкан 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "Абу тайб хукандийда 2006йил Тошкентда укидигон кизимиз борлар бамани оила кизимиз Араб тилини билишади.",
        "Навоийда 1989йил жувон борлар фарзандлари йук инситутда сиртки талимда укишади.",
        "2004йил жувон борлар одобли тарбияли 1та фарзандлари бор.",
        "Богдод туманида 2004йил жувонча борлар оз муддат яшаган инситутда 3курсда укишади.",
        "2006йил табиий чиройли кизимиз борлар келишган истарали бамани инсонлар фарзанди.",
        "2002йил жувон борлар 1ёш кизчалари бор оила яхши.",
        "Окжар кишлогида 2003йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Дангарада 1989йил жувон борлар фарзандлари йук бамани яхши жувон ишлаб чикаришда ишлашади.",
        "ХУРМАТЛИ ГРУХИМИЗ АЗОЛАРИ ШУ КИЗИМИЗИ УНАШТИРИШИБДИ БАХТЛИ БУЛИШСИН 🤲🤲🤲",
        "КИМГА БЕРГАН БУСАМ УЧИРИБ КУЙИЛАР😄😄😄😄😄",
        "ХУРМАТЛИ ГРУХИМИЗ АЗИЗ АЁЛЛАРИ РОССА КАМЕЙИБ КЕТТИК",
        "КОНТАКТ КУШИЛАР ЯНГИ АДРЕСЛАР БОР КИЗ ЖУВОНЛАР",
        "Дангарада 1990йил жувон борлар келишган одобли чеварлар 1та 6ёш фарзандлари бор яхши оила.",
        "Учкуприк туманида 1991йил турмуш уртоглори вафот эткан жувон борлар нозик 1та кизчалари бор уйда утиришади.",
        "1994 йил олий маьлумотли, аклли, истарали, урта буй бир киз борлар, зиёли оила фарзанди. Уйланганга беришмайди, оиласи зиёли, узи укимишли, иши тайин йигитга беришади. Таги Куконлик Тошкентда яшайдиганга беришади.",
        "Кора теппа махалласида 2006йил чиройли келишкан киз бола бор.",
        "Ойдин кучадан 2006йил истаралик келишкан новча узларига тук хонадон.",
        "Дангарада 1988йил фарзандсизлик сабаб ажрашишкан жувон борлар мактабда ишлашади, унверситетда укишади.",
        "Бака чорсуда 2006йил урта буй ширингина киз борлар.",
        "Учкуприк туманида 2005-йил Тошкентда Араб тилида укидигон зиели оилани кизи бор.",
        "Диёр кўчасида 2004-йилда туғилган, турмушидан жуда оз муддат яшаб ажрашган новчагина, келишган, қоши кўзи табиий қора, истарали, бамани жувонча бор. Фарзанди йўқ. укимишли кизимиз богчада ишлашади.",
        "Учкуприк туманида 2000йил олий малумотли кизимиз борлар мактабда ингилиз тилидан дарс беришади.",
        "Бувайда туманида 1995йил киз бола бор катта чевар акилли хушли кизимиз.",
        "Навоийда 2006йил оппок чиройли кизимиз борлар келишган уй хамширалигини тамомлашкан уйда утиришади.",
        "Урта кишлогда 2004йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Бувайда туманида 1990йилда тугилган турмушга чиқмаган киз бола бор.",
        "Бувайда туманида 1997йил оз муддат яшаган фарзанди йук жувон борлар.",
        "2005йио нозиккина ширингина кизимиз борлар.",
        "Бувайда туманида 1998йил оз муддат яшаган жувон борлар фарзандлари йук.",
        "Бувайда туманида 1994йил жувон борлар фарзандлари йук оила яхши истарали жувон.",
        "1992йил кизимиз борлар урта буй истарали яхши жой буса чикаришади.",
        "2006йил уйда утиредигон кизимиз борлар ширингина оила бамани.",
        "2006йил илимли кизимиз борлар уйда утиришади олилалари яхши.",
        "2005йил нозик келишкан новча хушбичим кизимиз борлар.",
        "2005йил урта буй истарали кизимиз борлар Аялари бамани.",
        "Бабушкинда 1996йил олий малумотли киз бола бор ишлашади новча.",
        "Бахмалбоб кучасида 2005йил истаралик киз бола бор.",
        "Бахмалбоб кучасида 2006йил ширингина уйда утиредигон кизимиз борлар.",
        "2005йил новча истарали кизимиз борлар.",
        "2006йил уйда утиредигон яхши кизимиз борлар.",
        "2005йил сал гавдалирок чиройли истарали кизимиз борлар.",
        "Бобобек кучасида 2006йил инситутда укидигон киз бола бор.",
        "Навоийда 2003йил жувонча борлар оз муддат яшаганлар фарзандлари йук инситутда укишади.",
        "Риштон туманида 1991йил турмушга чиқмаган олий малумотли киз бола борлар куринишига караганда ёш куринишади оила яхши яхши номзод булса Куконга хам беришоради.",
        "Дангара Курик кишлогида 1990йил турмушка чикмаган киз бола бор.",
        "1997йил олий малумотли киз бола бор яхши жой буса чикаришади.",
        "Навоийда 1994-йилда туғилган, турмушга чиқмаган ўрта бўйли, оппоқ истарали говдалик қиз бола бор.",
        "1994йил яхши келишкан истарали жувон борлар фарзандсизлик сабаб ажрашишган тиниб тинчидигон жой буса чикаришади.",
        "2006йил истаралик келишкан кизимиз борлар.",
        "2005йил урта буй табий чиройлик киз бола бор.",
        "Дустлик кучасида 2006йил оппок нозик чиройли келишкан киз бола бор.",
        "2006йил 2007йил кизлар бор яхши жой буса чикаришади оила бамани истарали келишкан кизлар.",
        "Яйпанда 1998йил чевар таййор чикариледигон киз бола бор.",
        "Аширкулмерганда урта буй истарали 2006йил ширингина киз бола бор.",
        "2005йил новча сал гавдалирок кизимиз борлар укишади оила бамани.",
        "2006йил уйда утиредигон киз бола бор.",
        "1991йил хамшира жувон борлар 2та кизчалари бор бамани истарали жувон.",
        "2006йил урта буй ширингина киз бола бор.",
        "2005йил Тошкентда 2курс кизимиз борлар чиройли келишкан истарали узларига тук хонадон узларига ухшаган жойга беришади.",
        "2004йил олий малумотли кизимиз борлар узларига тук хонадон.",
        "1990йил чиройли келишкан жувон борлар фарзандлари йук.",
        "2004йил КДПИДА 3курс музыкальныйни тугаткан уй хамширалигида укиган кизимиз борлар тикиш кулларидан келади озгина нуксонлари бор.",
        "Абу тайб хукандийда 2007йил чиройли келишкан кизимиз борлар.",
        "Шалдирамокда 2006йил замонавий кизимиз борлар банк коллежда укишкан аялари бамани.",
        "Ассалому алайкум азиз инсонлар. Мени ўғлим Бекзод 1992 йил, уйланмаган Тошкент шахар Сергили туманида яшайди.",
        "1 гурух ногирони ДЦП ҳассада юради номозхон кичкина тикув цехи бор. Соғлиги яхши оёқда нуқсони бор.",
        "Яқинда Ҳиндистонга бориб оёқларини операция қилдириб келдик, ОЛЛОХ га шукр ҳозир ўзи юра бошлади. Шароитимиз яхши.",
        "Азизлар савоб учун қиз топишга ёрдам беринглар. Ўғлимдан кичкина қизлар, 2гурух ногиронлиги бўлса хам Тошкент ва водийдан қиз керак, тикувчи бўлса жуда яхши бўларди.",
        "Ўқийман деса ўқитамиз. Бу тақдир. Эълон берувчи онаси.",
        "Мукимий шахарчасида 1998йил жувон борлар нозик келишкан истарали 1та кизчалари бор оналари олиб колишади такводор номозхон кизимиз.",
        "Навоийда 2002йил фарзандлари йук жувон борлар.",
        "Бувайда туманида 1987йил олий малумотли жувон борлар 1та фарзандлари бор олиб колишади.",
        "2006йил урта буй келишкан истарали киз бола бор.",
        "Мукимий шахарчасида 2002йил фарзандлари йук жувон борлар.",
        "1981йил кизимиз борлар оила бамани яхши жой буса турмушка чикишади кизимиз ишлашади умрага бориб келишкан огир босик кизимиз.",
        "Гузар кучасида 2004йил инситутда 2курс акилли келишкан истарали доим кулиб турадигон кизимиз борлар хам диний хам дунёвий илимга эга.",
        "1994йил жувон борлар оила яхши 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "1995йил олий малумотли жувон борлар оила зиёлик 1та фарзандлари бор оналари олиб колишади кизимиз нозиккина хушбичим истарали.",
        "1999йил новча олий малумотли сал гавдалирок киз бола бор.",
        "2006йил бувили кизимиз борлар эпчил чаккон.",
        "2004йил Тошкентда 3курс кизимиз борлар оила бамани кизимиз истарали.",
        "Чинобод кишлогида 1987йил киз бола бор ота оналари утиб колишкан яхши жой буса чикаришади.",
        "Учкуприк туманида 1991йил олий малумотли врач кизимиз борлар Фаргонада ишлашади узларига ухшаган олий малумотли инсонга турмушга чикишади кизимиз хам диний хам дунёвий илимга эга оила зиёлик.",
        "1999йил олий малумотли кизимиз борлар оила яхши бувили.",
        "2006йил кизимиз борлар оппокина.",
        "2006йил новча кизимиз борлар оила яхши.",
        "Токзор кўчасида 2001-йилда туғилган, турмушга чиқмаган, оппоқ, новчагина истарали қиз бола бор. Олий маълумотли. ўқимишли йигитга беришади.",
        "Дангарада 2003йил АДМИда 4курс кизимиз борлар чиройли бамани яхши киз.",
        "Гумойлида 2003-2005йил опа сингиллар бор.",
        "2002йил 1та кизчалари бор бамани жувон борлар хужейинлари утиб коган.",
        "Абу тайб хукандийда 1987йил жувон борлар 1та фарзандлари бор фарзандлари билан кабул киледигон инсонга турмушга чикишади.",
        "Абу тайб хукандийда 2007йил кизимиз борлар урта буй истарали.",
        "2006йил бувили кизимиз борлар истарали оппок.",
        "2001йил олий малумотли кизимиз борлар оила зиёли.",
        "2005йил кизимиз борлар оила бамани бувилик.",
        "2006йил уйда утиредигон кизимиз борлар истарали.",
        "2006йил кизимиз борлар истарали пазанда.",
        "1992йил жувон борлар 1та фарзандлари бор бамани истарали кизимиз тиниб тинчидигон жой буса чикаришади.",
        "1986йил киз бола бор яхши жой буса чикаришади.",
        "Сарик камиш кучасида 2005йил унверситетда 2курс. Курон хатим килишкан илимли кизимиз борлар.",
        "2000йил жувон борлар фарзандлари йук.",
        "Навоийда 1984йил жувон борлар олий малумотли мактабда ишлашади келишкан истарали 1та кизлари бор чикаришкан.",
        "2006йил говдалирок истарали киз борлар оила бамани.",
        "Навоийда 2005йил кизимиз борлар новча келишкан.",
        "Шалдирамок кучасида 1988йил фарзандлари йук жувон борлар.",
        "Учkupрик туманида 1988-1991йил опа сингиллар бор эпчил чаккон.",
        "2005йил бамани одобли кизимиз борлар бувилик.",
        "1999йил жувон борлар фарзандлари йук.",
        "Бувайда туманида 2000йил олий малумотли стоматолог кизимиз борлар.",
        "Яна Бувайда туманида 2000йил мед инситут тамомлаган киз бола бор.",
        "Бувайда туманида 2004йил жувонча бор.",
        "Бувайда туманида 2000йил олий малумотли киз бола бор.",
        "Бувайда туманида 2002йил Тошкентда Инс Institutda укидигон кизимиз борлар.",
        "Амир темур кучасида 2005йил истаралик оппок хушбичим киз бола бор.",
        "Навоийда 1989йил фарзандлари йук истарали эпчил чаккон жувон борлар.",
        "Телемин кишлогида 2005йил Тошкентда укидигон кизимиз борлар оила бамани.",
        "2006йил озода пазанда кизимиз борлар оила бамани келишкан истарали узларига тук кизимиз Курон хатим килишкан Умрага боришкан.",
        "Навоийда 1988йил жувон борлар фарзандлари йук.",
        "Навоийда 2001йил жувон борлар фарзандлари йук.",
        "Навоийда 1992йил олий малумотли жувон борлар 1та фарзандлари бор фарзандларини бошини силедигон инсон буса оила куришади.",
        "Абу тайб хукандийда 1993йил оз муддат яшаган жувон борлар фарзандлари йук ширингина бамани.",
        "2006йил юридическига кирган кизимиз борлар кизимиз табий чиройлик кош кузлари кора.",
        "Абу тайб хукандийда 2004йил Тошкентда укидигон кизимиз борлар пазанда истарали келишкан Илимлари бор.",
        "Нефт базани кучасида 2001йил олий малумотли кизимиз борлар.",
        "1995йил фарзандлари йук врач жувон борлар оила бамани.",
        "1997йил жувон борлар фарзандсизлик сабаб ажрашишган оила зиёли кизимиз олий малумотлилар новча Врач.",
        "Олмаота кучасида 2000йил жувон борлар 1та фарзандлари бор эпчил чакон бамани яхши жой буса чикаришади.",
        "Хужакент кучасида 1985-1990йил опа сингиллар бор 1тадан фарзандлари бор тиниб тинчидигон жой буса чикаришади.",
        "2005йил кизимиз борлар яхши оила.",
        "Шилдирда 1992йил жувон борлар фарзандлари йук оила бамани медиклар хам чевар Умрага бориб келишкан яхши жой буса чикаришади.",
        "Навоийда 1988йил жувон борлар оз муддат яшаганлар фарзандлари йук истарали кош кузлари кора.",
        "Учкуприк туманида 1998йил олий малумотли кизимиз борлар Куконда ингилиз тилидан дарс беришади Курон укиган уранган киз.",
        "Сулаймон махалласида 1985йил жувон борлар оз муддат яшаганлар жиддий сабаб билан ажрашишган фарзандлари йук чеварлар хам медик.",
        "Фуркат туманида 1998йил олий малумотли киз бола борлар мактабда ишлашади яхши оила.",
        "Шикаргох кучасида 2005йил опа сингиллар бор инситутда укишади оила бамани.",
        "2004йил истарали новча бамани киз бола бор.",
        "2004йил КДПИДА 3курс музыкальныйни тугаткан уй хамширалигида укиган кизимиз борлар тикиш кулларидан келади озгина нуксонлари бор.",
        "2007йил чиройли тарбияли кизимиз борлар.",
        "Гузар кучасида 2004йил Инситутда укидигон илимли чиройли киз бола бор.",
        "1981йил киз борлар ишлашади Умрага бориб келишкан оила бамани тенгилари чикса турмуш килишади.",
        "Яйпанда 2002йил келишкан чевар кизимиз борлар истарали тарбияли кизимиз оила бамани Куконгаям беришоради.",
        "Абу тайб хукандийда 2006йил бувили кизимиз борлар.",
        "Учкуприк туманида 1998йил укитувчи кизимиз борлар укиганга беришади.",
        "Маргилонда 1992йил фарзандлари йук жувон борлар келишкан истарали оналари врач яхши жой буса чикаришади.",
        "2000йил оппок чиройли келишкан жувон борлар фарзандлари йук узларига ухшаган оз муддат яшаган фарзанди йук йигитка беришади.",
        "2001йил фарзандлари йук жувон борлар.",
        "2004йил 3курс кизимиз борлар яхши оила.",
        "1999йил Тошмини битириб кеган врач кизимиз борлар истарали узларига ухшаган жойга беришади.",
        "2005йил оппок новча келишкан кизимиз борлар.",
        "1994йил илимли жувон борлар оилалари бамани 1та кизчалари бор фарзандлари билан кабул киледигон Аллохни таниган инсонга беришади.",
        "2006йил илимли кизимиз борлар истарали.",
        "2003йил келишкан истарали кизимиз борлар оппок новча уйда утиришади.",
        "2003йил узларига тук истарали кизимиз борлар.",
        "2003йил унверситетда укидигон кизимиз борлар.",
        "Пахлавон кучасида 2005йил чиройли одобли нуткларида сал нуксонлари бор киз бола бор.",
        "Учкуприк тумани Гиждон кишлогида 2003йил Укимишли кизимиз борлар.",
        "Учkupрик туманида 2003йил Укимишли кизимиз борлар оила бамани Врачка беришади.",
        "Men gaplashdim qizlar bilan.",
        "raxmat menam gaplashdim.",
        "elon berdim qizlar telefon qilishdi 🤣.",
        "xa qildi 😁.",
        "Munisa raxmat sizga.",
        "munis raxmat elon uchun.",
        "Opa raxmat elonimni uchiring.",
        "munisa opa raxmat sizga elonimni olib tashlang.",
        "mani elonimni uchiring opa baxtimni topdim.",
        "raxmat opalar ishlarizga omad.",
        "kod sotib olmoqchiman.",
        "kod kirak manga.",
        "kodni kim biladi aytvoriyla.",
        "Diyora ismim 2007 man.",
        "Shaxlo man 26 yosh ajrashgan.",
        "Malika ismim oila qurmagan man 2004 yil.",
        "2005 yil man Odina ismim.",
        "Nelu ismim toshkent.",
        "Surxondaryodan yegitlar bormi.",
        "xush kelib siz yaxshi yegit.",
        "samarqandliklar bormi.",
        "man samarqandan.",
        "navoiydan man.",
        "jizzaxdan Dildora ismim.",
        "nichinchi yil siz.",
        "Guli man buxorolik 2003 yil oila qurmagan man.",
        "Turmushga chiqmagan man 2001 yil man.",
        "elon berdim🤣.",
        "Шахсонам ман 2003 йил бухородан.",
        "Хоразимдан ман 2002 йил.",
        "элон бердим рахмат хаммага.",
        "Элон килдим куёвликка.",
        "Элон жойлаб беринг опа.",
        "Элонизни каналга жойладик.",
        "Мани элонимни олиб ташанг опа бахтимни топдим.",
        "муниса киз мени элонимни каналдан учиринг бахтимни топдим.",
        "опа мен мурод ман элонимни учиринг безор килди кизлар телфон килишиб манга.",
        "опа ха сизга рахмат.",
        "Муниса синглим рахмат сизга.",
        "Рахмат манам бахтимни шу каналда топдим.",
        "Мунис сизга каттакон рахмат.",
        "опа мени элонимни янгилаб беринг.",
        "хуш келиб сиз.",
        "саломат булинг.",
        "✋️ ёлгон малумот берманглар.",
        "хакорат килганлар спам ❌️.",
        "Элон бергандим опа янгилаб бероласизми.",
        "хоп лечкамга ёзинг элонизни янгилайман.",
        "Муниса синглим мани элонимни янгилаб беринг кизлар телфон килмай куйдику.",
        "ноинсоф булманглар элон берганда битта киз блан гаплашинглар эркаклар.",
        "Elon bergandan sung bitta qizni tanlab usha bilan gaplashinglar 100 qizni ushlab vaxtini olmaylar.",
        "Elon berdim xammasi rost ekan.",
        "Baraka toping Munisa elon berdim natija Zo'r.",
        "Zo'r raxmat.",
        "Opa raxmat kichagi elonimni uchirvorsagizam buladi.",
        "apa raxmat sizga manga qizlar telfon qilishayabdi.",
        "opa manga erdan ajrashgan ayollar telfon qilib bezor qildi.",
        "Munisa singlim man ajrashgan erkak man nega manga qiz bollar ham telfon qilayabdi.",
        "Opa manga ham qiz bollar telfon qilayabdi ayting faqat ajrashganlar telfon qilsin manga.",
        "Ajrashgan ayollar telfon qilsin.",
        "Telfon nomer tarqatmayla.",
        "Manam elon beraman bugun.",
        "Kuyovlikka nomzodimni quyib keldim hozir.",
        "Munisa lichkamga karta tashang tulov qilib elon joylamoqchiman.",
        "Синглим карта беринг.",
        "Элон жойлаш кирак муниса.",
        "карта беринг.",
        "Мен муниса элон беришни хохласангиз личкамга ёзинг.",
        "Элон бериш учун тулов киласиз личкамга ёзинг.",
        "Кандай элон беришни билмаябман.",
        "элон жойлаб бераман личкамга ёзинг.",
        "мани личкам бу @Munisa_Admen.",
        "Elon Joylayab man kanalga kim Uz nomzodini quymoqchi lichkamga yoziyal.",
        "Diqqat diqqat elon qabul boshlandi.",
        "kimda elon bor lichkamga yozvoriyla.",
        "Elon qabul qilaman lichkamga yoziyla.",
        "Kimda elon bor qabul boshlandi.",
        "Manga yozing elon joylaymiz.",
        "Elon berish uchun admenga yozing.",
        "Kuyovlik uchun nomzodini qoymoqchi buganlar yozinglar elon qilib beramiz.",
        "Barno man 2008 yil.",
        "Kirgiziyadan man 2006 yil.",
        "Man andijondan Muxlisa 2006.",
        "Lola man erga tegib ajrashgan man 21 yosh.",
        "22 yosh man hilola.",
        "Hilola 23 yosh man vodiydan.",
        "Xurshida man ajrashgan 20 yosh.",
        "Elon beraman diganlar lichkamga yozing.",
        "Dildora 2005 ajrashgan.",
        "Man ajrashgan man aka.",
        "Xa qiz bola man.",
        "Gulustondan man Sevara ismim.",
        "2001 yil man Farangiz.",
        "Фарангиз ман 1999 йил.",
        "Латофат исмим 1987 йил.",
        "Лола ман ажрашган 1980 йил.",
        "Farida ismim ajrashgan man 19 yoshda man.",
        "Negina sizga gapim bor.",
        "zirikkan qizla lichkamga yoziyla tanishamiz.",
        "elon berib keldim.",
        "Voy munisa raxmat sizga xamma telfon qilaybdi elon berganimga."
        ];

        const bots = ['Foydalanuvchi', 'Foydalanuvchi', 'Foydalanuvchi'];

        let botInterval;

        // Botlardan tasodifiy xabar yuborish
        function sendRandomBotMessages() {
            const botName = bots[Math.floor(Math.random() * bots.length)];
            const messageContent = botMessages[Math.floor(Math.random() * botMessages.length)];
            const messageElement = document.createElement('div');
            messageElement.className = 'chat-message bot-message'; // Bot xabari
            messageElement.innerHTML = `<span class="bot-name">${botName}</span>: ${messageContent}`; // Bot nomini qizil rangda
            document.getElementById('chatBox').appendChild(messageElement);

            scrollChatToBottom();
        }

        // Botlardan xabar yuborishni boshlash
        function startBotMessages() {
            botInterval = setInterval(sendRandomBotMessages, 2000);
        }

        // Pinni tekshirish
        function verifyPin(event) {
            event.preventDefault();
            const pin = document.getElementById('pin').value;
            const correctPin = '9225';
            const errorMessage = document.getElementById('error-message');

            if (pin === correctPin) {
                alert('Kirish muvaffaqiyatli!');
            } else {
                errorMessage.style.display = 'block';
            }
        }

        // Foydalanuvchi sahifaga yuklanganda bot xabarlarini boshlash
        window.onload = function() {
            startBotMessages();
        }

        // Xabar yuborish
        function sendMessage() {
            const chatBox = document.getElementById('chatBox');
            const chatMessage = document.getElementById('chatMessage');
            const message = chatMessage.value;

            if (message) {
                const messageElement = document.createElement('div');
                messageElement.className = 'chat-message user-message'; // Foydalanuvchi xabari
                messageElement.textContent = `Siz: ${message}`;
                chatBox.appendChild(messageElement);
                chatMessage.value = ''; // Xabar kiritish maydonini tozalash

                // Chat oynasini pastki qismga aylanish
                scrollChatToBottom();
            }
        }

        // Chat oynasini pastki qismga aylantirish
        function scrollChatToBottom() {
            const chatBox = document.getElementById('chatBox');
            chatBox.scrollTop = chatBox.scrollHeight;
        }
    </script>
</body>
</html>
