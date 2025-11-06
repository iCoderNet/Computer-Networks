# SNMP - Tarmoqni Monitoring Qilish Protokoli
## Dars Ishlanma

---

## 1. Kirish

**Simple Network Management Protocol (SNMP)** — bu tarmoq qurilmalarini masofadan boshqarish va monitoring qilish uchun mo'ljallangan internet protokoli hisoblanadi. SNMP zamonaviy tarmoq infratuzilmasining ajralmas qismi bo'lib, tarmoq administratorlarga qurilmalar holati, ishlashi va xatolari haqida real vaqt rejimida ma'lumot olish imkonini beradi.

### 1.1. SNMP ning ahamiyati

Zamonaviy kompyuter tarmoqlari yuzlab, hatto minglab qurilmalardan iborat bo'lishi mumkin. Har bir qurilmani qo'lda nazorat qilish deyarli imkonsizdir. SNMP quyidagi muammolarni hal qiladi:

- Tarmoq qurilmalarining markazlashtirilgan monitoringi
- Muammolarni erta aniqlash va diagnostika qilish
- Tarmoq resurslarining samaradorligini tahlil qilish
- Avtomatlashtirilgan ogohlantirish tizimlari
- Tarmoq konfiguratsiyasini masofadan boshqarish

---

## 2. SNMP ning Tarixi va Rivojlanishi

### 2.1. Paydo bo'lish tarixi

SNMP protokoli 1980-yillarning oxirida Internet tarmoqlarini boshqarish zarurati tufayli yaratildi. Dastlab Simple Gateway Monitoring Protocol (SGMP) asosida ishlab chiqilgan bo'lib, 1988-yilda birinchi versiyasi (SNMPv1) RFC 1067 standartida e'lon qilindi.

### 2.2. Versiyalar evolyutsiyasi

**SNMPv1 (1988)**
- Birinchi standart versiya
- Asosiy monitoring funksiyalari
- Zaif xavfsizlik mexanizmlari (community string)
- Oddiy va tez amalga oshiriladigan

**SNMPv2c (1993-1996)**
- SNMPv2 ning eng keng tarqalgan varianti
- Yaxshilangan xato qaytarish mexanizmlari
- GetBulk operatsiyasi qo'shildi (samaradorlik oshdi)
- 64-bitli hisoblagichlar qo'llab-quvvatlandi
- Community-based xavfsizlik saqlanib qoldi

**SNMPv3 (2002)**
- Xavfsizlik jihatidan eng rivojlangan versiya
- Autentifikatsiya va shifrlash qo'shildi
- Foydalanuvchilar boshqaruvi (User-Based Security Model)
- Kirish huquqlarini boshqarish (View-Based Access Control)
- Zamonaviy tarmoqlarda tavsiya etiladi

---

## 3. SNMP Arxitekturasi va Tuzilishi

### 3.1. Asosiy komponentlar

SNMP arxitekturasi uchta asosiy komponentdan iborat:

#### 3.1.1. SNMP Manager (Boshqaruvchi)
- Tarmoqni monitoring qiluvchi markaziy tizim
- Qurilmalardan ma'lumot so'raydi va to'playdi
- Olingan ma'lumotlarni tahlil qiladi va saqlaydi
- Network Management Station (NMS) sifatida ham tanilgan
- Misol: Nagios, PRTG, Zabbix, SolarWinds

#### 3.1.2. SNMP Agent (Agent)
- Har bir tarmoq qurilmasida ishlaydigan dasturiy ta'minot
- Qurilma holatini monitoring qiladi
- Manager so'rovlariga javob beradi
- Muhim hodisalar haqida trap yuboradi
- Router, switch, server va boshqa qurilmalarda faol ishlaydi

#### 3.1.3. Management Information Base (MIB)
- Boshqarish ma'lumotlarining tuzilgan bazasi
- Qurilmalar haqida olinishi mumkin bo'lgan ma'lumotlar ro'yxati
- Ierarxik daraxt strukturasida tashkil etilgan
- Object Identifier (OID) orqali identifikatsiya qilinadi
- Standart va maxsus (vendor-specific) MIBlar mavjud

### 3.2. SNMP arxitektura sxemasi

```
┌─────────────────────────────────────────────────┐
│         SNMP Manager (NMS)                      │
│    ┌──────────────────────────────┐            │
│    │  Management Application      │            │
│    └──────────────────────────────┘            │
│    ┌──────────────────────────────┐            │
│    │  SNMP Engine                 │            │
│    └──────────────────────────────┘            │
└─────────────────┬───────────────────────────────┘
                  │ SNMP Messages
                  │ (UDP 161/162)
         ─────────┴─────────
         │                 │
┌────────▼─────┐  ┌────────▼─────┐
│  Agent 1     │  │  Agent 2     │
│  (Router)    │  │  (Switch)    │
│ ┌──────────┐ │  │ ┌──────────┐ │
│ │   MIB    │ │  │ │   MIB    │ │
│ └──────────┘ │  │ └──────────┘ │
└──────────────┘  └──────────────┘
```

---

## 4. SNMP Operatsiyalari va Xabarlar

### 4.1. Asosiy SNMP operatsiyalari

#### 4.1.1. GET
- Manager agentdan bitta qiymatni so'raydi
- Eng sodda va tez-tez ishlatiladigan operatsiya
- Misol: interfeys holati, CPU foydalanishi

```
Manager → Agent: GET(OID: 1.3.6.1.2.1.1.1.0)
Agent → Manager: RESPONSE(Value: "Cisco IOS Router")
```

