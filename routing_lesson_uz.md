# Mashrutlash nima va uning ishlash mexanizmi

## Dars haqida ma'lumot
**Fan:** Kompyuter tarmoqlari  
**Mavzu:** Mashrutlash nima va uning ishlash mexanizmi  
**Dars turi:** Nazariy va amaliy  
**Davomiyligi:** 2 akademik soat

---

## 1. Kirish

### 1.1. Mashrutlashning ta'rifi

**Mashrutlash (Routing)** - bu ma'lumot paketlarini manba qurilmadan maqsad qurilmagacha eng optimal yo'l orqali yetkazish jarayonidir. Mashrutlash kompyuter tarmoqlarining asosiy funksiyalaridan biri bo'lib, Internetning ishlashi uchun zaruriy mexanizmdir.

Oddiy qilib aytganda, mashrutlash - bu ma'lumotlarning tarmoqda qanday harakat qilishi kerakligini aniqlash jarayonidir, xuddi GPS navigatsiya tizimi yo'lni topganidek.

### 1.2. Mashrutlashning ahamiyati

Zamonaviy tarmoqlarda mashrutlash muhim rol o'ynaydi:

- **Global aloqa**: Internetda milyardlab qurilmalar bir-biri bilan bog'lanishi uchun samarali marshrutlash zarur
- **Tarmoq samaradorligi**: To'g'ri marshrutlash tarmoq resurslaridan optimal foydalanishni ta'minlaydi
- **Ishonchlilik**: Bir yo'l ishlamay qolsa, alternativ yo'llar orqali ma'lumotlar yetkaziladi
- **Kengayuvchanlik**: Tarmoq o'sishi bilan mashrutlash tizimi ham moslashib boradi

---

## 2. Marshrutlashning asosiy tushunchalari

### 2.1. IP manzil va subnet mask

**IP manzil** - bu tarmoqdagi har bir qurilmaning noyob raqamli identifikatori. IPv4 formatida IP manzil 4 ta oktetdan iborat:

```
192.168.1.10
```

**Subnet mask** - tarmoq va host qismlarini ajratish uchun ishlatiladi:

```
255.255.255.0 yoki /24
```

### 2.2. Router (marshrutizator)

**Router** - bu turli tarmoqlarni bir-biriga bog'lab, ma'lumot paketlarini yo'naltirish uchun mo'ljallangan maxsus qurilma. Router quyidagi asosiy vazifalarni bajaradi:

- Paketlarni qabul qilish va tahlil qilish
- Maqsad manzilni aniqlash
- Eng yaxshi yo'lni tanlash
- Paketlarni keyingi routerga yoki maqsadga jo'natish

### 2.3. Marshrutlash jadvali (Routing Table)

Marshrutlash jadvali - bu routerda saqlanadigan va turli tarmoqlarga yo'llarni ko'rsatuvchi ma'lumotlar to'plami. Har bir yozuv quyidagilarni o'z ichiga oladi:

