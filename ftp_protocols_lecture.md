# FTP, TFTP va SFTP Protokollari

## Dars Ishlanma
**Fan:** Kompyuter tarmoqlari  
**Mavzu:** FTP, TFTP va SFTP protokollari  
**Maqsad:** Talabalarga fayl uzatish protokollarining asosiy tamoyillari, arxitekturasi va qo'llanilish sohasini o'rgatish

---

## 1. Kirish: Fayl Uzatish Protokollarining Zaruriyati

Zamonaviy kompyuter tarmoqlarida ma'lumotlarni bir kompyuterdan ikkinchisiga uzatish eng muhim vazifalardan biridir. Fayl uzatish protokollari (File Transfer Protocols) tarmoq orqali fayllarni samarali va ishonchli tarzda ko'chirish uchun mo'ljallangan maxsus dasturiy vositalardir.

### 1.1. Tarixiy Kontekst

Fayl uzatish protokollari 1970-yillarning boshlarida ARPANET tarmoqida paydo bo'lgan. O'sha davrda kompyuterlar o'rtasida ma'lumot almashish zarurati tug'ildi va bu vazifani hal qilish uchun birinchi FTP protokoli ishlab chiqildi.

### 1.2. Zamonaviy Ahamiyati

Bugungi kunda fayl uzatish protokollari quyidagi sohalarda keng qo'llaniladi:
- Veb-saytlarni server'larga yuklash va yangilash
- Katta hajmdagi fayllarni tarmoq orqali uzatish
- Ma'lumotlar bazalarini zaxiralash va tiklash
- Tizim administratorlari tomonidan masofadan boshqarish
- Internet orqali dasturiy ta'minotni tarqatish

---

## 2. FTP (File Transfer Protocol)

### 2.1. FTP Protokolining Umumiy Ta'rifi

**FTP (File Transfer Protocol)** - bu kompyuter tarmoqlarida mijoz va server o'rtasida fayllarni uzatish uchun mo'ljallangan standart tarmoq protokolidir. FTP 1971-yilda Abhay Bhushan tomonidan ishlab chiqilgan va RFC 959 hujjatida rasmiy standartlashtirilgan.

### 2.2. FTP Arxitekturasi

FTP klassik mijoz-server arxitekturasiga asoslangan:

#### 2.2.1. Ikki Kanalli Tizim

FTP o'ziga xos xususiyatga ega - u ikkita alohida TCP ulanishidan foydalanadi:

1. **Control Connection (Boshqaruv ulanishi)** - Port 21
   - Buyruqlar va javoblarni uzatish uchun
   - Seansning butun davomida ochiq turadi
   - Foydalanuvchi autentifikatsiyasi va buyruqlar yuborish

2. **Data Connection (Ma'lumot ulanishi)** - Port 20
   - Fayllar va kataloglar ma'lumotlarini uzatish
   - Har bir fayl uzatish operatsiyasi uchun yangi ulanish ochiladi
   - Uzatish tugagach yopiladi

#### 2.2.2. FTP Ishlash Rejimi

**Active Mode (Faol rejim):**
- Server mijozga ma'lumot ulanishini boshlaydi
- Mijoz server'ga o'z portini bildiradi
- Server 20-portdan mijoz portig ulanadi
- Firewall bilan muammolar yuzaga kelishi mumkin

**Passive Mode (Passiv rejim):**
- Mijoz ham boshqaruv, ham ma'lumot ulanishini boshlaydi
- Server passiv rejimga o'tadi va o'z portini bildiradi
- Mijoz ushbu portga ulanadi
- Zamonaviy tarmoqlarda ko'proq qo'llaniladi

### 2.3. FTP Buyruqlari

FTP protokolida 30 dan ortiq buyruq mavjud. Eng ko'p ishlatiladiganlar:

| Buyruq | Vazifasi |
|--------|----------|
| USER | Foydalanuvchi nomini yuborish |
| PASS | Parolni yuborish |
| LIST | Katalog tarkibini ko'rish |
| RETR | Faylni yuklab olish (retrieve) |
| STOR | Faylni yuklash (store) |
| DELE | Faylni o'chirish |
| MKD | Yangi katalog yaratish |
| RMD | Katalogni o'chirish |
| PWD | Joriy katalogni aniqlash |
| CWD | Katalogni o'zgartirish |
| QUIT | Seansni tugatish |

### 2.4. FTP Javob Kodlari

FTP server'i har bir buyruqqa uch raqamli kod bilan javob beradi:

- **1xx** - Ijobiy boshlang'ich javob (kutish kerak)
- **2xx** - Ijobiy tugatish javobi (muvaffaqiyat)
- **3xx** - Ijobiy oraliq javob (qo'shimcha ma'lumot kerak)
- **4xx** - Vaqtinchalik salbiy javob (qayta urinish mumkin)
- **5xx** - Doimiy salbiy javob (xato)

Misollar:
- `220` - Server tayyor
- `230` - Foydalanuvchi tizimga kirdi
- `331` - Foydalanuvchi nomi qabul qilindi, parol kerak
- `425` - Ma'lumot ulanishini ochib bo'lmadi
- `530` - Tizimga kirish rad etildi

### 2.5. FTP Ma'lumot Uzatish Rejimlari

#### 2.5.1. ASCII Rejim
- Matnli fayllar uchun
- Turli operatsion tizimlar o'rtasida satr oxiri belgilarini avtomatik konvertatsiya qiladi
- UNIX: LF, Windows: CRLF, Mac: CR

#### 2.5.2. Binary (Image) Rejim
- Ikkilik fayllar uchun (rasmlar, video, dasturlar)
- Faylni o'zgartirishsiz uzatadi
- Zamonaviy FTP mijozlarda standart rejim

### 2.6. FTP Afzalliklari va Kamchiliklari

**Afzalliklari:**
- Keng tarqalgan va yaxshi qo'llab-quvvatlanadigan
- Ko'plab operatsion tizimlarda o'rnatilgan
- Oddiy va tushunarli protokol
- Katta fayllarni uzatish qobiliyati
- Katalog tuzilmalari bilan ishlash imkoniyati

**Kamchiliklari:**
- Xavfsizlik yo'q (ma'lumotlar ochiq uzatiladi)
- Parol va foydalanuvchi nomi shifrlangan emas
- Zamonaviy firewall'lar bilan muammolar
- Ikki portdan foydalanish murakkablik yaratadi
- Man-in-the-middle hujumlariga moyil

