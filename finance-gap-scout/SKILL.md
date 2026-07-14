---
name: finance-gap-scout
description: ค้นคว้าเชิงลึกด้วย web search จำนวนมาก (15-30 ครั้ง) เพื่อหา gap ในระบบการเงินสายที่ผู้ใช้เลือก (NPL/หนี้เสีย, wealth management, กองทุน/fund, การลงทุน/invest) สำหรับงาน hackathon AI x finance ครอบคลุม gap ทั้ง 2 แบบ คือสิ่งที่ตลาดยังไม่มีเลย และสิ่งที่มีอยู่แล้วแต่ยังพัฒนาต่อได้ (แพงเกินไป ช้าเกินไป ยัง manual ครอบคลุมลูกค้าไม่ครบ) ทุก gap ต้องมีแหล่งอ้างอิง แล้วสรุปเป็นรายงาน gap analysis (Markdown + Word .docx) พร้อมไอเดีย hackathon จัดอันดับตาม impact, demo-ability และศักยภาพลดต้นทุน ใช้ทุกครั้งที่ผู้ใช้พูดว่า "หา gap", "หาไอเดีย hackathon", "ระบบ NPL ขาดอะไร", "ช่องว่างใน robo-advisor", "กองทุนไทยยังไม่มีอะไร", "fintech gap analysis", "hackathon idea AI finance", "wealth tech ยังขาดอะไร" หรือกำลังเตรียมแข่ง hackathon สายการเงิน/การลงทุน แม้ไม่พูดคำว่า gap ตรง ๆ ห้ามใช้กับคำถามเรื่อง AI adoption ของบริษัทการเงินทั่วไป (นั่นคืองานของ skill financial-ai-adoption-report) — skill นี้เจาะเฉพาะการหา gap เพื่อสร้างของใหม่
---

# Finance Gap Scout

ค้นหา gap ในระบบการเงินสายที่ผู้ใช้เลือก เพื่อให้ได้ไอเดีย hackathon ที่อ้างอิงหลักฐานจริง
ไม่ใช่ไอเดียลอย ๆ จากความรู้สึก

**กติกาห้ามละเมิด:**

1. **ต้องถามสายงานก่อนเริ่มทุกครั้ง (ถ้าผู้ใช้ยังไม่ระบุ)** — NPL, Wealth, Fund
   หรือ Invest ห้ามเดาเอง ถ้ามี tool ถามแบบปุ่มตัวเลือก (AskUserQuestion) ให้ใช้
2. **ทุกข้อเท็จจริง ตัวเลข และ gap ที่รายงาน ต้องมีแหล่งอ้างอิง** (ชื่อแหล่ง + URL +
   วันที่เข้าถึง) ข้อมูลที่หาแหล่งยืนยันไม่ได้ให้ระบุชัดว่าเป็นการประมาณการ
   และทุกรายงานต้องมี section "แหล่งอ้างอิง" ท้ายเอกสารเสมอ
3. **Gap ต้องครอบคลุม 2 ประเภทเสมอ** — ห้ามรายงานแค่ white space อย่างเดียว
   - **ประเภท A — white space:** สิ่งที่ตลาดยังไม่มีเลย
   - **ประเภท B — improvement gap:** สิ่งที่มีอยู่แล้วแต่พัฒนาต่อได้ เช่น ทำงานได้แต่
     แพงเกินไป (AI ลดต้นทุนได้), ครอบคลุมแค่ segment บน, UX/ความแม่นยำ/ความเร็ว
     ยังห่างจาก best practice, หรือยังเป็น manual process ทั้งที่ automate ได้

## Workflow

### 1. เก็บโจทย์

ถามผู้ใช้ (ใช้ AskUserQuestion ถ้ามี) ให้ได้ครบ:

1. **สายงาน** — เลือกหนึ่ง: (1) NPL — หนี้เสีย, debt collection, restructuring
   (2) Wealth — wealth management, private banking, robo-advisor
   (3) Fund — กองทุนรวม, asset management, fund operations
   (4) Invest — การลงทุน/เทรด, brokerage, portfolio
2. **โจทย์/theme ของ hackathon** (ถ้ามีประกาศแล้ว)
3. **ตลาดเป้าหมาย** — ไทย, global, หรืออื่น ๆ
4. **เวลาที่มีในการแข่ง และขนาด/skill ของทีม** (มีผลต่อคะแนน demo-ability)

### 2. เตรียมแผนวิจัย

อ่านไฟล์เสริม 2 ตัวก่อนเริ่ม search:

- `references/research-playbook.md` — วิธีวิจัย 5 มุม + rubric ให้คะแนนไอเดีย
- ไฟล์ domain ตามสายที่เลือก (อ่านเฉพาะสายเดียว):
  - NPL → `references/domain-npl.md`
  - Wealth → `references/domain-wealth.md`
  - Fund → `references/domain-fund.md`
  - Invest → `references/domain-invest.md`

### 3. วิจัย (web search 15-30 ครั้ง)

ทำตาม 5 มุมใน playbook โดยใช้ query set ของ domain ที่เลือก:

1. Landscape ผลิตภัณฑ์/ระบบที่มีอยู่จริง
2. Pain point จากรีวิว/ฟอรัม/งานวิจัย
3. Regulation + cost benchmark
4. ของใหม่ที่เพิ่งเกิด (funding news, product launch) — กันการเสนอไอเดียที่มีคนทำแล้ว
5. จุดอ่อนของผลิตภัณฑ์ที่มีอยู่ — รีวิวผู้ใช้จริง, complaint, feature comparison
   ระหว่างเจ้าตลาด (มุมนี้คือแหล่งหลักของ gap ประเภท B)

จดแหล่งอ้างอิงทันทีที่เจอข้อมูลที่จะใช้ อย่ารอถึงตอนเขียนรายงาน

### 4. วิเคราะห์ gap

จัด gap ที่พบเข้า 2 ประเภท (A/B) และ 5 หมวด:

| หมวด | ความหมาย |
|---|---|
| Feature gap | ความสามารถที่ขาดหรือยังทำได้ไม่ดี |
| Segment gap | กลุ่มลูกค้าที่ถูกมองข้าม (เช่น mass affluent, SME) |
| Cost gap | จุดที่ต้นทุนสูงเกินควร — โอกาสใช้ AI ลด |
| Experience gap | UX/ความเร็ว/ความโปร่งใสที่ต่ำกว่าที่ควร |
| Process gap | ขั้นตอน manual ที่ automate ได้ |

ทุก gap ต้องมี: หลักฐานอ้างอิง, เหยื่อของปัญหา (ใครเจ็บ), และเหตุผลว่าทำไม AI
ช่วยได้จริง (ไม่ใช่แปะป้าย AI)

### 5. ให้คะแนนและจัดอันดับไอเดีย

แปลง gap เด่น ๆ เป็นไอเดีย hackathon 5-8 ไอเดีย ให้คะแนนตาม rubric ใน playbook
(impact, demo-ability ภายในเวลาแข่ง, ความชัดของ cost reduction story,
ความเสี่ยง regulation) แล้วเลือก top 3 พร้อมเหตุผล

### 6. เขียนรายงานและส่งมอบ

1. เขียน `gap-analysis.md` ตามโครง: บทสรุปผู้บริหาร → landscape สายงานที่เลือก →
   ตาราง gap (ประเภท/หมวด/หลักฐาน) → ไอเดียจัดอันดับพร้อมคะแนน → top 3 เจาะลึก →
   แหล่งอ้างอิง
2. แปลงเป็น Word ด้วย `python scripts/build_docx.py gap-analysis.md gap-analysis.docx`
   (ต้องมี python-docx — ถ้าไม่มีให้ `pip install python-docx` ก่อน)
3. สรุป top 3 ให้ผู้ใช้ในแชท แล้วชี้ต่อ: เลือกไอเดียแล้วใช้ skill
   `finance-pitch-builder` เพื่อทำ solution concept + pitch ต่อได้เลย

## Output

- `gap-analysis.md` — รายงานเต็ม อ่าน/แก้ง่าย ใช้เป็น input ของ skill ถัดไป
- `gap-analysis.docx` — ฉบับ Word สำหรับส่งกรรมการ/แชร์ทีม
- ทั้งสองไฟล์ต้องมี section แหล่งอ้างอิงท้ายเอกสาร

## ข้อควรระวัง

- อย่าเหมาว่า gap ที่คิดออกเองคือของจริง — ทุก gap ต้องผ่านมุมที่ 4 (เช็คว่ายังไม่มี
  คนทำ หรือมีแต่ยังอ่อน) ก่อนเข้ารายงาน
- ตลาดไทยกับ global ต่างกันมากเรื่อง regulation — ถ้าผู้ใช้เลือกตลาดไทย
  ให้น้ำหนักแหล่งข้อมูลไทย (ธปท., ก.ล.ต., ข่าว fintech ไทย) มากกว่า
- ไอเดียที่ demo ไม่ได้ในเวลาแข่ง ต่อให้ impact สูงก็ห้ามติด top 3 —
  hackathon ตัดสินจากของที่โชว์ได้
