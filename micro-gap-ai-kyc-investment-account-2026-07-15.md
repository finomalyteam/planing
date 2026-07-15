# Micro-Gap Analysis: AI ตรวจเอกสาร KYC สำหรับเปิดบัญชีลงทุน (ตลาดไทย)

วันที่วิเคราะห์: 15 กรกฎาคม 2026 | ทุกแหล่งอ้างอิงเข้าถึงวันที่ 15 ก.ค. 2026

---

## 1. สรุปไอเดีย

**ไอเดีย:** ระบบ AI ช่วยตรวจสอบเอกสาร KYC ในขั้นตอนเปิดบัญชีลงทุน (บัญชีหุ้น/กองทุน)
เพื่อลดเวลารออนุมัติที่ทำให้ลูกค้าหลุด (drop-off)

**ตลาดเป้าหมาย:** ไทย — ขาย B2B ให้บริษัทหลักทรัพย์ (บล.) และบริษัทหลักทรัพย์จัดการกองทุน (บลจ.)

**Pain ที่ยืนยันจากหลักฐานจริง:**
- ผู้ใช้ Pantip เปิดบัญชีออนไลน์กับ บล. 2 เจ้า ส่งเอกสารครบแล้ว แต่ "เงียบทั้งสองเจ้า"
  ไม่รู้สถานะ ไม่รู้ต้องรอกี่วัน [25]
- Finnomena ระบุว่าถ้าเทียบใบหน้าไม่ผ่าน 3 ครั้ง เคสตกไปคิว manual review
  และลูกค้าต้องรออีเมลแจ้งผล 1–2 วัน [26]
- การทบทวน KYC + Suitability Test ทุก 2 ปีตามเกณฑ์ ก.ล.ต. — ถ้าลูกค้าไม่ทำ
  บัญชีถูกระงับซื้อ (Lock Buy) และการปลดล็อกใช้เวลา 3–5 วันทำการ [29][30]

---

## 2. คู่แข่งที่เทียบ (5 เจ้า)

| เจ้า | ประเภท | เหตุผลที่เลือก |
|---|---|---|
| **AppMan** (ไทย) | eKYC + onboarding platform | เจ้าตลาด eKYC ไทยสายการเงิน/หลักทรัพย์ มีลูกค้าอย่าง Webull, Bitkub [1][5] |
| **iApp Technology** (ไทย) | eKYC API/SDK | Challenger ไทยสาย developer-first เปิดราคา public, SDK open-source [7][9] |
| **AIGEN** (ไทย) | Document AI + eKYC | เจ้าเดียวในไทยที่เด่นเรื่อง OCR เอกสารประกอบภาษาไทย 20+ ชนิด [13][14] |
| **Sumsub** (Global) | Full-stack verification | ผู้เล่น global ที่รุกไทยชัดเจน — เพิ่ง launch Thailand DOPA verification มี.ค. 2026 [16] |
| **Jumio** (Global) | Identity verification | ผู้เล่น global รายใหญ่ มี Thai DOPA risk signal ใน docs [22] |

---

## 3. Component Map (13 ชิ้น)

ตาม user journey การเปิดบัญชีลงทุน + ชั้น cross-cutting:

| # | Component | คำอธิบาย |
|---|---|---|
| C1 | OCR บัตรประชาชนไทย + ตรวจ DOPA | อ่านบัตร + ตรวจเลข laser หลังบัตรกับกรมการปกครอง |
| C2 | Liveness + face comparison | ยืนยันว่าเป็นคนจริง เทียบหน้ากับบัตร |
| C3 | เชื่อมต่อ NDID/ThaID | ทางเลือกยืนยันตัวตนผ่าน identity provider |
| C4 | ตรวจจับเอกสารปลอม/ตัดต่อ | forgery, recapture, injection attack, deepfake |
| C5 | เช็คคุณภาพภาพ real-time ก่อน submit | กันวงจร reject → ถ่ายใหม่ → รอใหม่ |
| C6 | อ่าน+ตรวจเอกสารประกอบภาษาไทย | statement, สลิปเงินเดือน, ทะเบียนบ้าน — OCR + ตรวจความสอดคล้องกับข้อมูลที่กรอก |
| C7 | AML/PEP/sanction screening ชื่อไทย | รวม adverse media ภาษาไทย + จัดการ transliteration |
| C8 | AI ช่วยคิว manual review | จัดลำดับเคส, ลด false positive, อธิบายเหตุผลที่ flag |
| C9 | สื่อสารสถานะลูกค้าอัตโนมัติ | แจ้งสถานะ, ขอเอกสารเพิ่ม, ตาม drop-off กลับมาทำต่อ |
| C10 | Integration ระบบสายลงทุนไทย | FundConnext, Settrade e-Open Account, back-office บล. |
| C11 | Suitability Test / re-KYC automation | แบบประเมิน + การทบทวน KYC ทุก 2 ปีตามเกณฑ์ ก.ล.ต. |
| C12 | Pricing ที่ บล./บลจ. เล็กจ่ายไหว | ราคาโปร่งใส ไม่ต้อง minimum commitment สูง |
| C13 | Compliance ไทย | เกณฑ์ ก.ล.ต./ETDA, PDPA, audit trail |

