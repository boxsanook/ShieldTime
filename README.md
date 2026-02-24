# AppController — Android App

> ควบคุมแอปและ Media บนอุปกรณ์ Android ด้วยกฎเวลา, PIN lock และระบบอัตโนมัติ

---

## ✨ ฟีเจอร์หลัก

### 🕐 กฎเวลา (Rules)
- เพิ่มกฎควบคุมแอปตามวันและช่วงเวลาที่กำหนด
- เลือกได้ว่าจะ **บล็อกการเปิดแอป** หรือ **ปิดเสียง Media**
- กดค้างที่กฎเพื่อแก้ไขหรือลบ

### 🎵 การหยุด Media
- **นับถอยหลัง** — ตั้งเวลาล่วงหน้าก่อนหยุด Media
- **อัตโนมัติ** — กำหนดเวลาตายตัวในแต่ละวัน
- **ห้ามใช้ลำโพง** — บังคับปิดเสียงในช่วงเวลาที่กำหนด
- ไม่ปิดเสียงหากเสียบหูฟังหรือเชื่อมต่อ Bluetooth

### 🔐 ล็อกแอปด้วย PIN
- เลือกแอปที่ต้องกรอก PIN ก่อนเปิดทุกครั้ง
- หน้าจอ PIN แสดงขึ้นทันทีเมื่อเปิดแอปที่ล็อก
- Auth หมดอายุใน 30 วินาที

### 🛡 แอปที่อนุญาตให้ใช้งาน
- กำหนด whitelist แอปที่ใช้งานได้
- แอปนอก whitelist จะถูกบล็อกทั้งหมด
- แอประบบสำคัญ (Launcher, Phone, Settings) ไม่ถูกบล็อกเด็ดขาด

### 📍 ระบบอัตโนมัติตามพิกัด
- ปิดเสียงอัตโนมัติเมื่อเข้าในรัศมีที่กำหนด (เช่น ออฟฟิศ)
- กำหนดพิกัดจากตำแหน่งปัจจุบัน หรือเลือกจากแผนที่
- ปรับรัศมีได้อิสระ

### 🔒 ความปลอดภัย
- ล็อกการแก้ไขด้วย PIN
- Device Admin — ป้องกันการถอนติดตั้งโดยไม่ได้รับอนุญาต
- รายการสายด่วน — เบอร์สำคัญดังได้แม้ปิดเสียง
- ลบข้อมูลทั้งหมด — รีเซ็ตกลับค่าเริ่มต้น

---

## 🔧 Permissions ที่ต้องการ

| Permission | ใช้สำหรับ |
|---|---|
| `ACCESSIBILITY_SERVICE` | ตรวจจับการเปิดแอปและบล็อก |
| `SYSTEM_ALERT_WINDOW` | แสดงหน้าจอ PIN ทับบนแอปอื่น |
| `QUERY_ALL_PACKAGES` | โหลดรายชื่อแอปที่ติดตั้ง |
| `MODIFY_AUDIO_SETTINGS` | ควบคุมเสียง |
| `ACCESS_FINE_LOCATION` | ระบบพิกัดอัตโนมัติ |
| `ACCESS_BACKGROUND_LOCATION` | Geofencing เมื่อแอปอยู่เบื้องหลัง |
| `READ_PHONE_STATE` | ระบบสายด่วน |
| `BIND_DEVICE_ADMIN` | ป้องกันการถอนติดตั้ง |

---

## 🚀 การติดตั้ง

1. เปิดแอปหลังติดตั้ง
2. อนุญาต **แสดงทับแอปอื่น** (Draw over apps) เมื่อระบบขอ
3. ไปที่ **ตั้งค่า → ⚠️ เปิดใช้งาน Accessibility** แล้วเปิด service
4. เปลี่ยน PIN เริ่มต้น `123456` ทันที

> ⚠️ ปิดการประหยัดพลังงาน (Battery Optimization) สำหรับแอปนี้ เพื่อให้ทำงานเบื้องหลังได้ต่อเนื่อง

---

## 🏗 โครงสร้างโปรเจกต์

```
app/src/main/java/com/appcontroller/app/
├── MainActivity.java          # UI หลัก + 5 tabs
├── AppBlockService.java       # Accessibility Service ตรวจจับแอป
├── MediaControlService.java   # ควบคุม Media
├── LockActivity.java          # หน้าจอกรอก PIN
├── RuleEngine.java            # Logic ตัดสินใจบล็อก/ปิดเสียง
├── GlobalState.java           # State กลางของแอป
├── SecurityManager.java       # ตรวจสอบแอประบบสำคัญ
├── PinOverlayManager.java     # PIN overlay บนแอปอื่น
├── HistoryManager.java        # บันทึกประวัติการทำงาน
├── CallManager.java           # ระบบสายด่วน
├── MapPickerActivity.java     # เลือกพิกัดจากแผนที่
└── GeofenceReceiver.java      # รับ event พิกัด
```

---

## 👨‍💻 ผู้พัฒนา

**boxs.me**
📧 support@boxs.me
