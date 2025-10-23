# Mashrutlash (Routing): Ishlash Mexanizmi va Asosiy Tushunchalar

## Dars ishlanma
**Fan:** Kompyuter tarmoqlari  
**Mavzu:** Mashrutlash nima va uning ishlash mexanizmi  
**Dars turi:** Nazariy

---

## 1. Kirish: Mashrutlash Tushunchasi

**Mashrutlash (Routing)** - bu ma'lumotlar paketlarini manba (source) dan maqsad (destination) gacha eng samarali yo'l orqali yetkazish jarayonidir. Bu jarayon Internet va boshqa kompyuter tarmoqlarining asosiy funksiyalaridan biridir.

### 1.1. Mashrutlashning Ahamiyati

Zamonaviy Internet milliardlab qurilmalarni birlashtirgan ulkan tarmoqdir. Bir kompyuterdan ikkinchisiga ma'lumot yuborilganda, bu ma'lumot ko'pincha o'nlab yoki yuzlab oraliq tarmoq qurilmalaridan o'tishi kerak. Mashrutlash aynan shu yo'lni topish va ma'lumotlarni to'g'ri yo'nalishda yuborish vazifasini bajaradi.

**Misol:** Toshkentdagi kompyuterdan Londondagi serverga so'rov yuborilganda, bu so'rov turli mamlakatlardagi ko'plab marshrutizatorlardan (router) o'tib, eng optimal yo'l bo'yicha manzilga yetib boradi.

---

## 2. Marshrutizator (Router) va Uning Vazifasi

### 2.1. Marshrutizator Nima?

**Marshrutizator (Router)** - bu tarmoqlarni bir-biriga ulash va ma'lumotlar paketlarini to'g'ri yo'nalishda yo'llash uchun mo'ljallangan maxsus tarmoq qurilmasi. Marshrutizator OSI modelining 3-qatlami (Network Layer) da ishlaydi.

### 2.2. Marshrutizatorning Asosiy Vazifalaari

1. **Yo'l tanlash (Path Selection)** - eng optimal marshrutni aniqlash
2. **Paketlarni yo'naltirish (Packet Forwarding)** - paketlarni tanlangan yo'l bo'yicha yuborish
3. **Tarmoqlarni ajratish** - broadcast domenlarini ajratish va tarmoq xavfsizligini oshirish
4. **NAT (Network Address Translation)** - IP manzillarni o'zgartirish
5. **Firewall funksiyalari** - tarmoq xavfsizligini ta'minlash

### 2.3. Marshrutizatorning Tuzilishi

Marshrutizator quyidagi asosiy komponentlardan iborat:

- **CPU (Protsessor)** - marshrutlash qarorlarini qabul qilish
- **RAM** - mashrutlash jadvallarini va konfiguratsiyani saqlash
- **ROM/Flash Memory** - operatsion tizim (IOS) ni saqlash
- **Interfacelar** - turli tarmoqlarga ulanish uchun portlar
- **Console port** - konfiguratsiya qilish uchun

---

## 3. Marshrutlash Jadvali (Routing Table)

### 3.1. Marshrutlash Jadvali Tushunchasi

**Marshrutlash jadvali** - bu marshrutizator xotirasida saqlanadigan ma'lumotlar bazasi bo'lib, unda tarmoq manzillari va ularga qanday yo'l bilan borish kerakligi haqida ma'lumotlar mavjud.

### 3.2. Marshrutlash Jadvalidagi Ma'lumotlar

Har bir marshrutlash jadvali yozuvi (entry) quyidagi ma'lumotlarni o'z ichiga oladi:

1. **Maqsad tarmoq (Destination Network)** - qayerga borish kerak
2. **Keyingi hop (Next Hop)** - paketni qaysi marshrutizatorga yuborish kerak
3. **Chiqish interfeysi (Exit Interface)** - qaysi portdan yuborish kerak
4. **Metrika (Metric)** - yo'lning "narxi" yoki masofasi
5. **Marshrutning turi** - statik yoki dinamik

**Marshrutlash jadvali namunasi:**

```
Maqsad Tarmoq        Next Hop        Interface    Metrika
192.168.1.0/24       -               Eth0         0 (Direct)
10.0.0.0/8           192.168.1.1     Eth1         1
172.16.0.0/16        192.168.1.2     Eth2         2
0.0.0.0/0            192.168.1.254   Eth1         1 (Default)
```

### 3.3. Marshrutlar Turlari

#### 3.3.1. Bevosita ulangan tarmoqlar (Directly Connected)
Bu marshrutizatorning o'zi biriktirilgan tarmoqlardir. Ular avtomatik ravishda marshrutlash jadvaliga qo'shiladi.

#### 3.3.2. Statik marshrutlar (Static Routes)
Administrator tomonidan qo'lda kiritilgan marshrutlardir. Kichik va barqaror tarmoqlarda samarali.

