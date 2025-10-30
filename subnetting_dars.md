# Subnetting - Tarmoqlarni Kichik Segmentlarga Bo'lish

## Dars Ishlanma
**Fan:** Kompyuter tarmoqlari  
**Mavzu:** Subnetting - tarmoqlarni kichik segmentlarga bo'lish  
**Davomiyligi:** 4 soat (2 ta dars)

---

## 1. Kirish

### 1.1 Mavzuning dolzarbligi

Zamonaviy kompyuter tarmoqlarida IP manzillarni samarali boshqarish va tarmoqni mantiqiy segmentlarga bo'lish muhim ahamiyatga ega. Subnetting - bu katta tarmoqni kichikroq, boshqariladigan qism-tarmoqlarga (subnet) bo'lish jarayoni bo'lib, u tarmoq resurslarini optimal taqsimlash, xavfsizlikni oshirish va tarmoq trafigini samarali boshqarish imkonini beradi.

### 1.2 Darsning maqsadi

- Talabalar subnetting tushunchasini chuqur o'zlashtirishlari
- IP manzillar va subnet maskalari bilan ishlash ko'nikmalarini rivojlantirishlari
- Tarmoqni kichik segmentlarga bo'lish zarurligi va afzalliklarini tushunishlari
- Subnetting amaliyotida qo'llaniladigan asosiy usullar va formulalarni o'rganishlari

---

## 2. Nazariy Qism

### 2.1 Subnetting Nima?

**Subnetting** (inglizcha: subnet - qism tarmoq) - bu bir IP tarmoqni bir nechta kichikroq mantiqiy tarmoqlarga bo'lish jarayoni. Bu jarayon subnet mask (qism tarmoq niqobi) yordamida amalga oshiriladi va tarmoq manzilining qaysi qismi tarmoq identifikatoriga, qaysi qismi esa host identifikatoriga tegishli ekanligini belgilaydi.

Subnetting asosiy ikki komponentdan iborat:
- **Tarmoq qismi (Network portion)** - barcha hostlar uchun bir xil bo'lgan qism
- **Host qismi (Host portion)** - har bir qurilma uchun noyob bo'lgan qism

### 2.2 Subnettingning Kelib Chiqishi va Rivojlanishi

1980-yillarda Internetning tez sur'atlar bilan o'sishi bilan IP manzillar taqchilligi muammosi paydo bo'ldi. Dastlabki classful addressing tizimi (A, B, C sinflar) IP manzillarni samarasiz ishlatishga olib keldi. Masalan, C sinf tarmoq 254 ta hostni qo'llab-quvvatlagan bo'lsa-da, ko'pgina tashkilotlar bunga muhtoj emas edi. Shu muammo CIDR (Classless Inter-Domain Routing) va subnetting texnologiyalarining yaratilishiga sabab bo'ldi.

### 2.3 Subnettingning Afzalliklari

1. **IP manzillarni tejash**: Katta tarmoqlar o'rniga faqat kerakli o'lchamdagi tarmoqlar yaratish
2. **Tarmoq xavfsizligini oshirish**: Turli bo'limlarni mantiqan ajratish va kirish nazoratini yaxshilash
3. **Broadcast domenini kamaytirish**: Har bir subnet o'zining broadcast domeni bo'lib, bu tarmoq yukini kamaytiradi
4. **Tarmoqni boshqarish qulayligi**: Kichikroq tarmoqlarni boshqarish va nosozliklarni bartaraf etish osonroq
5. **Tarmoq samaradorligini oshirish**: Trafik lokallashtirish va tarmoq tiqilinchini kamaytirish
6. **Geografik yoki funktsional ajratish**: Turli joylashuvdagi yoki bo'limlardagi qurilmalarni mantiqiy guruhlash

### 2.4 IP Manzil Strukturasi

IPv4 manzil 32 bitdan iborat bo'lib, odatda to'rtta oktet (8 bitlik qism) ko'rinishida yoziladi:

```
192.168.1.100 = 11000000.10101000.00000001.01100100
```

Har bir oktet 0 dan 255 gacha qiymat olishi mumkin.

### 2.5 Subnet Mask (Tarmoq Niqobi)