---

## 4. Feature-Gap Matrix

✅ ทำแล้วทำได้ดี | ⚠️ ทำแล้วแต่อ่อน | ❌ ยังไม่ทำ (ยืนยัน ≥2 แหล่ง)

| Component | AppMan | iApp | AIGEN | Sumsub | Jumio |
|---|---|---|---|---|---|
| C1 OCR บัตร + DOPA | ✅ OCR 98.7% ตรวจ DOPA+AMLO [1] | ✅ OCR 98% อ่าน laser จางได้ DOPA ผ่าน blog [7][8][11] | ✅ laser code + auto-check DOPA (ลูกค้าต้องขอสิทธิ์ DOPA เอง) [12][15] | ✅ Thailand DOPA verification (เพิ่ง launch มี.ค. 2026) [16][17] | ✅ Thai DOPA risk signal [22] |
| C2 Liveness + face compare | ✅ 3D liveness, anti-deepfake [1][4] | ✅ hybrid liveness, iBeta certified [7] | ✅ face compare 99% แต่ liveness เป็น optional [12][15] | ✅ [17][18] | ⚠️ false-reject สูงบนมือถือผู้ใช้จริง (glare/blur) [23][24] |
| C3 NDID/ThaID | ⚠️ วาง positioning ใช้ร่วมกับ NDID/ThaID แต่ไม่ใช่ integration สำเร็จรูป [3][32] | ❌ ไม่ปรากฏทั้ง product page และ docs [7][8] | ⚠️ แนะนำให้ใช้ NDID/dip chip สำหรับ high-risk แต่ไม่ได้ให้บริการเอง [15] | ❌ ไม่มีใน supported docs/changelog [16][17] | ❌ ไม่ปรากฏใน docs [22][24] |
| C4 ตรวจเอกสารปลอม | ✅ microprint, font, hologram, recapture [1] | ⚠️ anti-spoofing ใบหน้า (รวม deepfake) แต่ไม่พูดถึง forgery ตัวเอกสาร [7] | ⚠️ ไม่ได้ชูเป็น feature หลัก [12][15] | ✅ deepfake/fraud detection [18][20] | ✅ จุดแข็งหลัก catch-rate ดีตามรีวิว B2B [23][24] |
| C5 เช็คคุณภาพ real-time | ⚠️ ไม่ระบุรายละเอียด capture SDK [1][2] | ✅ pipeline รองรับ glare/laser จาง, SDK ครบทุก platform [8][9] | ⚠️ ไม่ระบุรายละเอียด [12][15] | ⚠️ end-user รีวิวติเรื่องวน reject/UX สับสน [19] | ⚠️ "blurry-image" error คือ complaint หลักของ end-user [23] |
| C6 เอกสารประกอบภาษาไทย | ⚠️ มี Thai OCR สายสินเชื่อ/ลีสซิ่ง แต่ไม่ bundle ใน eKYC flow [6] | ⚠️ มี Document OCR แยกเป็นคนละ product กับ eKYC (ใน eKYC มีแค่ bank book) [7][10] | ✅ aiScript 20+ ชนิด รวม statement ทุกธนาคาร + สลิปเงินเดือน สรุปรายได้อัตโนมัติ [13][14] | ⚠️ proof-of-address ระดับ global ไม่เจาะ statement ไทย [17] | ⚠️ template นอก library ตกคิว manual [23] |
| C7 AML screening ชื่อไทย | ⚠️ ตรวจ AMLO list ผ่าน gateway แต่ไม่มี adverse media ไทย [1] | ❌ ไม่ปรากฏทั้ง product page และ docs [7][8] | ❌ ไม่ปรากฏใน product pages [12][13][15] | ⚠️ screening global ครบ แต่ adverse media/transliteration ชื่อไทยคือจุดอ่อนของทั้งอุตสาหกรรม [20][21][31] | ⚠️ AML เป็น add-on ทำให้ต้นทุนต่อเช็คเพิ่ม 30–40% [23] |
| C8 AI ช่วยคิว manual review | ⚠️ "KYC Agent" คือบริการคน follow-up ไม่ใช่ AI triage [2] | ❌ มีแค่ backend จัดการ transaction [7][8] | ❌ ไม่ปรากฏ [12][13][15] | ✅ AI case management, false-positive reduction, alert prioritization [20] | ⚠️ manual-review bottleneck คือ complaint อันดับ 1 บน Trustpilot [23] |
| C9 สื่อสารลูกค้า/ตาม drop-off | ⚠️ follow-up โดยคน (KYC Agent) ไม่ automated [2] | ❌ ไม่ปรากฏ [7][8] | ❌ ไม่ปรากฏ [12][13][15] | ❌ ไม่มี re-engagement ฝั่งลูกค้า — รีวิว end-user บ่นไม่รู้สถานะ [18][19] | ❌ ไม่ปรากฏ + end-user บ่นเรื่องไม่รู้สาเหตุ reject [23][24] |
| C10 Integration FundConnext/Settrade | ❌ ไม่ปรากฏใน product pages [1][2] | ❌ ไม่ปรากฏ [7][8] | ❌ ไม่ปรากฏ [13][15] | ❌ ไม่ปรากฏ [16][17] | ❌ ไม่ปรากฏ [22][24] |
| C11 Suitability/re-KYC automation | ❌ ไม่ปรากฏ [1][2] | ❌ ไม่ปรากฏ [7][8] | ❌ ไม่ปรากฏ [12][13] | ❌ ไม่ปรากฏ (มี re-verification ทั่วไป แต่ไม่ map กับเกณฑ์ ก.ล.ต./Suitability ไทย) [16][17] | ❌ ไม่ปรากฏ [22][24] |
| C12 Pricing สำหรับเจ้าเล็ก | ⚠️ quote-based ไม่เปิดราคา [1][2] | ✅ เปิดราคา API public + SDK ฟรี open-source [7][9] | ⚠️ quote-based [13][15] | ⚠️ รีวิว G2 ติว่าแพงสำหรับ SME/startup [18] | ⚠️ opaque 100% quote-based, add-on ดันราคา +30–40% [23] |
| C13 Compliance ไทย | ✅ ETDA-compliant, ISO 27001 [1] | ✅ PDPA, iBeta [7] | ✅ PDPA [12][15] | ⚠️ compliance framework global ไม่ได้ localize เกณฑ์ ก.ล.ต. [17][18] | ⚠️ เช่นเดียวกัน [23][24] |

