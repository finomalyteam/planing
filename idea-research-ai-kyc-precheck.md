# Idea Deep Research: AI Pre-Check เอกสาร KYC / Source of Wealth ก่อน Sales ส่ง Backoffice (เปิดพอร์ตหุ้น)

- **ไอเดีย:** ระบบ AI ตรวจความครบถ้วน-ถูกต้อง-สมเหตุสมผลของชุดเอกสาร KYC และ Source of Wealth (SoW) ที่ฝั่ง Sales **ก่อน** ส่งต่อให้ Backoffice เพื่อลดเวลาเปิดพอร์ตและลดการตีกลับ
- **บริบท:** hackathon AI x finance (ทีม 5 คน, ~1 สัปดาห์) · **ตลาดเป้าหมาย:** ไทย
- **วันที่ค้นคว้า:** 14 กรกฎาคม 2569 (2026-07-14) — วันที่เข้าถึงแหล่งอ้างอิงทุกรายการ
- **Hypothesis ที่ทดสอบ:** เอกสาร KYC/SoW ที่ผิด/ไม่ครบจากฝั่ง Sales เป็นคอขวดที่ทำให้เปิดพอร์ตช้า และ AI pre-check ลดเวลา/ปัญหาได้อย่างมีนัย

---

## บทสรุปผู้บริหาร

> **Verdict: CONDITIONAL GO — 20/30 คะแนน**
> Pain จริงและวัดเป็นตัวเลขได้ (งานเข้า QA ผ่านรอบแรกเพียง 20-60%, ตรวจ KYC manual ใช้ 30-60 นาที/ราย, 70% ของสถาบันการเงินเสียลูกค้าเพราะ onboarding ช้า) และ why-now แรงมาก: ก.ล.ต. เพิ่งยกระดับแนวปฏิบัติ KYC/CDD (มิ.ย. 2569) บังคับเก็บ "ความสมเหตุสมผลของอาชีพ ฐานะการเงิน แหล่งที่มาของรายได้และเงินลงทุน" + มีเคสกล่าวโทษอาญา บล. จริง จุดอ่อนคือ **ตลาดไทยแคบ** (บล. สมาชิก ตลท. 36 แห่ง) ทำให้มูลค่าตลาดเป็นข้อจำกัดหลัก — เหมาะเป็น B2B product ที่ต้องออกแบบให้ขยายข้าม vertical (บลจ./ประกัน/ธนาคาร) ตั้งแต่แรก

**Hypothesis: ยืนยัน** — หลักฐาน global ชี้ว่างาน KYC ผ่านการตรวจรอบแรกแค่ 20-60% (ที่เหลือต้อง follow-up หลายรอบ) และ 88% ของทีม compliance บอกว่า "การตามแก้เอกสาร" คือ pain อันดับหนึ่ง ฝั่งไทยมีหลักฐาน severity ระดับ regulator (เคสฟินันเซีย)

### ตัวเลขผลกระทบที่ผู้ใช้ถามหา (impact headline)