Subnet mask IP manzilning qaysi qismi tarmoq identifikatori, qaysi qismi esa host identifikatori ekanligini ko'rsatadi. Subnet maskda tarmoq qismiga mos keladigan bitlar "1", host qismiga mos keladigan bitlar esa "0" qiymatiga ega.

**Standart Subnet Maskalar:**

- **Class A**: 255.0.0.0 (/8) - birinchi oktet tarmoq uchun
- **Class B**: 255.255.0.0 (/16) - birinchi ikki oktet tarmoq uchun
- **Class C**: 255.255.255.0 (/24) - birinchi uch oktet tarmoq uchun

**CIDR Notatsiyasi:**

Subnet maskni "/" belgisi va bitlar soni bilan ifodalash. Masalan:
- /24 = 255.255.255.0 (24 ta "1" bit)
- /28 = 255.255.255.240 (28 ta "1" bit)
- /30 = 255.255.255.252 (30 ta "1" bit)

### 2.6 Subnetting Matematik Asoslari

#### 2.6.1 Asosiy Formulalar

1. **Subnetlar soni** = 2^n
   - n = qarz olingan bitlar soni (host qismidan)

2. **Har bir subnetdagi hostlar soni** = 2^h - 2
   - h = host bitlari soni
   - 2 ayriladi (tarmoq manzili va broadcast manzili uchun)

3. **Subnet intervali** = 256 - subnet mask oxirgi o'nli qiymati

#### 2.6.2 Qarz Olish Kontseptsiyasi (Borrowing)

Subnetting jarayonida host qismidan bitlarni "qarz olib", ularni tarmoq qismiga qo'shamiz. Qancha ko'p bit qarz olsak, shuncha ko'p subnet yaratamiz, lekin har bir subnetda hostlar soni kamayadi.

**Misol:**
- Asl tarmoq: 192.168.1.0/24 (254 host)
- 1 bit qarz olamiz: /25 (2 subnet, har birida 126 host)
- 2 bit qarz olamiz: /26 (4 subnet, har birida 62 host)
- 3 bit qarz olamiz: /27 (8 subnet, har birida 30 host)

### 2.7 Tarmoq Turlari va Ularning Xususiyatlari

#### 2.7.1 Classful Addressing (Sinflarga Asoslangan)

**Class A (1.0.0.0 - 126.255.255.255)**
- Default mask: /8 (255.0.0.0)
- Tarmoqlar: 126 ta
- Har bir tarmoqdagi hostlar: 16,777,214
- Birinchi oktet: 0-127
- Ishlatilishi: Juda katta tashkilotlar

**Class B (128.0.0.0 - 191.255.255.255)**
- Default mask: /16 (255.255.0.0)
- Tarmoqlar: 16,384 ta
- Har bir tarmoqdagi hostlar: 65,534
- Birinchi oktet: 128-191
- Ishlatilishi: O'rta va yirik tashkilotlar

**Class C (192.0.0.0 - 223.255.255.255)**
- Default mask: /24 (255.255.255.0)
- Tarmoqlar: 2,097,152 ta
- Har bir tarmoqdagi hostlar: 254
- Birinchi oktet: 192-223
- Ishlatilishi: Kichik tarmoqlar

**Class D (224.0.0.0 - 239.255.255.255)**
- Multicast manzillar uchun
- Subnetting qo'llanilmaydi

**Class E (240.0.0.0 - 255.255.255.255)**
- Eksperimental maqsadlar uchun zahirada
- Ommaviy ishlatishda emas

#### 2.7.2 Classless Addressing (CIDR)

CIDR (Classless Inter-Domain Routing) - 1993 yilda joriy etilgan, IP manzillarni ancha moslashuvchan tarzda taqsimlash imkonini beruvchi sistema. CIDR yordamida istalgan o'lchamdagi tarmoqlar yaratish mumkin.

### 2.8 Maxsus IP Manzillar

- **Tarmoq manzili**: Subnetdagi birinchi manzil (barcha host bitlari 0)
- **Broadcast manzili**: Subnetdagi oxirgi manzil (barcha host bitlari 1)
- **Loopback manzili**: 127.0.0.1 - qurilmani o'zini test qilish uchun
- **Private IP ranges** (RFC 1918):
  - 10.0.0.0/8 (10.0.0.0 - 10.255.255.255)
  - 172.16.0.0/12 (172.16.0.0 - 172.31.255.255)
  - 192.168.0.0/16 (192.168.0.0 - 192.168.255.255)