---

## 5. Micro-Gap จัดอันดับ

### ตารางคะแนนทุก gap (เกณฑ์ละ 0–5 รวม 15)

| Gap | Component | หลักฐาน | Defensibility | ความง่ายลงมือ | รวม |
|---|---|---|---|---|---|
| G1 ตัวช่วยสื่อสารสถานะ + กู้ drop-off อัตโนมัติ | C9 | 4 | 2 | 5 | **11** |
| G2 Suitability Test / re-KYC 2 ปี automation | C11 | 4 | 3 | 4 | **11** |
| G3 AI triage คิว manual review เจาะบริบท บล. ไทย | C8 | 4 | 3 | 4 | **11** |
| G4 Connector สำเร็จรูป FundConnext/Settrade | C10 | 3 | 4 | 3 | **10** |
| G5 ตรวจความสอดคล้องเอกสารประกอบ (ไม่ใช่แค่ OCR) | C6 | 3 | 3 | 4 | **10** |
| G6 Pre-submission coaching ลด false reject | C5 | 3 | 2 | 5 | **10** |
| G7 Adverse media ภาษาไทย + Thai name matching | C7 | 3 | 4 | 2 | **9** |
| G8 NDID-as-a-service bundle ใน flow เดียว | C3 | 3 | 2 | 2 | **7** |