**Afzalliklari:**
- Tarmoq resurslarini tejaydi (protokol trafiki yo'q)
- Xavfsizroq (ma'lumot almashish yo'q)
- To'liq nazorat

**Kamchiliklari:**
- Katta tarmoqlarda qo'llash qiyin
- Moslashuvchan emas
- Tarmoq o'zgarganda qo'lda o'zgartirish kerak

#### 3.3.3. Dinamik marshrutlar (Dynamic Routes)
Marshrutlash protokollari orqali avtomatik o'rganiladigan marshrutlardir.

**Afzalliklari:**
- Avtomatik yangilanadi
- Tarmoq o'zgarishlariga moslashadi
- Katta tarmoqlar uchun ideal

**Kamchiliklari:**
- Ko'proq resurs talab qiladi
- Konfiguratsiya murakkab
- Xavfsizlik xavfi oshadi

---

## 4. Marshrutlash Protokollari

### 4.1. Marshrutlash Protokoli Nima?

**Marshrutlash protokoli** - bu marshrutizatorlar o'rtasida tarmoq topologiyasi haqida ma'lumot almashish va optimal yo'llarni aniqlash uchun ishlatilаdigаn qoidalar to'plamidir.

### 4.2. Marshrutlash Protokollarining Klassifikatsiyasi

#### 4.2.1. IGP va EGP Protokollari

**IGP (Interior Gateway Protocol)** - avtonom tizim (AS) ichida ishlaydi:
- RIP (Routing Information Protocol)
- OSPF (Open Shortest Path First)
- EIGRP (Enhanced Interior Gateway Routing Protocol)
- IS-IS (Intermediate System to Intermediate System)

**EGP (Exterior Gateway Protocol)** - avtonom tizimlar o'rtasida ishlaydi:
- BGP (Border Gateway Protocol) - Internetning asosiy protokoli

#### 4.2.2. Distance Vector va Link State Protokollari

**Distance Vector (Masofa Vektori):**
- Marshrutizatorlar qo'shni marshrutizatorlar bilan marshrutlash jadvalini almashadi
- Har bir marshrutizator faqat qo'shnilari haqida ma'lumotga ega
- Oddiy konfiguratsiya
- Misollar: RIP, IGRP

**Link State (Kanal Holati):**
- Har bir marshrutizator butun tarmoq topologiyasini biladi
- SPF (Shortest Path First) algoritmi qo'llaniladi
- Tez konvergentsiya (convergence)
- Misollar: OSPF, IS-IS

---

## 5. Asosiy Marshrutlash Protokollari

### 5.1. RIP (Routing Information Protocol)

**RIP** - eng qadimgi va eng oddiy distance vector protokolidir.

**Asosiy xususiyatlari:**
- **Metrika:** Hop count (maksimal 15 hop)
- **Yangilanish vaqti:** Har 30 soniyada
- **Versiyalar:** RIPv1 (classful), RIPv2 (classless, VLSM qo'llab-quvvatlaydi)
- **Administrative Distance:** 120

**Afzalliklari:**
- Juda oddiy konfiguratsiya
- Kam resurs talab qiladi
- Kichik tarmoqlar uchun yetarli

**Kamchiliklari:**
- 15 hopdan katta tarmoqlarda ishlamaydi
- Sekin konvergentsiya
- Tarmoq resurslarini ko'p iste'mol qiladi (muntazam yangilanishlar)

**RIP ishlash prinsipi:**
1. Marshrutizator o'z marshrutlash jadvalini qo'shnilarga yuboradi
2. Qo'shnilar bu ma'lumotlarni qabul qilib, o'z jadvallarini yangilaydi
3. Har bir marshrutga 1 hop qo'shiladi
4. Eng kam hop count bo'lgan yo'l tanlanadi

### 5.2. OSPF (Open Shortest Path First)

**OSPF** - keng tarqalgan link state protokoli bo'lib, katta korxona tarmoqlari uchun mo'ljallangan.

**Asosiy xususiyatlari:**
- **Metrika:** Cost (kanal kengligi asosida hisoblanadi)
- **Algoritm:** Dijkstra SPF algoritmi
- **Ierarxik tuzilma:** Area (zonalar) tushunchasi
- **Administrative Distance:** 110

**OSPF ning afzalliklari:**
- Tez konvergentsiya
- VLSM va CIDR qo'llab-quvvatlash
- Miqyoslanuvchi (scalable)
- Tarmoq resurslаrini samarali ishlatadi
- Marshrutlar avtomat sumlash (summarization)

**OSPF ning ishlash bosqichlari:**

1. **Neighbor Discovery** - qo'shni marshrutizatorlarni topish (Hello paketlar orqali)
2. **Database Exchange** - LSDB (Link State Database) almashish
3. **SPF Calculation** - Dijkstra algoritmi yordamida eng qisqa yo'lni hisoblash
4. **Routing Table Update** - marshrutlash jadvalini yangilash

**OSPF Paket turlari:**
- **Hello** - qo'shnilarni aniqlash
- **DBD (Database Description)** - bazalar ro'yxati
- **LSR (Link State Request)** - qo'shimcha ma'lumot so'rash
- **LSU (Link State Update)** - yangi ma'lumotlarni yuborish
- **LSAck** - qabul qilishni tasdiqlash

### 5.3. EIGRP (Enhanced Interior Gateway Routing Protocol)

**EIGRP** - Cisco kompaniyasining rivojlangan hibrid protokoli (distance vector va link state xususiyatlarini birlashtiradi).

**Asosiy xususiyatlari:**
- **Metrika:** Bandwidth, Delay, Load, Reliability (kompozit metrika)
- **Algoritm:** DUAL (Diffusing Update Algorithm)
- **Administrative Distance:** 90 (internal), 170 (external)
- **Protokol:** IP 88

**EIGRP ning afzalliklari:**
- Juda tez konvergentsiya
- Loop-free (DUAL algoritmi orqali)
- VLSM qo'llab-quvvatlash
- Avtomatik marshrutlar sumlash
- Load balancing (teng narxdagi yo'llar bo'yicha)
- Kam tarmoq trafigi

**EIGRP Terminologiyasi:**
- **Feasible Distance (FD)** - maqsadgacha eng yaxshi metrika
- **Advertised Distance (AD)** - qo'shnining maqsadgacha metrikasi
- **Successor** - eng yaxshi yo'l
- **Feasible Successor** - zaxira yo'l

### 5.4. BGP (Border Gateway Protocol)

**BGP** - Internetning asosiy marshrutlash protokoli bo'lib, avtonom tizimlar (AS) o'rtasida ishlaydi.

**Asosiy xususiyatlari:**
- **Protokol:** Path Vector
- **Port:** TCP 179
- **Administrative Distance:** 20 (eBGP), 200 (iBGP)
- **Versiya:** BGP-4 (hozirda ishlatiladi)

**BGP ning xususiyatlari:**
- Juda miqyoslanuvchi (butun Internet uchun)
- Siyosat-asoslangan marshrutlash (policy-based routing)
- AS-Path orqali looplarning oldini olish
- Ko'plab atributlar orqali yo'l tanlash

**BGP Atributlari:**
- **AS-Path** - o'tilgan AS'lar ro'yxati
- **Next-Hop** - keyingi hop manzili
- **Local Preference** - chiquvchi trafikni boshqarish
- **MED (Multi-Exit Discriminator)** - kiruvchi trafikni boshqarish

---

## 6. Marshrutlash Metrikalari

**Metrika** - bu yo'lning "narxi" yoki sifatini baholovchi raqamli qiymat. Har bir protokol o'z metrikasiga ega.

### 6.1. Metrika Turlari

| Protokol | Metrika | Eng yaxshi qiymat |
|----------|---------|-------------------|
| RIP | Hop Count | Eng kam hop |
| OSPF | Cost (100Mbps/Bandwidth) | Eng kam cost |
| EIGRP | Bandwidth + Delay | Eng kam kompozit qiymat |
| BGP | Path Attributes | Siyosatga bog'liq |

### 6.2. Administrative Distance (AD)

Agar bir xil tarmoq uchun turli protokollardan marshrutlar kelsa, **Administrative Distance** orqali qaysi protokolga ishonish kerakligi aniqlanadi.

**AD qiymatlari:**
- Directly Connected: 0
- Static Route: 1
- EIGRP: 90
- OSPF: 110
- RIP: 120
- External EIGRP: 170
- iBGP: 200
- Unknown: 255

**Qoida:** Eng past AD qiymatiga ega marshrutga ishoniladi.

---

## 7. Marshrutlash Jarayoni

### 7.1. Paket Yo'naltirishning Bosqichlari

Marshrutizator paket olganda quyidagi bosqichlarni bajaradi:

1. **Paketni qabul qilish** - kiruvchi interfeys orqali
2. **Paket tekshiruvi** - CRC, TTL tekshirish
3. **Maqsad IP manzilni aniqlash** - paket sarlavhasidan
4. **Marshrutlash jadvalida qidirish:**
   - Aniq moslashma (exact match)
   - Eng uzun prefiks moslashmasi (longest prefix match)
   - Default marshrutni qo'llash
5. **TTL ni kamaytirish** - 1 ga
6. **Paketni yo'naltirish** - tanlangan interfeys orqali
7. **Kadr yaratish** - Data Link qatlami sarlavhasini qo'shish

### 7.2. Longest Prefix Match

Bu zamonaviy marshrutizatorlarda qo'llaniladigan asosiy qidiruv usulidir. Marshrutizator marshrutlash jadvalidagi eng ko'p bit moslashadigan marshrutni tanlaydi.

**Misol:**

Marshrutlash jadvali:
- 192.168.1.0/24
- 192.168.0.0/16
- 0.0.0.0/0 (default)

Maqsad: 192.168.1.100

**Natija:** 192.168.1.0/24 tanlanadi (24 bit mos keladi, bu eng uzun prefiks)

---

## 8. Maxsus Marshrutlar

### 8.1. Default Route (Default Gateway)

**Default marshrutni** marshrutlash jadvalida aniq moslashma topilmagan barcha paketlar uchun ishlatiladi.

**Belgilanishi:** 0.0.0.0/0

**Qo'llanilishi:**
- Tarmoq chеti (edge) marshrutizatorlarida
- Kichik tarmoqlarda
- Internet'ga chiqish uchun

### 8.2. Loopback Interface

**Loopback** - marshrutizator ichida mavjum bo'lgan virtual interfeys.

**Manzil:** 127.0.0.0/8 diapazoni (127.0.0.1 eng mashhuri)

**Afzalliklari:**
- Hech qachon "down" bo'lmaydi
- Marshrutizatorni identifikatsiya qilish uchun
- Management uchun ishlatiladi

### 8.3. Summary Route (Marshrutlarni Umumlashtirish)

Bir nеchta tarmoq manzillarini bitta marshrutda umumlashtirish jarayoni.

**Misol:**
```
192.168.0.0/24
192.168.1.0/24
192.168.2.0/24
192.168.3.0/24
```

Bu marshrutlarni quyidagicha umumlashtirish mumkin:
```
192.168.0.0/22
```

**Foydalari:**
- Marshrutlash jadvalini kichiklashtirish
- Yangilanish trafikini kamaytirish
- Tarmoq bardoshliligini oshirish

---

## 9. Konvergentsiya (Convergence)

### 9.1. Konvergentsiya Tushunchasi

**Konvergentsiya** - tarmoq topologiyasidagi o'zgarishlardan keyin barcha marshrutizatorlar marshrutlash jadvallarini yangilab, yana barqaror holatga kelish jarayonidir.

### 9.2. Konvergentsiya Vaqti

Har bir protokol uchun konvergentsiya vaqti har xil:

- **RIP:** 90-180 soniya (sekin)
- **OSPF:** 2-10 soniya (tez)
- **EIGRP:** 1-5 soniya (juda tez)

### 9.3. Konvergentsiyaga Ta'sir Qiluvchi Omillar

1. Marshrutlash protokolining turi
2. Tarmoq hajmi va murakkabligi
3. Timerlar konfiguratsiyasi
4. Marshrutizatorlarning ishlash qobiliyati

---

## 10. Marshrutlash Muammolari va Ularning Yechimlari

### 10.1. Routing Loop (Marshrutlash Halqasi)

**Routing Loop** - paket bir nеchta marshrutizatorlar orasida cheksiz aylanib yuradigan holat.

**Sabablari:**
- Sekin konvergentsiya
- Noto'g'ri konfiguratsiya
- Marshrutlash jadvallarining notizimi

**Yechimlari:**
1. **Maximum Hop Count** (RIP: 15)
2. **Split Horizon** - ma'lumot kelgan interfeysdаn qaytarib yuborilmaydi
3. **Route Poisoning** - ishlamay qolgan marshrutga cheksiz metrika beriladi
4. **Hold-down Timer** - marshrutni darhol qabul qilmaslik

### 10.2. Suboptimal Routing

Eng yaxshi yo'l o'rniga yomonroq yo'ldan foydalanish holati.

**Sabablari:**
- Noto'g'ri metrika sozlamalari
- Statik marshrutlarning noto'g'ri qo'llanilishi
- Administrative Distance muammolari

### 10.3. Route Flapping

Marshrutning tez-tez o'chirilishi va yoqilishi.

**Sabablari:**
- Kanalning beqarorligi
- Marshrutizator ishlash muammolari

**Yеchin:** Route dampening - marshrutni vaqtincha bloklash

---

## 11. IPv4 va IPv6 Marshrutlash

### 11.1. IPv4 Marshrutlash

**IPv4** - 32-bitli manzil maydonidan foydalanadi.

**Xususiyatlari:**
- Classful (A, B, C, D, E) va Classless (CIDR) marshrutlash
- NAT (Network Address Translation) zarur
- Broadcast qo'llab-quvvatlaydi

### 11.2. IPv6 Marshrutlash

**IPv6** - 128-bitli manzil maydonidan foydalanadi.

**Xususiyatlari:**
- Faqat Classless
- NAT kerak emas
- Broadcast o'rniga Multicast
- Soddalashtirilgan sarlavha
- Ko'proq xavfsizlik (IPSec o'rnatilgan)

**IPv6 marshrutlash protokollari:**
- RIPng (RIP next generation)
- OSPFv3
- EIGRP for IPv6
- MP-BGP (Multiprotocol BGP)

---

## 12. Zamonaviy Mashrutlash Texnologiyalari

### 12.1. MPLS (Multiprotocol Label Switching)

**MPLS** - paketlarga yorliqlar (labels) qo'yib, tez yo'naltirish texnologiyasi.

**Afzalliklari:**
- Juda tez paket yo'naltirish
- Traffic Engineering imkoniyati
- VPN yaratish oson
- QoS qo'llab-quvvatlash

### 12.2. SD-WAN (Software-Defined WAN)

**SD-WAN** - dasturiy ta'minot orqali boshqariladigan keng hududli tarmoq.

**Xususiyatlari:**
- Markazlashtirilgan boshqaruv
- Dinamik yo'l tanlash
- Arzon Internet kanallaridan foydalanish
- Bulutli ilovalar bilan integratsiya

### 12.3. Segment Routing

**Segment Routing** - marshrutga oldindan aniq yo'l belgilab berish texnologiyasi.

**Afzalliklari:**
- SDN bilan yaxshi integratsiya
- MPLS'dan oddiyroq
- Moslashuvchan Traffic Engineering

---

## 13. Marshrutlash Xavfsizligi

### 13.1. Asosiy Tahdidlar

1. **Route Hijacking** - marshrutlarni o'g'irlash
2. **DoS Hujumlari** - marshrutizatorni to'ldirib qo'yish
3. **Man-in-the-Middle** - paketlarni tutib olish
4. **Spoofing** - soxta marshrutlash ma'lumotlari

### 13.2. Himoya Choralari

1. **Autentifikatsiya** - MD5 yoki SHA hash qo'llash
2. **Filtrlash:**
   - Prefix list
   - Route map
   - Access Control List (ACL)
3. **TTL Security** - 1 hop qo'shnilar bilan ishlash
4. **RPKI (Resource Public Key Infrastructure)** - BGP uchun raqamli imzo
5. **Rate Limiting** - marshrutlash paketlarini cheklash

---

## 14. Marshrutlashni Optimallashtirish

### 14.1. Load Balancing

Bir nеchta teng qiymatli yo'llar bo'yicha trafikni taqsimlash.

**Turlarі:**
- **Equal-Cost Load Balancing** - teng narxdagi yo'llar
- **Unequal-Cost Load Balancing** - turli narxdagi yo'llar (faqat EIGRP)

### 14.2. Policy-Based Routing (PBR)

Trafikni manzil o'rniga boshqa mezonlar asosida yo'naltirish.

**Mezonlar:**
- Manba manzil
- Dastur turi (HTTP, FTP, va h.k.)
- Paket o'lchaml
- Kiruvchi interfeys

### 14.3. Quality of Service (QoS)

Muhim trafikka ustunlik berish mexanizmi.

**QoS usullari:**
- **Classification** - trafikni turkumlash
- **Marking** - paketlarga belgi qo'yish (DSCP, CoS)
- **Policing** - tezlikni cheklash
- **Shaping** - trafikni tekislash
- **Queuing** - navbatga qo'yish

---

## 15. Marshrutlashning Kelajagi

### 15.1. Yangi Yo'nalishlar

1. **AI va Machine Learning** - avtomatik marshrutni optimallashtirish
2. **Intent-Based Networking** - maqsadga yo'naltirilgan tarmoq
3. **5G Integration** - mobil va statsionar tarmoqlarning birlashuvi
4. **Quantum Networking** - kvant texnologiyalari

### 15.2. Cloud va Edge Computing

Zamonaviy marshrutlash bulutli xizmatlar va edge computing bilan chambarchas ishlaydi:

- **Multi-cloud Routing** - bir nеchta bulut provayderlar o'rtasida
- **Edge Computing** - markazlashtirilmagan hisoblash
- **IoT Routing** - Narsalar Interneti uchun maxsus protokollar

---

## 16. Xulosa

Marshrutlash - zamonaviy tarmoqlarning asosiy qismidir. Tushunilishi kerak bo'lgan asosiy nuqtalar:

### 16.1. Asosiy Takliflar

1. **Mashrutlash** - ma'lumotlarni manbadan maqsadga yetkazishning eng yaxshi yo'lini topish jarayoni
2. **Marshrutizator** - bu jarayonni amalga oshiruvchi qurilma
3. **Marshrutlash protokollari** - marshrutizatorlar o'rtasida ma'lumot almashish qoidalari
4. **Kichik tarmoqlar** uchun RIP yoki statik marshrutlar yetarli
5. **Katta korxonalar** uchun OSPF yoki EIGRP tavsiya etiladi
6. **Internet oraliq** uchun BGP zarur

### 16.2. To'g'ri Tanlash

Marshrutlash protokolini tanlashda quyidagilarni hisobga oling:

- Tarmoq hajmi va murakkabligi
- Konvergentsiya vaqti talablari
- Administrator tajribasi
- Qurilmalar qo'llab-quvvatlashi
- Xavfsizlik talablari
- Skalabilite (miqyoslanish) zaruriyati

### 16.3. Eng Yaxshi Amaliyotlar

1. Marshrutlash protokollarida autentifikatsiya qo'llang
2. Summarization-dan foydalaning
3. Default marshrut o'rnating
4. Loopback interfeys yarating
5. Monitoring va logging o'rnating
6. Muntazam backup oling
7. Konvergentsiya vaqtini test qiling
8. Dokumentatsiya yuritib boring

---

## 17. Qo'shimcha Resurslar

### 17.1. Standartlar va RFC Hujjatlari

- **RFC 2328** - OSPF Version 2
- **RFC 4271** - BGP-4
- **RFC 2453** - RIP Version 2
- **RFC 7868** - EIGRP

### 17.2. O'qish Uchun Tavsiyalar

- Cisco Networking Academy materiallari
- CCNA va CCNP kurslari
- "TCP/IP Illustrated" - W. Richard Stevens
- "Routing TCP/IP" - Jeff Doyle

### 17.3. Amaliy Mashqlar

1. GNS3 yoki Packet Tracer'da laboratoriya ishlari
2. Turli protokollarni taqqoslash
3. Xatoliklar simulyatsiyasi
4. Monitoring vositalarini o'rganish

---

## Nazorat Savollari

1. Marshrutlash va kommutatsiya (switching) o'rtasidagi farq nimada?
2. Statik va dinamik marshrutlashning afzalliklari va kamchiliklari nimalar?
3. RIP protokolining asosiy chеklоvi nimada?
4. OSPF protokoli SPF algoritmidan qanday foydalanadi?
5. Administrative Distance nima va u nima uchun kerak?
6. Routing loop nima va uni qanday oldini olish mumkin?
7. BGP protokoli nima uchun Internet uchun tanlangan?
8. EIGRP va OSPF o'rtasidagi asosiy farqlar nimalar?
9. Default route nima va qachon ishlatiladi?
10. Konvergentsiya vaqti tarmoq ishlashiga qanday ta'sir qiladi?

---

## Glossariy

**AS (Autonomous System)** - bir tashkilot tomonidan boshqariladigan tarmoqlar to'plami

**BGP (Border Gateway Protocol)** - avtonom tizimlar o'rtasida ishlaydigan marshrutlash protokoli

**Broadcast** - barcha qurilmalarga ma'lumot yuborish

**CIDR (Classless Inter-Domain Routing)** - sinfsiz marshrutlash usuli

**Convergence** - barcha marshrutizatorlarning marshrutlash jadvallarini yangilash jarayoni

**Cost** - OSPF protokolida marshrutning "narxi"

**Default Gateway** - tarmoqdan tashqariga chiqish uchun asosiy yo'l

**Distance Vector** - marshrutlash protokollarining bir turi

**DUAL (Diffusing Update Algorithm)** - EIGRP protokolida ishlatiladigan algoritm

**EIGRP** - Cisco kompaniyasining rivojlangan marshrutlash protokoli

**Hop** - paketning bir marshrutizatordan o'tishi

**IGP (Interior Gateway Protocol)** - avtonom tizim ichida ishlaydigan protokol

**Interface** - marshrutizatorning tarmoqqa ulanish porti

**Link State** - marshrutlash protokollarining bir turi

**Longest Prefix Match** - eng uzun prefiks bo'yicha qidiruv usuli

**Loopback** - marshrutizatordagi virtual interfeys

**LSA (Link State Advertisement)** - OSPF'da kanal holati haqida xabar

**Metric** - marshrutning sifatini baholovchi qiymat

**MPLS** - yorliqlar orqali paket yo'naltirish texnologiyasi

**Multicast** - guruhga ma'lumot yuborish

**NAT (Network Address Translation)** - IP manzillarni o'zgartirish

**Next Hop** - paketni yuborish kerak bo'lgan keyingi marshrutizator

**OSPF** - Link State protokoli

**Packet** - ma'lumotlar to'plami

**Path** - manbadan maqsadgacha bo'lgan yo'l

**Prefix** - tarmoq manzili va subnet mask

**QoS (Quality of Service)** - xizmat sifati

**RIP (Routing Information Protocol)** - eng oddiy marshrutlash protokoli

**Route** - marshrutlash jadvalidagi yozuv

**Router** - marshrutizator, paketlarni yo'naltiradigan qurilma

**Routing Loop** - paketning cheksiz aylanishi

**Routing Protocol** - marshrutlash protokoli

**Routing Table** - marshrutlash jadvali

**SD-WAN** - dasturiy ta'minot bilan boshqariladigan WAN

**SPF (Shortest Path First)** - eng qisqa yo'lni topish algoritmi

**Static Route** - qo'lda kiritilgan marshrutni

**Subnet** - kichik tarmoq

**Summarization** - marshrutlarni umumlashtirish

**TTL (Time To Live)** - paketning "yashash vaqti"

**Unicast** - bitta manzilga ma'lumot yuborish

**VLSM (Variable Length Subnet Mask)** - o'zgaruvchan uzunlikdagi subnet mask

---

## 18. Amaliy Misollar va Stsenariylar

### 18.1. Stsenariy 1: Kichik Ofis Tarmoqi

**Vaziyat:** 50 ta kompyuterli ofis, ikkita marshrutizator, internet ulanishi.

**Tavsiya:**
- Statik marshrutlardan foydalaning
- Default gateway o'rnating
- NAT konfiguratsiya qiling
- Oddiy ACL qo'shing

**Sabab:** Kichik tarmoq uchun dinamik protokollar ortiqcha. Statik marshrutlar to'liq nazorat beradi va resurs talab qilmaydi.

### 18.2. Stsenariy 2: O'rta Hajmdagi Korxona

**Vaziyat:** 5 ta bino, har birida 200+ kompyuter, 20 ta marshrutizator.

**Tavsiya:**
- OSPF protokolini qo'llang
- Har bir binoni alohida Area qiling
- Summarization qo'llang
- Redundant yo'llar yarating

**Sabab:** OSPF tez konvergentsiya beradi, miqyoslanuvchi va katta tarmoqlar uchun mo'ljallangan.

### 18.3. Stsenariy 3: Ko'p Filiallik Kompaniya

**Vaziyat:** Bosh ofis va 50 ta filial, har xil ISP'lar, Internet orqali bog'lanish.

**Tavsiya:**
- SD-WAN yechimidan foydalaning
- MPLS yoki VPN texnologiyalari
- QoS konfiguratsiya qiling
- Markazlashtirilgan monitoring

**Sabab:** SD-WAN arzon, moslashuvchan va bulutli ilovalar bilan yaxshi ishlaydi.

### 18.4. Stsenariy 4: Internet Service Provider (ISP)

**Vaziyat:** Minglab mijozlar, boshqa ISP'lar bilan ulanish, Internet trafik transit.

**Tavsiya:**
- BGP protokolini qo'llang (must!)
- OSPF yoki IS-IS ichki tarmoq uchun
- MPLS Traffic Engineering
- Redundant BGP sessiyalar

**Sabab:** BGP - Internetning asosiy protokoli, politika-asoslangan marshrutlash imkonini beradi.

---

## 19. Marshrutlash Dizayni Prinsiplari

### 19.1. Ierarxik Dizayn

Zamonaviy tarmoqlar uch qatlamli ierarxiya bo'yicha quriladi:

**1. Core Layer (Yadro Qatlami)**
- Maksimal tezlik
- Minimal dasturlash
- Redundancy (zaxira yo'llar)
- Paket filtrlash yo'q

**2. Distribution Layer (Taqsimot Qatlami)**
- Marshrutlash va filtrlash
- QoS qo'llash
- Tarmoqlarni ajratish
- Summarization

**3. Access Layer (Kirish Qatlami)**
- Foydalanuvchilarni ulash
- VLAN yaratish
- Port xavfsizligi
- Power over Ethernet (PoE)

### 19.2. Redundancy va Fault Tolerance

**Redundancy** - tarmoqda bir nеchta zaxira yo'llarning mavjudligi.

**Texnikalar:**
- **Dual Homing** - ikkita ISP'ga ulanish
- **HSRP/VRRP** - virtual gateway
- **Multiple paths** - bir nеchta yo'l
- **Backup links** - zaxira kanallar

**Afzalliklari:**
- Yuqori mavjudlik (High Availability)
- Uzilishlar minimal
- Load balancing imkoniyati

### 19.3. Scalability (Miqyoslanish)

Tarmoq o'sishi bilan muammolar paydo bo'lmasligi uchun:

1. **Ierarxik tuzilma** - qatlamli arxitektura
2. **Summarization** - marshrutlar sonini kamaytirish
3. **VLSM** - IP manzillarni samarali taqsimlash
4. **Modullar tizimi** - kengaytirish oson bo'lishi

### 19.4. Xavfsizlik Prinsiplari

**Defense in Depth** - ko'p qatlamli himoya:

1. **Perimeter Security** - chegarada (Firewall, IPS)
2. **Network Segmentation** - VLAN va ACL orqali
3. **Encryption** - VPN va TLS
4. **Authentication** - marshrutlash protokollarida
5. **Monitoring** - doimiy nazorat

---

## 20. Marshrutlash Monitoring va Diagnostika

### 20.1. Monitoring Vositalari

**1. SNMP (Simple Network Management Protocol)**
- Marshrutizator holatini kuzatish
- Statistika to'plash
- Alertlar olish

**2. NetFlow/sFlow**
- Trafik oqimlarini tahlil qilish
- Tarmoq xarajatlarini aniqlash
- Anomaliyalarni topish

**3. Syslog**
- Log xabarlarni yig'ish
- Xatoliklar tahlili
- Audit uchun

**4. NMS (Network Management System)**
- Markazlashtirilgan boshqaruv
- Vizualizatsiya
- Avtomatik xabar berish

### 20.2. Diagnostika Buyruqlari (Konseptual)

Marshrutizatorlarda ishlatilаdigаn asosiy buyruqlar (Cisco syntax):

**Marshrutlash jadvalini ko'rish:**
```
show ip route
```

**Interfeys holatini tekshirish:**
```
show ip interface brief
```

**OSPF qo'shnilarini ko'rish:**
```
show ip ospf neighbor
```

**BGP holatini tekshirish:**
```
show ip bgp summary
```

**Marshrutlash protokoli ma'lumotlari:**
```
show ip protocols
```

**Statistika:**
```
show ip route summary
```

### 20.3. Muammolarni Hal Qilish Metodologiyasi

**1. Muammoni Aniqlash**
- Foydalanuvchi shikoyatlari
- Monitoring alertlari
- Performance degradation

**2. Ma'lumot To'plash**
- Topology diagramma
- Marshrutlash jadvallari
- Log fayllari
- Trafik statistikasi

**3. Tahlil Qilish**
- Marshrutlar mavjudligini tekshirish
- Metrikalарni taqqoslash
- Loop borligini aniqlash
- Konfiguratsiyani tekshirish

**4. Gipoteza Yaratish**
- Mumkin bo'lgan sabablar
- Test qilish rejalari

**5. Test va Tekshirish**
- Ping, traceroute
- Vaqtinchalik o'zgarishlar
- Monitoring natijalari

**6. Yechim Qo'llash**
- To'g'ri konfiguratsiya
- Hujjatlash
- Testing
- Rollback rejasi

**7. Monitoring**
- Muammo qaytmasligini tekshirish
- Preventive measures

---

## 21. Marshrutlash va Boshqa Texnologiyalar

### 21.1. Marshrutlash va Switching

**Switching (L2):**
- MAC manzillar bilan ishlaydi
- Bir tarmoq ichida
- Tez va oddiy
- Broadcast domeni katta

**Routing (L3):**
- IP manzillar bilan ishlaydi
- Tarmoqlar orasida
- Murakkab qarorlar
- Broadcast domenini ajratadi

**L3 Switch:**
- Ikkalasining imkoniyatlari
- VLAN orasida marshrutlash
- Hardware-accelerated
- Korxona tarmoqlarida

### 21.2. Marshrutlash va VLAN

**VLAN (Virtual LAN)** - mantiqiy tarmoq segmentlari.

**Inter-VLAN Routing:**
- Router-on-a-Stick
- L3 Switch
- External Router

**Foydalari:**
- Xavfsizlik
- Trafik ajratish
- Broadcast dоmеnini kamaytirish

### 21.3. Marshrutlash va VPN

**VPN (Virtual Private Network)** - xavfsiz ulanish Internet orqali.

**VPN Turlari:**
- **Site-to-Site VPN** - ikkita tarmoq o'rtasida
- **Remote Access VPN** - foydalanuvchi va tarmoq o'rtasida
- **MPLS VPN** - provayderning tarmoqida

**Marshrutlash bilan integratsiya:**
- VPN tunnel - virtual interfeys
- VPN orqali marshrutlar
- Dynamic routing over VPN

### 21.4. Marshrutlash va Cloud

**Cloud Routing:**
- Virtual routers
- Software-defined
- On-demand
- Pay-as-you-go

**Hybrid Cloud:**
- On-premises va cloud o'rtasida
- Direct Connect / Express Route
- BGP over dedicated links

---

## 22. Kelajak Tendensiyalari va Innovatsiyalar

### 22.1. Software-Defined Networking (SDN)

**SDN** - boshqaruv va ma'lumot yo'nalishini ajratish.

**Arxitektura:**
- **Application Layer** - biznes logika
- **Control Layer** - SDN Controller
- **Infrastructure Layer** - switch va router

**Afzalliklari:**
- Markazlashtirilgan boshqaruv
- Programmable
- Avtomatizatsiya
- Agile

**Protokollar:**
- OpenFlow
- NETCONF
- RESTCONF

### 22.2. Intent-Based Networking (IBN)

**IBN** - tarmoqqa maqsad aytish, u o'zi amalga oshiradi.

**Prinsiplar:**
- Translation - maqsadni texnik tilga o'girish
- Activation - avtomatik konfiguratsiya
- Assurance - doimiy tekshirish va optimizatsiya

**Misol:**
"Guest Wi-Fi foydalanuvchilari faqat Internet'ga kirishi kerak" - IBN tizimi buni avtomatik amalga oshiradi.

### 22.3. AI va Machine Learning

**Qo'llanish sohalari:**
- **Predictive Analytics** - muammolarni oldindan aniqlash
- **Auto-remediation** - avtomatik tuzatish
- **Traffic Optimization** - trafik marshrutini optimallashtirish
- **Anomaly Detection** - g'ayritabiiy xatti-harakatni aniqlash

**Misol:** Google'ning B4 tarmoqi - AI orqali tarmoq kanallarining 95% unumdorligiga erishgan.

### 22.4. Segment Routing va SRv6

**SRv6 (Segment Routing over IPv6):**
- IPv6 sarlavhalariga yo'l kodlash
- MPLS'dan sodda
- Programmable
- Service chaining

**Afzalliklari:**
- MPLS signaling protokollar kerak emas
- Traffic engineering
- Low latency
- Simplicity

### 22.5. Quantum Networking

**Quantum networking** - kvant mexanikasi prinsiplarida asoslangan.

**Xususiyatlari:**
- Quantum entanglement
- Absolute security
- Instant communication (nazariy)

**Hozirgi holat:** Tadqiqot bosqichida, ammo katta kelajak.

---

## 23. Real World Case Studies

### 23.1. Case Study: Google'ning Global Network

**Muammo:** Global miqyosda million serverlarni samarali bog'lash.

**Yechim:**
- B4 - dasturiy ta'minot bilan boshqariladigan WAN
- Openflow SDN controller
- Centralized Traffic Engineering
- AI-based optimization

**Natija:**
- 95% kanal unumdorligi
- Minimal latency
- Avtomatik yo'l tanlash

### 23.2. Case Study: Netflix Content Delivery

**Muammo:** Global miqyosda video kontentni tez yetkazish.

**Yechim:**
- Open Connect CDN
- BGP Anycast
- Strategik joylashuv (ISP'larda)
- Intelligent routing

**Natija:**
- Internet trafikining ~15%
- Yuqori sifat
- Past latency

### 23.3. Case Study: Amazon AWS Global Infrastructure

**Muammo:** 30+ regionda cloud xizmatlarini bog'lash.

**Yechim:**
- Private global network
- Multiple redundant paths
- DX (Direct Connect) xizmati
- Advanced BGP configuration

**Natija:**
- 99.99% availability
- Low latency
- Secure connectivity

---

## 24. Best Practices va Tavsiyalar

### 24.1. Dizayn Best Practices

1. **Soddalik** - murakkablikdan qoching
2. **Standartlar** - umumiy standartlarga amal qiling
3. **Dokumentatsiya** - hamma narsani hujjatlang
4. **Redundancy** - zaxira yo'llar
5. **Scalability** - kelajakni o'ylang
6. **Security-first** - xavfsizlikni birinchi o'ringa qo'ying

### 24.2. Konfiguratsiya Best Practices

1. **Authentication** - barcha protokollarda
2. **Passive interfaces** - kerak bo'lmaganda o'chiring
3. **Summarization** - imkon qadar qo'llang
4. **Loopback** - identifikatsiya uchun
5. **Timers tuning** - ehtiyotkorlik bilan
6. **Filtering** - kerakli marshrutlarni qabul qiling

### 24.3. Operational Best Practices

1. **Change Management** - o'zgarishlarni rejalang
2. **Testing** - ishlab chiqarishdan oldin test qiling
3. **Monitoring** - doimiy kuzating
4. **Backup** - muntazam backup oling
5. **Documentation** - yangilab turing
6. **Training** - jamoani o'rgating

### 24.4. Security Best Practices

1. **Least Privilege** - minimal ruxsat
2. **Defense in Depth** - ko'p qatlamli himoya
3. **Authentication** - kuchli parollar
4. **Encryption** - management trafikni shifrlang
5. **Logging** - barcha hodisalarni yozib turing
6. **Regular Updates** - firmware va software yangilang

---

## 25. Xulosa va Yakuniy Fikrlar

### 25.1. Asosiy Xulosalar

Marshrutlash - bu:
- **Asosiy texnologiya** - Internet'siz marshrutlash yo'q
- **Kompleks fan** - ko'p bilim talab qiladi
- **Doimo rivojlanuvchi** - yangi texnologiyalar
- **Kritik ahamiyatga ega** - biznes uzluksizligi uchun

### 25.2. Muvaffaqiyat Kalitlari

1. **Nazariy bilim** - protokollar va algoritmlarni tushunish
2. **Amaliy tajriba** - laboratoriya ishlari
3. **Troubleshooting skills** - muammolarni hal qilish
4. **Uzluksiz o'rganish** - yangiliklar bilan tanishish
5. **Sertifikatsiya** - CCNA, CCNP, CCIE

### 25.3. O'rganish Yo'li

**Boshlang'ich darajа:**
1. IP addressing va subnetting
2. Statik marshrutlash
3. RIP protokoli
4. Oddiy topologiyalar

**O'rta daraja:**
5. OSPF single area
6. EIGRP asoslari
7. ACL va filtrlash
8. VLANs va inter-VLAN routing

**Ilg'or daraja:**
9. OSPF multi-area
10. BGP asoslari
11. Redistribution
12. Advanced troubleshooting

**Ekspert daraja:**
13. BGP advanced
14. MPLS
15. QoS
16. Network design

### 25.4. Foydali Maslahatlar

1. **Amaliyot** - laboratoriya ishlari eng muhim
2. **Xatolardan o'rganing** - har bir xato - tajriba
3. **Qo'l bilan yozing** - diagram va jadvallar
4. **Izohlab bering** - boshqalarga o'rgatish orqali o'rganing
5. **Real dunyo** - haqiqiy muammolarni hal qiling

### 25.5. Karyera Imkoniyatlari

Marshrutlash bo'yicha mutaxassislar:
- **Network Engineer** - tarmoq muhandisi
- **Network Architect** - tarmoq arxitektori
- **Network Administrator** - tarmoq administratori
- **Network Security Specialist** - xavfsizlik mutaxassisi
- **Cloud Network Engineer** - bulut tarmoq muhandisi
- **ISP Engineer** - provayderda ishchi

**Ish haqi:** Yuqori darajada va talab katta (ayniqsa ekspertlar uchun)

---

## Yakuniy So'z

Marshrutlash - bu zamonaviy raqamli dunyoning asosi. Har bir veb-sahifa, har bir video qo'ng'iroq, har bir bulutli xizmat - bularning barchasi marshrutlash tufayli ishlaydi. Bu texnologiyani o'rganish - kuchli va zarur investitsiyadir.

**Esda tuting:**
- Bosqichma-bosqich o'rganing
- Amaliyotga ko'p vaqt ajrating
- Hech qachon o'rganishni to'xtatmang
- Hamjamiyat bilan bo'lining

**Omad tilayman!** 🚀

---

## Qo'shimcha Manbalar

### Онлайн Курслар:
- Cisco Networking Academy
- Coursera - Computer Networks
- Udemy - CCNA va CCNP kurslari

### Kitoblar:
- "Computer Networks" - Andrew Tanenbaum
- "TCP/IP Illustrated" - W. Richard Stevens
- "Routing TCP/IP, Volume I & II" - Jeff Doyle

### Laboratoriya Vositalari:
- GNS3 (https://www.gns3.com)
- EVE-NG (https://www.eve-ng.net)
- Packet Tracer (Cisco)

### Foydali Saytlar:
- https://www.cisco.com
- https://www.ietf.org (RFC dokumentlar)
- https://packetlife.net
- https://networklessons.com

---

**Muallif Izohi:** Ushbu dars ishlanma "Kompyuter tarmoqlari" fanini o'rganuvchi talabalar, tarmoq mutaxassislari va o'z bilimlarini oshirishni istagan barcha qiziquvchilar uchun tayyorlandi.

**Versiya:** 1.0  
**Sana:** 2025-yil

---

*"Tarmoq - bu faqat kabellar va qurilmalar emas, bu aloqa va imkoniyatlardir"*