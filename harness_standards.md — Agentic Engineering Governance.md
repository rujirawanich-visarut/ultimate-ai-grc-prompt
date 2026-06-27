**harness\_standards.md — Agentic Engineering Governance**  
**1\. THE FUNDAMENTAL PHILOSOPHY: AGENT \= MODEL \+ HARNESS**

* **The 90/10 Rule:** ในระบบ Agentic ระดับ Production ความเชื่อถือได้ 90% มาจาก "Harness" (ระบบควบคุมและโครงสร้างพื้นฐาน) และเพียง 10% มาจาก "Model" (เครื่องยนต์ประมวลผลภาษา).  
* **Functionality:** Harness คือสิ่งที่เปลี่ยน Stateless Language Model ให้กลายเป็น Functional Agent ที่สามารถรักษาสถานะ (State), ประมวลผลเครื่องมือ (Tools), และรับข้อมูลป้อนกลับ (Feedback) ได้อย่างมีระบบ.  
* **Core Properties:** มาตรฐาน Harness ต้องมุ่งเน้น 3 คุณสมบัติหลักคือ:  
  * **Executable:** เปลี่ยนเจตนา (Intent) ให้เป็นการทำงานที่ตรวจสอบได้จริง.  
  * **Inspectable:** เปิดเผยกระบวนการคิดและขั้นตอนการทำงาน (Traces) เพื่อการวินิจฉัย.  
  * **Stateful:** รักษาสถานะความคืบหน้าของงานและบริบทข้ามขั้นตอนได้อย่างแม่นยำ.

**2\. COMPONENT ARCHITECTURE CANVAS**  
ทุกการออกแบบ Harness ต้องระบุองค์ประกอบบริบท (Context Components) ตามโครงสร้างดังนี้:

* **Instruction Context:** กำหนดบทบาทและขอบเขต (Do/Do Not).  
* **Knowledge Context:** แหล่งข้อมูลอ้างอิงที่ผ่านการอนุมัติ (Approved Evidence).  
* **Tool Context:** ชุดฟังก์ชันและ API ที่ได้รับอนุญาต (Permissions & Schemas).  
* **Memory Context:** ระบบจัดการความจำ (Working, Semantic, Experiential, Long-term).  
* **State Context:** สถานะปัจจุบันของ Workflow และสภาพแวดล้อม.  
* **Constraint Context:** กฎเหล็กที่ห้ามละเมิด (Hard Constraints) และจุดตัดสินใจที่ต้องใช้มนุษย์ (HITL).  
* **Verification Context:** เกณฑ์การวัดผลและกลไกการตรวจสอบ (CoVe, Static Analysis, Unit Tests).

**3\. OPERATIONAL PROTOCOLS**  
**3.1 The PEV Control Loop (Plan-Execute-Verify)**  
Harness ต้องบังคับใช้ลูปการทำงานแบบปิด เพื่อควบคุมความถูกต้องของสถานะระบบ:

1. **Plan:** สร้าง "สัญญา" (Contract) ของการเปลี่ยนแปลงที่ตั้งใจและเกณฑ์การตรวจสอบ.  
2. **Execute:** ดำเนินการภายในสภาพแวดล้อมที่แยกส่วน (Sandbox) และจำกัดสิทธิ์ (Permissioned).  
3. **Verify:** ตรวจสอบผลลัพธ์ผ่าน Deterministic Sensors (Linters, Tests, Static Analyzers) ก่อนจะยอมรับการเปลี่ยนสถานะ.

**3.2 4-Step Context Deployment Pipeline**  
ทุก Skill ต้องรันผ่านท่อส่งข้อมูล 4 ขั้นตอนเพื่อรักษาเสถียรภาพของการใช้เหตุผล:

1. **Epistemic Isolation:** สกัดแก่นคงที่ (Invariant Core) และกรอง Noise ออก.  
2. **Hierarchical Decomposition:** แตกงานเป็น Atomic Nodes ที่เป็นอิสระต่อกัน.  
3. **Operational Patches:** ติดติดตั้งแท็ก `[DIRECTION]` และ `[CONSTRAINT]` พร้อมระบบ Uncertainty Surfacing.  
4. **Context Checkpoints:** ทำ Chain of Verification (CoVe) เพื่อตรวจสอบตัวเองก่อนส่งคำตอบ.

**4\. THE 7-PILLAR SECURITY HARNESS**  
Harness ต้องทำหน้าที่เป็น "Safety Governor" ตามเสาหลักความมั่นคงปลอดภัยดังนี้:

* **Pillar 1: Infrastructure** – แยกส่วนการทำงานด้วย Ephemeral Sandboxing (เช่น gVisor).  
* **Pillar 2: Data** – ควบคุมสิทธิ์การเข้าถึงแบบ Least Privilege และแยกส่วนหน่วยความจำข้าม Tenant.  
* **Pillar 3: Model** – ปกป้องระบบคำสั่ง (System Instructions) เสมือนเป็น Source Code ที่ต้องมีการรับรอง.  
* **Pillar 4: Runtime** – ติดตั้ง Hooks ที่จุดตัดสินใจสำคัญ และใช้ Agent Gateway ควบคุมการประสานงาน.  
* **Pillar 5: IAM** – กำหนดตัวตนที่เป็นเอกลักษณ์ (Unique Identity) และใช้ Just-In-Time (JIT) token downscoping.  
* **Pillar 6: Observability** – สร้าง "Vibe Trajectory" เพื่อตรวจสอบย้อนกลับกระบวนการคิดของ Agent.  
* **Pillar 7: Governance** – สร้าง Immutable Audit Trail และเปลี่ยนปุ่ม "Approval" เป็น "Logic Review".

**5\. SPEC & EVALUATION STANDARDS (SDD & EDD)**

* **Hybrid SDD Structure:** ทุก Spec ต้องประกอบด้วย 5 ชั้นข้อมูล: Markdown (Meaning), Gherkin (Execution), YAML (Rules), JSON (Cases), และ Python (Truth).  
* **Evaluation-Driven Development (EDD):** ต้องเขียน JSON Eval Cases (Input/Expected Tools/Expected Output) อย่างน้อย 3 เคสก่อนเริ่มร่าง Skill เสมอ เพื่อลดความคลุมเครือ.  
* **Uncertainty Surfacing:** Harness ต้องบังคับให้ Agent หยุดทำงานและส่งสัญญาณ `[UNCERTAINTY ALERT]` ทันทีหากข้อมูลไม่เพียงพอ แทนการเดาสุ่ม (No Guessing).

**6\. MULTI-AGENT ORCHESTRATION STANDARDS**

* **Role Specialization:** แบ่งความรับผิดชอบให้ชัดเจน (Architect, Programmer, Tester, Reviewer, Executor) เพื่อเพิ่มความสามารถในการตรวจสอบ.  
* **Shared Substrate:** ใช้ Repository และ Shared State เป็นศูนย์กลางการทำงาน มากกว่าการส่งต่อข้อมูลผ่านแชทเพียงอย่างเดียว.  
* **State Convergence:** การยุติการทำงาน (Termination) ต้องพึ่งพา "Objective Behavioral Signals" (เช่น ผลการทดสอบผ่าน 100%) ไม่ใช่แค่ "Model Confidence".

