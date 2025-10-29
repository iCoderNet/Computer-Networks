# Standart (Default) Shlyuz Tushunchasi

## Dars ishlanma
**Fan:** Kompyuter tarmoqlari  
**Mavzu:** Standart (default) shlyuz tushunchasi  
**Dars turi:** Nazariy-amaliy  

---

## 1. Kirish

Zamonaviy kompyuter tarmoqlarida qurilmalar o'rtasida ma'lumot almashish jarayoni murakkab infratuzilma asosida amalga oshiriladi. Har bir tarmoq qurilmasi o'z tarmog'i ichida bemalol aloqa qilishi mumkin, ammo boshqa tarmoqlarga ulanish uchun maxsus mexanizm talab etiladi. Aynan shu vazifani standart shlyuz bajaradi.

Standart shlyuz (default gateway) - bu mahalliy tarmoqdan tashqaridagi manziллarga yo'naltirilgan barcha ma'lumot paketlarini qabul qiluvchi va ularni kerakli yo'nalishga yo'naltiruvchi tarmoq qurilmasidir. Oddiy qilib aytganda, shlyuz tarmoqning "eshigi" vazifasini bajaradi.

---

## 2. Standart Shlyuzning Asosiy Tushunchalari

### 2.1. Shlyuz nima?

**Shlyuz (Gateway)** - bu ikki yoki undan ortiq tarmoqlarni bir-biri bilan bog'laydigan tarmoq tugunidir. U turli protokollar, ma'lumot formatlari va tarmoq arxitekturalarini bir-biriga moslashtirish vazifasini bajaradi.

Shlyuzlar quyidagi funktsiyalarni bajaradi:
- Turli tarmoqlar o'rtasida ma'lumot uzatish
- Protokollarni konvertatsiya qilish
- Xavfsizlik funksiyalarini ta'minlash
- Trafik filtrlash va boshqarish

### 2.2. Standart Shlyuz va Oddiy Shlyuz Farqi

**Standart shlyuz** - bu tarmoq sozlamalarida ko'rsatilgan standart marshrutizator manzilidir. Agar kompyuter yubormoqchi bo'lgan paketning manzili mahalliy tarmoqda bo'lmasa, paket avtomatik ravishda standart shlyuzga yuboriladi.

**Oddiy shlyuz** esa maxsus marshrutlar uchun mo'ljallangan bo'lishi mumkin va faqat ma'lum yo'nalishlar uchun ishlatiladi.

### 2.3. OSI Modelida Shlyuzning O'rni

Shlyuzlar OSI (Open Systems Interconnection) modelining turli qatlamlarida ishlashi mumkin:

- **Tarmoq qatlami (Layer 3):** IP manzillar bilan ishlaydigan marshrutizatorlar
- **Transport qatlami (Layer 4):** Port asosida filtrlash
- **Ilova qatlami (Layer 7):** Proksi-serverlar va ilova shlyuzlari

Standart shlyuz asosan Tarmoq qatlamida (Layer 3) ishlaydi va IP manzillar bilan bog'liq vazifalarni bajaradi.

---

## 3. Standart Shlyuzning Ishlash Prinsipi

### 3.1. Marshrutizatsiya Jarayoni

Kompyuter ma'lumot paketini yuborishdan oldin quyidagi mantiqiy tekshiruvni amalga oshiradi:

1. **Manzilni tahlil qilish:** Yuborilayotgan paket IP manzili mahalliy tarmoqqa tegishlimi?
2. **Subnet mask qo'llash:** Subnet mask yordamida manziлning tarmoq qismi aniqlanadi
3. **Qaror qabul qilish:**
   - Agar manzil mahalliy tarmoqda bo'lsa → paket to'g'ridan-to'g'ri jo'natiladi
   - Agar manzil mahalliy tarmoqda bo'lmasa → paket standart shlyuzga yuboriladi

### 3.2. ARP Protokoli va Shlyuz

Standart shlyuzga paket yuborish uchun kompyuter shlyuzning MAC manzilini bilishi kerak. Bu jarayon ARP (Address Resolution Protocol) orqali amalga oshiriladi:

1. Kompyuter ARP so'rovini yuboradi: "IP manzili X.X.X.X bo'lgan qurilmaning MAC manzili nima?"
2. Shlyuz javob beradi: "Mening MAC manzilim YY:YY:YY:YY:YY:YY"
3. Kompyuter bu ma'lumotni ARP keshida saqlaydi
4. Keyingi paketlar to'g'ridan-to'g'ri shu MAC manziliga yuboriladi

### 3.3. Paket Yo'naltirish Algoritmi

```
1. Paket yaratildi (manba: 192.168.1.100, maqsad: 8.8.8.8)
2. Maqsad manzili mahalliy tarmoqda? (192.168.1.0/24)
   → YO'Q
3. Marshrutlash jadvalida maxsus marshrut bormi?
   → YO'Q
4. Paket standart shlyuzga (192.168.1.1) yo'naltiriladi
5. Shlyuz paketni qabul qiladi va keyingi sakrashga (next hop) yuboradi
6. Jarayon maqsadga yetguncha davom etadi
```

---

## 4. Standart Shlyuz Konfiguratsiyasi

### 4.1. Statik va Dinamik Konfiguratsiya

**Statik konfiguratsiya:**
- Administrator tomonidan qo'lda sozlanadi
- Barqaror tarmoqlarda qo'llaniladi
- O'zgartirish uchun qo'lda aralashuv kerak

**Dinamik konfiguratsiya (DHCP):**
- Avtomatik ravishda tayinlanadi
- DHCP server tomonidan boshqariladi
- Moslashuvchan va boshqarish oson

### 4.2. DHCP va Standart Shlyuz

DHCP (Dynamic Host Configuration Protocol) serveri mijozga quyidagi ma'lumotlarni beradi:

- **IP manzil:** Mijoz uchun noyob manzil
- **Subnet mask:** Tarmoq chegarasini belgilaydi
- **Standart shlyuz:** Tashqi tarmoqlarga yo'l
- **DNS serverlar:** Domen nomlarini IP manzilga aylantirish uchun
- **Lease time:** Manzil amal qilish muddati

### 4.3. Subnet Mask va Shlyuz

Subnet mask standart shlyuzning zarurligini aniqlashda muhim rol o'ynaydi.

**Misol:**
- IP manzil: 192.168.1.100
- Subnet mask: 255.255.255.0 (/24)
- Tarmoq: 192.168.1.0/24
- Standart shlyuz: 192.168.1.1

Bu sozlamada 192.168.1.1 dan 192.168.1.254 gacha bo'lgan manzillar mahalliy tarmoqda, qolgan barcha manzillar esa shlyuz orqali erishiladi.

---

## 5. Standart Shlyuzning Turlari va Arxitekturasi

### 5.1. Marshrutizator (Router)

Eng keng tarqalgan shlyuz turi. Marshrutizator:
- Tarmoqlar o'rtasida paketlarni yo'naltiradi
- Marshrutlash jadvaliga ega
- NAT (Network Address Translation) ni qo'llab-quvvatlaydi
- Firewall funksiyalarini bajarishi mumkin

### 5.2. Layer 3 Switch

Katta korporativ tarmoqlarda qo'llaniladigan qurilma:
- Switch va marshrutizator funksiyalarini birlashtiradi
- Yuqori tezlikda ishlaydi
- VLAN o'rtasida marshrutizatsiya qiladi
- Mahalliy tarmoq uchun optimallashtirilgan

### 5.3. Firewall va Shlyuz

Zamonavir tarmoqlarda firewall ko'pincha shlyuz vazifasini ham bajaradi:
- Xavfsizlik siyosatlarini qo'llaydi
- Trafik nazorati va filtrlash
- IDS/IPS (Intrusion Detection/Prevention System)
- VPN ulanishlarini boshqarish

### 5.4. Ko'p Shlyuzli Arxitektura

Katta tashkilotlarda bir nechta shlyuz bo'lishi mumkin:

**Active-Passive konfiguratsiya:**
- Bitta faol shlyuz ishlatiladi
- Ikkinchisi zaxira sifatida kutadi
- VRRP (Virtual Router Redundancy Protocol) orqali boshqariladi

**Active-Active konfiguratsiya:**
- Bir nechta shlyuz parallel ishlaydi
- Trafik ulararo taqsimlanadi
- Yuqori o'tkazuvchanlik va ishonchlilik

---

## 6. Standart Shlyuz va Xavfsizlik

### 6.1. Shlyuz - Xavfsizlik Chegarasi

Standart shlyuz tarmoq xavfsizligining muhim elementi:

- **Perimeter xavfsizligi:** Ichki va tashqi tarmoqlar o'rtasida chegara
- **Trafik nazorati:** Kiruvchi va chiquvchi trafik monitoring
- **Tahdid aniqlash:** Zararli faoliyatni topsih va bloklash
- **Jurnal yuritish:** Barcha faoliyatni qayd etish

### 6.2. NAT va Shlyuz

Network Address Translation (NAT) standart shlyuzning muhim funksiyasi:

**NAT turlari:**
- **SNAT (Source NAT):** Ichki IP manzillarni yashirish
- **DNAT (Destination NAT):** Port forwarding uchun
- **PAT (Port Address Translation):** Ko'p qurilmalarni bitta IP orqali ulash

**NAT afzalliklari:**
- IPv4 manzillar tanqisligini kamaytiradi
- Ichki tarmoq tuzilmasini yashiradi
- Qo'shimcha xavfsizlik qatlami yaratadi

### 6.3. Demilitarizatsiya Zonasi (DMZ)

DMZ shlyuz arxitekturasining muhim qismi:

```
Internet → Tashqi Firewall → DMZ (Web serverlar) → Ichki Firewall → Ichki Tarmoq
```

DMZ xususiyatlari:
- Ommaviy serverlar joylashadi
- Ichki tarmoqdan ajratilgan
- Ikki tomonlama himoyalangan

---

## 7. Muammolar va Ularning Yechimlari

### 7.1. Standart Shlyuz Ishlamayotganda

**Alomatlar:**
- Mahalliy tarmoq ishlaydi, ammo Internet yo'q
- "Destination Host Unreachable" xatoligi
- DNS ishlamaydi

**Sabablari:**
- Shlyuz noto'g'ri sozlangan
- Shlyuz qurilmasi o'chiq yoki ishlamayotgan
- Tarmoq kabeli uzilgan
- Firewall kirish huquqini bloklagan

### 7.2. Noto'g'ri Shlyuz Manzili

**Muammo:** Kompyuter mavjud bo'lmagan shlyuz manziliga yo'naltirilgan

**Yechim:**
- Shlyuz mavjudligini ping orqali tekshirish
- DHCP sozlamalarini tekshirish
- Marshrutlash jadvalini tahlil qilish

### 7.3. MTU Muammolari

Maximum Transmission Unit (MTU) muammolari:
- Katta paketlar uzatilmaydi
- Ba'zi saytlar ochilmaydi, ba'zilari ochiladi
- Path MTU Discovery ishlamayotgan

**Yechim:** MTU o'lchamini moslash yoki PMTUD ni yoqish

---

## 8. Amaliy Qo'llash (Qisqacha)

### 8.1. Windows'da Standart Shlyuzni Ko'rish

**Command Prompt orqali:**
```cmd
ipconfig /all
```

**Natijada ko'rinadigan ma'lumotlar:**
- IP Address
- Subnet Mask
- Default Gateway
- DNS Servers

### 8.2. Linux'da Standart Shlyuzni Ko'rish

**Terminal buyruqlari:**
```bash
# Usul 1: ip route
ip route show

# Usul 2: route
route -n

# Usul 3: netstat
netstat -rn
```

### 8.3. Shlyuzni Tekshirish

**Ping testi:**
```cmd
ping 192.168.1.1
```

**Traceroute/Tracert:**
```cmd
# Windows
tracert google.com

# Linux
traceroute google.com
```

Bu buyruq paketning shlyuz orqali qanday yo'l bosganini ko'rsatadi.