#### 4.1.2. GET-NEXT
- Keyingi OID qiymatini olish uchun ishlatiladi
- MIB daraxtini ketma-ket o'rganish imkonini beradi
- Dinamik kashfiyot uchun foydali

#### 4.1.3. GET-BULK (SNMPv2c/v3)
- Bir nechta qiymatlarni bir vaqtning o'zida olish
- Katta jadvallar bilan ishlashda samaradorlikni oshiradi
- Tarmoq trafigini kamaytiradi

#### 4.1.4. SET
- Qurilma konfiguratsiyasini o'zgartirish
- Parametrlarni masofadan sozlash
- Xavfsizlik nuqtai nazaridan ehtiyotkorlik talab etadi

```
Manager → Agent: SET(OID: 1.3.6.1.2.1.1.6.0, Value: "Server Room A")
Agent → Manager: RESPONSE(Status: Success)
```

#### 4.1.5. TRAP
- Agent tomonidan avtomatik yuboriladi
- Muhim hodisalar haqida xabar beradi
- Manager so'rovisiz ishlaydi
- Kritik voqealarni darhol bildiradi

```
Agent → Manager: TRAP(OID: linkDown, Interface: eth0, Time: 14:30:25)
```

#### 4.1.6. INFORM (SNMPv2c/v3)
- Trap ga o'xshash, lekin tasdiqlash talab etadi
- Ishonchliroq xabar yetkazish mexanizmi
- Manager tasdiq qaytarishi kerak

### 4.2. SNMP xabar formati

SNMP xabarlari Abstract Syntax Notation One (ASN.1) formatida kodlanadi va Basic Encoding Rules (BER) yordamida uzatiladi.

**Asosiy xabar tuzilishi:**
```
┌─────────────────────────────┐
│  SNMP Version               │
├─────────────────────────────┤
│  Community String / Security│
├─────────────────────────────┤
│  PDU Type                   │
├─────────────────────────────┤
│  Request ID                 │
├─────────────────────────────┤
│  Error Status               │
├─────────────────────────────┤
│  Error Index                │
├─────────────────────────────┤
│  Variable Bindings (OID+Val)│
└─────────────────────────────┘
```

---

## 5. Management Information Base (MIB)

### 5.1. MIB tuzilishi

MIB ierarxik daraxt strukturasida tashkil etilgan bo'lib, har bir tugun Object Identifier (OID) bilan identifikatsiya qilinadi.

#### 5.1.1. OID ierarxiyasi

```
                    root
                     │
        ┌────────────┼────────────┐
        │            │            │
      iso(1)      itu(0)      joint(2)
        │
      org(3)
        │
      dod(6)
        │
    internet(1)
        │
    ┌───┴────┬──────────┬──────────┐
    │        │          │          │
directory(1) mgmt(2)  experimental(3) private(4)
             │                      │
          mib-2(1)              enterprises(1)
             │                      │
    ┌────────┴─────┐           ┌───┴────┐
 system(1)  interfaces(2)   cisco(9) juniper(2636)
```

### 5.2. Standart MIB-II ob'ektlari

**system (1.3.6.1.2.1.1)** - Tizim ma'lumotlari
- sysDescr: Tizim tavsifi
- sysObjectID: Mahsulot identifikatori
- sysUpTime: Ishlash vaqti
- sysContact: Administrator kontakti
- sysName: Tizim nomi
- sysLocation: Jismoniy manzil

**interfaces (1.3.6.1.2.1.2)** - Tarmoq interfeyslari
- ifNumber: Interfeyslar soni
- ifTable: Interfeyslar jadvali
- ifDescr: Interfeys tavsifi
- ifType: Interfeys turi
- ifSpeed: Tezlik
- ifOperStatus: Operatsion holat
- ifInOctets/ifOutOctets: Kirim/chiqim trafik

**ip (1.3.6.1.2.1.4)** - IP statistikasi
- ipForwarding: Marshrutlash holati
- ipInReceives: Qabul qilingan paketlar
- ipInDelivers: Yetkazilgan paketlar
- ipOutRequests: Yuborilgan paketlar

**tcp (1.3.6.1.2.1.6)** - TCP statistikasi
- tcpActiveOpens: Faol ulanishlar
- tcpPassiveOpens: Passiv ulanishlar
- tcpCurrEstab: Joriy ulanishlar
- tcpInSegs: Qabul qilingan segmentlar

**udp (1.3.6.1.2.1.7)** - UDP statistikasi
- udpInDatagrams: Kiruvchi datagrammalar
- udpOutDatagrams: Chiquvchi datagrammalar
- udpNoPorts: Port topilmagan xatolari

### 5.3. Vendor-specific MIB lar

Har bir ishlab chiqaruvchi o'z maxsus MIB larini yaratishi mumkin:
- Cisco: 1.3.6.1.4.1.9
- Juniper: 1.3.6.1.4.1.2636
- HP: 1.3.6.1.4.1.11
- Dell: 1.3.6.1.4.1.674

---

## 6. SNMP Xavfsizligi

### 6.1. SNMPv1 va v2c xavfsizligi

**Community String** - oddiy parol mexanizmi
- **Read Community**: Faqat o'qish huquqi (default: public)
- **Write Community**: Yozish huquqi (default: private)
- Ochiq matnda uzatiladi (xavfsizlik zaiflik)
- Man-in-the-middle hujumlarga moyil

**Xavfsizlik tavsifalari:**
- Default community string larni o'zgartiring
- Murakkab community string lar ishlating
- ACL (Access Control List) orqali kirish cheklang
- SNMPv3 ga o'ting (eng yaxshi yechim)

### 6.2. SNMPv3 xavfsizlik modeli