หมายเหตุการให้คะแนนหลักฐาน: G1–G3 มีทั้งรีวิว/คำบ่นผู้ใช้จริงอิสระจาก vendor + การยืนยัน ❌/⚠️ จาก
หน้า product ≥2 แหล่งต่อเจ้า จึงได้ 4; G4–G8 หลักฐานหลักคือ "การไม่ปรากฏ" ใน product pages
และบทความอุตสาหกรรม ยังไม่มีเสียงลูกค้า B2B ตรง ๆ จึงได้ 3

### 🥇 Top 1 — G1: ตัวช่วยสื่อสารสถานะ + กู้ drop-off อัตโนมัติ (11/15)

**ของเดิมทำได้แค่ไหน:** ทุกเจ้าจบหน้าที่ที่ "ผลตรวจ" แล้วโยนกลับให้ บล. จัดการลูกค้าเอง
AppMan มี "KYC Agent" แต่เป็นบริการมนุษย์ follow-up ไม่ใช่ automation [2]
ฝั่ง end-user ของ Sumsub/Jumio รีวิวติเรื่องเดียวกัน: reject แล้วไม่รู้สาเหตุ ไม่รู้ต้องทำอะไรต่อ [19][23]
หลักฐาน pain ฝั่งไทยชัด: ผู้สมัครเปิดบัญชีหุ้นบ่นใน Pantip ว่าส่งเอกสารแล้ว "เงียบทั้งสองเจ้า" [25]
และ flow มาตรฐานคือรออีเมล 1–2 วันหลังถูกตี [26]

**เราเสียบตรงไหน:** layer ที่นั่งทับผลตรวจของ engine ไหนก็ได้ — ใช้ LLM แปลงเหตุผล reject
เชิงเทคนิคเป็นข้อความภาษาไทยที่บอกชัดว่าต้องถ่ายใหม่ยังไง/ส่งเอกสารอะไรเพิ่ม ยิงผ่าน
LINE OA/SMS ทันที + dashboard drop-off funnel ให้ บล. เห็นว่าลูกค้าหลุดขั้นไหน แล้วยิง
re-engagement อัตโนมัติ ขายเป็น add-on ที่ไม่ต้องแย่งลูกค้ากับ eKYC เจ้าเดิม

**ความเสี่ยงถูกปิด:** สูง — feature เชิง UX ที่เจ้าเดิม copy ได้ใน 1–2 quarter
ตัวกันคือความเร็ว + ความเข้าใจ flow เอกสารไทย + ผูก integration LINE OA ให้แน่น

### 🥈 Top 2 — G2: Suitability Test / re-KYC ทุก 2 ปี automation (11/15)

**ของเดิมทำได้แค่ไหน:** ไม่มี vendor ใดใน 5 เจ้าแตะเรื่องนี้เลย (❌ ทั้งแถว ยืนยันจาก
product pages ≥2 แหล่งต่อเจ้า) ทุกวันนี้ บล./บลจ. ทำเองในแอป/ฟอร์มตัวเอง [29]
Pain จริง: ถ้าลูกค้าไม่ทบทวนตามกำหนด บัญชีถูก Lock Buy และปลดล็อกกินเวลา 3–5 วันทำการ [30]
— นี่คือ "การเสียลูกค้า" ที่เกิดซ้ำทุก 2 ปีกับลูกค้าทุกราย ไม่ใช่แค่ตอนเปิดบัญชี

**เราเสียบตรงไหน:** โมดูล re-KYC-as-a-service: ตรวจจับวันครบกำหนดล่วงหน้า, ยิงแบบทบทวน
แบบ pre-filled (AI ดึงข้อมูลเดิม + ตรวจว่ามีอะไรเปลี่ยน), เตือนผ่าน LINE ก่อนโดน Lock Buy,
และปลดล็อกอัตโนมัติทันทีที่ทำเสร็จแทนที่จะรอ 3–5 วัน ตลาดตรวจสอบง่าย: ลูกค้าบัญชีหุ้น
ทุกคนต้องเจอ event นี้

