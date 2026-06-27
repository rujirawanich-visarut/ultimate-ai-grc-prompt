name: okf-knowledge-extraction
description: |
  สกัดและทำความสะอาดข้อมูลดิบ (Frictionless Subtraction) โดยใช้ The System 2 Lenses 
  เพื่อแปลงเนื้อหาให้เป็นมาตรฐาน Agent-Ready Data (OKF v0.1) 
  Trigger ทักษะนี้เมื่อผู้ใช้ต้องการล้างข้อมูลความลับองค์กร, ทำความสะอาดเอกสาร, หรือขอให้ออกแบบ Knowledge SKU
version: 1.0.0
license: MIT
---

# Skill: OKF Knowledge Bundle Generator (Silver-Layer Data Sanitization Pipeline)

## When to use
- เมื่อได้รับข้อมูลระดับ Bronze Layer (ข้อมูลดิบ, ข่าวลือ, หรือเอกสารภายในที่มี PII)
- เมื่อต้องการล้างข้อมูลระบุตัวตนและยกระดับความรู้เป็น Agent-Ready Data

## When NOT to use
- เมื่อข้อมูลอยู่ในฟอร์แมต OKF v0.1 อยู่แล้ว
- เมื่อผู้ใช้ต้องการให้ดำเนินการทางกายภาพ เช่น ส่งอีเมล หรือแก้ไขโค้ดโปรแกรม

## Workflow (กระบวนการทำงาน)
1. **Apply The System 2 Lenses:** กรองข้อมูลผ่าน 3 เลนส์อย่างเคร่งครัด:
   - *Rational-Scientific Lens:* สกัดเฉพาะ First Principles กฎฟิสิกส์ หรือข้อจำกัดทางวิศวกรรม
   - *System-Causal Lens:* เปิดเผยความสัมพันธ์แฝง (Hidden Coupling) ตัวแปรสำคัญ และ Data Flows
   - *Human-Contextual Lens:* รีเฟรมผ่านความต้องการของผู้ใช้งาน ใช้คำว่า "บทบาท (Role)" แทนชื่อคนจริงเสมอ
2. **De-identify (ลบตัวตน):** ถอดชื่อคนจริง ชื่อแบรนด์ รหัสผ่าน หรือ IP Address ออกให้หมด
3. **Abstract (ยกระดับสู่สัจธรรม):** แปลงเรื่องราวดราม่าองค์กรให้กลายเป็น "รูปแบบเชิงสถาปัตยกรรมทั่วไป (Generic Architectural Patterns)"

## Output format (มาตรฐาน OKF v0.1)
ผลลัพธ์จะต้องเป็นไฟล์ Markdown 1 ไฟล์ที่มีโครงสร้างดังนี้เท่านั้น:

**SECTION A: YAML Frontmatter** (ต้องอยู่บนสุด ปิดด้วย `---`)
- `type`: [ประเภทความรู้ เช่น Architecture Pattern, Playbook]
- `title`: [ชื่อหัวข้อที่ไร้การระบุองค์กร]
- `description`: [สรุปความแบบ Progressive Disclosure ด้วยความยาว "1 ประโยค" เท่านั้น]
- `tags`: [YAML array เช่น architecture, pattern]
- `timestamp`: [รูปแบบ ISO 8601 DateTime เช่น 2026-06-27T14:00:00Z]

**SECTION B: Structural Markdown Body**
- ใช้ Headings (`#`, `##`), Tables, Bulleted Lists และ Fenced Code Blocks
- ปิดท้ายด้วยหัวข้อ `# Citations` โดยอ้างอิงเป็นนามแฝงเชิงแนวคิด เช่น " Internal System Post-Mortem (Anonymized)"

## Anti-patterns to avoid
- ห้ามเขียนเป็นเรียงความพรรณนายาวๆ โดยเด็ดขาด
- ห้ามใส่ข้อมูลที่สร้างขึ้นมาเอง (Hallucinate) เพื่อเติมเต็มสิ่งที่หายไป
```