SNMPv3 uchta xavfsizlik darajasini taqdim etadi:

#### 6.2.1. NoAuthNoPriv
- Autentifikatsiya va shifrlash yo'q
- Faqat foydalanuvchi nomi tekshiriladi
- Xavfsiz bo'lmagan muhitlar uchun

#### 6.2.2. AuthNoPriv
- Autentifikatsiya bor, shifrlash yo'q
- HMAC-MD5 yoki HMAC-SHA algoritmlari
- Xabar yaxlitligini ta'minlaydi
- Parollar himoyalangan

#### 6.2.3. AuthPriv (tavsiya etiladi)
- Autentifikatsiya va shifrlash
- DES, 3DES yoki AES shifrlash
- To'liq xavfsizlik
- Maxfiylik va yaxlitlik kafolatlanadi

### 6.3. User-Based Security Model (USM)

SNMPv3 da foydalanuvchilar quyidagicha sozlanadi:

```
Foydalanuvchi parametrlari:
├── Username (foydalanuvchi nomi)
├── Authentication Protocol (MD5/SHA)
├── Authentication Password (autentifikatsiya paroli)
├── Privacy Protocol (DES/AES)
└── Privacy Password (shifrlash paroli)
```

### 6.4. View-Based Access Control Model (VACM)

Kirish huquqlarini aniq belgilash:
- **Read View**: O'qish mumkin bo'lgan OID lar
- **Write View**: Yozish mumkin bo'lgan OID lar
- **Notify View**: Trap yuborish mumkin bo'lgan OID lar

---

## 7. SNMP Transport protokoli

### 7.1. UDP protokoli

SNMP asosan UDP (User Datagram Protocol) ustida ishlaydi:

**Standart portlar:**
- **UDP 161**: Agent so'rovlari uchun (GET, SET)
- **UDP 162**: Trap va Inform xabarlari uchun

**UDP ning afzalliklari:**
- Kam resurs talab qiladi
- Tez ishlaydi
- Oddiy ulanish
- Tarmoq yuklamasini kamaytiradi

**UDP ning kamchiliklari:**
- Ishonchsiz (unreliable)
- Paketlar yo'qolishi mumkin
- Tartibsiz yetib kelishi mumkin
- Qayta yuborish mexanizmi yo'q (SNMP darajasida hal qilinadi)

### 7.2. TCP qo'llab-quvvatlashi

SNMPv3 TCP ustida ham ishlashi mumkin (RFC 3430):
- Ishonchli ulanish
- Katta ma'lumotlar uchun qulay
- Firewall orqali oson o'tkazish
- Kam qo'llaniladi (UDP standart hisoblanadi)

---

## 8. SNMP Polling va Trapping

### 8.1. Polling (So'rov yuborish)

Manager muntazam ravishda agentlardan ma'lumot so'raydi:

**Polling turlari:**

1. **Fixed Interval Polling** - Belgilangan interval
   - Har N soniyada so'rov
   - Oddiy va bashorat qilinadigan
   - Misol: Har 5 daqiqada CPU load ni tekshirish

2. **Adaptive Polling** - Moslashuvchan
   - Holat o'zgarganda interval o'zgaradi
   - Resurslarni tejash
   - Murakkab konfiguratsiya

3. **Event-Driven Polling** - Hodisaga asoslangan
   - Trap kelganda batafsil so'rov
   - Samarali monitoring

**Polling intervallari:**
- Critical qurilmalar: 30 sekund - 1 daqiqa
- Normal qurilmalar: 5 - 10 daqiqa
- Statistik ma'lumotlar: 15 - 30 daqiqa

### 8.2. Trap (Ogohlantirish)

Agent muhim hodisalar haqida avtomatik xabar beradi:

**Standart trap turlari:**

1. **coldStart (0)** - Qurilma qayta ishga tushdi
2. **warmStart (1)** - SNMP agent qayta boshlandi
3. **linkDown (2)** - Interfeys o'chdi
4. **linkUp (3)** - Interfeys yondi
5. **authenticationFailure (4)** - Autentifikatsiya xatosi
6. **egpNeighborLoss (5)** - EGP qo'shni yo'qoldi
7. **enterpriseSpecific (6)** - Maxsus trap

**Trap konfiguratsiyasi:**
```
Trap parametrlari:
├── Trap Destination (Manager IP manzili)
├── Trap Community String (xavfsizlik)
├── Trap Version (v1, v2c, v3)
└── Trap Filter (qaysi trap lar yuborilsin)
```

---

## 9. SNMP Performance va Optimization

### 9.1. Samaradorlikni oshirish usullari

#### 9.1.1. GetBulk ishlatish
- Bir nechta qiymatni bitta so'rovda olish
- Tarmoq yuklamasini 70-80% ga kamaytirish
- Katta jadvallar uchun muhim

#### 9.1.2. Parallel so'rovlar
- Bir vaqtning o'zida bir nechta qurilmaga so'rov
- Umumiy monitoring vaqtini qisqartirish
- Thread pool yoki async dasturlash

#### 9.1.3. Kesh mexanizmi
- Tez-tez so'ralaydigan ma'lumotlarni keshlash
- Database ga yozish oldidan to'plash
- Memory cache (Redis, Memcached)

#### 9.1.4. MIB optimizatsiyasi
- Faqat kerakli OID larni so'rash
- Keraksiz MIB yuklamasini kamaytirish
- Custom MIB yaratish

### 9.2. Tarmoq yuklamasini boshqarish