| ตัวชี้วัด | ก่อน (manual) | หลัง (AI/IDP-assisted) | แหล่ง | Confidence |
|---|---|---|---|---|
| เวลาตรวจเอกสาร KYC ต่อลูกค้า | 30-60 นาที | 5-10 นาที (**ลด 70-80%**) | [Docsumo IDP Report](https://www.docsumo.com/blogs/intelligent-document-processing/intelligent-document-processing-market-report-2025) | กลาง |
| อัตราความผิดพลาดในการตรวจเอกสาร | 15-20% | 2-5% | [Docsumo](https://www.docsumo.com/blogs/intelligent-document-processing/intelligent-document-processing-market-report-2025) | กลาง |
| ต้นทุนประมวลผลต่อเอกสาร | $6-25 | $0.50-2.00 (**ลด 70-90%**) | [Docsumo](https://www.docsumo.com/blogs/intelligent-document-processing/intelligent-document-processing-market-report-2025) | กลาง |
| เวลาประมวลผลเอกสารของลูกค้า Fenergo | — | **ลดลง 50%** | [Fenergo](https://www.fenergo.com/) | กลาง |
| งาน KYC ที่ผ่านรอบแรก (first-pass) | **แค่ 20-60%** — ที่เหลือตีกลับ/ตามเอกสารเพิ่มหลายรอบ | เป้าของ pre-check คือดันตัวเลขนี้ขึ้น | [Fintech Global 2026](https://fintech.global/2026/04/27/how-firms-are-failing-at-periodic-kyc-reviews/) | กลาง |

---

## Module 1 — Problem & Demand

### 1.1 ขนาดและความถี่ของปัญหา (ใครเจ็บ เจ็บแค่ไหน)

- **First-pass rate ต่ำ:** งานตรวจ KYC ผ่านรอบแรกเพียง **20-60%** — ที่เหลือต้อง follow-up หลาย touchpoint กว่าจะปิดได้ — [Fintech Global](https://fintech.global/2026/04/27/how-firms-are-failing-at-periodic-kyc-reviews/) (Confidence: กลาง)
- **การตามแก้/ตามเอกสารคือ pain อันดับ 1:** 88% ของผู้ตอบแบบสำรวจฝั่ง compliance ชี้ว่า remediation & follow-up คือจุดเจ็บที่สุด และ 88% เก็บข้อมูล KYC กระจายใน ≥2 ระบบ (46% กระจายใน 5-9 ระบบ) — [Fintech Global](https://fintech.global/2026/04/27/how-firms-are-failing-at-periodic-kyc-reviews/) (Confidence: กลาง)
- **เวลาตรวจ:** เช็ค KYC มาตรฐานเฉลี่ย 1-2 ชม. และ **1 ใน 5 เคสใช้เวลาเกิน 24 ชม.** — [ID-Pal](https://www.id-pal.com/blog/kyc-delays-slowing-customer-onboarding/) (Confidence: กลาง)
- **SoW คือส่วนที่ manual สุด:** การตรวจ Source of Wealth แบบ manual "ใช้เวลาหลายวันและหลายรอบรีวิว" ขณะที่แบบอัตโนมัติทำได้ในไม่ถึงชั่วโมงสำหรับลูกค้าจำนวนมาก — [smartKYC](https://smartkyc.com/source-of-wealth-verification-guide/) (Confidence: กลาง)

### 1.2 Cost of inaction

- **เสียลูกค้า:** 70% ของสถาบันการเงินเคยเสีย prospect เพราะ onboarding ช้า/ซับซ้อน (เพิ่มจาก 48% ในปี 2023) — [Fenergo อ้างใน Fintech Global](https://fintech.global/2025/10/08/70-of-banks-lose-clients-due-to-slow-onboarding/) (Confidence: กลาง)
- **ผู้สมัครถอดใจ:** 68% ของผู้บริโภคเคยทิ้งใบสมัครบริการการเงินกลางคัน; KYC ที่ถูกทิ้งกลางทางคิดเป็นมูลค่า **$3.3 พันล้าน/ปี** ของภาคธนาคารทั่วโลก — [Jumio](https://www.jumio.com/how-to-reduce-customer-abandonment/) (Confidence: กลาง)
- **ความเสี่ยง regulator (หลักฐานไทยตรง ๆ):** ก.ล.ต. **กล่าวโทษ บล.ฟินันเซีย ต่อ บก.ปอศ.** (โทษอาญาตามมาตรา 113/282 พ.ร.บ.หลักทรัพย์ฯ) จากระบบ KYC/CDD ไม่รัดกุม — จุดที่พลาดตรงกับไอเดียนี้พอดี: ไม่ระบุ UBO ครบ, ไม่ตรวจเพิ่มเมื่อขอวงเงินสูง, ไม่ทำ Enhanced CDD เมื่อธุรกรรม**ไม่สอดคล้องกับศักยภาพการเงิน** (คือ SoW reasonableness) — [The Standard](https://thestandard.co/sec-charges-finansia-kyc-lax/) (Confidence: กลาง)
- ต้นทุนแรงงานตรวจ manual: นักวิเคราะห์ทำได้ 15-25 เคส/วัน ต้นทุนรวมต่อเช็ค **$7.95-19.00** (รวม QA, ตามเอกสาร, คีย์ข้อมูล) — [CheckFile.ai](https://www.checkfile.ai/en-US/blog/kyc-solution-pricing-cost-breakdown-roi-tco) (Confidence: กลาง)

### 1.3 บริบทไทย: ช่องว่างอยู่ที่เคสที่ NDID ช่วยไม่ได้

เส้นทางเปิดบัญชีออนไลน์รายย่อยผ่าน NDID เร็วแล้ว (บล.บัวหลวงโฆษณา "อนุมัติใน 15 นาที" — [Bualuang](https://www.bualuang.co.th/article/openaccount)) แต่ NDID แก้เฉพาะ **identity verification** — ไม่ได้แก้การตรวจ **ชุดเอกสารประกอบ**: หลักฐานรายได้/แหล่งที่มาเงินลงทุน, งบการเงิน, เอกสารนิติบุคคล, เคสวงเงินสูง/HNW ที่ต้อง Enhanced CDD ซึ่งยังเป็น manual ระหว่าง Sales ↔ Backoffice — กระทู้ Pantip ยืนยันว่าบางเคสรอ "นานสุดหลายวันถึงสัปดาห์" ([Pantip](https://pantip.com/topic/38131509)) (Confidence: กลาง — หลักฐานพฤติกรรม tier 3)

### 1.4 ปัจจัยที่ทำให้ปัญหาคงอยู่

(1) มาตรฐานการตัดสิน "เอกสารใช้ได้" ไม่ตรงกันระหว่าง Sales, Backoffice และ compliance — ไฟล์ที่คนหนึ่งผ่าน อีกคนตีกลับ ([Fintech Global](https://fintech.global/2026/06/03/how-to-fix-broken-kyc-records-before-regulators-do/)) (2) Sales มี incentive ปิดการขาย ไม่ใช่ความสมบูรณ์ของเอกสาร (3) checklist กระดาษ/Excel ไม่บังคับความสอดคล้องข้ามเอกสาร (เช่น อาชีพใน ID ไม่ match รายได้ใน statement) (Confidence: กลาง — ข้อ 2-3 เป็นการวิเคราะห์จากโครงสร้าง incentive)

---

## Module 2 — Market Size & Timing

### 2.1 ฐานตลาดไทย (bottom-up)

- ผู้ลงทุนในตลาดหุ้นไทยรวม **4,487,056 ราย** (พ.ค. 2569) เปิดใหม่ **440,071 ราย ใน 5 เดือนแรกปี 2569** (~88,000 ราย/เดือน ≈ run-rate ~1 ล้านราย/ปี) — [Hoonsmart](https://hoonsmart.com/archives/426621) (Confidence: กลาง)
- บริษัทสมาชิก ตลท. (โบรกเกอร์) **36 แห่ง** — [SET](https://www.set.or.th/th/market/information/member-list/main) (Confidence: สูง)

### 2.2 TAM / SAM / SOM (ประมาณการ — แสดงวิธีคิด)

> ตัวเลขส่วนนี้เป็น**การประมาณการของผู้วิเคราะห์** — Confidence: ต่ำ

- **TAM (KYC ops ของตลาดทุนไทย):** ~1M บัญชีใหม่/ปี × เอกสาร 3-5 ชิ้น/เคส × ต้นทุน manual $6-25/เอกสาร → มูลค่างานตรวจเอกสารที่ automate ได้ราว **650-4,300 ล้านบาทของต้นทุนแฝง/ปี** (เฉพาะโบรกเกอร์; ยังไม่รวม บลจ./ประกัน/ธนาคารที่มีโจทย์เดียวกัน)
- **SAM (รายได้ SaaS ที่เก็บได้จริงจาก บล.):** 36 บล. × สมมติ subscription 0.5-3 ล้านบาท/ปี/ราย (อิงว่า KYC review ระดับสถาบัน global อยู่ที่ $2,001-2,500/เคส corporate — [Statista](https://www.statista.com/statistics/1614858/kyc-review-cost-corporate-banking/)) → **18-108 ล้านบาท/ปี**
- **SOM (3 ปี):** เจาะ บล. 5-8 แห่ง → **5-25 ล้านบาท/ปี** — ตลาดแคบคือข้อจำกัดหลักของไอเดียนี้ ต้องขยายไป บลจ./ประกัน/สินเชื่อเพื่อให้ตลาดใหญ่พอ

### 2.3 Why now — catalyst (จุดแข็งที่สุดของไอเดีย)

1. **ก.ล.ต. ยกระดับแนวปฏิบัติ KYC/CDD (ข่าว 30 มิ.ย. 2569)** — บังคับเก็บและประเมิน "ความสมเหตุสมผลของอาชีพ ฐานะการเงิน **แหล่งที่มาของรายได้และเงินลงทุน**" + เจาะ UBO กันบัญชีม้า → ภาระตรวจเอกสารต่อเคส**เพิ่มขึ้นทันที**ทั้งอุตสาหกรรม — [Hoonsmart](https://hoonsmart.com/archives/425894) (Confidence: กลาง)
2. **เคสฟินันเซียเพิ่งเกิด (พฤติการณ์ปี 2567-2568)** — ทั้งอุตสาหกรรมกำลังกลัวเรื่องนี้พอดี งบ compliance ถูกปลดล็อก — [The Standard](https://thestandard.co/sec-charges-finansia-kyc-lax/) (Confidence: กลาง)
3. **เทคโนโลยีเพิ่งพร้อม:** multimodal LLM + Thai OCR (iApp/AppMan อ่านเอกสารไทยได้ 98% accuracy — [AppMan](https://www.appman.co.th/en/appman-ocr-plus-en/)) ทำ cross-document reasoning ได้ ซึ่ง 2-3 ปีก่อนทำไม่ได้
4. **ภัยเอกสารปลอมจาก GenAI โตเร็ว** — เอกสารปลอมทำได้ใน "$15 และครึ่งชั่วโมง", 67% ของ synthetic identity fraud ใช้เอกสารปลอมเจาะด่าน KYC — คนตรวจด้วยตาจับไม่ได้แล้ว ต้องใช้ AI สู้ AI — [Middesk](https://www.middesk.com/blog/how-fraudsters-are-using-ai-to-bypass-traditional-kyb-checks), [Hesper AI](https://gethesperai.com/blog/kyc-document-fraud-fintechs/) (Confidence: กลาง)

---

## Module 3 — Competition

### 3.1 ผู้เล่นไทย

| ผู้เล่น | ทำอะไร | ช่องว่างเทียบไอเดียเรา | แหล่ง |
|---|---|---|---|
| **NDID** | ยืนยันตัวตนดิจิทัลกลางประเทศ ใช้เปิดบัญชีหลักทรัพย์ | identity เท่านั้น — ไม่ตรวจชุดเอกสารประกอบ/SoW | [NDID/บล.กสิกรไทย](https://www.kasikornsecurities.com/th/startinvesting/ndid) |
| **AppMan** (OCR+, eKYC) | OCR เอกสารไทย 98% accuracy, eKYC ประกัน/การเงิน | อ่านเอกสารรายชิ้น (extraction) — ไม่ทำ case-level QC ว่า "ชุดเอกสารครบ สอดคล้อง สมเหตุสมผลตามเกณฑ์ ก.ล.ต./ปปง. ไหม" | [AppMan](https://www.appman.co.th/en/appman-ocr-plus-en/) |
| **iApp Technology** | Thai OCR API (บัตรประชาชน, passport, book bank) | เหมือนกัน — extraction layer ไม่ใช่ decision layer | [iApp](https://iapp.co.th/docs/intro) |
| **e-Open Account (SET)** | ระบบเปิดบัญชีกลางของ ตลท. | workflow ส่งข้อมูล — การตรวจยังเป็นคนที่ Backoffice ของแต่ละ บล. | [SET](https://www.set.or.th/th/settrade/services/e-open-account) |

**สรุป:** ชั้น identity และ OCR ในไทย**แข่งดุแล้ว** แต่ชั้น "AI ตรวจความครบถ้วน-สอดคล้อง-สมเหตุสมผลของทั้งเคสก่อนส่ง Backoffice" (pre-submission QC agent) **ยังไม่พบผู้เล่นไทยที่ทำตรง ๆ** (Confidence: กลาง — อาจมี in-house system ของ บล. ใหญ่ที่ไม่เปิดเผย)

### 3.2 ผู้เล่นต่างประเทศ

- **Fenergo** — CLM/KYC ครบวงจรสำหรับสถาบัน อ้างลูกค้า "ลดเวลาประมวลเอกสาร 50%, auto-resolve screening hits 95%" — [Fenergo](https://www.fenergo.com/) (Confidence: กลาง)
- **smartKYC** — AI เจาะ Source of Wealth โดยเฉพาะ (EDD สำหรับ private banking) — [smartKYC](https://smartkyc.com/solutions/source-of-wealth/) (Confidence: กลาง)
- **Inscribe / Klippa / Hesper** — AI document fraud detection (จับเอกสารปลอมระดับ pixel) — [Inscribe](https://www.inscribe.ai/) (Confidence: กลาง)
- ราคา KYC automation ตลาด: **$1-5 ต่อ verification** ตาม volume/ความซับซ้อน — [ComplyCube](https://www.complycube.com/en/how-much-does-kyc-cost/) (Confidence: กลาง)
- เจ้าพวกนี้ยังไม่ localize เกณฑ์ ก.ล.ต./ปปง. + เอกสารภาษาไทย → ช่องว่างของเรา

### 3.3 Substitutes (คู่แข่งตัวจริง)

Checklist กระดาษ/Excel ที่ Sales ใช้เช็คเอง, การ train Sales ซ้ำ ๆ, จ้างคน Backoffice เพิ่ม, และ "ปล่อยให้ตีกลับเป็นเรื่องปกติ" — ทั้งหมด scale ไม่ได้และไม่ทิ้ง audit trail (Confidence: กลาง — จากโครงสร้างกระบวนการที่พบใน 1.4)

### 3.4 Failure case / ความเสี่ยงจากตลาด

ไม่พบ startup ไทยที่ทำแล้วเจ๊งตรง segment นี้ (ตลาดยังใหม่) — บทเรียนที่ใกล้เคียง: เครื่องมือ IDV มาตรฐาน "ตรวจ identity แต่ไม่ตรวจความสมบูรณ์ระดับ pixel ของเอกสาร จึงพลาดของปลอมจาก GenAI" ([Hesper AI](https://gethesperai.com/blog/kyc-document-fraud-fintechs/)) — ถ้าเราขาย "AI ผ่านเอกสารให้เร็วขึ้น" โดยไม่มีชั้นตรวจของปลอม จะกลายเป็นช่องโหว่แทนที่จะเป็นตัวช่วย (Confidence: กลาง)

---

## Module 4 — Feasibility

### 4.1 Regulatory

- **จุดแข็ง: เป็นเครื่องมือ internal ops ของ บล.** — ไม่แตะการแนะนำการลงทุน จึง**ไม่ต้องมี license ก.ล.ต.** (ต่างจากไอเดีย robo-advisor) และ ก.ล.ต. มีแนวทางสนับสนุนการใช้เทคโนโลยีใน KYC อยู่แล้ว — [แนวทางปฏิบัติการนำเทคโนโลยีมาใช้ทำความรู้จักลูกค้า, ก.ล.ต.](https://publish.sec.or.th/nrs/8327s.pdf) (Confidence: กลาง)
- ความรับผิดชอบสุดท้ายยังอยู่ที่ บล. (มาตรา 113) — product ต้องวางตัวเป็น **decision support + audit trail** ไม่ใช่ auto-approve; มนุษย์กดผ่านเสมอ
- PDPA เต็มรูปแบบ (เอกสารการเงิน+บัตรประชาชน = ข้อมูลอ่อนไหว) → ต้องรองรับ on-premise/private cloud สำหรับ บล. ใหญ่

### 4.2 เทคโนโลยี

(1) OCR ภาษาไทย — ใช้ API ที่มีอยู่ (iApp/AppMan) หรือ multimodal LLM (2) **LLM ทำ 3 งาน:** ตรวจครบถ้วนตาม checklist เกณฑ์, ตรวจความสอดคล้องข้ามเอกสาร (อาชีพ-รายได้-เงินลงทุน), ประเมิน reasonableness ของ SoW พร้อมเหตุผล (3) rule engine เข้ารหัสแนวปฏิบัติ ก.ล.ต./ปปง. (4) ชั้นตรวจเอกสารปลอม (metadata/pixel forensics) — เฟสหลัง demo ได้ทุกชิ้นใน 1 สัปดาห์ด้วย mock documents (Confidence: สูง — ประเมินเชิงวิศวกรรม)

### 4.3 Data availability

ได้เปรียบ: **ลูกค้า (บล.) เป็นเจ้าของเอกสารเอง** ไม่ต้องรอ open data ใด ๆ — ใน demo ใช้เอกสาร mock (บัตรประชาชน/สลิปเงินเดือน/statement ปลอมที่สร้างเอง) ส่วน production เป็น on-prem processing ใต้ PDPA ของ บล. เกณฑ์อ้างอิง (แนวปฏิบัติ ก.ล.ต./ปปง.) เป็นเอกสารสาธารณะ — [ASCO](https://www.asco.or.th/uploads/articles_attc/1653559283.pdf), [ปปง.](https://sed.amlo.go.th/content/download/316) (Confidence: สูง)

### 4.4 Partnership

สมาคมบริษัทหลักทรัพย์ไทย (ASCO — เจ้าของแนวทางปฏิบัติกลาง), ตลท. (เจ้าของ e-Open Account — จุด integrate ธรรมชาติ), vendor OCR ไทย (AppMan/iApp — เป็น partner ชั้น extraction แทนที่จะแข่ง), บริษัท core system ของ บล. (Freewill ฯลฯ)

---

## Module 5 — Economics

### 5.1 Willingness to pay

- ฝั่ง compliance ของสถาบันการเงิน**จ่ายอยู่แล้วและจ่ายหนัก**: ค่าใช้จ่าย AML/KYC ops เฉลี่ยของสถาบันระดับ global สูงถึง **$72.9M/ปี/แห่ง** ([Fenergo](https://resources.fenergo.com/newsroom/global-financial-institutions-struggle-with-rising-client-losses-and-compliance-costs-as-ai-adoption-increases-fenergo)) และ KYC review ลูกค้า corporate อยู่ที่ **$2,001-2,500/เคส** ([Statista](https://www.statista.com/statistics/1614858/kyc-review-cost-corporate-banking/)) — สเกลไทยเล็กกว่ามากแต่โครงสร้างต้นทุนเหมือนกัน (Confidence: กลาง — ตัวเลขไทยตรง ๆ ไม่พบ; ค้นด้วย "ต้นทุน KYC บริษัทหลักทรัพย์ไทย" แล้วไม่เจอข้อมูลเปิดเผย)
- แรงจูงใจไม่ใช่แค่ต้นทุน แต่คือ**ความเสี่ยงโทษอาญา** (เคสฟินันเซีย) — งบประเภท "กันคุก" อนุมัติง่ายกว่างบ efficiency

### 5.2 Pricing benchmark + unit economics

- ราคาตลาด KYC automation: **$1-5/verification**; IDP: **$0.50-2.00/เอกสาร** เทียบ manual $6-25 — ส่วนต่างคือ value ที่แบ่งกันได้ ([ComplyCube](https://www.complycube.com/en/how-much-does-kyc-cost/), [Docsumo](https://www.docsumo.com/blogs/intelligent-document-processing/intelligent-document-processing-market-report-2025)) (Confidence: กลาง)
- โมเดลที่เหมาะ: **SaaS ต่อ บล.** (platform fee + per-case) — ลูกค้าเป้าหมายมีแค่ 36 ราย → ขาย direct ไม่มี CAC แบบ mass marketing แต่ sales cycle องค์กรการเงินยาว (security review, procurement 6-12 เดือน) (ประมาณการ; Confidence: ต่ำ)
- ตัวอย่าง ROI ที่เล่าได้: บล. ที่เปิด 50,000 บัญชี/ปี × เอกสาร 4 ชิ้น × ประหยัด $5-20/เอกสาร ≈ **35-140 ล้านบาท→ 1-5 ล้านบาท** ของงานตรวจที่หายไป (ประมาณการจาก benchmark ข้างต้น; Confidence: ต่ำ)

---

## Module 6 — Strategy

### 6.1 Competitive advantage ที่สร้างได้

1. **Thai rulebook เป็น moat:** เข้ารหัสแนวปฏิบัติ ก.ล.ต./ปปง. ฉบับใหม่ (มิ.ย. 2569) + อ่านเอกสารราชการ/การเงินภาษาไทย — Fenergo/smartKYC ไม่ localize เรื่องนี้ และ OCR ไทยเจ้าเดิมยังไม่ทำ decision layer
2. **ตำแหน่ง "shift-left":** ตรวจที่ฝั่ง Sales ก่อนส่ง ไม่ใช่ automate ที่ Backoffice — ตัดวงจรตีกลับตั้งแต่ต้นทาง (แก้ first-pass 20-60% ตรง ๆ) พร้อม audit trail ทุกเคสไว้โชว์ ก.ล.ต.
3. **จังหวะ:** เกณฑ์ใหม่เพิ่งบังคับ + เคสอาญาเพิ่งเกิด — หน้าต่างการขาย 12-24 เดือนก่อน incumbent ทำตาม

### 6.2 Beachhead segment

**บล. ขนาดกลางที่มีลูกค้า HNW/วงเงินสูง** (ต้องทำ Enhanced CDD + SoW บ่อยแต่ไม่มีทีม dev ใหญ่พอจะสร้างเอง) — เจ็บสุดจากเกณฑ์ใหม่, ตัดสินใจเร็วกว่า บล. ใหญ่, และเคสฟินันเซียคือ cautionary tale ของ segment นี้พอดี

### 6.3 ความเสี่ยงหลัก + mitigation

| ความเสี่ยง | ระดับ | Mitigation |
|---|---|---|
| ตลาดแคบ (36 บล.) — เพดานรายได้ต่ำ | สูง | ออกแบบ rulebook เป็น module ขยายไป บลจ./ประกัน/สินเชื่อ (โจทย์ KYC เดียวกัน); มอง exit เป็น acquisition โดย core-system vendor |
| AI ผ่านเอกสารผิด/ของปลอม → บล. รับโทษ | สูง | วางตัวเป็น decision support (คนอนุมัติเสมอ) + confidence score ต่อเช็ค + ชั้น fraud forensics + audit log ทุกการตัดสิน |
| บล. ใหญ่/AppMan ทำเอง | กลาง | เร็วกว่า + ขายเป็น white-label/partner กับ vendor OCR แทนที่จะแข่ง |
| Sales cycle องค์กรการเงินยาว | กลาง | เริ่มจาก pilot แบบ shadow mode (ตรวจคู่ขนานไม่แตะ flow จริง) ให้เห็นตัวเลข first-pass ก่อนซื้อ |
| PDPA / ข้อมูลอ่อนไหว | กลาง | สถาปัตยกรรม on-prem/private cloud ตั้งแต่ออกแบบ |

### 6.4 Positioning ที่แนะนำ

> "AI ผู้ช่วยตรวจเอกสาร KYC/SoW ที่ฝั่ง Sales — จับเอกสารขาด เอกสารขัดแย้ง และแหล่งเงินที่ไม่สมเหตุสมผล **ก่อน** เคสถูกส่งเข้า Backoffice — เปลี่ยนงานตีกลับหลายรอบให้เป็นการผ่านรอบเดียว พร้อม audit trail ที่ ก.ล.ต. อยากเห็น"

---

## ตารางคะแนน Rubric

| มิติ | คะแนน (1-5) | เหตุผลอิงหลักฐาน |
|---|---|---|
| 1. ขนาดปัญหา | **4** | Pain วัดได้ (first-pass 20-60%, ตรวจ 30-60 นาที/ราย, 70% เสียลูกค้า) + severity ระดับโทษอาญา (เคสฟินันเซีย) — หัก 1 เพราะผู้เจ็บโดยตรงคือ ops ของ 36 บล. ไม่ใช่ mass |
| 2. ขนาดตลาด | **2** | ลูกค้าเป้าหมายไทยแคบมาก (36 บล.) SAM 18-108 ล้านบาท/ปี — ต้องขยาย vertical จึงจะพ้นเพดาน |
| 3. การแข่งขัน (กลับด้าน) | **3** | ชั้น identity/OCR แข่งดุ (NDID, AppMan, iApp) แต่ชั้น case-level QC + SoW reasonableness ภาษาไทยยังว่าง; global player มีของแต่ไม่ localize |
| 4. Feasibility | **5** | ไม่ต้องมี license, เทคโนโลยีพร้อม, ข้อมูลเป็นของลูกค้าเอง, ก.ล.ต. สนับสนุนการใช้เทคโนโลยีใน KYC, demo ได้จริงใน 1 สัปดาห์ |
| 5. Economics | **3** | WTP ฝั่ง compliance ชัด (งบ "กันคุก") + benchmark ราคา per-doc มีจริง — แต่ตลาดเล็กและ sales cycle ยาวกดตัวเลขรวม |
| 6. ความได้เปรียบ | **3** | Thai rulebook + shift-left positioning เป็นแต้มต่อจริง แต่ AppMan/iApp ต่อยอดขึ้นมาได้ ต้องรีบ lock partnership |
| **รวม** | **20/30** | **Conditional Go** (เกณฑ์: 15-21) |

## Verdict: CONDITIONAL GO — เงื่อนไขที่ต้องแก้/พิสูจน์

1. **แก้เพดานตลาด:** ห้ามออกแบบผูกกับโบรกเกอร์อย่างเดียว — วาง rulebook เป็นชั้นถอดเปลี่ยนได้ เพื่อขยายไป บลจ., ประกัน, สินเชื่อ (โจทย์ KYC/SoW เดียวกัน ลูกค้ารวมหลายร้อยราย)
2. **ต้องมีชั้นตรวจของปลอม ไม่ใช่แค่ความครบ:** ถ้า pre-check เร่งให้เอกสารปลอมผ่านเร็วขึ้น product จะกลายเป็นความเสี่ยงเอง — ใส่ fraud signal (metadata/pixel) อย่างน้อยระดับ flag ตั้งแต่ MVP
3. **สำหรับ hackathon: demo "เคสตีกลับที่หายไป"** — โชว์ Sales อัปโหลดชุดเอกสาร → AI จับ 3 ปัญหา (เอกสารหมดอายุ, รายได้ไม่สอดคล้องเงินลงทุน, SoW ไม่มีหลักฐานรองรับ) → แก้ก่อนส่ง → ผ่านรอบเดียว พร้อมโชว์ dashboard first-pass rate — ใช้ตัวเลข 20-60% → เป้า 90% เป็นแกนเรื่อง

---

## แหล่งอ้างอิง (เข้าถึงทั้งหมดวันที่ 14 ก.ค. 2569)

### Tier 1 — หน่วยงานรัฐ / regulator / ตลาดหลักทรัพย์

1. ก.ล.ต. — แนวทางปฏิบัติการนำเทคโนโลยีมาใช้ทำความรู้จักลูกค้า — https://publish.sec.or.th/nrs/8327s.pdf
2. ปปง. — แนวทางปฏิบัติการตรวจสอบเพื่อทราบข้อเท็จจริงเกี่ยวกับลูกค้า — https://sed.amlo.go.th/content/download/316
3. ตลท. — รายชื่อบริษัทสมาชิก (36 แห่ง) — https://www.set.or.th/th/market/information/member-list/main
4. ตลท. — ระบบ e-Open Account — https://www.set.or.th/th/settrade/services/e-open-account
5. ASCO — Update กฎเกณฑ์ AML แนวปฏิบัติ KYC/CDD — https://www.asco.or.th/uploads/articles_attc/1653559283.pdf

### Tier 2 — ข่าวธุรกิจ / research / vendor report

6. The Standard — ก.ล.ต. กล่าวโทษ บล.ฟินันเซีย เหตุระบบ KYC/CDD หละหลวม — https://thestandard.co/sec-charges-finansia-kyc-lax/
7. Hoonsmart — เจาะแนวปฏิบัติ KYC/CDD ใหม่ของ ก.ล.ต. (30 มิ.ย. 2569) — https://hoonsmart.com/archives/425894
8. Hoonsmart — เปิดบัญชีใหม่ 4.4 แสนราย 5 เดือนแรกปี 2569 — https://hoonsmart.com/archives/426621
9. Statista — KYC review costs corporate banking 2024 ($2,001-2,500) — https://www.statista.com/statistics/1614858/kyc-review-cost-corporate-banking/
10. Fintech Global — first-pass rate 20-60%, remediation pain 88% — https://fintech.global/2026/04/27/how-firms-are-failing-at-periodic-kyc-reviews/
11. Fintech Global — 70% of banks lose clients to slow onboarding — https://fintech.global/2025/10/08/70-of-banks-lose-clients-due-to-slow-onboarding/
12. Fenergo — compliance cost & AI adoption report — https://resources.fenergo.com/newsroom/global-financial-institutions-struggle-with-rising-client-losses-and-compliance-costs-as-ai-adoption-increases-fenergo
13. Fenergo — 50% document processing reduction — https://www.fenergo.com/
14. Jumio — onboarding abandonment (68%, $3.3B) — https://www.jumio.com/how-to-reduce-customer-abandonment/
15. ID-Pal — 1 in 5 KYC checks >24 hours — https://www.id-pal.com/blog/kyc-delays-slowing-customer-onboarding/
16. Docsumo — IDP benchmarks (เวลา -70-80%, error 15-20%→2-5%, cost $6-25→$0.5-2) — https://www.docsumo.com/blogs/intelligent-document-processing/intelligent-document-processing-market-report-2025
17. CheckFile.ai — ต้นทุน manual KYC check $7.95-19 — https://www.checkfile.ai/en-US/blog/kyc-solution-pricing-cost-breakdown-roi-tco
18. ComplyCube — KYC pricing $1-5/verification, retail manual $13-130 — https://www.complycube.com/en/how-much-does-kyc-cost/
19. AppMan — OCR+ (98% accuracy เอกสารไทย) — https://www.appman.co.th/en/appman-ocr-plus-en/
20. iApp Technology — Thai OCR API docs — https://iapp.co.th/docs/intro
21. smartKYC — Source of Wealth verification guide — https://smartkyc.com/source-of-wealth-verification-guide/
22. Middesk — AI-powered fraud bypassing KYB/KYC ($15/30 นาที) — https://www.middesk.com/blog/how-fraudsters-are-using-ai-to-bypass-traditional-kyb-checks
23. Hesper AI — KYC document fraud (67% synthetic identity ใช้เอกสารปลอม) — https://gethesperai.com/blog/kyc-document-fraud-fintechs/
24. Inscribe — AI document fraud detection — https://www.inscribe.ai/
25. บล.บัวหลวง — เปิดบัญชีออนไลน์อนุมัติ 15 นาที — https://www.bualuang.co.th/article/openaccount
26. บล.กสิกรไทย — บริการ NDID — https://www.kasikornsecurities.com/th/startinvesting/ndid

### Tier 3 — ฟอรัม (หลักฐานพฤติกรรม)

27. Pantip — เปิดบัญชีหุ้นใช้เวลานานแค่ไหน — https://pantip.com/topic/38131509 · ระยะเวลาเปิดพอร์ตนานสุดกี่วัน — https://pantip.com/topic/30070568

*หมายเหตุ: TAM/SAM/SOM (Module 2.2) และตัวอย่าง ROI (Module 5.2) เป็นการประมาณการของผู้วิเคราะห์จาก benchmark ข้างต้น ไม่ใช่ตัวเลขจากแหล่งเดียวโดยตรง · ไม่พบข้อมูลเปิดเผยของ "ต้นทุน KYC ต่อเคสของ บล. ไทย" และ "อัตราตีกลับเอกสารของ บล. ไทย" — ใช้ benchmark global แทนและติด confidence กลาง*