### 2.7. FTP Amaliy Qo'llanilishi

```bash
# Buyruq satridan FTP ishlatish misoli (Linux/Unix)
ftp ftp.example.com
# Foydalanuvchi nomi: user
# Parol: ********

# Faylni yuklash
put localfile.txt remotefile.txt

# Faylni yuklab olish
get remotefile.txt localfile.txt

# Chiqish
bye
```

---

## 3. TFTP (Trivial File Transfer Protocol)

### 3.1. TFTP Protokolining Ta'rifi

**TFTP (Trivial File Transfer Protocol)** - bu FTP protokolining soddalashtirilgan versiyasidir. TFTP 1981-yilda RFC 783 (keyinchalik RFC 1350) da standartlashtirilgan va juda oddiy fayl uzatish ehtiyojlari uchun mo'ljallangan.

### 3.2. TFTP Arxitekturasi

#### 3.2.1. Asosiy Xususiyatlari

- **UDP protokolidan foydalanadi** - Port 69
- **Autentifikatsiya yo'q** - foydalanuvchi nomi va parol talab qilinmadi
- **Juda oddiy** - faqat 5 ta buyruq
- **Kichik hajm** - protokol implementatsiyasi juda yengil
- **Ishonchliligi past** - UDP tufayli

#### 3.2.2. TFTP Buyruqlari

TFTP faqat beshta asosiy operatsiyaga ega:

1. **RRQ (Read Request)** - Faylni o'qish so'rovi
2. **WRQ (Write Request)** - Faylni yozish so'rovi
3. **DATA** - Ma'lumot paketlari
4. **ACK (Acknowledgment)** - Tasdiqlash
5. **ERROR** - Xato xabari

### 3.3. TFTP Ishlash Mexanizmi

#### 3.3.1. Ma'lumot Uzatish Jarayoni

1. Mijoz RRQ yoki WRQ paketini yuboradi
2. Server ma'lumotni 512 baytlik bloklarda yuboradi
3. Har bir DATA paketidan keyin ACK kutiladi
4. 512 baytdan kichik paket uzatish oxirini bildiradi
5. Xato yuz berganda ERROR paketi yuboriladi

#### 3.3.2. Timeout va Qayta Yuborish

- Agar ACK kelmasa, paket qayta yuboriladi
- Standart timeout: 5 sekund
- Maksimal qayta urinishlar: 5 marta
- Oddiy lekin samarali ishonchlilik mexanizmi

### 3.4. TFTP Qo'llanilish Sohalari

TFTP asosan quyidagi vaziyatlarda ishlatiladi:

1. **Tarmoq qurilmalarini boot qilish**
   - Router va switch'larni ishga tushirish
   - PXE (Preboot Execution Environment) orqali kompyuterlarni yuklash
   - Diskless workstation'larni ishga tushirish

2. **Firmware yangilash**
   - Tarmoq qurilmalari uchun
   - VoIP telefonlar uchun
   - IoT qurilmalari uchun

3. **Konfiguratsiya fayllarini saqlash**
   - Router konfiguratsiyalarini backup qilish
   - Oddiy sozlamalarni uzatish

4. **Embedded tizimlar**
   - Resurslari cheklangan qurilmalar
   - Boot loader'lar

### 3.5. TFTP Afzalliklari va Kamchiliklari

**Afzalliklari:**
- Juda oddiy implementatsiya
- Minimal resurs talab qiladi
- Tez ishlaydi (kichik fayllar uchun)
- Diskless boot uchun ideal
- Kichik hajmdagi kod

**Kamchiliklari:**
- Xavfsizlik yo'q
- Autentifikatsiya mexanizmi yo'q
- Katalog operatsiyalari yo'q
- Faqat fayllarni o'qish/yozish
- UDP tufayi ishonchsizroq
- Katta fayllar uchun mos emas
- 512 baytlik blok cheklovi

### 3.6. TFTP va FTP Taqqoslash

| Xususiyat | FTP | TFTP |
|-----------|-----|------|
| Transport protokol | TCP | UDP |
| Portlar | 20, 21 | 69 |
| Autentifikatsiya | Ha | Yo'q |
| Komplekslik | Murakkab | Oddiy |
| Buyruqlar soni | 30+ | 5 |
| Katalog operatsiyalari | Ha | Yo'q |
| Xavfsizlik | Past | Yo'qqa teng |
| Qo'llanish | Umumiy maqsad | Boot, firmware |

### 3.7. TFTP Amaliy Misol