**Hisoblash formulasi:**
```
Bir so'rov hajmi ≈ 150-200 bayt
Polling interval = 5 daqiqa
Qurilmalar soni = 1000
Har bir qurilmadan 50 OID

Traffic per hour = (1000 × 50 × 200 bayt × 12) / 1024² ≈ 114 MB/soat
```

**Optimizatsiya strategiyalari:**
- Muhim metrikalar uchun qisqa interval
- Kam muhim ma'lumotlar uchun uzoq interval
- SNMP traffic ni alohida VLAN ga ajratish
- QoS sozlamalari

---

## 10. SNMP Monitoring Tizimlarini Tashkil Etish

### 10.1. Monitoring arxitekturasi

#### 10.1.1. Markazlashtirilgan model
```
              ┌─────────────┐
              │   Manager   │
              │    (NMS)    │
              └──────┬──────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
    ┌───▼───┐   ┌───▼───┐   ┌───▼───┐
    │Agent 1│   │Agent 2│   │Agent 3│
    └───────┘   └───────┘   └───────┘
```
- Oddiy boshqarish
- Bitta nuqtadan nazorat
- Single point of failure xavfi

#### 10.1.2. Distributed model
```
    ┌──────────┐       ┌──────────┐
    │ Manager 1│       │ Manager 2│
    └────┬─────┘       └────┬─────┘
         │                  │
    ┌────┴─────┬───────────┴────┐
    │          │                 │
┌───▼───┐  ┌──▼────┐      ┌────▼───┐
│Agent 1│  │Agent 2│      │Agent 3 │
└───────┘  └───────┘      └────────┘
```
- Yuqori ishonchlilik
- Geografik tarqatilgan tarmoqlar uchun
- Murakkab konfiguratsiya

### 10.2. Monitoring metrikalar

#### 10.2.1. Qurilma sog'ligi
- CPU foydalanishi (%)
- Xotira foydalanishi (%)
- Temperatura (°C)
- Fan tezligi (RPM)
- Quvvat manbai holati

#### 10.2.2. Tarmoq performance
- Interfeys holati (up/down)
- Bandwidth foydalanishi (%)
- Paket yo'qotilishi (%)
- Xatolar soni
- Trafik hajmi (bps)

#### 10.2.3. Xizmat sifati (QoS)
- Latency (ms)
- Jitter (ms)
- Packet loss rate (%)
- Throughput (Mbps)

### 10.3. Threshold va alerting

**Alert darajalari:**
1. **Information** - Ma'lumot xarakterdagi hodisa
2. **Warning** - Ogoh qilish, ehtiyot choralarini ko'rish
3. **Critical** - Kritik holat, darhol aralashish kerak
4. **Emergency** - Favqulodda holat, tizim ishlamayapti

**Alert kanallari:**
- Email xabarnomalar
- SMS jo'natish
- Telegram/Slack bot
- SNMP trap forwarding
- Syslog integratsiyasi
- Dashboard notification

---

## 11. Mashhur SNMP Monitoring Tizimlari

### 11.1. Open Source yechimlari

#### 11.1.1. Nagios
- Keng tarqalgan monitoring tizimi
- Plugin arxitekturasi
- Kuchli ogohlantirish tizimi
- Web interfeysi

#### 11.1.2. Zabbix
- Professional monitoring platformasi
- Auto-discovery funksiyasi
- Template lar tizimi
- Distributed monitoring
- Database backend (MySQL, PostgreSQL)

#### 11.1.3. Cacti
- Grafik monitoring tizimi
- RRDTool asosida
- Chiroyli graflar
- Template lar kolleksiyasi

#### 11.1.4. Prometheus + Grafana
- Zamonaviy monitoring stack
- Time-series database
- PromQL so'rov tili
- Grafana visualization
- SNMP exporter orqali integratsiya

### 11.2. Enterprise yechimlari

#### 11.2.1. SolarWinds Network Performance Monitor
- Professional enterprise yechim
- NetPath network topology mapping
- PerfStack performance correlation
- Intelligent alerting

#### 11.2.2. PRTG Network Monitor
- Foydalanuvchiga qulay interfeys
- Auto-discovery
- 250+ sensor turlari
- Mobile apps

#### 11.2.3. ManageEngine OpManager
- Keng funksional imkoniyatlar
- Network mapping
- Workflow automation
- Multi-vendor qo'llab-quvvatlash

---

## 12. SNMP Troubleshooting

### 12.1. Keng tarqalgan muammolar

#### 12.1.1. So'rov javob bermayapti (Timeout)
**Sabablar:**
- Agent ishlamayapti
- Firewall bloklab qo'ygan
- Noto'g'ri community string
- Tarmoq ulanish muammosi
- Agent yuklangan

**Yechim:**
```bash
# SNMP agent holati
service snmpd status

# Firewall qoidalarini tekshirish
iptables -L -n | grep 161

# Manual so'rov yuborish
snmpget -v2c -c public 192.168.1.1 sysDescr.0
```

#### 12.1.2. Authentication xatosi
**Sabablar:**
- Noto'g'ri community string
- SNMPv3 parol xatosi
- ACL cheklovi
- Version mismatch

**Yechim:**
- Konfiguratsiyani tekshirish
- Community string ni yangilash
- ACL qoidalarini ko'rib chiqish

#### 12.1.3. OID topilmadi
**Sabablar:**
- MIB yuklanmagan
- Noto'g'ri OID
- Qurilma qo'llab-quvvatlamaydi

**Yechim:**
- MIB fayllarini yuklash
- MIB walk orqali mavjud OID larni topish
- Vendor dokumentatsiyasini tekshirish

### 12.2. Diagnostika vositalari

