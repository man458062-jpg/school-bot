From datetime import date
from telegram import Update, ReplyKeyboardMarkup
from telegram.ext import ApplicationBuilder, CommandHandler, MessageHandler, filters, ContextTypes

BOSHLANISH = date(2026, 11, 10)

B_QONGIROQ = "🔔 Qo'ng'iroq jadvali"
B_BAYRAM = "🎉 Bayramgacha"
B_SAVOL = "❓ Kunlik savol"
B_SOZ = "🌍 Kunlik so'zlar"
B_YANGILIK = "📰 Yangiliklar"
B_ADMIN = "👨‍💻 Admin"

MATN = """👋 Salom, xush kelibsiz! 🎓
Men 5-sonli maktabning kelajak botiman 🤖✨
Menda maktab uchun kerak bo'ladigan juda ko'p manbalarni topishingiz mumkin 📚
Quyidagi tugmalardan birini tanlang 👇"""

MENYU = ReplyKeyboardMarkup(
    [[B_QONGIROQ, B_BAYRAM],
     [B_SAVOL, B_SOZ],
     [B_YANGILIK, B_ADMIN]],
    resize_keyboard=True,
)

QONGIROQ = """🔔 Qo'ng'iroq jadvali (1-smena)

1-dars: 8:15 – 9:00
2-dars: 9:05 – 9:50
3-dars: 9:55 – 10:40
4-dars: 10:45 – 11:30
5-dars: 11:40 – 12:25
6-dars: 12:30 – 13:15
7-dars: 13:20 – 14:05"""

ADMIN = """👨‍💻 Admin bilan bog'lanish
👤 Admin: Lutfulloyev Muhammad
📞 Telefon: +998910760611
💬 Telegram: @muhammad_198542

━━━━━━━━━━━━━━━━━━━

✍️ Savol, taklif yoki murojaatlaringiz bo'lsa, shu yerga yozib qoldiring. Administratorimiz tez orada siz bilan bog'lanadi!"""

YANGILIK = """🏫 𝓜𝓪𝓴𝓽𝓪𝓫 𝓨𝓪𝓷𝓰𝓲𝓵𝓲𝓴𝓵𝓪𝓻𝓲 ✨

📢 Eng so'nggi xabarlar shu yerda!
🔔 Obuna bo'ling 👇
https://t.me/+TYEuI-TmkHtiNzU6"""

BAYRAMLAR = {
    "Yangi yil": (1, 1),
    "Vatan himoyachilari kuni": (1, 14),
    "Xalqaro xotin-qizlar kuni": (3, 8),
    "Navro'z": (3, 21),
    "Xotira va qadrlash kuni": (5, 9),
    "Mustaqillik kuni": (9, 1),
    "O'qituvchilar kuni": (10, 1),
    "Davlat tili kuni": (10, 21),
    "Konstitutsiya kuni": (12, 8),
}

SAVOLLAR = [
    ("O'zbekistonning poytaxti qaysi shahar?", "Toshkent"),
    ("Dunyodagi eng katta okean qaysi?", "Tinch okeani"),
    ("Suv necha darajada qaynaydi?", "100 °C"),
    ("Quyosh tizimida nechta sayyora bor?", "8 ta"),
    ("Alisher Navoiy qaysi asrda yashagan?", "XV asr"),
    ("Yilda nechta oy bor?", "12 ta"),
    ("Haftada necha kun bor?", "7 kun"),
    ("Eng katta qit'a qaysi?", "Osiyo"),
    ("Quyosh qaysi tomondan chiqadi?", "Sharqdan"),
    ("O'zbekiston mustaqilligi qaysi yili e'lon qilingan?", "1991-yil"),
    ("Dunyodagi eng baland tog' cho'qqisi qaysi?", "Everest (Jomolungma)"),
    ("Qaysi sayyora Qizil sayyora deyiladi?", "Mars"),
    ("Oy Yerning nimasi hisoblanadi?", "Tabiiy yo'ldoshi"),
    ("Suv necha darajada muzlaydi?", "0 °C"),
    ("Quruqlikdagi eng katta hayvon qaysi?", "Afrika fili"),
    ("O'zbekiston pul birligi nima?", "So'm"),
    ("Mirzo Ulug'bek qaysi sohada mashhur?", "Astronomiya"),
    ("Quyosh tizimidagi eng katta sayyora qaysi?", "Yupiter"),
    ("Kattalarda nechta tish bo'ladi?", "32 ta"),
    ("Nafas olishimiz uchun zarur gaz qaysi?", "Kislorod"),
    ("Samarqanddagi mashhur maydon nomi nima?", "Registon"),
    ("Boburnoma asarining muallifi kim?", "Zahiriddin Muhammad Bobur"),
    ("Bir soatda necha daqiqa bor?", "60 daqiqa"),
    ("Qaysi hayvon cho'l kemasi deyiladi?", "Tuya"),
    ("Insonning ikki qo'lida nechta barmoq bor?", "10 ta"),
]

