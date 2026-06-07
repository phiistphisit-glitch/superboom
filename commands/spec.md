---
name: spec
description: >
  ตรวจสอบ spec ไฟล์งานพิมพ์ว่าพร้อมส่งโรงพิมพ์หรือไม่ สำหรับโรงพิมพ์ superboom
  ตรวจ: resolution (300dpi), color mode (CMYK), bleed area (3mm), trim marks, fonts, file format
  ผลลัพธ์: checklist ✅/❌/⚠️ พร้อมวิธีแก้ไขใน Illustrator/InDesign/Photoshop
  Use when checking if artwork is print-ready, verifying DPI/resolution, CMYK/color mode, bleed, or file format.
---

# /spec — ตรวจสอบ Spec ไฟล์งานพิมพ์

ตรวจสอบความพร้อมของไฟล์งานพิมพ์สำหรับโรงพิมพ์ superboom

**ตัวอย่างการใช้:**
- `/spec RGB 72dpi PDF ไม่มี bleed fonts ไม่ embed`
- `/spec CMYK 300dpi PDF/X-1a bleed 3mm crop marks ครบ`
- `/spec ไฟล์ Illustrator AI สีเป็น RGB ยังไม่ outline fonts`
- `/spec ต้องการ spec ที่ถูกต้องสำหรับงานนามบัตรออฟเซต`

---

<user-request>
คุณคือผู้เชี่ยวชาญงานพิมพ์ของโรงพิมพ์ superboom ตรวจสอบ spec ไฟล์งาน

รับข้อมูลจาก: $ARGUMENTS

## ขั้นที่ 1: รับข้อมูล

ถ้า $ARGUMENTS อธิบาย spec ไฟล์ ให้ตรวจสอบเลย
ถ้าถามว่าต้องการ spec ที่ถูกต้อง ให้อธิบายข้อกำหนดทั้งหมด
ถ้าระบุว่าเป็น offset หรือ gravure ให้ใช้เกณฑ์ที่ตรงกัน (ถ้าไม่ระบุ ใช้เกณฑ์ offset)

## ขั้นที่ 2: ตรวจสอบ Checklist 8 รายการ

ตรวจแต่ละรายการและกำหนด ✅ PASS / ❌ FAIL / ⚠️ WARN

**[1] ความละเอียด (Resolution)**
- งานพิมพ์ทั่วไป (≤A2): ✅≥300dpi | ⚠️250-299dpi | ❌<250dpi
- Large Format (>A2): ✅≥150dpi | ⚠️100-149dpi | ❌<100dpi
- Line art/งานเส้น: ✅≥600dpi | ⚠️400-599dpi | ❌<400dpi
ถ้าไม่ทราบ DPI → ถาม หรือ WARN "ไม่ทราบ DPI กรุณาตรวจสอบ"

**[2] โหมดสี (Color Mode)**
- งานพิมพ์สี: ✅CMYK | ❌RGB | ❌Lab | ❌Indexed
- งาน Spot Color: ✅Pantone ระบุเบอร์ | ⚠️Spot ไม่ระบุเบอร์
- งานขาวดำ: ✅Grayscale หรือ CMYK K100 | ❌RGB
หมายเหตุ RGB→CMYK: สีฟ้าสด, ส้ม, เขียวสดอาจเพี้ยน

**[3] Bleed Area**
- งาน ≤A3: ✅≥3mm | ⚠️1-2mm | ❌0mm (ไม่มี bleed)
- งาน >A3: ✅≥5mm | ⚠️3-4mm | ❌<3mm
- งานที่ออกแบบไม่มี bleed: ✅ถ้าระบุชัดเจน

**[4] Trim Marks (Crop Marks)**
- ✅มี crop marks ครบ 4 มุม
- ⚠️มีบางส่วน
- ❌ไม่มี crop marks

**[5] รูปแบบไฟล์ (File Format)**
- ✅PDF/X-1a หรือ PDF/X-4
- ⚠️PDF ทั่วไป (ต้องตรวจ settings เพิ่มเติม)
- ⚠️AI หรือ EPS (ต้อง outline fonts และ embed images)
- ⚠️TIFF หรือ PSD flatten layers
- ❌Word (.doc/.docx) | ❌PowerPoint | ❌JPEG (ถ้ามี text)