#### 12.2.1. snmpwalk
MIB daraxtini to'liq o'rganish:
```bash
snmpwalk -v2c -c public 192.168.1.1
```

#### 12.2.2. snmpget
Aniq qiymatni olish:
```bash
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.5.0
```

#### 12.2.3. snmpset
Qiymatni o'zgartirish:
```bash
snmpset -v2c -c private 192.168.1.1 sysContact.0 s "admin@example.com"
```

#### 12.2.4. Wireshark
SNMP paketlarini tahlil qilish:
- UDP port 161/162 filtri
- SNMP xabarlar strukturasi
- Community string ko'rish (v1/v2c)

---

## 13. Amaliy Ishlatish

### 13.1. Linux da SNMP agent o'rnatish

```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install snmpd snmp

# CentOS/RHEL
sudo yum install net-snmp net-snmp-utils

# Agent ni ishga tushirish
sudo systemctl start snmpd
sudo systemctl enable snmpd
```

### 13.2. Asosiy konfiguratsiya

**/etc/snmp/snmpd.conf** fayli:
```bash
# Community string sozlamasi
rocommunity public 192.168.1.0/24
rwcommunity private 192.168.1.10

# System ma'lumotlari
syslocation "Server Room, Building A"
syscontact "admin@example.com"

# Kirish cheklash
agentaddress udp:161
```

### 13.3. Oddiy monitoring skripti (Python)

```python
from pysnmp.hlapi import *

def snmp_get(host, community, oid):
    iterator = getCmd(
        SnmpEngine(),
        CommunityData(community),
        UdpTransportTarget((host, 161)),
        ContextData(),
        ObjectType(ObjectIdentity(oid))
    )
    
    errorIndication, errorStatus, errorIndex, varBinds = next(iterator)
    
    if errorIndication:
        print(f"Error: {errorIndication}")
    else:
        for varBind in varBinds:
            return varBind[1]

# Foydalanish
hostname = snmp_get('192.168.1.1', 'public', '1.3.6.1.2.1.1.5.0')
print(f"Hostname: {hostname}")
```

### 13.4. Monitoring dashboard yaratish

Oddiy skript yordamida monitoring:
```python
import time
from pysnmp.hlapi import *

def monitor_interface(host, community, interface_index):
    # Interface holati
    oid_status = f'1.3.6.1.2.1.2.2.1.8.{interface_index}'
    # Kirish trafik
    oid_in = f'1.3.6.1.2.1.2.2.1.10.{interface_index}'
    # Chiqish trafik
    oid_out = f'1.3.6.1.2.1.2.2.1.16.{interface_index}'
    
    while True:
        status = snmp_get(host, community, oid_status)
        in_octets = snmp_get(host, community, oid_in)
        out_octets = snmp_get(host, community, oid_out)
        
        print(f"Status: {status}, In: {in_octets}, Out: {out_octets}")
        time.sleep(60)  # Har 1 daqiqada
```

---

## 14. SNMP Kelajagi va Alternativlar

### 14.1. SNMP ning kelajagi

SNMP 30 yildan ortiq vaqt davomida tarmoq monitoringida dominant protokol bo'lib kelgan. Ammo zamonaviy texnologiyalar bilan birga yangi yondashuvlar paydo bo'lmoqda:

**SNMP ning kuchli tomonlari:**
- Barcha tarmoq qurilmalarida qo'llab-quvvatlanadi
- Standartlashtirilgan va yaxshi hujjatlashtirilgan
- Oddiy va samarali
- Keng instrument ekotizimi

**Muammoli jihatlar:**
- Polling mexanizmi overhead yaratadi
- MIB lar murakkab va noqulay
- Real-time monitoring cheklangan
- Zamonaviy cloud muhitlar uchun mos emas

### 14.2. Zamonaviy alternativlar

#### 14.2.1. NETCONF/YANG
- XML asosidagi konfiguratsiya protokoli
- Transactional operatsiyalar
- Programmatic API
- Modern SDN uchun qulay

```xml
<rpc message-id="101">
  <get-config>
    <source><running/></source>
  </get-config>
</rpc>
```

#### 14.2.2. gRPC va gNMI
- Google tomonidan ishlab chiqilgan
- Binary protokol (Protocol Buffers)
- Streaming ma'lumotlar
- Yuqori samaradorlik

#### 14.2.3. RESTCONF
- RESTful API yondashuvi
- HTTP/HTTPS asosida
- JSON yoki XML formatlar
- Web-friendly

#### 14.2.4. Telemetry (Model-Driven)
- Push mexanizmi (polling emas)
- Real-time ma'lumotlar
- Kam latency
- Cisco, Juniper qo'llab-quvvatlaydi

### 14.3. Hybrid yondashuv

Zamonaviy tarmoqlarda SNMP va yangi texnologiyalar birga ishlatiladi:

```
Legacy qurilmalar → SNMP monitoring
Modern routerlar → Telemetry + SNMP
SDN Controllers → NETCONF/RESTCONF
Applications → REST API + Metrics
```

---

## 15. Best Practices va Tavsiyalar

### 15.1. Xavfsizlik bo'yicha tavsiyalar

1. **SNMPv3 ishlatish**
   - AuthPriv darajasida konfiguratsiya
   - Murakkab parollar tanlash
   - Parollarni davriy yangilash

2. **ACL sozlash**
   - Faqat kerakli IP manzillarga ruxsat
   - Management VLAN ajratish
   - Segment-based kirish cheklash

3. **Default sozlamalarni o'zgartirish**
   - 'public' va 'private' community stringlarni o'chirish
   - Yangi, murakkab stringlar yaratish
   - SNMP write kirish cheklash