- **Maqsad tarmoq manzili** (Destination Network)
- **Subnet mask** (Network Mask)
- **Gateway** (keyingi sakrash manzili - Next Hop)
- **Interface** (chiqish interfeysi)
- **Metrika** (yo'lning qiymati yoki masofasi)

**Marshrutlash jadvali namunasi:**

| Maqsad tarmoq | Subnet Mask | Gateway | Interface | Metrika |
|---------------|-------------|---------|-----------|---------|
| 192.168.1.0 | 255.255.255.0 | Bevosita | eth0 | 0 |
| 10.0.0.0 | 255.255.255.0 | 192.168.1.1 | eth0 | 1 |
| 0.0.0.0 | 0.0.0.0 | 192.168.1.254 | eth0 | 10 |

### 2.4. Default Gateway (Standart shlyuz)

Default gateway - bu mahalliy tarmoqdan tashqaridagi manzillarga yuborilgan barcha paketlar uchun ishlatiluvchi router. Marshrutlash jadvalida odatda `0.0.0.0/0` yoki `default route` sifatida ko'rsatiladi.

---

## 3. Marshrutlash turlari

### 3.1. Statik marshrutlash (Static Routing)

**Ta'rif:** Tarmoq administratori tomonidan qo'lda sozlangan va o'zgarmas marshrutlar.

**Afzalliklari:**
- To'liq nazorat ostida
- Tarmoq resurslarini tejaydi (dinamik protokollar kerak emas)
- Xavfsizroq (yangilanishlar bo'lmaydi)
- Kichik tarmoqlar uchun qulay

**Kamchiliklari:**
- Katta tarmoqlarda boshqarish qiyin
- Avtomatik moslashish yo'q
- Ishdan chiqishda qo'lda tuzatish kerak
- Xatolarga moyil

**Qo'llanish holatlari:**
- Kichik tarmoqlar
- Stub tarmoqlar (faqat bitta chiqish yo'li bo'lgan)
- Maxsus xavfsizlik talablari bo'lgan joylar
- Laboratoriya muhitlari

**Konfiguratsiya namunasi (Cisco):**
```
Router(config)# ip route 10.0.0.0 255.255.255.0 192.168.1.1
```

### 3.2. Dinamik marshrutlash (Dynamic Routing)

**Ta'rif:** Marshrutlash protokollari yordamida avtomatik ravishda yangilanadigan marshrutlar.

**Afzalliklari:**
- Avtomatik yangilanish
- Tarmoq o'zgarishlariga tez moslashish
- Katta tarmoqlar uchun samarali
- Ishdan chiqishlarni avtomatik aniqlash

**Kamchiliklari:**
- Qo'shimcha tarmoq resurslari talab qiladi
- Murakkab konfiguratsiya
- Xavfsizlik xavflari (hujumlar mumkin)
- Konvergentsiya vaqti kerak

**Qo'llanish holatlari:**
- Katta korporativ tarmoqlar
- Internet provayderlar
- Tez o'zgaruvchan topologiyali tarmoqlar
- Yuqori darajadagi ishonchlilik talab qilinadigan joylar

---

## 4. Mashrutlash protokollari

### 4.1. Interior Gateway Protocols (IGP)

IGP protokollari bitta avtonom tizim (AS) ichida ishlaydi.

#### 4.1.1. RIP (Routing Information Protocol)

**Xususiyatlari:**
- Distance-vector protokoli
- Hop count (sakrashlar soni)ni metrika sifatida ishlatadi
- Maksimal 15 hop (16 = infinity)
- Har 30 soniyada yangilanish
- Oddiy konfiguratsiya

**RIP versiyalari:**
- **RIPv1**: Classful, broadcast ishlatadi, autentifikatsiya yo'q
- **RIPv2**: Classless (CIDR), multicast, autentifikatsiya bor
- **RIPng**: IPv6 uchun

**Afzalliklari:**
- O'rganish va konfiguratsiya qilish oson
- Kichik tarmoqlar uchun yetarli
- Barcha routerlarda qo'llab-quvvatlanadi

**Kamchiliklari:**
- Sekin konvergentsiya (3-4 daqiqa)
- Tarmoq diametri cheklangan (15 hop)
- Katta tarmoqlarda samarasiz
- Bandwidth, kechikish kabi parametrlarni hisobga olmaydi

**Konfiguratsiya namunasi:**
```
Router(config)# router rip
Router(config-router)# version 2
Router(config-router)# network 192.168.1.0
Router(config-router)# no auto-summary
```

#### 4.1.2. OSPF (Open Shortest Path First)

**Xususiyatlari:**
- Link-state protokoli
- Dijkstra algoritmini ishlatadi
- Ixtiyoriy metrika (cost), odatda bandwidth asosida
- Tez konvergentsiya
- Classless (VLSM va CIDR qo'llab-quvvatlanadi)

**OSPF konsepsiyalari:**
- **Area**: Tarmoqni mantiqiy bo'laklarga ajratish
- **Area 0 (Backbone)**: Barcha arealar orqali o'tadigan markaziy area
- **Router turlari**: Internal, Backbone, ABR, ASBR
- **Paket turlari**: Hello, DBD, LSR, LSU, LSAck

**OSPF ishlash jarayoni:**
1. **Neighbor Discovery**: Hello paketlari orqali qo'shnilarni topish
2. **Database Exchange**: Link-state ma'lumotlarini almashish
3. **SPF Calculation**: Dijkstra algoritmi bilan eng qisqa yo'lni hisoblash
4. **Routing Table Update**: Marshrutlash jadvalini yangilash

**Afzalliklari:**
- Tez konvergentsiya (soniyalar ichida)
- Katta tarmoqlarni qo'llab-quvvatlaydi
- VLSM va CIDR qo'llab-quvvatlanadi
- Load balancing (bir xil cost bo'lgan yo'llar)
- Ierarxik dizayn (arealar)

**Kamchiliklari:**
- Murakkab konfiguratsiya va boshqarish
- Ko'proq CPU va xotira talab qiladi
- Kichik tarmoqlar uchun ortiqcha

**Konfiguratsiya namunasi:**
```
Router(config)# router ospf 1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# router-id 1.1.1.1
```

#### 4.1.3. EIGRP (Enhanced Interior Gateway Routing Protocol)

**Xususiyatlari:**
- Cisco-ning proprietar protokoli (2013-yildan open standard)
- Gibrid protokol (distance-vector va link-state xususiyatlari)
- Tez konvergentsiya (DUAL algoritmi)
- Classless, VLSM va CIDR qo'llab-quvvatlanadi

**EIGRP metrikalari:**
- Bandwidth (tarmoqlovchi kengligi)
- Delay (kechikish)
- Reliability (ishonchlilik)
- Load (yuklama)
- MTU (maksimal uzatish birligi)

**Afzalliklari:**
- Juda tez konvergentsiya
- Loop-free (DUAL algoritmi tufayli)
- Bandwidth samarali ishlatish
- Moslashuvchan (manual summarization)
- Unequal cost load balancing

**Kamchiliklari:**
- Cisco routerlar bilan cheklangan (tarixiy)
- OSPF kabi keng tarqalmagan
- Murakkab metrika hisoblashlari

**Konfiguratsiya namunasi:**
```
Router(config)# router eigrp 100
Router(config-router)# network 192.168.1.0 0.0.0.255
Router(config-router)# no auto-summary
```

### 4.2. Exterior Gateway Protocols (EGP)

#### 4.2.1. BGP (Border Gateway Protocol)

**Xususiyatlari:**
- Path-vector protokoli
- Internet uchun asosiy protokol
- Avtonom tizimlar o'rtasida ishlaydi
- AS Path va Policy-based routing

**BGP konsepsiyalari:**
- **AS (Autonomous System)**: Mustaqil boshqariladigan tarmoqlar guruhi
- **eBGP**: Turli AS'lar o'rtasida
- **iBGP**: Bitta AS ichida
- **BGP Attributes**: AS_PATH, NEXT_HOP, LOCAL_PREF, MED va boshqalar

**Afzalliklari:**
- Miqyoslanuvchi (global Internet)
- Policy-based routing (siyosatlar asosida)
- Multipath va load balancing
- Ishonchli va barqaror

**Kamchiliklari:**
- Juda murakkab
- Sekin konvergentsiya (daqiqalar)
- Katta resurslarga talab
- Korporativ tarmoqlar ichida ishlatilmaydi

**Konfiguratsiya namunasi:**
```
Router(config)# router bgp 65001
Router(config-router)# neighbor 10.1.1.2 remote-as 65002
Router(config-router)# network 192.168.1.0 mask 255.255.255.0
```

---

## 5. Marshrutlashning ishlash mexanizmi

### 5.1. Paket yuborish jarayoni

Marshrutlash jarayonini qadamma-qadam ko'rib chiqamiz:

**1-qadam: Paket yaratish**
- Manba kompyuter ma'lumot paketini yaratadi
- IP sarlavhasiga manba va maqsad IP manzillarini qo'yadi
- Maqsad manzil mahalliy tarmoqdami yoki yo'qmi tekshiradi

**2-qadam: Mahalliy tarmoq tekshiruvi**
- Agar maqsad mahalliy tarmoqda bo'lsa: bevosita yuboradi (ARP orqali)
- Agar mahalliy tarmoqda bo'lmasa: default gateway'ga yuboradi

**3-qadam: Router tomonidan qabul qilish**
- Router paketni qabul qiladi
- IP sarlavhasini tahlil qiladi
- Maqsad IP manzilni aniqlaydi

**4-qadam: Marshrutlash jadvali qidirish**
- Router marshrutlash jadvalida mos manzilni qidiradi
- Eng aniq moslikni (longest prefix match) tanlaydi
- Agar topilmasa, default route ishlatiladi
- Agar umuman yo'l bo'lmasa, paket tashlanadi

**5-qadam: TTL va paket tekshiruvi**
- TTL (Time To Live) qiymatini 1 ga kamaytiradi
- Agar TTL = 0 bo'lsa, paket tashlanadi va ICMP Time Exceeded xabari yuboriladi
- Checksum qayta hisoblanadi

**6-qadam: Keyingi hop'ga yuborish**
- Paket keyingi routerga yoki maqsad qurilmaga yuboriladi
- Data-link layer sarlavhasi yangilanadi (MAC manzillar)
- Paket tegishli interfeys orqali jo'natiladi

**7-qadam: Jarayon takrorlanishi**
- Keyingi router ham xuddi shu jarayonni takrorlaydi
- Paket maqsadga yetguncha davom etadi

### 5.2. Marshrutni tanlash algoritmlari

#### 5.2.1. Longest Prefix Match

Router bir nechta mos marshrutlardan eng aniq (eng uzun prefix)ni tanlaydi.

**Misol:**
```
Maqsad IP: 192.168.10.50

Marshrutlar:
1. 192.168.0.0/16    - 16 bit mos
2. 192.168.10.0/24   - 24 bit mos (tanlanadi!)
3. 0.0.0.0/0         - 0 bit (default)
```

#### 5.2.2. Administrative Distance (AD)

Turli marshrutlash manbalari uchun ishonchlilik darajasi:

| Manba | AD qiymati |
|-------|------------|
| Bevosita ulangan | 0 |
| Statik marshrut | 1 |
| EIGRP summary | 5 |
| eBGP | 20 |
| EIGRP internal | 90 |
| OSPF | 110 |
| RIP | 120 |
| EIGRP external | 170 |
| iBGP | 200 |

Kichikroq AD qiymatiga ega bo'lgan yo'l tanlanadi.

#### 5.2.3. Metrika

Bir xil protokoldagi yo'llarni solishtirish uchun:
- **RIP**: Hop count (kam bo'lsa yaxshi)
- **OSPF**: Cost (kam bo'lsa yaxshi)
- **EIGRP**: Kompozit metrika (bandwidth, delay)
- **BGP**: Path attributes (murakkab qoidalar)

### 5.3. Marshrutlash tsikllari va ularning oldini olish

**Marshrutlash tsikli (Routing Loop)** - paket bir nechta routerlar o'rtasida cheksiz aylanib yurishi.

**Oldini olish mexanizmlari:**

1. **TTL (Time To Live)**
   - Har bir sakrashda 1 ga kamayadi
   - 0 ga yetganda paket tashlanadi

2. **Split Horizon**
   - Ma'lumot qabul qilingan interfeys orqali qaytarib yuborilmaydi

3. **Route Poisoning**
   - Ishlamay qolgan yo'l "infinity" metrika bilan e'lon qilinadi

4. **Hold-down Timer**
   - Yo'l o'zgarganda ma'lum vaqt kutiladi

5. **Triggered Updates**
   - Tarmoq o'zgarganda darhol yangilanish yuboriladi

---

## 6. NAT (Network Address Translation)

### 6.1. NAT nima va nega kerak?

**NAT** - bu mahalliy (private) IP manzillarni global (public) IP manzillarga o'zgartirish mexanizmi.

**Sabablari:**
- IPv4 manzillar tanqisligi
- Xavfsizlik (ichki tarmoqni yashirish)
- Tarmoq boshqaruvini osonlashtirish

### 6.2. NAT turlari

#### 6.2.1. Static NAT
Bitta private IP bitta public IP ga doimiy moslanadi.

```
Inside Local    →    Inside Global
192.168.1.10    →    203.0.113.10
```

#### 6.2.2. Dynamic NAT
Private IP'lar public IP'lar poolidan dinamik tanlanadi.

```
192.168.1.10    →    203.0.113.20 (vaqtincha)
192.168.1.11    →    203.0.113.21 (vaqtincha)
```

#### 6.2.3. PAT (Port Address Translation) / NAT Overload
Ko'plab private IP'lar bitta public IP va turli portlar orqali chiqadi.

```
192.168.1.10:1500  →  203.0.113.1:50001
192.168.1.11:2000  →  203.0.113.1:50002
192.168.1.12:3000  →  203.0.113.1:50003
```

**PAT jadval namunasi:**

| Inside Local | Inside Global | Protocol |
|--------------|---------------|----------|
| 192.168.1.10:1500 | 203.0.113.1:50001 | TCP |
| 192.168.1.11:2000 | 203.0.113.1:50002 | TCP |
| 192.168.1.10:53 | 203.0.113.1:50003 | UDP |

### 6.3. NAT konfiguratsiyasi (Cisco)

```
! Inside interfeysi
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# ip nat inside

! Outside interfeysi
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip address 203.0.113.1 255.255.255.252
Router(config-if)# ip nat outside

! PAT konfiguratsiyasi
Router(config)# access-list 1 permit 192.168.1.0 0.0.0.255
Router(config)# ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

---

## 7. Marshrutlashda xavfsizlik

### 7.1. Asosiy xavflar

1. **Marshrutlash ma'lumotlarini o'zgartirish**
   - Noto'g'ri marshrutlar kiritish
   - Man-in-the-middle hujumlari

2. **DDoS hujumlari**
   - Router resurslarini to'liq ishlatish
   - Marshrutlash protokollarini buzish

3. **Ma'lumotlarni tinglash**
   - Paketlarni tutish (packet sniffing)
   - Trafik tahlili

### 7.2. Himoya choralari

#### 7.2.1. Autentifikatsiya

**MD5 autentifikatsiyasi (OSPF):**
```
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip ospf message-digest-key 1 md5 MySecretKey
Router(config)# router ospf 1
Router(config-router)# area 0 authentication message-digest
```

**EIGRP autentifikatsiyasi:**
```
Router(config)# key chain MyKeyChain
Router(config-keychain)# key 1
Router(config-keychain-key)# key-string MyPassword

Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip authentication mode eigrp 100 md5
Router(config-if)# ip authentication key-chain eigrp 100 MyKeyChain
```

#### 7.2.2. Access Control Lists (ACL)

```
! Tashqi tarmoqdan kirayotgan trafik uchun
Router(config)# access-list 100 deny ip 192.168.0.0 0.0.255.255 any
Router(config)# access-list 100 deny ip 10.0.0.0 0.255.255.255 any
Router(config)# access-list 100 permit ip any any

Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip access-group 100 in
```

#### 7.2.3. Route Filtering

```
! Prefix-list orqali filterlash
Router(config)# ip prefix-list FILTER-ROUTES deny 172.16.0.0/16
Router(config)# ip prefix-list FILTER-ROUTES permit 0.0.0.0/0 le 32

Router(config)# router ospf 1
Router(config-router)# distribute-list prefix FILTER-ROUTES in
```

#### 7.2.4. Xavfsizlik tamoyillari

1. **Minimal imtiyozlar**: Faqat kerakli marshrutlarni ulashing
2. **Defense in Depth**: Ko'p qatlamli himoya
3. **Regular Updates**: Routerlarni muntazam yangilang
4. **Monitoring**: Trafik va marshrutlarni kuzating
5. **Backup**: Konfiguratsiyalarni saqlang

---

## 8. Troubleshooting (Muammolarni hal qilish)

### 8.1. Asosiy diagnostika vositalari

#### 8.1.1. Ping

Tarmoq ulanishini tekshirish:

```
ping 192.168.1.1
ping google.com
```

**Natijalar:**
- Reply: Muvaffaqiyatli
- Request timeout: Maqsad javob bermayapti
- Destination host unreachable: Marshrut topilmadi

#### 8.1.2. Traceroute / Tracert

Paketning yo'lini kuzatish:

```
# Windows
tracert 8.8.8.8

# Linux/Mac
traceroute 8.8.8.8
```

**Natijalar:** Har bir hop va kechikish vaqti ko'rsatiladi.

#### 8.1.3. Router buyruqlari

**Marshrutlash jadvalini ko'rish:**
```
Router# show ip route
```

**OSPF ma'lumotlari:**
```
Router# show ip ospf neighbor
Router# show ip ospf database
Router# show ip ospf interface
```

**EIGRP ma'lumotlari:**
```
Router# show ip eigrp neighbors
Router# show ip eigrp topology
```

**BGP ma'lumotlari:**
```
Router# show ip bgp summary
Router# show ip bgp neighbors
```

**Interfeys holati:**
```
Router# show ip interface brief
Router# show interface GigabitEthernet0/0
```

### 8.2. Keng tarqalgan muammolar va yechimlar

#### Muammo 1: Marshrutlash jadvali bo'sh

**Belgilari:**
- `show ip route` buyrug'i hech narsa ko'rsatmaydi
- Tarmoq aloqasi yo'q

**Yechimlar:**
- Interfeys holatini tekshiring: `show ip interface brief`
- Interfeys faolligini ta'minlang: `no shutdown`
- IP manzillarni tekshiring
- Marshrutlash protokolini to'g'ri konfiguratsiya qiling

#### Muammo 2: Neighbor munosabatlari o'rnatilmayapti

**OSPF uchun:**
- Hello/Dead intervallari bir xil bo'lishi kerak
- Area ID bir xil bo'lishi kerak
- Autentifikatsiya sozlamalari mos bo'lishi kerak
- MTU o'lchamlari mos bo'lishi kerak

**Tekshirish:**
```
Router# show ip ospf interface
Router# debug ip ospf adj
```

#### Muammo 3: Marshrutlar ko'rinmayapti

**Sabablari:**
- Network statement noto'g'ri
- Passive interface sozlangan
- ACL yoki distribute-list taqiqlagan
- Administrative distance muammosi

**Tekshirish:**
```
Router# show ip protocols
Router# show run | section router
```

#### Muammo 4: Asymmetrik marshrutlash

**Belgilari:**
- Bir tomonga trafik o'tadi, qaytmaydi
- NAT muammolari
- Firewall blocklashi

**Yechimlar:**
- Traceroute ikki tomonlama ishlatish
- NAT konfiguratsiyasini tekshirish
- Stateful firewall sozlamalarini ko'rish

### 8.3. Debug buyruqlari

**Ehtiyot bo'ling!** Debug buyruqlari router'ni sekinlashtirishi mumkin.

```
! OSPF debugging
Router# debug ip ospf adj
Router# debug ip ospf events

! EIGRP debugging
Router# debug eigrp packets
Router# debug ip eigrp

! O'chirish
Router# no debug all
yoki
Router# undebug all
```

---

## 9. Amaliy misollar

### 9.1. Kichik ofis tarmoqini marshrutlash

**Ssenariy:**
- 1 ta Internet ulanishi
- 2 ta VLAN (Boshqaruv va Ishchilar)
- 1 ta router

**Topologiya:**
```
Internet
    |
  Router (R1)
    |
    |----VLAN 10 (192.168.10.0/24) - Boshqaruv
    |----VLAN 20 (192.168.20.0/24) - Ishchilar
```

**Konfiguratsiya:**

```
! Outside interfeysi
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address dhcp
Router(config-if)# ip nat outside
Router(config-if)# no shutdown

! VLAN 10 sub-interface
Router(config)# interface GigabitEthernet0/1.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# ip nat inside

! VLAN 20 sub-interface
Router(config)# interface GigabitEthernet0/1.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# ip nat inside

! NAT konfiguratsiyasi
Router(config)# access-list 1 permit 192.168.10.0 0.0.0.255
Router(config)# access-list 1 permit 192.168.20.0 0.0.0.255
Router(config)# ip nat inside source list 1 interface GigabitEthernet0/0 overload

! Default route
Router(config)# ip route 0.0.0.0 0.0.0.0 GigabitEthernet0/0
```

### 9.2. Ikkita ofisni bog'lash (OSPF)

**Ssenariy:**
- 2 ta ofis (Toshkent va Samarqand)
- WAN ulanish (leased line)
- OSPF orqali marshrutlash

**Topologiya:**
```
Toshkent Office (192.168.1.0/24)
        |
      R1 (10.0.0.1/30)
        |
    WAN Link (10.0.0.0/30)
        |
      R2 (10.0.0.2/30)
        |
Samarqand Office (192.168.2.0/24)
```

**R1 (Toshkent) konfiguratsiyasi:**

```
! LAN interfeysi
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.1 255.255.255.0
Router(config-if)# no shutdown

! WAN interfeysi
Router(config)# interface Serial0/0/0
Router(config-if)# ip address 10.0.0.1 255.255.255.252
Router(config-if)# clock rate 128000
Router(config-if)# no shutdown

! OSPF konfiguratsiyasi
Router(config)# router ospf 1
Router(config-router)# router-id 1.1.1.1
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# passive-interface GigabitEthernet0/0
```

**R2 (Samarqand) konfiguratsiyasi:**

```
! LAN interfeysi
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.2.1 255.255.255.0
Router(config-if)# no shutdown

! WAN interfeysi
Router(config)# interface Serial0/0/0
Router(config-if)# ip address 10.0.0.2 255.255.255.252
Router(config-if)# no shutdown

! OSPF konfiguratsiyasi
Router(config)# router ospf 1
Router(config-router)# router-id 2.2.2.2
Router(config-router)# network 192.168.2.0 0.0.0.255 area 0
Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
Router(config-router)# passive-interface GigabitEthernet0/0
```

**Tekshirish:**
```
R1# show ip ospf neighbor
R1# show ip route ospf
R1# ping 192.168.2.1
```

### 9.3. Redundant marshrutlash (HSRP bilan)

**Ssenariy:**
- Yuqori mavjudlik (high availability)
- 2 ta router
- Avtomatik failover

**Topologiya:**
```
        Internet
         /    \
        /      \
      R1        R2
    (Primary) (Standby)
        \      /
         \    /
       LAN Switch
           |
      192.168.1.0/24
```

**R1 konfiguratsiyasi:**

```
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.2 255.255.255.0
Router(config-if)# standby 1 ip 192.168.1.1
Router(config-if)# standby 1 priority 110
Router(config-if)# standby 1 preempt
Router(config-if)# no shutdown
```

**R2 konfiguratsiyasi:**

```
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip address 192.168.1.3 255.255.255.0
Router(config-if)# standby 1 ip 192.168.1.1
Router(config-if)# standby 1 priority 100
Router(config-if)# no shutdown
```

**Natija:**
- Virtual IP: 192.168.1.1 (klientlar uchun default gateway)
- R1 active bo'ladi (priority 110)
- R1 ishdan chiqsa, R2 avtomatik active bo'ladi

---

## 10. Zamonaviy marshrutlash texnologiyalari

### 10.1. SDN (Software-Defined Networking)

**Ta'rif:** Tarmoq boshqaruvini markazlashtirilgan dasturiy ta'minot orqali amalga oshirish.

**Asosiy komponentlar:**
- **Control Plane**: Qarorlar qabul qiladi (Controller)
- **Data Plane**: Ma'lumotlarni uzatadi (Switch/Router)
- **Management Plane**: Monitoring va konfiguratsiya

**Afzalliklari:**
- Markazlashgan boshqaruv
- Avtomatizatsiya va dasturlash imkoniyati
- Tez o'zgarishlar
- Resurslarni samarali ishlatish

**Qo'llaniladigan joylar:**
- Data markazlar
- Cloud provayderlar
- Katta korporatsiyalar

### 10.2. SD-WAN (Software-Defined Wide Area Network)

**Ta'rif:** WAN tarmoqlarini dasturiy ta'minot orqali boshqarish va optimallashtirish.

**Xususiyatlari:**
- Ko'plab WAN ulanishlarni boshqarish (MPLS, Internet, LTE)
- Avtomatik yo'l tanlash
- Trafikni prioritetlashtirish
- Xavfsizlikni ta'minlash

**Afzalliklari:**
- Xarajatlarni kamaytirish
- Performance yaxshilanishi
- Oson boshqaruv
- Moslashuvchanlik

### 10.3. IPv6 marshrutlash

**IPv6 xususiyatlari:**
- 128-bit manzil (IPv4: 32-bit)
- Ierarxik manzil tuzilmasi
- NAT ga ehtiyoj yo'q
- Improved routing efficiency

**IPv6 marshrutlash protokollari:**
- OSPFv3
- EIGRP for IPv6
- RIPng (RIP next generation)
- MP-BGP (Multiprotocol BGP)

**IPv6 konfiguratsiyasi (OSPFv3):**

```
! IPv6 ni yoqish
Router(config)# ipv6 unicast-routing

! Interfeys konfiguratsiyasi
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ipv6 address 2001:db8:1:1::1/64
Router(config-if)# ipv6 ospf 1 area 0

! OSPFv3 konfiguratsiyasi
Router(config)# ipv6 router ospf 1
Router(config-rtr)# router-id 1.1.1.1
```

### 10.4. MPLS (Multiprotocol Label Switching)

**Ta'rif:** Label-based marshrutlash texnologiyasi.

**Ishlash printsipi:**
1. Paketga label qo'yiladi (Ingress router)
2. Label asosida tez marshrutlash (Core routers)
3. Label olib tashlanadi (Egress router)

**Afzalliklari:**
- Tez marshrutlash
- Traffic Engineering
- VPN qo'llab-quvvatlash
- QoS (Quality of Service)

**Qo'llaniladigan joylar:**
- ISP tarmoqlari
- Enterprise WAN
- Data center interconnect

### 10.5. Segment Routing

**Ta'rif:** Source-based marshrutlash - manba paketning to'liq yo'lini belgilaydi.

**Xususiyatlari:**
- SDN bilan yaxshi integratsiya
- State ma'lumotlarni kamroq saqlash
- Trafik boshqaruvini osonlashtirish

**Afzalliklari:**
- Oddiyroq protokol
- Moslashuvchan yo'l tanlash
- Kamroq overhead

---

## 11. Load Balancing va Redundancy

### 11.1. Equal-Cost Multi-Path (ECMP)

**Ta'rif:** Bir xil cost'ga ega bo'lgan bir nechta yo'llardan foydalanish.

**Misol (OSPF):**
```
! Ikkita yo'l bir xil cost
Router# show ip route
O    10.0.0.0/24 [110/2] via 192.168.1.2, GigabitEthernet0/0
                  [110/2] via 192.168.1.3, GigabitEthernet0/1
```

**Afzalliklari:**
- Bandwidth oshadi
- Redundancy ta'minlanadi
- Avtomatik failover

### 11.2. Unequal-Cost Load Balancing (EIGRP)

**Ta'rif:** Turli cost'li yo'llardan ham proportional foydalanish.

**Konfiguratsiya:**
```
Router(config)# router eigrp 100
Router(config-router)# variance 2
```

**Natija:**
- Eng yaxshi yo'ldan ko'proq trafik
- Ikkinchi darajali yo'ldan kamroq trafik
- Barcha yo'llar faol ishlatiladi

### 11.3. Gateway Redundancy Protocols

#### HSRP (Hot Standby Router Protocol)
- Cisco proprietar
- Active/Standby rejim
- Virtual IP va MAC

#### VRRP (Virtual Router Redundancy Protocol)
- Open standard (RFC 5798)
- Master/Backup rejim
- Real MAC ishlatish mumkin

#### GLBP (Gateway Load Balancing Protocol)
- Cisco proprietar
- Bir vaqtning o'zida load balancing va redundancy
- Bir nechta router active bo'ladi

---

## 12. Monitoring va Performance

### 12.1. Marshrutlash metrikalarini kuzatish

**Muhim ko'rsatkichlar:**
- **Latency**: Kechikish vaqti
- **Jitter**: Kechikish o'zgaruvchanligi
- **Packet Loss**: Yo'qolgan paketlar foizi
- **Throughput**: O'tkazish qobiliyati
- **Route Flapping**: Marshrutlarning tez-tez o'zgarishi

### 12.2. Monitoring vositalari

**SNMP (Simple Network Management Protocol):**
```
Router(config)# snmp-server community public RO
Router(config)# snmp-server host 192.168.1.100 version 2c public
```

**NetFlow / sFlow:**
```
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip flow ingress
Router(config-if)# ip flow egress

Router(config)# ip flow-export version 9
Router(config)# ip flow-export destination 192.168.1.100 9996
```

**Syslog:**
```
Router(config)# logging host 192.168.1.100
Router(config)# logging trap informational
```

### 12.3. Proaktiv monitoring

**Route Change Monitoring:**
- Marshrutlar o'zgarishini kuzatish
- Alert sistemasi o'rnatish
- Avtomatik ta'mirlash skriptlari

**Health Checks:**
- Interfeys holati
- CPU va Memory ishlatilishi
- Routing protocol holati
- Neighbor munosabatlari

---

## 13. Best Practices (Eng yaxshi amaliyotlar)

### 13.1. Dizayn tamoyillari

1. **Ierarxik dizayn**
   - Core, Distribution, Access qatlamlari
   - To'g'ri segmentatsiya
   - Kengayuvchanlik nazarda tutish

2. **Redundancy**
   - Bir nuqtali nosozlik yo'q (no single point of failure)
   - Backup yo'llar
   - Redundant router va linklar

3. **Skalabilnost**
   - Summarization ishlatish
   - Routing protocol to'g'ri tanlash
   - Arealar va hierarchy

4. **Xavfsizlik**
   - Autentifikatsiya
   - Filtering va ACL
   - Segmentatsiya

### 13.2. Konfiguratsiya tamoyillari

1. **Dokumentatsiya**
   - Barcha o'zgarishlarni yozib borish
   - Tarmoq diagrammalarini yangilab turish
   - Konfiguratsiya backup

2. **Naming Convention**
   - Tushunarli nomlar berish
   - Standartlashtirilgan format
   - Konsistent bo'lish

3. **Change Management**
   - Test muhitda sinab ko'rish
   - Maintenance window
   - Rollback rejasi

4. **Monitoring va Logging**
   - Barcha muhim eventlarni yozish
   - Proaktiv monitoring
   - Alert sistemasi

### 13.3. Operational Best Practices

1. **Regular Maintenance**
   - IOS/Firmware yangilanishlari
   - Konfiguratsiya backup (haftalik)
   - Hardware tekshirish

2. **Capacity Planning**
   - Trafik trendlarini tahlil qilish
   - O'sishni bashorat qilish
   - Vaqtida upgrade qilish

3. **Disaster Recovery**
   - Backup router va linklar
   - Configuration backup
   - Tiklash plani

---

## 14. Amaliy mashqlar

### Mashq 1: Statik marshrutlash

**Vazifa:** Uchta tarmoqni statik marshrutlar orqali bog'lang.

```
Tarmoq A: 192.168.1.0/24 - R1 - eth0
         R1 (192.168.1.1)
           |
           | eth1: 10.0.0.1/30
           |
Tarmoq B: 10.0.0.0/30
           |
           | 10.0.0.2/30
         R2 (10.0.0.2)
           |
           | eth1: 192.168.2.1/24
           |
Tarmoq C: 192.168.2.0/24 - R2 - eth1
```

**R1 konfiguratsiyasi:**
```
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

**R2 konfiguratsiyasi:**
```
ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

### Mashq 2: OSPF multi-area

**Vazifa:** OSPF'da Area 0, Area 1 va Area 2 yarating.

```
Area 1 --- ABR1 --- Area 0 --- ABR2 --- Area 2
```

**ABR1 konfiguratsiyasi:**
```
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.0 0.0.0.255 area 1
 network 10.0.0.0 0.0.0.3 area 0
```

### Mashq 3: NAT konfiguratsiyasi

**Vazifa:** PAT yordamida ichki tarmoqni Internetga chiqaring.

```
! Konfiguratsiya
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

### Mashq 4: Troubleshooting

**Muammo:** Ikkita ofis o'rtasida aloqa yo'q.

**Qadamlar:**
1. Ping loopback interfeyslari
2. Ping to'g'ridan-to'g'ri ulangan interfeys
3. Traceroute qiling
4. Marshrutlash jadvalini tekshiring
5. Routing protocol holatini ko'ring
6. Interfeys holatini tekshiring

---

## 15. Nazorat savollari

### Nazariy savollar

1. Marshrutlash nima va u nega muhim?
2. Statik va dinamik marshrutlash o'rtasidagi asosiy farqlar nimada?
3. Distance-vector va link-state protokollari qanday farqlanadi?
4. Marshrutlash jadvalida qanday ma'lumotlar saqlanadi?
5. TTL nima va u qanday ishlaydi?
6. NAT nima va u nega ishlatiladi?
7. Administrative Distance (AD) nima?
8. Longest Prefix Match qanday ishlaydi?
9. Routing loop nima va uning oldini qanday olish mumkin?
10. OSPF arealarining maqsadi nima?

### Amaliy savollar

1. RIP konfiguratsiyasini yozing va tushuntiring.
2. OSPF neighbor munosabatlari o'rnatilishi uchun qanday shartlar kerak?
3. PAT jadvalida qanday ma'lumotlar bo'ladi?
4. `show ip route` buyrug'i chiqishini tushuntirib bering.
5. Routing loop muammosini qanday hal qilasiz?
6. OSPF va EIGRP o'rtasida qaysi birini qachon tanlaysiz?
7. Default gateway nima va u qanday sozlanadi?
8. Multi-area OSPF qanday afzalliklar beradi?
9. HSRP qanday ishlaydi va u qachon kerak?
10. BGP qanday holatda ishlatiladi?

---

## 16. Qo'shimcha manbalar

### Kitoblar

1. **"Routing TCP/IP, Volume 1"** - Jeff Doyle
   - Interior Gateway Protocols haqida keng ma'lumot
   - RIP, IGRP, EIGRP, OSPF

2. **"Routing TCP/IP, Volume 2"** - Jeff Doyle
   - Exterior Gateway Protocols
   - BGP, Multicast, IPv6

3. **"CCNA Routing and Switching Complete Study Guide"** - Todd Lammle
   - Boshlang'ich daraja uchun
   - Cisco sertifikatsiyasi uchun

4. **"Internet Routing Architectures"** - Sam Halabi
   - BGP va Internet marshrutlash
   - ISP level

### Online resurslar

1. **Cisco Learning Network**
   - https://learningnetwork.cisco.com
   - Bepul laboratoriya mashqlari
   - Forum va hamjamiyat

2. **Packet Tracer**
   - Cisco simulyatori
   - Amaliy mashqlar uchun

3. **GNS3**
   - https://www.gns3.com
   - Real router IOS'larini simulyatsiya qilish

4. **RFC Documents**
   - https://www.rfc-editor.org
   - Protocol standartlari

### Video kurslar

1. **CBT Nuggets** - Jeremy Cioara
2. **INE (IP Networks)** 
3. **Udemy** - David Bombal
4. **YouTube** - NetworkChuck, Keith Barker

---

## 17. Xulosa

Marshrutlash zamonaviy tarmoqlarning asosi bo'lib, u ma'lumotlarni global miqyosda bir nuqtadan ikkinchi nuqtaga yetkazish imkonini beradi. Bu darsda biz quyidagilarni o'rgandik:

### Asosiy xulosalar:

1. **Marshrutlashning mohiyati**
   - Ma'lumot paketlarini manzilgacha yetkazish jarayoni
   - Router va marshrutlash jadvalining roli

2. **Marshrutlash turlari**
   - Statik: qo'lda sozlash, kichik tarmoqlar uchun
   - Dinamik: avtomatik, katta tarmoqlar uchun

3. **Protokollar**
   - RIP: oddiy, distance-vector
   - OSPF: link-state, tez konvergentsiya
   - EIGRP: gibrid, Cisco
   - BGP: Internet uchun

4. **Xavfsizlik va ishonchlilik**
   - Autentifikatsiya
   - Redundancy (HSRP, VRRP)
   - Monitoring va troubleshooting

5. **Zamonaviy tendensiyalar**
   - SDN va SD-WAN
   - IPv6
   - Segment Routing

### Keyingi qadamlar:

1. **Amaliy tajriba to'plash**
   - Packet Tracer yoki GNS3 da mashq qilish
   - Real jihozlarda tajriba orttirish

2. **Chuqur o'rganish**
   - CCNA sertifikatsiyasiga tayyorlanish
   - Ilg'or mavzularni o'rganish (BGP, MPLS)

3. **Doimiy yangilanib turish**
   - Yangi texnologiyalar (SDN, SD-WAN)
   - Best practices va industry trends

Marshrutlash - bu tarmoq muxandisligining asosiy ko'nikma bo'lib, uni yaxshi bilish karyerangizni rivojlantirishda katta yordam beradi.

---

## Glossariy (Atamalar lug'ati)

| Atama | Ta'rif |
|-------|--------|
| **Router** | Turli tarmoqlarni bog'lovchi va paketlarni yo'naltiruvchi qurilma |
| **Routing Table** | Marshrutlar haqida ma'lumot saqlovchi jadval |
| **Hop** | Paketning bir routerdan ikkinchisiga o'tishi |
| **Metric** | Marshrutni baholash uchun ishlatiladigan son |
| **Convergence** | Barcha routerlar marshrutlash haqida kelishuvga erishish jarayoni |
| **Subnet Mask** | Tarmoq va host qismlarini ajratuvchi niqob |
| **Default Gateway** | Mahalliy tarmoqdan tashqariga chiqish uchun ishlatiladigan router |
| **NAT** | IP manzillarni o'zgartirish mexanizmi |
| **TTL** | Paketning maksimal umr muddati (hop sonida) |
| **Prefix Length** | Tarmoq qismining bit uzunligi (/24, /30, va h.k.) |
| **AS (Autonomous System)** | Bitta boshqaruv ostidagi tarmoqlar to'plami |
| **Neighbor** | To'g'ridan-to'g'ri ulangan router |
| **Adjacency** | Ikki router o'rtasida o'rnatilgan marshrutlash munosabati |
| **LSA (Link State Advertisement)** | OSPF'da marshrutlash ma'lumotlari |
| **Topology** | Tarmoqning mantiqiy yoki fizik tuzilishi |
| **Redundancy** | Zaxira resurslari yoki yo'llar |
| **Failover** | Asosiy resurs ishdan chiqqanda zaxiraga o'tish |
| **Load Balancing** | Trafikni bir nechta yo'lga taqsimlash |
| **Split Horizon** | Paketni kelgan yo'ldan qaytarmaslik qoidasi |
| **Route Poisoning** | Ishlamay qolgan marshrutni infinity metrika bilan e'lon qilish |

---

**Dars muallifi:** Kompyuter tarmoqlari kafedra  
**Yangilangan sana:** 2025-yil  
**Versiya:** 2.0  

**Maslahatlar va savollar uchun:**  
Email: network.dept@university.uz  
Telefon: +998 XX XXX XX XX

---

*Bu dars ishlanma talabalarning mustaqil ishini qo'llab-quvvatlash va kompyuter tarmoqlari bo'yicha bilimlarini chuqurlashtirish maqsadida tayyorlangan. Barcha huquqlar himoyalangan.*