---

## 9. Ilg'or Mavzular

### 9.1. Policy-Based Routing (PBR)

Standart shlyuzdan tashqari, maxsus marshrutlash siyosatlari:
- Manba IP asosida marshrutlash
- Ilova turi bo'yicha yo'naltirish
- QoS (Quality of Service) ni ta'minlash

### 9.2. Software-Defined Networking (SDN)

Zamonaviy yondashuv:
- Markazlashtirilgan boshqaruv
- Dinamik shlyuz konfiguratsiyasi
- Dasturiy yo'sinda marshrutlash

### 9.3. IPv6 va Standart Shlyuz

IPv6 da standart shlyuz:
- Router Advertisement orqali e'lon qilinadi
- Link-local manzillar ishlatilishi mumkin
- Stateless va Stateful konfiguratsiya

---

## 10. Xulosa

Standart shlyuz zamonaviy tarmoq infratuzilmasining muhim komponentidir. U mahalliy tarmoq va tashqi dunyo o'rtasidagi ko'prik vazifasini bajarib, quyidagi asosiy funktsiyalarni ta'minlaydi:

### Asosiy Xulasalar:

1. **Tarmoq ulanishi:** Mahalliy tarmoqdan tashqaridagi resurslarga kirish imkonini beradi
2. **Marshrutizatsiya:** Paketlarni to'g'ri yo'nalishga yo'naltiradi
3. **Xavfsizlik:** Tarmoq chegarasida xavfsizlik nazoratini amalga oshiradi
4. **Tarjima:** NAT orqali IP manzillarni boshqaradi
5. **Boshqaruv:** Tarmoq trafigini nazorat qiladi va optimallashtiradi

### Amaliy Ahamiyati:

- Har bir tarmoq qurilmasi to'g'ri shlyuz sozlamalariga ega bo'lishi kerak
- Shlyuz ishlamay qolishi butun tarmoqning Internetga kirishini to'xtatadi
- To'g'ri arxitektura va konfiguratsiya tarmoq ishlashini va xavfsizligini ta'minlaydi
- Zamonavir tarmoqlarda zaxira shlyuzlar va yuqori mavjudlik muhim ahamiyatga ega

### Kelajak Yo'nalishlari:

- Cloud-based shlyuz xizmatlari
- AI asosida marshrutlash optimizatsiyasi
- IoT qurilmalari uchun maxsus shlyuz arxitekturalari
- 5G va edge computing integratsiyasi

---

## Nazorat Savollari

1. Standart shlyuz nima va uning asosiy vazifasi nimadan iborat?
2. Kompyuter paketni mahalliy tarmoqda yoki shlyuz orqali yuborishni qanday hal qiladi?
3. NAT texnologiyasi nima va u standart shlyuzda qanday rol o'ynaydi?
4. DHCP server standart shlyuz haqida qanday ma'lumot beradi?
5. Active-Passive va Active-Active shlyuz arxitekturasi o'rtasida qanday farq bor?
6. Standart shlyuz ishlamay qolganda qanday alomatlar paydo bo'ladi?
7. DMZ nima va u tarmoq xavfsizligida qanday rol o'ynaydi?
8. IPv6 da standart shlyuz qanday e'lon qilinadi?

---

## Adabiyotlar va Qo'shimcha O'rganish Uchun Manbalar

1. **RFC Hujjatlari:**
   - RFC 1122 - Host Requirements
   - RFC 1812 - Requirements for IP Version 4 Routers
   - RFC 4861 - Neighbor Discovery for IPv6

2. **Tavsiya etiladigan kitoblar:**
   - "Computer Networks" - Andrew S. Tanenbaum
   - "TCP/IP Illustrated" - W. Richard Stevens
   - "Network Warrior" - Gary A. Donahue

3. **Online resurslar:**
   - Cisco Networking Academy
   - CompTIA Network+ materiallar
   - NetworkLessons.com

---

**Darsni tayyorlovchi:** [O'qituvchi ismi]  
**Sana:** 2025-yil  
**Versiya:** 1.0