- **APIPA**: 169.254.0.0/16 - DHCP mavjud bo'lmaganda avtomatik tayinlanadi

### 2.9 VLSM (Variable Length Subnet Masking)

VLSM - bu turli o'lchamdagi subnetlar yaratish imkonini beruvchi texnologiya. VLSM yordamida IP manzillarni yanada samaraliroq ishlatish mumkin, chunki har bir subnet o'zining alohida mask uzunligiga ega bo'lishi mumkin.

**VLSM afzalliklari:**
- IP manzillarni maksimal tejash
- Tarmoq topologiyasiga moslashuvchanlik
- Hierarchical tarmoq dizayni imkoniyati
- Marshrutlash jadvallari optimallashtirish

**VLSM qo'llash prinsiplari:**
1. Eng katta tarmoqdan boshlab subnet yaratish
2. Har bir subnet uchun zarur hostlar soniga qarab mask tanlash
3. Subnetlarni ketma-ketlikda joylashtirish (overlap qilmaslik)
4. Marshrutlash protokoli VLSM ni qo'llab-quvvatlashi kerak (RIPv2, OSPF, EIGRP)

### 2.10 Supernetting (Route Aggregation)

Supernetting - bu bir nechta kichik tarmoqlarni bitta katta tarmoqqa birlashtirish jarayoni. Bu marshrutlash jadvallarini qisqartirish va Internet'dagi marshrutlash samaradorligini oshirish uchun ishlatiladi.

**Supernetting shartlari:**
1. Tarmoqlar ketma-ket joylashgan bo'lishi kerak
2. Tarmoqlar soni 2 ning darajasi bo'lishi kerak (2, 4, 8, 16...)
3. Birinchi tarmoq manzili supernet mask bilan bo'linishi kerak

### 2.11 Subnetting Strategiyalari

#### 2.11.1 Fixed-Length Subnetting

Barcha subnetlar bir xil o'lchamda bo'ladi. Oddiy, lekin IP manzillarni tejash jihatidan unchalik samarali emas.

#### 2.11.2 Variable-Length Subnetting (VLSM)

Turli bo'limlarga turli o'lchamdagi subnetlar ajratiladi. Murakkab, lekin IP manzillarni tejashda juda samarali.

#### 2.11.3 Hierarchical Subnetting

Katta tashkilotlarda geografik yoki funktsional bo'linmalarga qarab ierarxik tarzda subnetlar yaratish.

---

## 3. Amaliy Qism

### 3.1 Subnetting Jarayoni Bosqichlari

**1-qadam:** Kerakli subnetlar sonini aniqlash  
**2-qadam:** Har bir subnetda kerakli hostlar sonini hisoblash  
**3-qadam:** Mos subnet maskni tanlash  
**4-qadam:** Subnet manzillarini hisoblash  
**5-qadam:** Host manzillari diapazonini aniqlash

### 3.2 Amaliy Misol 1: Oddiy Subnetting

**Masala:** 192.168.10.0/24 tarmoqni 4 ta subnetga bo'ling.

**Yechim:**

1. Subnetlar soni: 4 = 2^2, demak 2 bit qarz olish kerak
2. Yangi mask: /24 + 2 = /26 (255.255.255.192)
3. Har bir subnetdagi hostlar: 2^6 - 2 = 62 host
4. Subnet intervali: 256 - 192 = 64

**Subnetlar:**
- Subnet 1: 192.168.10.0/26 (hostlar: .1 - .62, broadcast: .63)
- Subnet 2: 192.168.10.64/26 (hostlar: .65 - .126, broadcast: .127)
- Subnet 3: 192.168.10.128/26 (hostlar: .129 - .190, broadcast: .191)
- Subnet 4: 192.168.10.192/26 (hostlar: .193 - .254, broadcast: .255)

### 3.3 Amaliy Misol 2: VLSM Bilan Ishlash