SOZLAR = [
    ("apple", "яблоко", "olma"),
    ("book", "книга", "kitob"),
    ("school", "школа", "maktab"),
    ("teacher", "учитель", "o'qituvchi"),
    ("water", "вода", "suv"),
    ("friend", "друг", "do'st"),
    ("house", "дом", "uy"),
    ("city", "город", "shahar"),
    ("time", "время", "vaqt"),
    ("world", "мир", "dunyo"),
    ("cat", "кот", "mushuk"),
    ("dog", "собака", "it"),
    ("mother", "мама", "ona"),
    ("father", "папа", "ota"),
    ("sun", "солнце", "quyosh"),
    ("moon", "луна", "oy"),
    ("day", "день", "kun"),
    ("night", "ночь", "tun"),
    ("red", "красный", "qizil"),
    ("blue", "синий", "ko'k"),
    ("big", "большой", "katta"),
    ("small", "маленький", "kichik"),
    ("eat", "есть", "yemoq"),
    ("drink", "пить", "ichmoq"),
    ("read", "читать", "o'qimoq"),
    ("write", "писать", "yozmoq"),
    ("good", "хороший", "yaxshi"),
    ("new", "новый", "yangi"),
    ("bread", "хлеб", "non"),
    ("student", "ученик", "o'quvchi"),
]


def qolgan_kun(oy, kun):
    bugun = date.today()
    sana = date(bugun.year, oy, kun)
    if sana < bugun:
        sana = date(bugun.year + 1, oy, kun)
    return (sana - bugun).days


def kun_raqami():
    return (date.today() - BOSHLANISH).days


async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text(MATN, reply_markup=MENYU)


async def xabar(update: Update, context: ContextTypes.DEFAULT_TYPE):
    t = update.message.text
    n = kun_raqami()

    if t == B_QONGIROQ:
        await update.message.reply_text(QONGIROQ)

    elif t == B_BAYRAM:
        matn = ""
        for nom, (oy, kun) in BAYRAMLAR.items():
            matn += f"🎉 {nom}: {qolgan_kun(oy, kun)} kun qoldi\n"
        await update.message.reply_text(matn)

    elif t == B_SAVOL:
        savol, javob = SAVOLLAR[n % len(SAVOLLAR)]
        matn = f"❓ {n % 100 + 1}-kun savoli:\n\n{savol}\n\nJavob: <tg-spoiler>{javob}</tg-spoiler>"
        await update.message.reply_text(matn, parse_mode="HTML")

    elif t == B_SOZ:
        matn = f"🌍 {n % 100 + 1}-kun so'zlari:\n\n"
        for i in range(5):
            en, ru, uz = SOZLAR[(n * 5 + i) % len(SOZLAR)]
            matn += f"🇬🇧 {en} – 🇷🇺 {ru} – 🇺🇿 {uz}\n"
        await update.message.reply_text(matn)

    elif t == B_YANGILIK:
        await update.message.reply_text(YANGILIK)

    elif t == B_ADMIN:
        await update.message.reply_text(ADMIN)


app = ApplicationBuilder().token("9089880096:AAF8klGzqH7IJHBoVHLODSvjcd7Fs6SUwLo").build()
app.add_handler(CommandHandler("start", start))
app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, xabar))
app.run_polling()
mana shu kodni .py file qilib ber