4. **Monitoring va logging**
   - Authentication xatolari logini yozish
   - Anomaliyalarni aniqlash
   - SNMP trafigini monitoring qilish

5. **Firewall qoidalar**
```bash
# Faqat monitoring server dan ruxsat
iptables -A INPUT -p udp --dport 161 -s 192.168.1.10 -j ACCEPT
iptables -A INPUT -p udp --dport 161 -j DROP
```

### 15.2. Performance optimizatsiya

1. **Optimal polling interval tanlash**
   - Critical metrikalar: 1-2 daqiqa
   - Oddiy metrikalar: 5-10 daqiqa
   - Statistik ma'lumotlar: 15-30 daqiqa

2. **GetBulk ishlatish**
   - Katta jadvallar uchun majburiy
   - Max-repetitions parametrini sozlash
   - Tarmoq yuklamasini 70% ga kamaytirish

3. **Parallel processing**
   - Multi-threading yoki async
   - Timeout ni to'g'ri sozlash
   - Connection pooling

4. **Ma'lumotlarni saqlash strategiyasi**
   - Time-series database (InfluxDB, Prometheus)
   - Data aggregation va downsampling
   - Retention policies

### 15.3. Konfiguratsiya boshqaruvi

1. **Template lar yaratish**
   - Qurilma tipiga qarab
   - Vendor-specific konfiguratsiyalar
   - Version control (Git)

2. **Automation**
   - Ansible, Puppet, Chef
   - Auto-discovery skriptlari
   - Automatic onboarding

3. **Dokumentatsiya**
   - MIB lar ro'yxati
   - Custom OID lar
   - Alert qoidalar
   - Troubleshooting qo'llanma

### 15.4. Kapatsiyani rejalashtirish

1. **Resource monitoring**
   - NMS server resurslari
   - Database o'sish sur'ati
   - Network bandwidth foydalanish

2. **Scalability**
   - Horizontal scaling strategiyasi
   - Load balancing
   - Database sharding

3. **Backup va recovery**
   - Konfiguratsiya fayllari backup
   - Historical data backup
   - Disaster recovery plan

---

## 16. Real Dunyo Stsenariyalari

### 16.1. Sssenariya 1: Datacenter monitoring

**Vazifa:** 500 serverli datacenter ni monitoring qilish

**Yechim:**
- Zabbix yoki Nagios ishlatish
- Auto-discovery konfiguratsiya
- Template lar yaratish (Linux, Windows, VMware)
- 5 daqiqalik polling interval
- Critical alert lar uchun Telegram bot

**Monitoring metrikalar:**
- CPU, Memory, Disk foydalanishi
- Network interfeys holati
- RAID status
- Temperatura sensorlari
- UPS holati

### 16.2. Sssenariya 2: ISP tarmoq monitoringi

**Vazifa:** 100+ router va switchni monitoring qilish

**Yechim:**
- LibreNMS yoki Observium
- SNMP v2c yoki v3
- Bandwidth monitoring (95th percentile)
- BGP peer monitoring
- Automated topology mapping

**Monitoring metrikalar:**
- Interface bandwidth foydalanish
- BGP session holati
- Routing table o'lchamlari
- QoS statistika
- Optical power levels (SFP)

### 16.3. Sssenariya 3: Enterprise campus network

**Vazifa:** Katta universitet kampusi tarmoqni monitoring

**Yechim:**
- PRTG Network Monitor
- Distributed poller lar
- VLAN-based monitoring
- Wireless controller monitoring
- Switch port mapping

**Monitoring metrikalar:**
- Access switch port holati
- Wireless AP ishlashi
- User authentication statistika
- DHCP pool foydalanish
- Network access control

---

## 17. SNMP Integration

### 17.1. Syslog bilan integratsiya

SNMP trap larni Syslog serverga yo'naltirish:

```bash
# snmptrapd.conf
traphandle default /usr/bin/logger -t snmptrapd -p local0.warning

# rsyslog.conf
local0.* @192.168.1.100:514
```

### 17.2. Ticketing tizimlar bilan

SNMP alertlardan avtomatik ticket yaratish:

```python
from pysnmp.hlapi import *
import requests

def create_ticket(alert_data):
    ticket_api = "https://helpdesk.example.com/api/tickets"
    payload = {
        "title": f"Network Alert: {alert_data['device']}",
        "description": alert_data['message'],
        "priority": "high"
    }
    requests.post(ticket_api, json=payload)

def trap_receiver():
    # Trap listener kodi
    # Alert kelganda create_ticket() ni chaqirish
    pass
```

### 17.3. Visualization platformalar

**Grafana integratsiyasi:**
- SNMP Exporter ishlatish
- Prometheus bilan bog'lash
- Custom dashboard yaratish
- Alert rules konfiguratsiya

**ELK Stack:**
- SNMP ma'lumotlarni Logstash ga yo'naltirish
- Elasticsearch da indekslash
- Kibana da visualize qilish

### 17.4. Chatops integratsiyasi

Slack/Telegram bot orqali SNMP monitoring:

```python
import telegram

def send_alert(bot_token, chat_id, message):
    bot = telegram.Bot(token=bot_token)
    bot.send_message(
        chat_id=chat_id,
        text=f"🚨 Network Alert\n\n{message}",
        parse_mode='Markdown'
    )

# Critical alert kelganda
if alert_severity == 'critical':
    send_alert(TOKEN, CHAT_ID, alert_message)
```

---

## 18. Lab Mashqlari va Amaliy Topshiriqlar

### 18.1. Lab 1: SNMP agent sozlash

**Maqsad:** Linux serverda SNMP agentni o'rnatish va sozlash