**ความเสี่ยงถูกปิด:** ปานกลาง — ต้องเข้าใจเกณฑ์ ก.ล.ต. และ workflow back-office ของ บล.
ซึ่ง vendor eKYC ทั่วไป (โดยเฉพาะ global) ไม่มี incentive มาลงลึก เพราะเป็น pain เฉพาะ
regulation ไทย เจ้าที่น่ากลัวกว่าคือ Settrade/SET เองถ้าตัดสินใจทำเป็น utility กลาง

### 🥉 Top 3 — G3: AI triage คิว manual review เจาะบริบท บล. ไทย (11/15)

**ของเดิมทำได้แค่ไหน:** Sumsub ทำแล้วทำได้ดีระดับ global (AI case management,
false-positive reduction) [20] แต่แพงสำหรับเจ้าเล็ก [18] และไม่ localize บริบทไทย
Jumio อ่อนชัด — manual-review bottleneck คือ complaint อันดับ 1 [23]
เจ้าไทยทั้งสาม (AppMan/iApp/AIGEN) ไม่มี AI triage เลย: AppMan ใช้คน [2],
iApp มีแค่ transaction backend [7][8] ดังนั้นเคสที่ auto-check ไม่ผ่าน (เช่นเทียบหน้า
fail 3 ครั้ง) ไปกองรอคนตรวจ 1–2 วัน [26]

**เราเสียบตรงไหน:** review console สำหรับทีม compliance ของ บล. ไทยโดยเฉพาะ —
AI จัดลำดับเคสตามความน่าจะอนุมัติ, สรุปเหตุผลที่ flag เป็นภาษาไทยพร้อมหลักฐานชี้จุด
บนภาพเอกสาร, one-click ขอเอกสารเพิ่ม (ต่อเข้ากับ G1), เก็บ audit trail ตามเกณฑ์ ก.ล.ต.
เป้าหมาย: กดเวลา review จาก 1–2 วันเหลือหลักนาที–ชั่วโมง

**ความเสี่ยงถูกปิด:** ปานกลาง — Sumsub มีของแล้วและกำลังรุกไทย (เพิ่ง launch DOPA
มี.ค. 2026 [16] แปลว่าไทยอยู่ใน roadmap จริง) ตัวกันคือราคา + ภาษาไทย +
ความเข้าใจเอกสาร/เกณฑ์ไทยที่ Sumsub ยังไม่ลงลึก

### ข้อสังเกตเชิงกลยุทธ์

สาม gap อันดับต้นประกอบกันเป็น product เดียวได้พอดี: **"layer หลังผลตรวจ"**
(post-verification orchestration) — คือทั้งอุตสาหกรรมแข่งกันที่ *ความแม่นของการตรวจ*
(C1–C4 เขียวเกือบหมดทั้งแถว) แต่ปล่อยช่วง *"ตรวจไม่ผ่านแล้วเกิดอะไรต่อ"* ว่างไว้
ซึ่งเป็นจุดที่ลูกค้าหลุดจริงตามหลักฐาน [19][23][25][26][30]
การเข้าตลาดแบบไม่ชนตรงกับ eKYC engine เจ้าเดิม (เป็น partner ไม่ใช่คู่แข่ง) ยังทำให้
ขายเข้า บล. ที่มีสัญญากับ AppMan/Sumsub อยู่แล้วได้ด้วย

**Gap ที่แนะนำให้เลี่ยง:** G8 (NDID bundle) — โครงสร้าง NDID ผูกกับการเป็นสมาชิก
platform และมีธนาคารเป็น IdP หลัก [32] ทีมเล็กเข้าไม่ได้ และ G7 (Thai adverse media)
— defensibility สูงจริง แต่ต้องสร้าง corpus ข่าวไทย + name matching engine ก่อนขายได้
ไม่เหมาะเป็น MVP แรก

---

## 6. แหล่งอ้างอิง (เข้าถึงทั้งหมดวันที่ 15 ก.ค. 2026)

### AppMan
- [1] https://www.appman.co.th/en/appman-e-kyc-eng/ — feature หลัก: OCR 98.7%, DOPA+AMLO, fraud detection, dip chip 8,500+ จุด
- [2] https://www.appman.co.th/en/customer-onboarding-e-kyc-en/ — onboarding, KYC Agent (บริการคน)
- [3] https://www.appman.co.th/en/digital-identity-verification-tools/ — positioning ร่วมกับ NDID/ThaID
- [4] https://www.appman.co.th/appman-and-skyict/ — partnership SKY ICT (OCR + liveness)
- [5] https://www.appman.co.th/en/seamless-digital-onboarding-the-success-story-behind-webull-x-appman-ekyc/ — case study Webull (บล.)
- [6] https://www.appman.co.th/ocr-thai-data-entry-leasing-business/ — Thai OCR สายสินเชื่อ/ลีสซิ่ง

