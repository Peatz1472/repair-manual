# คู่มืองานซ่อม | Repair Manual

เว็บแอพคู่มือซ่อมเครื่องล้างรถสำหรับช่างและพนักงาน รองรับ 2 แบรนด์: **QW** และ **WAG (Washtec)**

ออกแบบเป็น **Single-file Static App** (`index.html`) ที่ทำงานเต็มรูปแบบในเบราว์เซอร์เพียงไฟล์เดียว ไม่ต้องใช้ backend หรือ build step

---

## ✨ ฟีเจอร์หลัก

### สำหรับผู้ใช้
- **Brand selector** — เลือกระหว่าง QW / WAG พร้อม stats รวม
- **Hierarchical content** — หมวดหมู่ซ้อนได้หลายระดับ ลงไปจนถึง Solution
- **Search** — ค้นหารหัส error / อาการ / ชิ้นส่วน / เครื่องมือ ข้ามแบรนด์ได้
- **Diagrams + Hotspot** — แผนภาพเครื่อง คลิก hotspot ไป Solution ที่เกี่ยวข้อง
- **Spare parts catalog** — รายการอะไหล่พร้อมรูป
- **Bookmarks** — ⭐ ปักหมุด Solution ที่ใช้บ่อย
- **Recently viewed** — เห็นรายการที่เพิ่งดู
- **Step-by-step mode** — Solution มีโหมดเดินทีละขั้น พร้อม progress bar
- **Print-ready** — สั่งพิมพ์ได้สวย (ซ่อนปุ่ม นำ metadata ขึ้นหัวกระดาษ)
- **Floating support** — 💬 ปุ่มลอย โทรหาช่างผู้จัดทำได้ทันที

### Adaptive UI ตามระดับผู้ใช้
- 🌱 **เริ่มต้น / พนักงาน** — ตัวอักษรใหญ่, การ์ดกว้าง, default Step-by-step
- 🔧 **ช่าง** (default) — มุมมองสมดุล
- ⚡ **ผู้เชี่ยวชาญ** — มุมมองกระชับ การ์ดถี่

### Toolbar เหนือรายการ Solution
- กรองตามระดับความยาก: 🟢 ง่าย / 🟡 ปานกลาง / 🔴 ยาก
- เรียงลำดับ: ตามลำดับ / 🔥 ฮิต / ง่าย→ยาก / A→Z
- มุมมอง: ▤ ถี่ / ▥ ปกติ / ▦ กว้าง

### สำหรับ Admin
- 🔒 โหมดแก้ไขเข้าถึงด้วยรหัสผ่าน
- เพิ่ม / แก้ / ลบ Brand, Topic, Solution, Diagram, Spare part
- Import / Export ข้อมูลเป็น JSON
- ระบบแจ้งเตือนเมื่อมีการเปลี่ยนแปลงที่ยังไม่ได้ Publish

---

## 🚀 การใช้งาน

### เปิดดู
เปิดไฟล์ `index.html` ใน browser ได้เลย ไม่ต้องตั้ง server

### Deploy
รองรับ static hosting ทุกชนิด:
- **GitHub Pages** — ตั้งค่า Settings → Pages → Branch: `main` / Folder: `/ (root)`
- **Netlify / Vercel** — drag & drop หรือ connect repo ได้ทันที
- **Cloudflare Pages** — เหมือนกัน
- **Local file** — เปิดไฟล์ตรงๆ ก็ได้

### Tech stack
- HTML5 + CSS3 (Custom properties, Grid, Flexbox)
- Vanilla JavaScript (ไม่มี framework / dependency)
- Google Fonts: IBM Plex Sans Thai + JetBrains Mono
- localStorage สำหรับเก็บข้อมูลและ preferences ฝั่ง client

---

## 🗂 โครงสร้างข้อมูล

ข้อมูลทั้งหมดเก็บเป็น JavaScript object ฝัง inline ใน `index.html` (ภายใต้ `DEFAULT_DATA`) โครงสร้าง:

```
brands[]
 ├── id, name, fullName, color, logo, description
 ├── nodes[]              ← tree ของหมวดหมู่
 │    ├── id, title, description, isTop, taskType
 │    ├── solution { difficulty, estimatedTime, sections[] }
 │    └── children[]      ← recursive
 ├── diagrams[]
 │    └── hotspots[] → link ไป nodeId
 └── spareParts[]
```

ข้อมูลของผู้ใช้ (bookmarks, recent, search history, skill level, density) เก็บใน `localStorage`

---

## 🛠 การพัฒนา

แก้ไขผ่าน `index.html` ไฟล์เดียว แบ่งเป็นส่วนหลัก:
- `<style>` — CSS ทั้งหมดพร้อม design tokens (`:root` variables)
- `<body>` — โครง topbar / main / FAB
- `<script>` — data, state, render functions, navigation, admin

ไม่มี build step — แก้แล้ว refresh ได้เลย

---

## 📝 License

ภายในบริษัท / ใช้งานเอง — ปรับใช้ได้ตามสะดวก