**Topshiriqlar:**
1. snmpd o'rnatish
2. Community string sozlash
3. System ma'lumotlarini konfiguratsiya qilish
4. Firewall sozlamalari
5. snmpwalk bilan tekshirish

### 18.2. Lab 2: Oddiy monitoring skript yaratish

**Maqsad:** Python yordamida SNMP monitoring skripti

**Topshiriqlar:**
1. PyPi kutubxonalarni o'rnatish (pysnmp)
2. GET so'rovlar yuborish
3. Ma'lumotlarni CSV ga yozish
4. Cron job sozlash
5. Email alert qo'shish

### 18.3. Lab 3: Trap handler yaratish

**Maqsad:** SNMP trap larni qabul qilish va qayta ishlash

**Topshiriqlar:**
1. snmptrapd sozlash
2. Trap handler skripti yozish
3. Test trap yuborish
4. Log faylga yozish
5. Alert trigger qilish

### 18.4. Lab 4: Monitoring dashboard

**Maqsad:** Web-based monitoring dashboard yaratish

**Topshiriqlar:**
1. Flask web application yaratish
2. SNMP ma'lumotlarni olish
3. Chart.js bilan grafik chizish
4. Real-time yangilanish (WebSocket)
5. Responsive dizayn

---

## 19. Exam Savollari va Javoblari

### 19.1. Nazariy savollar

**1-savol:** SNMP ning qaysi versiyasi xavfsizlik jihatidan eng yaxshi va nima uchun?

**Javob:** SNMPv3 eng xavfsiz versiya hisoblanadi, chunki:
- Autentifikatsiya mexanizmi (HMAC-MD5/SHA)
- Shifrlash qo'llab-quvvatlanadi (DES/AES)
- User-Based Security Model (USM)
- Access Control (VACM)
- Ochiq matnda parol yuborilmaydi

**2-savol:** GET va GET-BULK operatsiyalari o'rtasidagi farq nima?

**Javob:** 
- GET: Bitta OID qiymatini oladi
- GET-BULK: Bir nechta qiymatni bitta so'rovda oladi
- GET-BULK samaradorroq (katta jadvallar uchun)
- GET-BULK SNMPv2c va v3 da mavjud

**3-savol:** MIB nima va qanday tuzilgan?

**Javob:** Management Information Base - ierarxik daraxt strukturasidagi ma'lumotlar bazasi. Har bir tugun OID (Object Identifier) bilan belgilanadi. ISO standartidan boshlanib, internet(1), mgmt(2), mib-2(1) va boshqa tarmoqlanishlar orqali tashkil etilgan.

### 19.2. Amaliy savollar

**4-savol:** 192.168.1.1 manzildagi qurilmadan hostname ni qanday olish mumkin?

**Javob:**
```bash
snmpget -v2c -c public 192.168.1.1 1.3.6.1.2.1.1.5.0
# yoki
snmpget -v2c -c public 192.168.1.1 sysName.0
```

**5-savol:** SNMP agent nima uchun javob bermasligi mumkin? (5 ta sabab)

**Javob:**
1. Agent service ishlamayapti
2. Firewall UDP 161 portini bloklab qo'ygan
3. Noto'g'ri community string
4. ACL da manager IP ruxsat berilmagan
5. Tarmoq ulanish muammosi

### 19.3. Scenario-based savollar

**6-savol:** Interface trafikning keskin o'sganini qanday monitoring qilasiz?

**Javob:**
1. ifInOctets va ifOutOctets ni muntazam polling qilish
2. Delta ni hisoblash (hozirgi - oldingi)
3. Threshold belgilash (masalan, 80% utilization)
4. Threshold oshganda alert yuborish
5. Trap qabul qilish uchun handler sozlash

---

## 20. Qo'shimcha Resurslar

### 20.1. Rasmiy hujjatlar

**RFC standartlari:**
- RFC 1157 - SNMPv1
- RFC 1905 - SNMPv2 Protocol Operations
- RFC 3411-3418 - SNMPv3
- RFC 2578-2580 - SMI (Structure of Management Information)