### iApp Technology
- [7] https://iapp.co.th/products/ekyc — feature + ราคา public, iBeta, ไม่มี NDID/AML/manual review
- [8] https://iapp.co.th/docs/ekyc/thai-national-id-card — docs OCR บัตร, รองรับ laser จาง
- [9] https://iapp.co.th/blog/iapp-ekyc-sdk-launch — launch SDK open-source (changelog ล่าสุด)
- [10] https://iapp.co.th/blog/iapp-4-new-document-ocr — Document OCR แยก product
- [11] https://iapp.co.th/blog/what-is-ekyc-complete-guide — การเชื่อม DOPA

### AIGEN
- [12] https://aigencorp.com/standalone-ekyc-service/ — laser code + DOPA auto-check, liveness optional
- [13] https://aigencorp.com/en/aiscript/ — aiScript 20+ ชนิดเอกสาร
- [14] https://aigencorp.com/ocr-for-finance-and-banking/ — statement ทุกธนาคาร, สลิปเงินเดือน, สรุปรายได้
- [15] https://aigencorp.com/ai-technology-for-ekyc/ — face compare 99%, เงื่อนไข DOPA/NDID

### Sumsub
- [16] https://docs.sumsub.com/changelog/march-2026 — launch Thailand DOPA verification (มี.ค. 2026)
- [17] https://sumsub.com/supported-documents/ — coverage 14,000+ เอกสาร 220+ ประเทศ
- [18] https://www.g2.com/products/sumsub/reviews — รีวิวติ: แพงสำหรับ SME, ช้า, UI ซับซ้อน
- [19] https://www.trustpilot.com/review/sumsub.com — end-user: วน reject, ไม่รู้สถานะ, support ช้า
- [20] https://sumsub.com/newsroom/sumsub-bolsters-aml-compliance-with-enhanced-case-management-and-advanced-false-positive-reduction/ — AI case management
- [21] https://sumsub.com/aml-screening/ — AML/PEP/adverse media screening

### Jumio
- [22] https://docs.jumio.com/production/Content/References/Risk%20Signals/Thai%20DOPA.htm — Thai DOPA risk signal (docs ย้ายไป documentation.jumio.ai)
- [23] https://beverified.org/providers/jumio/ — สรุปรีวิว: manual-review bottleneck complaint #1, opaque pricing, AML add-on +30–40%, false reject บนมือถือ
- [24] https://www.g2.com/products/jumio/reviews — รีวิว B2B: catch-rate ดี support ดี

### Ecosystem / Pain ฝั่งไทย
- [25] https://pantip.com/topic/38131509 — กระทู้: เปิดบัญชีหุ้นออนไลน์ ส่งเอกสารแล้วเงียบทั้ง 2 บล.
- [26] https://www.finnomena.com/บัญชียังไม่ได้รับอนุมั/ — face fail 3 ครั้ง → manual review, แจ้งผลทางอีเมล 1–2 วัน
- [27] https://www.set.or.th/th/dap/services/fundconnext — FundConnext: ระบบกลางเปิดบัญชี/ซื้อขายกองทุน มี API
- [28] https://www.set.or.th/th/settrade/services/e-open-account — Settrade e-Open Account
- [29] https://www.daolsecurities.co.th/en/highlight/activities/how-to-review-kyc-suitability-test — เกณฑ์ทบทวน KYC/Suitability ทุก 2 ปี
- [30] https://support.pi.financial/hc/th/articles/9931394982169-ทำไมท-านต-องทำแบบทบทวน-KYC-และ-Suitability-Test-เม-อหมดอาย — Lock Buy + ปลดล็อก 3–5 วันทำการ
- [31] https://amlwatcher.com/adverse-media-screening/ — ปัญหา transliteration non-Latin scripts ใน AML screening
- [32] https://ndid.co.th/en/platform-en-2/ — โครงสร้าง NDID platform / membership