**Masala:** 172.16.0.0/16 tarmoqdan quyidagi bo'limlar uchun subnetlar ajrating:
- Bo'lim A: 500 host kerak
- Bo'lim B: 200 host kerak
- Bo'lim C: 50 host kerak
- Bo'lim D: 20 host kerak

**Yechim:**

1. **Bo'lim A (500 host):**
   - Zarur: 2^9 - 2 = 510 ≥ 500
   - Mask: /23 (255.255.254.0)
   - Tarmoq: 172.16.0.0/23

2. **Bo'lim B (200 host):**
   - Zarur: 2^8 - 2 = 254 ≥ 200
   - Mask: /24 (255.255.255.0)
   - Tarmoq: 172.16.2.0/24

3. **Bo'lim C (50 host):**
   - Zarur: 2^6 - 2 = 62 ≥ 50
   - Mask: /26 (255.255.255.192)
   - Tarmoq: 172.16.3.0/26

4. **Bo'lim D (20 host):**
   - Zarur: 2^5 - 2 = 30 ≥ 20
   - Mask: /27 (255.255.255.224)
   - Tarmoq: 172.16.3.64/27

### 3.4 Subnetting Jadval

| Prefix | Subnet Mask | Subnetlar Soni | Hostlar Soni |
|--------|-------------|----------------|--------------|
| /24 | 255.255.255.0 | 1 | 254 |
| /25 | 255.255.255.128 | 2 | 126 |
| /26 | 255.255.255.192 | 4 | 62 |
| /27 | 255.255.255.224 | 8 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 32 | 6 |
| /30 | 255.255.255.252 | 64 | 2 |

### 3.5 Amaliyotda Qo'llash Maslahatlar

1. **Rejalashtirish:** Har doim kelajakdagi o'sishni hisobga oling
2. **Hujjatlashtirish:** Barcha subnet ma'lumotlarini yaxshi tashkil qiling
3. **Standartlashtirish:** Tashkilotda bir xil nomlash konvensiyalaridan foydalaning
4. **Monitoring:** Tarmoq resurslarini muntazam kuzatib boring
5. **O'rganib boring:** Dastlab kichik tarmoqlarda amaliyot o'tkazing

---

## 4. Xulosa

Subnetting zamonaviy tarmoq muhandisligining asosiy ko'nikmalaridan biridir. U IP manzillarni samarali boshqarish, tarmoq xavfsizligini oshirish va tarmoq infrastrukturasini mantiqiy tashkil etish imkonini beradi. Subnetting prinsiplarini chuqur tushunish har bir tarmoq mutaxassisi uchun zarurdir.

Talabalar ushbu mavzuni o'zlashtirgach, katta va murakkab tarmoqlarni loyihalash, mavjud tarmoqlarni tahlil qilish va tarmoq muammolarini hal qilishda muhim afzalliklarga ega bo'ladilar.

---

## 5. Nazorat Savollari

1. Subnetting nima va nima uchun kerak?
2. Subnet mask vazifasi nimadan iborat?
3. CIDR notatsiyasi nima va qanday ishlatiladi?
4. VLSM texnologiyasi qanday afzalliklar beradi?
5. /26 maskda nechta host joylashtirilishi mumkin?
6. Private IP manzillar diapazoni qanday?
7. Broadcast va tarmoq manzillari nima?
8. Supernetting qanday vazifani bajaradi?

---

## 6. Topshiriqlar

1. 192.168.50.0/24 tarmoqni 8 ta teng subnetga bo'ling va har birining parametrlarini hisoblang.
2. 10.0.0.0/8 tarmoqdan VLSM yordamida 5 ta bo'lim uchun subnetlar yarating (100, 50, 25, 10, 5 host).
3. Berilgan IP manzil va maskka qarab tarmoq manzili, broadcast manzili va host diapazonini aniqlang.

---

## 7. Foydalanilgan Adabiyotlar

1. Cisco Networking Academy - "Introduction to Networks"
2. Andrew S. Tanenbaum - "Computer Networks"
3. RFC 1878 - "Variable Length Subnet Table For IPv4"
4. RFC 1918 - "Address Allocation for Private Internets"
5. Douglas E. Comer - "Internetworking with TCP/IP"

---

**Darsni tayyorlagan:** Kompyuter tarmoqlari kafedrasi  
**Sana:** 2025-yil