**Foydali websaytlar:**
- [Net-SNMP](http://www.net-snmp.org/) - Eng keng tarqalgan SNMP toolkit
- [SNMP.com](https://www.snmp.com/) - SNMP ta'lim resursi
- [OID Repository](http://www.oid-info.com/) - OID ma'lumotlar bazasi
- [IANA](https://www.iana.org/assignments/enterprise-numbers/) - Enterprise numbers

### 20.2. Kutubxonalar va toollar

**Python:**
- PySNMP - To'liq SNMP stack
- EasySNMP - Oddiy interfeys
- Python-netsnmp - C kutubxona wrapper

**Monitoring platformalar:**
- Nagios - [nagios.org](https://www.nagios.org/)
- Zabbix - [zabbix.com](https://www.zabbix.com/)
- Prometheus - [prometheus.io](https://prometheus.io/)
- LibreNMS - [librenms.org](https://www.librenms.org/)

**MIB brauzerlar:**
- iReasoning MIB Browser
- Paessler MIB Importer
- ManageEngine MIB Browser

### 20.3. O'quv materiallari

**Kitoblar:**
- "Essential SNMP" by Douglas Mauro and Kevin Schmidt
- "SNMP, SNMPv2, SNMPv3, and RMON 1 and 2" by William Stallings
- "Network Management: Principles and Practice" by Mani Subramanian

**Online kurslar:**
- Udemy - Network Management with SNMP
- Coursera - Network Monitoring and Management
- Pluralsight - SNMP Fundamentals

**Video qo'llanmalar:**
- YouTube - NetworkChuck, David Bombal
- CBT Nuggets - SNMP tutorials
- INE - SNMP deep dive

### 20.4. Amaliyot uchun muhitlar

**Virtual lab:**
- GNS3 - Network emulator
- EVE-NG - Network emulator
- Cisco VIRL - Virtual Internet Routing Lab
- Packet Tracer - Cisco simulyatori

**Cloud platformalar:**
- AWS - EC2 instance lar
- Google Cloud - Compute Engine
- Azure - Virtual Machines
- DigitalOcean - Droplets

---

## 21. Xulosa

SNMP (Simple Network Management Protocol) - bu tarmoq monitoring va boshqaruv sohasida fundamental protokol bo'lib, 30 yildan ortiq vaqt davomida o'z ahamiyatini yo'qotmagan. Ushbu protokol tarmoq administratorlarga quyidagi imkoniyatlarni taqdim etadi:

### 21.1. Asosiy xulosalar

**SNMP ning afzalliklari:**
- Universal qo'llab-quvvatlanish (barcha vendor lar)
- Oddiy va samarali arxitektura
- Standartlashtirilgan yondashuv
- Keng instrumental ekotizim
- Kam resurs talab qilish

**Muhim jihatlar:**
- SNMPv3 ishlatish xavfsizlik uchun majburiy
- To'g'ri polling interval tanlash muhim
- MIB lar bilan ishlashni bilish zarur
- Monitoring strategiyasini oldindan rejalashtirish
- Best practices ga rioya qilish

**Kelajak istiqbollari:**
- SNMP hali ham keng qo'llaniladi
- Yangi texnologiyalar bilan hybrid yondashuv
- Telemetry va model-driven protokollar o'sishi
- Cloud-native monitoring evolyutsiyasi

### 21.2. Yakuniy tavsiyalar

Muvaffaqiyatli SNMP monitoring tizimini tashkil etish uchun:

1. **Puxta rejalashtirish** - Monitoring strategiyasi, metrikalar, threshold lar
2. **Xavfsizlikni ta'minlash** - SNMPv3, ACL, segmentatsiya
3. **Optimizatsiya** - Polling interval, GetBulk, parallel processing
4. **Avtomatlashtirish** - Auto-discovery, configuration management
5. **Integratsiya** - Ticketing, alerting, visualization
6. **Doimiy takomillashtirish** - Log tahlil, performance tuning
7. **Hujjatlashtirish** - Konfiguratsiya, proseduralar, troubleshooting

### 21.3. Xususiy topshiriq

Darsni yakunlash uchun talabalardan quyidagi loyihani bajarish tavsiya etiladi:

**Mini-loyiha:** O'z tarmoqingiz uchun monitoring tizimi yaratish
1. Kamida 3 ta qurilmani monitoring qilish
2. SNMPv2c yoki v3 dan foydalanish
3. 5-10 ta asosiy metrika yig'ish
4. Oddiy dashboard yaratish
5. Alert mexanizmi qo'shish

Bu loyiha orqali nazariy bilimlarni amaliyotda qo'llash va real tajriba orttirish mumkin.

---

## 22. Glossariy (Terminlar Lug'ati)

**Agent** - Tarmoq qurilmasida ishlaydigan SNMP dasturiy ta'minot moduli

**ASN.1** - Abstract Syntax Notation One, ma'lumotlarni aniqlash uchun standart

**BER** - Basic Encoding Rules, ASN.1 ni kodlash qoidalari

**Community String** - SNMPv1/v2c da autentifikatsiya uchun ishlatiladigan parol

**GetBulk** - Bir nechta OID qiymatlarini olish operatsiyasi

**Inform** - Tasdiqlash talab qiladigan SNMP xabari

**Manager** - SNMP monitoring tizimi, NMS

**MIB** - Management Information Base, ma'lumotlar bazasi

**NMS** - Network Management Station, monitoring server

**OID** - Object Identifier, ierarxik identifikator

**PDU** - Protocol Data Unit, SNMP xabar struktura birligi

**Polling** - Manager tomonidan muntazam so'rov yuborish

**RMON** - Remote Monitoring, tarmoqni masofadan monitoring qilish

**SMI** - Structure of Management Information, ma'lumot strukturasi

**Trap** - Agent tomonidan avtomatik yuborilgan xabar

**USM** - User-Based Security Model, SNMPv3 xavfsizlik modeli

**VACM** - View-Based Access Control Model, kirish huquqlarini boshqarish

---

**Dars ishlanmani tayyorlovchi:** [Kompyuter tarmoqlari kafedrasi]

**Sana:** 2024-2025 o'quv yili

**Versiya:** 1.0

---

## Adabiyotlar

1. Douglas R. Mauro, Kevin J. Schmidt. "Essential SNMP, Second Edition". O'Reilly Media, 2005.
2. William Stallings. "SNMP, SNMPv2, SNMPv3, and RMON 1 and 2, Third Edition". Addison-Wesley, 1999.
3. RFC 3416 - "Version 2 of the Protocol Operations for the Simple Network Management Protocol (SNMP)"
4. RFC 3584 - "Coexistence between Version 1, Version 2, and Version 3 of the Internet-standard Network Management Framework"
5. Clemm, A. "Network Management Fundamentals". Cisco Press, 2006.
6. Net-SNMP Documentation - http://www.net-snmp.org/docs/
7. Cisco SNMP Configuration Guide - https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/snmp/configuration/
8. IETF Network Management Research Group - https://datatracker.ietf.org/rg/nmrg/about/

---

**© 2024-2025. Barcha huquqlar himoyalangan.**