```bash
# Linux'da TFTP ishlatish
tftp 192.168.1.1
tftp> get config.txt
tftp> put backup.cfg
tftp> quit

# Yoki bir qatorda
tftp -i 192.168.1.1 get ios.bin
```

---

## 4. SFTP (SSH File Transfer Protocol)

### 4.1. SFTP Protokolining Ta'rifi

**SFTP (SSH File Transfer Protocol)** - bu SSH (Secure Shell) protokoli ustiga qurilgan xavfsiz fayl uzatish protokolidir. SFTP 1990-yillarning oxirida ishlab chiqilgan va SSH 2.0 protokolining bir qismi sifatida RFC 4251-4254 da standartlashtirilgan.

**Muhim:** SFTP va FTPS (FTP Secure) turli protokollar ekanligini ta'kidlash kerak. FTPS FTP+SSL/TLS, SFTP esa butunlay boshqa protokoldir.

### 4.2. SFTP Arxitekturasi

#### 4.2.1. SSH Asoslari

SFTP SSH tunneli orqali ishlaydi:
- SSH ulanishi o'rnatiladi (Port 22)
- Autentifikatsiya amalga oshiriladi
- Shifrlangan kanal ochiladi
- SFTP protokoli SSH ustida ishlaydi

#### 4.2.2. Bitta Ulanish

FTP'dan farqli ravishda, SFTP:
- Faqat bitta TCP ulanishidan foydalanadi
- Buyruqlar va ma'lumotlar bir kanalda uzatiladi
- Port 22 (SSH standart porti)
- Firewall bilan muammolar yo'q

### 4.3. SFTP Xavfsizlik Xususiyatlari

#### 4.3.1. Shifrlash

SFTP barcha ma'lumotlarni shifrlaydi:
- **Simmetrik shifrlash**: AES, 3DES, Blowfish
- **Assimetrik shifrlash**: RSA, DSA, ECDSA
- **Ma'lumot yaxlitligi**: HMAC algoritmlar
- **Kalit almashinuvi**: Diffie-Hellman

#### 4.3.2. Autentifikatsiya Usullari

1. **Parol autentifikatsiyasi**
   - Oddiy foydalanuvchi nomi va parol
   - Shifrlangan kanal orqali uzatiladi

2. **Kalitga asoslangan autentifikatsiya**
   - Ochiq/yopiq kalit juftligi
   - Parolga qaraganda xavfsizroq
   - Avtomatlashtirish uchun ideal

3. **Ikki faktorli autentifikatsiya**
   - Parol + OTP (One-Time Password)
   - Yuqori xavfsizlik talab qilinadigan muhitlar uchun

#### 4.3.3. Xavfsizlik Afzalliklari

- Man-in-the-middle hujumlardan himoya
- Paketlarni ushlab qolishdan himoya
- Ma'lumotlarning yaxlitligini ta'minlash
- Server va mijoz autentifikatsiyasi
- Session hijacking'dan himoya

### 4.4. SFTP Operatsiyalari

SFTP keng imkoniyatlar beradi:

#### 4.4.1. Fayl Operatsiyalari
- Fayllarni yuklash va yuklab olish
- Fayllarni o'chirish
- Fayllarni qayta nomlash
- Fayl atributlarini o'zgartirish
- Fayl ruxsatlarini boshqarish (chmod)

#### 4.4.2. Katalog Operatsiyalari
- Katalog yaratish va o'chirish
- Katalog tarkibini ko'rish
- Katalog atributlarini o'zgartirish
- Kataloglar bo'yicha navigatsiya

#### 4.4.3. Qo'shimcha Imkoniyatlar
- Symbolic link'lar bilan ishlash
- Fayl egasini o'zgartirish
- Vaqt tamg'alarini boshqarish
- Fayl hajmini olish

### 4.5. SFTP Protokol Xabarlari

SFTP quyidagi asosiy xabar turlarini ishlatadi:

| Xabar turi | Maqsadi |
|------------|---------|
| SSH_FXP_INIT | Protokol initsializatsiyasi |
| SSH_FXP_OPEN | Faylni ochish |
| SSH_FXP_CLOSE | Faylni yopish |
| SSH_FXP_READ | Fayldan o'qish |
| SSH_FXP_WRITE | Faylga yozish |
| SSH_FXP_REMOVE | Faylni o'chirish |
| SSH_FXP_RENAME | Faylni qayta nomlash |
| SSH_FXP_MKDIR | Katalog yaratish |
| SSH_FXP_RMDIR | Katalogni o'chirish |
| SSH_FXP_STAT | Fayl atributlarini olish |

### 4.6. SFTP vs FTP: Batafsil Taqqoslash

| Xususiyat | FTP | SFTP |
|-----------|-----|------|
| Xavfsizlik | Yo'q | Yuqori |
| Shifrlash | Yo'q | Ha (SSH) |
| Portlar | 20, 21 | 22 |
| Ulanishlar | 2 ta (control, data) | 1 ta |
| Firewall | Muammo | Oson |
| Autentifikatsiya | Oddiy | Ko'p variantli |
| Tezlik | Tezroq | Biroz sekinroq |
| Resurs talabi | Past | O'rtacha |
| Standartlashtirish | RFC 959 | RFC 4251-4254 |
| Mos kelish | Universal | SSH kerak |

### 4.7. SFTP Qo'llanilish Sohalari

SFTP quyidagi sohalarda keng qo'llaniladi:

1. **Veb-hosting va sayt boshqaruvi**
   - WordPress va boshqa CMS'lar
   - Statik saytlarni yuklash
   - Xavfsiz kontent boshqaruvi

2. **Korporativ muhit**
   - Moliyaviy ma'lumotlarni uzatish
   - Maxfiy hujjatlarni almashish
   - Kompaniya ichida xavfsiz fayl sharing

3. **Ma'lumotlar bazasi backup**
   - Xavfsiz zaxira nusxalari
   - Uzoq serverga ma'lumot uzatish

4. **Avtomatlashtirilgan jarayonlar**
   - Script'lar orqali fayl uzatish
   - CI/CD pipeline'larda deployment
   - Scheduled backup vazifalar

### 4.8. SFTP Amaliy Misol

```bash
# SFTP seansini boshlash
sftp user@example.com

# Masofadagi katalogni ko'rish
sftp> ls

# Mahalliy katalogni ko'rish
sftp> lls

# Faylni yuklash
sftp> put localfile.txt

# Faylni yuklab olish
sftp> get remotefile.txt

# Katalog yaratish
sftp> mkdir newfolder

# Faylni o'chirish
sftp> rm oldfile.txt

# Chiqish
sftp> exit
```

**Kalit bilan ulanish:**
```bash
# SSH kaliti yaratish
ssh-keygen -t rsa -b 4096

# Ochiq kalitni serverga ko'chirish
ssh-copy-id user@example.com

# Kalit bilan SFTP ulanish
sftp -i ~/.ssh/id_rsa user@example.com
```

---

## 5. Protokollarning Qiyosiy Tahlili

### 5.1. Umumiy Taqqoslash Jadvali

| Parametr | FTP | TFTP | SFTP |
|-----------|-----|------|------|
| **Transport** | TCP | UDP | SSH/TCP |
| **Port(lar)** | 20, 21 | 69 | 22 |
| **Xavfsizlik** | ❌ Yo'q | ❌ Yo'q | ✅ Yuqori |
| **Shifrlash** | ❌ Yo'q | ❌ Yo'q | ✅ Ha |
| **Autentifikatsiya** | ✅ Ha | ❌ Yo'q | ✅ Kuchli |
| **Komplekslik** | O'rtacha | Juda oddiy | Murakkab |
| **Ishonchlilik** | Yuqori | Past | Yuqori |
| **Tezlik** | Tez | Tez | O'rtacha |
| **Katalog operatsiyalari** | ✅ Ha | ❌ Yo'q | ✅ Ha |
| **Fayl hajmi** | Cheklovsiz | Cheklangan | Cheklovsiz |
| **Firewall** | Muammo | Muammo | Oson |
| **Qo'llanish sohasi** | Umumiy | Boot/Firmware | Xavfsiz uzatish |

### 5.2. Qachon Qaysi Protokolni Ishlatish Kerak

