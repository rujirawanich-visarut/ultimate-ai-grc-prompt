# OKF v0.1 Compliance & Permissive Consumption Rules
**Path:** `references/okf_compliance_rules.md`
**Description:** คู่มือข้อบังคับทางวิศวกรรม (Engineering Specifications) สำหรับ Agent ในการอ่านและสร้าง Knowledge Bundle ตามมาตรฐาน Open Knowledge Format (OKF) เวอร์ชัน 0.1 

---

## 1. Permissive Consumption Model (กฎความยืดหยุ่นในการอ่าน)
ระบบนิเวศของ OKF ถูกออกแบบมาให้รองรับการเติบโตและการเปลี่ยนแปลง (Refactoring) ได้ตลอดเวลา ดังนั้น Agent ในฐานะผู้บริโภคข้อมูล (Consumers) **ต้องไม่ (MUST NOT)** ปฏิเสธหรือทำให้ระบบขัดข้อง (Reject/Crash) เมื่อเผชิญกับเงื่อนไขดังต่อไปนี้:
*   ไม่พบฟิลด์ทางเลือก (Optional fields) ใน Frontmatter
*   พบค่า `type` ที่ไม่รู้จัก ให้ถือปฏิบัติต่อไฟล์นั้นเสมือนเป็น Generic Concept
*   พบคีย์ (Keys) ใหม่ใน Frontmatter ที่ระบบไม่รู้จัก
*   พบลิงก์ที่พัง (Broken cross-links) เนื่องจากลิงก์นั้นอาจหมายถึงความรู้ที่ยังไม่ได้ถูกเขียนขึ้นมา (Not-yet-written knowledge)
*   ไม่พบไฟล์ `index.md`

## 2. Concept ID Protocol (การกำหนดรหัสแนวคิด)
ในการอ้างอิงถึง Concept ใดๆ **Concept ID** จะต้องถูกนิยามโดยใช้ "Path ของไฟล์นั้นๆ ที่ถูกตัดนามสกุล `.md` ออกไปแล้ว" 
*   **ตัวอย่าง:** ไฟล์ที่อยู่ตำแหน่ง `tables/users.md` จะต้องมี Concept ID คือ `tables/users`

## 3. Strict Rules for Reserved Files (ข้อบังคับสำหรับไฟล์สงวน)
ไฟล์ `index.md` และ `log.md` ถือเป็นไฟล์สงวนที่ห้ามนำไปใช้เป็นชื่อไฟล์สำหรับ Concept documents โดยมีกฎการสร้างดังนี้:
*   **`index.md` (สำหรับการทำ Progressive Disclosure):** ห้ามมี YAML Frontmatter โดยเด็ดขาด *ยกเว้น* กรณีที่เป็นไฟล์ `index.md` ที่อยู่ระดับนอกสุด (Bundle root) ซึ่งอนุญาตให้ใส่ Frontmatter ได้เพียงแค่ค่า `okf_version: "0.1"` เท่านั้น เพื่อเป็นการประกาศเวอร์ชันของ Bundle
*   **`log.md` (สำหรับบันทึกประวัติ):** ต้องจัดเรียงรายการจาก **"ข้อมูลใหม่สุดไว้บนสุด (newest first)"** และหัวข้อวันที่ (Date headings) ต้องใช้รูปแบบมาตรฐาน ISO 8601 คือ `YYYY-MM-DD` อย่างเคร่งครัด

## 4. Conventional Headings (มาตรฐานของหัวข้อเนื้อหา)
แม้ Body ของ OKF จะเป็น Markdown อิสระ แต่หากเข้าข่ายเงื่อนไขต่อไปนี้ Agent ควร (SHOULD) ใช้หัวข้อมาตรฐานเพื่อให้โครงสร้างเรขาคณิตเป็นระเบียบ:
*   `# Schema`: ใช้สำหรับอธิบายโครงสร้าง Column หรือ Field ของ Asset
*   `# Examples`: ใช้สำหรับแสดงตัวอย่างการใช้งานที่เป็นรูปธรรม โดยมักอยู่ในรูปแบบ Fenced code blocks
*   `# Citations`: ใช้สำหรับรวบรวมแหล่งอ้างอิงภายนอกที่สนับสนุนข้อกล่าวอ้างในเนื้อหา
```