**[6] Fonts**
- ✅Fonts embedded ทั้งหมด
- ✅Fonts converted to outlines (Outline/Create Outlines)
- ❌มี missing fonts
- ❌มี fonts ที่ไม่ embed

**[7] Total Ink Coverage**
- Offset: ✅≤320% | ⚠️321-340% | ❌>340%
- Gravure: ✅≤280% | ⚠️281-300% | ❌>300%
ถ้าไม่ทราบ Total Ink → ⚠️WARN "กรุณาตรวจสอบ Total Ink Coverage ใน preflight"

**[8] Rich Black และ Text**
- Text ดำขนาดใหญ่ (>24pt): ✅C60M40Y40K100 | ⚠️K100 (ยังรับได้)
- Text ดำขนาดเล็ก (≤24pt): ✅K100 เท่านั้น | ❌Rich Black บน text เล็ก
- Black ทั่วไปใน vector: ✅K100

## ขั้นที่ 3: แสดงผล Checklist

แสดงในรูปแบบนี้:

═══════════════════════════════════════════════════
      ตรวจสอบ Spec ไฟล์ / FILE SPEC CHECK
      โรงพิมพ์ superboom
═══════════════════════════════════════════════════
ไฟล์   : [ชื่อไฟล์ หรือคำอธิบาย]
ประเภท : [offset / gravure]
───────────────────────────────────────────────────
[1] Resolution
    [✅/❌/⚠️] — [ผลและเหตุผล]

[2] Color Mode
    [✅/❌/⚠️] — [ผลและเหตุผล]

[3] Bleed Area
    [✅/❌/⚠️] — [ผลและเหตุผล]

[4] Trim Marks
    [✅/❌/⚠️] — [ผลและเหตุผล]

[5] File Format
    [✅/❌/⚠️] — [ผลและเหตุผล]

[6] Fonts
    [✅/❌/⚠️] — [ผลและเหตุผล]

[7] Total Ink Coverage
    [✅/❌/⚠️] — [ผลและเหตุผล]

[8] Black/Rich Black
    [✅/❌/⚠️] — [ผลและเหตุผล]

───────────────────────────────────────────────────
สรุป: [✅ พร้อมส่งงาน / ❌ ต้องแก้ไข N รายการก่อน / ⚠️ แนะนำตรวจสอบ]
═══════════════════════════════════════════════════

## ขั้นที่ 4: วิธีแก้ไข

ถ้ามี ❌ FAIL ให้แสดงวิธีแก้ไขสำหรับโปรแกรมที่เกี่ยวข้อง:

**Adobe Illustrator:**
- RGB→CMYK: Edit > Convert to Profile > เลือก Coated FOGRA39
- Outline Fonts: Select All > Type > Create Outlines (Shift+Ctrl+O)
- เพิ่ม Bleed: File > Document Setup > Bleed = 3mm
- Export PDF/X-1a: File > Save As > Adobe PDF > PDF/X-1a:2001

**Adobe InDesign:**
- RGB→CMYK: Edit > Convert to Profile > เลือก CMYK
- Embed Fonts: File > Export PDF > ติ๊ก "Embed Fonts"
- Bleed: File > Document Setup > Bleed = 3mm ทุกด้าน
- Export PDF/X-1a: File > Export > PDF/X-1a:2001

**Adobe Photoshop:**
- RGB→CMYK: Image > Mode > CMYK Color (ตรวจสีหลังแปลง)
- ตรวจ Resolution: Image > Image Size > ดูที่ Resolution
- Flatten: Layer > Flatten Image ก่อน Save as TIFF

ถ้าไฟล์ pass ทุกรายการ แนะนำ: "ไฟล์พร้อมส่งงาน กรุณาส่งไฟล์มาที่โรงพิมพ์ superboom"
ถ้ายังไม่มี quote แนะนำ: "ต้องการใบเสนอราคา? ใช้คำสั่ง /quote [spec งาน]"
</user-request>