#### 5.2.1. FTP ni tanlang:
- Ichki tarmoqda (Internet'siz)
- Legacy tizimlarda
- Juda tez uzatish kerak bo'lganda
- Xavfsizlik muhim emas

#### 5.2.2. TFTP ni tanlang:
- Tarmoq qurilmalarini boot qilishda
- Firmware yangilashda
- Minimal resurs bilan ishlaydigan qurilmalarda
- Juda oddiy vazifalar uchun

#### 5.2.3. SFTP ni tanlang:
- Internet orqali uzatishda
- Maxfiy ma'lumotlar uchun
- Zamonaviy tizimlarda
- Xavfsizlik ustuvor bo'lganda
- Production muhitda

### 5.3. Zamonaviy Tendentsiyalar

#### 5.3.1. Protokollarning Kelajagi

**FTP:**
- Asta-sekin e'tibordan chiqmoqda
- Ko'p brauzerlar FTP qo'llab-quvvatlashni to'xtatdi
- Legacy tizimlar uchun qolmoqda

**TFTP:**
- O'z niche'ida barqaror
- IoT va embedded tizimlarda davom etadi
- Boot protokol sifatida saqlanadi

**SFTP:**
- Faol rivojlanmoqda
- Standart xavfsiz fayl uzatish protokoli
- Korporativ muhitda keng qabul qilingan

#### 5.3.2. Alternativ Yechimlar

Zamonaviy muqobil protokollar:
- **FTPS** (FTP + SSL/TLS) - FTP'ning xavfsiz versiyasi
- **HTTPS** - Oddiy fayl yuklash uchun
- **SCP** (Secure Copy) - SFTP'ga o'xshash, lekin oddiyroq
- **WebDAV** - HTTP asosida fayl boshqaruvi
- **rsync** - Sinxronizatsiya uchun

---

## 6. Xavfsizlik va Himoya Choralari

### 6.1. Umumiy Xavfsizlik Tamoyillari

#### 6.1.1. Kuchli Autentifikatsiya
- Murakkab parollardan foydalanish
- Kalit asosida autentifikatsiya (SFTP uchun)
- Ikki faktorli autentifikatsiya yoqish
- Doimiy ravishda parollarni yangilash

#### 6.1.2. Tarmoq Darajasidagi Himoya
- Firewall sozlamalari
- VPN orqali ulanish
- IP whitelist yaratish
- Port forwarding cheklash

#### 6.1.3. Server Sozlamalari
- Anonym kirish taqiqlash
- Chroot jail muhitini sozlash
- Foydalanuvchi ruxsatlarini cheklash
- Log fayllarni yuritish

### 6.2. FTP Xavfsizligini Oshirish

FTP xavfsizligini yaxshilash usullari:

1. **FTPS (FTP Secure) ga o'tish**
   - SSL/TLS shifrlash qo'shish
   - Sertifikatlar bilan ishlash
   - Explicit yoki Implicit rejim

2. **Foydalanuvchi boshqaruvi**
   - Minimal zarur ruxsatlar berish
   - Virtual foydalanuvchilar yaratish
   - Har bir foydalanuvchiga alohida katalog

3. **Monitoring va audit**
   - Faol ulanishlarni kuzatish
   - Xato urinishlarni qayd etish
   - Muntazam audit o'tkazish

### 6.3. SFTP Best Practices

SFTP dan xavfsiz foydalanish bo'yicha tavsiyalar:

1. **Kalit boshqaruvi**
   - RSA 4096-bit yoki ECDSA kalitlar ishlatish
   - Private kalitlarni parol bilan himoya qilish
   - Kalitlarni xavfsiz saqlash
   - Eski kalitlarni o'chirish

2. **SSH konfiguratsiyasi**
   - Root login taqiqlash
   - Parol autentifikatsiyasini o'chirish
   - SSH protokol 2 ishlatish
   - Timeout sozlamalari

3. **Regulyar tekshiruvlar**
   - SSH log'larini tahlil qilish
   - Failed login attempts monitoring
   - Noto'g'ri trafikni aniqlash

---

## 7. Amaliy Qo'llanish va Dasturiy Ta'minot

### 7.1. Mashhur FTP Server Dasturlari

#### 7.1.1. ProFTPD (Linux)
- Yuqori konfiguratsiya qobiliyati
- Virtual hosting qo'llab-quvvatlash
- Yaxshi dokumentatsiya

#### 7.1.2. vsftpd (Very Secure FTP Daemon)
- Xavfsizlikga e'tibor
- Tez va barqaror
- Linux uchun ideal

#### 7.1.3. FileZilla Server (Windows)
- Grafikali interfeys
- Oson sozlash
- Windows uchun optimal

### 7.2. SFTP Server Sozlash

#### 7.2.1. OpenSSH Server
Ko'pchilik Linux distribut'tsiyalarida o'rnatilgan:

```bash
# SFTP uchun OpenSSH konfiguratsiyasi
# /etc/ssh/sshd_config faylida

Subsystem sftp /usr/lib/openssh/sftp-server

# SFTP faqat foydalanuvchilar uchun
Match User sftpuser
    ForceCommand internal-sftp
    ChrootDirectory /home/sftpuser
    AllowTcpForwarding no
```

### 7.3. Mijoz Dasturlari

#### 7.3.1. GUI Mijozlar
- **FileZilla** - Cross-platform, bepul
- **WinSCP** - Windows uchun, kuchli
- **Cyberduck** - Mac va Windows uchun
- **Transmit** - Mac uchun premium

#### 7.3.2. Buyruq Satri Vositalari
- **ftp** - Standart FTP mijozi
- **sftp** - OpenSSH SFTP mijozi
- **lftp** - Takomillashtirilgan mijoz
- **curl** - Ko'p maqsadli vosita

### 7.4. Avtomatlashtirilgan Fayl Uzatish

#### 7.4.1. Script Yordamida

**Bash script misoli (SFTP):**
```bash
#!/bin/bash
# SFTP orqali avtomatik backup

HOST="backup.example.com"
USER="backupuser"
BACKUP_DIR="/home/backups"
LOCAL_FILE="/tmp/backup_$(date +%Y%m%d).tar.gz"

sftp -i ~/.ssh/backup_key $USER@$HOST <<EOF
cd $BACKUP_DIR
put $LOCAL_FILE
bye
EOF
```

#### 7.4.2. Cron Job Orqali

```bash
# Har kuni soat 2:00 da backup
0 2 * * * /home/user/scripts/backup_sftp.sh
```

---

## 8. Muammolarni Bartaraf Etish

### 8.1. Umumiy Muammolar va Yechimlar

#### 8.1.1. Ulanish Muammolari

**Muammo:** "Connection refused"
- **Sabab:** Server ishlamayotgan yoki firewall bloklagan
- **Yechim:** 
  - Server statusini tekshiring
  - Firewall qoidalarini ko'zdan kechiring
  - Portlarni tekshiring (netstat, nmap)

**Muammo:** "Authentication failed"
- **Sabab:** Noto'g'ri login ma'lumotlari yoki ruxsat muammolari
- **Yechim:**
  - Foydalanuvchi nomi va parolni tekshiring
  - Server log'larini ko'ring
  - Foydalanuvchi ruxsatlarini tekshiring

**Muammo:** "Network unreachable"
- **Sabab:** Tarmoq ulanishi muammolari
- **Yechim:**
  - Ping orqali ulanishni tekshiring
  - Routing jadvallarini ko'ring
  - DNS ishlashini tekshiring

#### 8.1.2. FTP Passive Mode Muammolari

**Simptom:** Active rejimda ishlamaydi, passive rejimda ishlaydi
- **Sabab:** Firewall incoming ulanishlarni bloklaydi
- **Yechim:**
  - Passive rejimga o'ting
  - Firewall'da port range oching
  - Server konfiguratsiyasida passive port range belgilang

#### 8.1.3. SFTP Kalit Autentifikatsiyasi Muammolari

**Muammo:** "Permission denied (publickey)"
- **Sabab:** Kalit sozlamalari noto'g'ri
- **Yechim:**
  - `~/.ssh/authorized_keys` faylini tekshiring
  - Fayl ruxsatlarini to'g'rilang (600 yoki 644)
  - SSH agent ishga tushganini tekshiring
  ```bash
  chmod 600 ~/.ssh/id_rsa
  chmod 644 ~/.ssh/id_rsa.pub
  chmod 700 ~/.ssh
  ```

#### 8.1.4. Tezlik Muammolari

**Muammo:** Sekin fayl uzatish
- **Sabab:** Tarmoq bandwidth, latency yoki server yuklanganligi
- **Yechim:**
  - MTU (Maximum Transmission Unit) ni optimize qiling
  - Parallel ulanishlar sonini oshiring
  - Kompressiyani yoqing (SFTP uchun)
  - Tarmoq sifatini tekshiring

### 8.2. Diagnostika Vositalari

#### 8.2.1. Tarmoq Diagnostikasi

```bash
# Port ochiq ekanligini tekshirish
telnet example.com 21
nc -zv example.com 22

# Tarmoq yo'lini kuzatish
traceroute example.com

# DNS ni tekshirish
nslookup example.com
dig example.com
```

#### 8.2.2. FTP/SFTP Debugging

```bash
# FTP debug rejimida
ftp -d example.com

# SFTP verbose rejimda
sftp -vvv user@example.com

# SSH connection test
ssh -vvv user@example.com
```

#### 8.2.3. Log Fayllarni Tahlil Qilish

```bash
# Linux'da FTP loglar
tail -f /var/log/vsftpd.log
tail -f /var/log/proftpd/proftpd.log

# SSH/SFTP loglar
tail -f /var/log/auth.log
journalctl -u sshd -f
```

---

## 9. Performance Optimizatsiyasi

### 9.1. FTP Server Optimizatsiyasi

#### 9.1.1. Maksimal Ulanishlar
- Parallel ulanishlar sonini cheklash
- Per-IP ulanish limiti sozlash
- Global maksimum ulanishlar

**ProFTPD konfiguratsiyasi:**
```
MaxInstances 50
MaxClients 30
MaxClientsPerHost 5
```

#### 9.1.2. Bandwidth Boshqaruvi

**vsftpd konfiguratsiyasi:**
```
anon_max_rate=1024000  # 1 MB/s anonim uchun
local_max_rate=0       # Cheklovsiz registered uchun
```

#### 9.1.3. Timeout Sozlamalari

```
idle_session_timeout=300  # 5 daqiqa
data_connection_timeout=120  # 2 daqiqa
```

### 9.2. SFTP Performance Tuning

#### 9.2.1. SSH Konfiguratsiyasi

**Client tomonda (`~/.ssh/config`):**
```
Host fastserver
    HostName example.com
    User username
    Compression yes
    CompressionLevel 6
    Ciphers aes128-gcm@openssh.com
    MACs hmac-sha2-256
```

#### 9.2.2. TCP Window Size

```bash
# Linux'da TCP buffer size'ni oshirish
sysctl -w net.ipv4.tcp_window_scaling=1
sysctl -w net.core.rmem_max=134217728
sysctl -w net.core.wmem_max=134217728
```

#### 9.2.3. Multiple Connections

Katta fayllarni parallel uzatish uchun:
```bash
# lftp ishlatib parallel ulanishlar
lftp -e "set sftp:connect-program 'ssh -a -x'; mirror -P 4 /remote /local" sftp://user@host
```

### 9.3. Network Level Optimizatsiya

#### 9.3.1. MTU Sozlash
- Optimal MTU qiymatini aniqlash
- Path MTU Discovery yoqish
- Jumbo frames (10 Gigabit tarmoqlarda)

#### 9.3.2. QoS (Quality of Service)
- FTP/SFTP trafikka ustuvorlik berish
- Bandwidth management
- Traffic shaping

---

## 10. Monitoring va Logging

### 10.1. Log Fayllarni Boshqarish

#### 10.1.1. FTP Logging

**vsftpd logging:**
```
xferlog_enable=YES
xferlog_std_format=YES
xferlog_file=/var/log/vsftpd.log
log_ftp_protocol=YES
```

**Log format:**
```
Mon Oct 27 14:30:15 2025 1 192.168.1.100 1234567 /home/user/file.txt b _ i r user ftp 0 * c
```

#### 10.1.2. SFTP Logging

**OpenSSH sshd_config:**
```
LogLevel INFO
SyslogFacility AUTH
Subsystem sftp /usr/lib/openssh/sftp-server -l INFO
```

### 10.2. Monitoring Tools

#### 10.2.1. Real-time Monitoring

```bash
# Aktiv FTP ulanishlarni ko'rish
netstat -tn | grep :21

# SFTP sessiyalarni kuzatish
ps aux | grep sftp-server

# Bandwidth monitoring
iftop -i eth0
nethogs
```

#### 10.2.2. Statistika va Hisobotlar

**Kunlik fayl uzatish statistikasi:**
```bash
#!/bin/bash
# FTP xferlog dan statistika
echo "Top 10 yuklab olingan fayllar:"
grep " o " /var/log/xferlog | awk '{print $9}' | sort | uniq -c | sort -rn | head -10

echo "Top 10 foydalanuvchilar:"
awk '{print $8}' /var/log/xferlog | sort | uniq -c | sort -rn | head -10
```

### 10.3. Alerting va Notifikatsiya

#### 10.3.1. Failed Login Attempts

```bash
# SSH brute-force hujumlarni aniqlash
cat /var/log/auth.log | grep "Failed password" | awk '{print $11}' | sort | uniq -c | sort -rn
```

#### 10.3.2. Disk Space Monitoring

```bash
# Disk to'lganida ogohlantirish
#!/bin/bash
THRESHOLD=90
CURRENT=$(df /home | tail -1 | awk '{print $5}' | sed 's/%//')

if [ $CURRENT -gt $THRESHOLD ]; then
    echo "Disk space kritik: ${CURRENT}%" | mail -s "Disk Alert" admin@example.com
fi
```

---

## 11. Compliance va Standartlar

### 11.1. Xalqaro Standartlar

#### 11.1.1. ISO/IEC 27001
- Ma'lumot xavfsizligi menejment tizimi
- Shifrlangan uzatish talab qiladi
- Audit va monitoring zaruriyati

#### 11.1.2. PCI DSS (Payment Card Industry)
- Kredit karta ma'lumotlari himoyasi
- FTP taqiqlanadi (SFTP yoki FTPS majburiy)
- Kuchli shifrlash talabi

#### 11.1.3. HIPAA (Healthcare)
- Tibbiy ma'lumotlar maxfiyligi
- End-to-end shifrlash
- Access control va audit trail

#### 11.1.4. GDPR (Europe)
- Shaxsiy ma'lumotlar himoyasi
- Ma'lumot uzatishda xavfsizlik
- Data residency talablari

### 11.2. Best Practices Checklist

**Server sozlash:**
- [ ] Anonym kirish o'chirilgan
- [ ] Kuchli parollar majburiy
- [ ] SSL/TLS yoki SSH shifrlash yoqilgan
- [ ] Firewall to'g'ri sozlangan
- [ ] Regular backup o'rnatilgan
- [ ] Log rotation sozlangan
- [ ] Security updates avtomatik

**Foydalanuvchi boshqaruvi:**
- [ ] Minimal zarur ruxsatlar
- [ ] Muntazam parol yangilash
- [ ] Inactive akkauntlarni o'chirish
- [ ] Role-based access control
- [ ] Chroot environment

**Monitoring va audit:**
- [ ] Log fayllar yozilmoqda
- [ ] Failed login tracking
- [ ] File transfer audit
- [ ] Disk space monitoring
- [ ] Performance metrics

---

## 12. Kelajak Istiqbollari va Yangi Texnologiyalar

### 12.1. Cloud-based Fayl Uzatish

#### 12.1.1. Managed FTP Services
- AWS Transfer Family
- Azure File Transfer
- Google Cloud Storage Transfer

**Afzalliklari:**
- Infrastruktura boshqaruvi yo'q
- Avtomatik scaling
- Built-in backup va disaster recovery
- Pay-as-you-go model

#### 12.1.2. Hybrid Solutions
- On-premise va cloud integratsiyasi
- Multi-cloud strategiyalar
- Edge computing bilan birlashish

### 12.2. API-based Fayl Uzatish

#### 12.2.1. RESTful API
- HTTP/HTTPS asosida
- JSON yoki XML formatlar
- OAuth autentifikatsiyasi

#### 12.2.2. GraphQL
- Flexible data querying
- Real-time subscriptions
- Efficient data transfer

### 12.3. Blockchain va Distributed Storage

#### 12.3.1. IPFS (InterPlanetary File System)
- Desentralizatsiyalangan fayl saqlash
- Content addressing
- P2P tarmoq

#### 12.3.2. Blockchain Verification
- Fayl yaxlitligini tekshirish
- Immutable audit trails
- Smart contracts bilan integratsiya

### 12.4. AI va Machine Learning Integratsiyasi

#### 12.4.1. Intelligent File Management
- Avtomatik fayl klassifikatsiyasi
- Predictive caching
- Anomaly detection

#### 12.4.2. Security Enhancement
- Behavioral analysis
- Threat detection
- Automated response

### 12.5. Quantum-safe Kriptografiya

Kelajakda quantum kompyuterlar mavjud shifrlash algoritmlarini buzishi mumkin:
- Post-quantum kriptografiya algoritmlari
- Quantum key distribution (QKD)
- Hybrid classical-quantum systems

---

## 13. Xulosa

### 13.1. Asosiy Xulosalar

1. **FTP (File Transfer Protocol)**
   - Eng qadimgi va keng tarqalgan protokol
   - Oddiy va tushunarli
   - Xavfsizlik kamchiliklari mavjud
   - Legacy tizimlarda hali ham ishlatiladi
   - Zamonaviy muhitlarda tavsiya etilmaydi

2. **TFTP (Trivial File Transfer Protocol)**
   - Juda oddiy va minimal protokol
   - Tarmoq qurilmalarini boot qilish uchun ideal
   - Xavfsizlik va autentifikatsiya yo'q
   - Resurs cheklangan muhitlar uchun
   - Maxsus maqsadlar uchun saqlanadi

3. **SFTP (SSH File Transfer Protocol)**
   - Zamonaviy va xavfsiz yechim
   - SSH shifrlash va autentifikatsiyasi
   - Keng funksionallik
   - Internet orqali ishlatish uchun optimal
   - Kelajakda standart protokol

### 13.2. Protokol Tanlash Bo'yicha Tavsiyalar

**Yangi loyihalar uchun:**
- SFTP ni birinci o'rinda ko'rib chiqing
- Xavfsizlik talablari yuqori bo'lsa - SFTP majburiy
- Faqat ichki tarmoqda - FTP yoki FTPS
- Embedded tizimlarda - TFTP

**Mavjud tizimlarni yangilash:**
- FTP dan SFTP ga migratsiya rejasini tuzing
- Bosqichma-bosqich o'tish strategiyasi
- Foydalanuvchilarni o'rgatish
- Parallel ishlash davri

### 13.3. Xavfsizlik - Ustuvor Vazifa

Har qanday fayl uzatish tizimida:
- **Konfidensiallik** - ma'lumotlar maxfiyligi
- **Yaxlitlik** - ma'lumotlarning o'zgarmasligi
- **Autentifikatsiya** - foydalanuvchini tasdiqlash
- **Authorization** - ruxsatlarni boshqarish
- **Audit** - barcha operatsiyalarni qayd etish

### 13.4. O'rganish Yo'li

Talabalarga tavsiyalar:
1. FTP asoslaridan boshlang
2. TFTP soddaligini tushunib oling
3. SFTP/SSH chuqur o'rganing
4. Amaliy tajriba to'plang
5. Xavfsizlik tamoyillarini o'zlashtirig
6. Monitoring va troubleshooting ko'nikmalarini rivojlantiring
7. Zamonaviy alternativalarni kuzatib boring

---

## 14. Qo'shimcha Manbalar

### 14.1. Rasmiy Hujjatlar

**RFC Dokumentlar:**
- RFC 959 - File Transfer Protocol (FTP)
- RFC 1350 - TFTP Protocol (Revision 2)
- RFC 4251 - SSH Protocol Architecture
- RFC 4252 - SSH Authentication Protocol
- RFC 4253 - SSH Transport Layer Protocol
- RFC 4254 - SSH Connection Protocol

### 14.2. Foydali Veb-saytlar

- **OpenSSH:** https://www.openssh.com/
- **ProFTPD:** http://www.proftpd.org/
- **vsftpd:** https://security.appspot.com/vsftpd.html
- **FileZilla:** https://filezilla-project.org/

### 14.3. Kitoblar va O'quv Materiallari

1. **"SSH, The Secure Shell: The Definitive Guide"** - Daniel J. Barrett
2. **"Network Security Essentials"** - William Stallings
3. **"TCP/IP Illustrated"** - W. Richard Stevens

### 14.4. Online Kurslar

- Coursera - Computer Networks
- Udemy - Network Protocols va Security
- Cybrary - Network Security kurslari
- LinkedIn Learning - FTP va SFTP tutorials

### 14.5. Amaliy Mashg'ulotlar

**Laboratoriya ishlari uchun tavsiyalar:**
1. Virtual mashinada FTP server o'rnatish
2. SFTP konfiguratsiyasi va xavfsizlik
3. TFTP orqali router'ni boot qilish simulyatsiyasi
4. Wireshark da protokollarni tahlil qilish
5. Xavfsizlik audit o'tkazish

---

## 15. Test Savollari

### 15.1. Nazariy Savollar

1. FTP protokoli qaysi transport protokolidan foydalanadi va nima uchun ikkita port ishlatiladi?
2. TFTP ning FTP dan asosiy farqlari nimalardan iborat?
3. SFTP va FTPS orasidagi farqni tushuntiring.
4. FTP Active va Passive rejimlari qanday ishlaydi?
5. TFTP qaysi vaziyatlarda ishlatiladi va nima uchun?
6. SFTP da qanday autentifikatsiya usullari mavjud?
7. FTP protokolining xavfsizlik zaiflikları nimalardan iborat?
8. TFTP UDP dan foydalanganda ishonchlilikni qanday ta'minlaydi?

### 15.2. Amaliy Topshiriqlar

1. Linux serverda vsftpd o'rnatib, sozlang
2. SFTP kalit autentifikatsiyasini sozlang
3. FTP trafikini Wireshark da ushlang va tahlil qiling
4. SFTP orqali avtomatik backup script yozing
5. FTP serverda chroot jail muhitini sozlang
6. TFTP server o'rnatib, test faylni uzating

### 15.3. Muammolarni Hal Qilish

1. "Connection refused" xatosini qanday bartaraf etasiz?
2. FTP passive mode ishlamasa nima qilish kerak?
3. SFTP "Permission denied" xatosi yechimi?
4. Sekin fayl uzatishni qanday optimizatsiya qilish mumkin?

---

## 16. Yakuniy Fikrlar

Fayl uzatish protokollari zamonaviy IT infratuzilmasining ajralmas qismidir. FTP, TFTP va SFTP har biri o'z o'rnida muhim rol o'ynaydi:

- **FTP** tarixiy ahamiyatga ega va hali ham ko'plab legacy tizimlarda ishlatiladi
- **TFTP** o'zining soddaligi tufayli embedded va tarmoq qurilmalarida zarur
- **SFTP** zamonaviy xavfsizlik talablariga javob beruvchi optimal yechim

Talabalar bu protokollarning nazariy asoslari, amaliy qo'llanilishi va xavfsizlik jihatlarini puxta o'zlashtirishlari zarur. Kelajakda ushbu bilimlar tarmoq muhandisligi, tizim administratorligi va kiberxavfsizlik sohalarida muvaffaqiyatli faoliyat yuritish uchun mustahkam poydevor bo'ladi.

---

**Muallif:** Kompyuter tarmoqlari kursi o'qituvchilari  
**Sana:** 2025-yil  
**Versiya:** 1.0

**© Barcha huquqlar himoyalangan. Ushbu material faqat ta'lim maqsadlarida foydalanish uchun mo'ljallangan.**