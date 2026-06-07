# superboom — Thai Printing Shop Plugin for Claude Code

Claude Code plugin สำหรับโรงพิมพ์ไทย (superboom) คำนวณราคา วิเคราะห์ต้นทุน ตรวจ spec ไฟล์ และเปรียบเทียบตัวเลือกงานพิมพ์ ทั้งหมดในภาษาไทย หน่วย THB

> A Claude Code plugin for Thai printing shops. Provides instant printing quotations, cost analysis, prepress file spec checking, and option comparisons — all in Thai (฿ THB).

---

## ติดตั้ง / Install

เพิ่มใน `.claude/settings.json` ของโปรเจคที่ต้องการใช้:

```json
{
  "enabledPlugins": {
    "superboom@phisit": true
  }
}
```

หรือติดตั้งผ่าน Claude Code marketplace:
```
claude plugin install superboom@phisit
```

---

## Skills / คำสั่งที่ใช้ได้

### `/quote [spec งาน]` — ใบเสนอราคา

สร้างใบเสนอราคาแบบละเอียดพร้อม VAT

```
/quote นามบัตร Art Card 350gsm 4สี UV หน้าเดียว 1,000 ชิ้น ส่งกทม
/quote โบรชัวร์ A4 สี่พับ Art Card 150gsm 4/4 Laminate Matt 2,500 ชิ้น
/quote ถุงกระดาษ Craft 120gsm 1สี 5,000 ชิ้น
/quote ปฏิทินตั้งโต๊ะ A5 Art Card 300gsm 4สี Saddle Stitch 500 ชิ้น
```

ผลลัพธ์: ใบเสนอราคาพร้อมราคาทุกรายการ, VAT 7%, ราคาต่อชิ้น

---

### `/cost [spec งาน]` — วิเคราะห์ต้นทุน

แสดง cost breakdown แยก วัตถุดิบ / แรงงาน / Setup / Overhead

```
/cost นามบัตร Art Card 350gsm 4สี 1,000 ชิ้น
/cost โบรชัวร์ A5 offset 4/4 Laminate 2,500 ชิ้น
```

ผลลัพธ์: ตาราง breakdown + Gross Margin % + Break-even quantity + คำแนะนำ

---

### `/spec [คำอธิบาย]` — ตรวจ Spec ไฟล์

ตรวจว่าไฟล์งานพิมพ์พร้อมส่งโรงพิมพ์หรือไม่

```
/spec RGB 72dpi PDF ไม่มี bleed fonts ไม่ embed
/spec CMYK 300dpi PDF/X-1a bleed 3mm crop marks ครบ
/spec ไฟล์ Illustrator AI สีเป็น RGB ยังไม่ outline fonts
/spec ต้องการ spec ที่ถูกต้องสำหรับงานนามบัตรออฟเซต
```

ผลลัพธ์: Checklist ✅/❌/⚠️ สำหรับ resolution, color mode, bleed, fonts พร้อมวิธีแก้ไขใน AI/InDesign/Photoshop

---

### `/compare [ตัวเลือก]` — เปรียบเทียบ

เปรียบเทียบตัวเลือกงานพิมพ์

```
/compare offset vs gravure ฉลากสินค้า 4สี 20,000 ชิ้น
/compare 500 vs 1000 vs 5000 ชิ้น นามบัตร Art Card 350gsm 4สี
/compare art card 300gsm vs bond 120gsm โบรชัวร์ A5 4สี 1,000 ชิ้น
/compare UV coating vs laminate matt นามบัตร 1,000 ชิ้น
```

ผลลัพธ์: ตารางเปรียบเทียบราคา + Breakeven (Offset vs Gravure) + คำแนะนำ

---

## ปัจจัยราคา / Pricing Factors

| ปัจจัย | รายละเอียด |
|--------|-----------|
| กระดาษ | Art Card (115–350gsm), Bond (70–120gsm), Craft (80–150gsm) |
| สีพิมพ์ | 1 สี / 2 สี / 4 สี CMYK |
| Finishing | UV, Laminate Matt/Gloss, Die-cut, Emboss, Foil Stamp, Saddle Stitch, Perfect Binding |
| ค่าแม่พิมพ์ | Plate (offset) / Cylinder (gravure) + Prepress |
| Tiered pricing | จำนวนมาก = ราคา/ชิ้นถูกลง (5 tiers) |
| ค่าขนส่ง | รับเอง / ส่งกทม / ต่างจังหวัด / ด่วน |
| VAT | 7% (แสดงทั้งก่อนและหลัง VAT) |

---

## ประเภทงาน / Supported Print Types

| ประเภท | เหมาะสำหรับ | จำนวนขั้นต่ำ |
|--------|------------|------------|
| Offset Printing | นามบัตร, โบรชัวร์, แผ่นพับ, ปฏิทิน, หนังสือ | 500 ชิ้น |
| Gravure Printing | บรรจุภัณฑ์ฟิล์ม, ฉลากสินค้าปริมาณสูง | 10,000 ชิ้น |

---

## หมายเหตุ / Notes

- ราคาในระบบเป็น **ราคาประมาณการ** — ควรปรับตารางราคาใน `agents/print-specialist.md` ให้ตรงกับต้นทุนจริง
- สกุลเงิน: บาทไทย (฿ THB)
- ภาษา: ตอบภาษาไทยโดยค่าเริ่มต้น (English ถ้าถามเป็น English)

---

## License

MIT

---

*โรงพิมพ์ superboom — คำนวณแม่น ราคาชัด งานพิมพ์คุณภาพ*
