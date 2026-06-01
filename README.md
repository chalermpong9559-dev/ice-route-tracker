# 🧊 สุรินทร์น้ำทิพย์ — Ice Route Tracker

เว็บแอปสำหรับบันทึกและจัดการสายการขายน้ำแข็งของโรงน้ำแข็งสุรินทร์น้ำทิพย์  
เป้าหมาย: ให้ใครก็ได้วิ่งสายแทนคนขับเดิมได้ โดยไม่ต้องพึ่งความจำ

**🌐 Live:** https://chalermpong9559-dev.github.io/ice-route-tracker/

---

## ฟีเจอร์หลัก

- 📋 จัดการสายส่ง 26 สาย (เพิ่ม / แก้ไข / ลบ)
- 🏪 บันทึกข้อมูลร้านในแต่ละจุดส่ง (ชื่อร้าน, ราคา, ประเภทน้ำแข็ง, จำนวน)
- 📷 ถ่ายรูปร้านค้า
- 📍 ปักหมุด GPS พิกัดร้าน
- 💰 คำนวณยอดรวมอัตโนมัติ
- 🎁 ติดตามโปรโมชัน (ซื้อ 10 แถม 1)
- 🗺️ แสดงเส้นทางบนแผนที่ (OpenStreetMap + Google Maps นำทาง)
- 📊 สรุปรายงานสาย + Export CSV
- ☰ Sidebar เปิด/ปิดได้ — สลับสายได้รวดเร็ว

---

## ประเภทน้ำแข็ง

| รหัส | ชื่อ |
|------|------|
| `ts` | 🔵 หลอดเล็ก |
| `tl` | 🔷 หลอดใหญ่ |
| `cc` | 🌨️ บดหยาบ |
| `cf` | ❄️ บดละเอียด |

---

## Tech Stack

| ส่วน | เทคโนโลยี |
|------|-----------|
| Frontend | HTML5 + CSS + Vanilla JavaScript (ไฟล์เดียว) |
| Backend / Database | [Supabase](https://supabase.com) (PostgreSQL + Storage) |
| Hosting | GitHub Pages |
| แผนที่ | Leaflet.js (OpenStreetMap) + Google Maps API |

---

## โครงสร้างโปรเจกต์

```
ice-route-tracker/
└── index.html      # ทั้งแอปอยู่ในไฟล์เดียว (HTML + CSS + JS)
```

---

## Supabase Tables

### `routes`
| คอลัมน์ | ชนิด | คำอธิบาย |
|---------|------|----------|
| `id` | int8 | Primary key |
| `name` | text | ชื่อสาย |
| `sort_order` | int4 | ลำดับการแสดงผล |

### `shops`
| คอลัมน์ | ชนิด | คำอธิบาย |
|---------|------|----------|
| `id` | int8 | Primary key |
| `route_name` | text | ชื่อสายที่สังกัด |
| `num` | int4 | ลำดับร้านในสาย |
| `name` | text | ชื่อร้าน |
| `price` | int4 | ราคาต่อถุง (บาท) |
| `ice` | jsonb | จำนวนแต่ละประเภท `{ts,tl,cc,cf}` |
| `has_bonus` | bool | มีโปรแถมไหม |
| `total_qty` | int4 | รวมถุง |
| `total_bonus` | int4 | ถุงแถม |
| `total_money` | int4 | ยอดเงิน |
| `gps` | jsonb | `{lat, lng, acc}` |
| `photo_url` | text | URL รูปใน Storage |
| `note` | text | หมายเหตุ |
| `time` | text | เวลาบันทึก |

---

## การพัฒนาต่อ

- [ ] บันทึกเส้นทางทั้ง 26 สายให้ครบ
- [ ] Template ร้านประจำสาย (โหลดรายชื่อร้านที่วิ่งประจำ)
- [ ] ระบบ Login (Supabase Auth) + Row Level Security
- [ ] บันทึกยอดขายรายวัน / คิดเงินเดือนคนขับ
- [ ] รายงานยอดขายรายเดือน

---

## วิธีรัน Local

เปิดไฟล์ `index.html` ในเบราว์เซอร์ได้เลย ไม่ต้องติดตั้งอะไร  
(ต้องการ internet เพื่อเชื่อม Supabase และโหลดแผนที่)
