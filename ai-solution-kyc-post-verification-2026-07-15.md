# AI Solution Design: Post-Verification Layer สำหรับ KYC เปิดบัญชีลงทุน

วันที่วิเคราะห์: 15 กรกฎาคม 2026 | ราคา/เงื่อนไขทุกตัวเช็ค ณ วันที่นี้
ต่อยอดจาก: `micro-gap-ai-kyc-investment-account-2026-07-15.md` (Top 3 gap: G1 สื่อสารสถานะ, G2 re-KYC automation, G3 AI triage manual review)

---

## 1. สรุปเคส

**ปัญหา:** สร้าง "post-verification orchestration layer" — product ที่นั่งทับผลตรวจของ eKYC engine
(AppMan/Sumsub/ฯลฯ) เพื่อปิด 3 gap: (G1) ลูกค้าถูก reject แล้วเงียบ/ไม่รู้ต้องทำอะไรต่อ,
(G2) การทบทวน KYC/Suitability ทุก 2 ปีที่ทำให้บัญชีโดน Lock Buy และปลดล็อกช้า 3–5 วัน,
(G3) เคสตกคิว manual review แล้วรอคนตรวจ 1–2 วัน

**ข้อจำกัดที่รับมา:** ทีมเล็กมี dev เขียนโค้ดได้ (เน้น API ประกอบเอง) | ใช้ cloud LLM ได้
ถ้า provider ไม่เอาข้อมูลไป train ต่อ | ข้อมูล KYC เป็นข้อมูลส่วนบุคคลอ่อนไหว (PDPA)

---

## 2. แผนที่ปัญหา

| # | ส่วนย่อย | ใช้ AI? | เหตุผล |
|---|---|---|---|
| P1 | แปลงเหตุผล reject เชิงเทคนิค → ข้อความไทยที่ actionable (G1) | **(ก) AI แก้ได้ดี** | งานแปลงภาษา + ปรับ tone ตามบริบท คือจุดแข็งของ LLM ตรง ๆ |
| P2 | ส่งข้อความหาลูกค้า (LINE/SMS) + ตาม drop-off ตามกำหนดเวลา (G1) | **(ค) ไม่ควรใช้ AI** | เป็น messaging + scheduling ธรรมดา — LINE Messaging API + workflow engine ถูกกว่า เร็วกว่า deterministic กว่า |
| P3 | ตัดสินใจว่าจะยิง re-engagement เมื่อไหร่/บ่อยแค่ไหน (G1) | **(ค) เริ่มจาก rule-based** | ช่วงแรกยังไม่มี data พฤติกรรมพอ train โมเดล — กฎง่าย ๆ (24 ชม./72 ชม. หลัง drop) วัดผลได้ก่อน |
| P4 | ตรวจจับวันครบกำหนด re-KYC + trigger flow (G2) | **(ค) ไม่ควรใช้ AI** | cron job + database query — deterministic 100% พลาดไม่ได้เพราะผูกกับเกณฑ์ ก.ล.ต. |
| P5 | Pre-fill แบบทบทวน + ตรวจว่าข้อมูล/เอกสารใหม่ต่างจากเดิมตรงไหน (G2) | **(ก) AI แก้ได้ดี** | สกัดข้อมูลจากเอกสาร + เปรียบเทียบ field ต่อ field + สรุปว่าอะไรเปลี่ยน — งาน extraction/comparison ของ LLM |
| P6 | สรุปเคสให้ reviewer: เหตุผลที่ flag เป็นภาษาไทย + ชี้จุดบนภาพเอกสาร (G3) | **(ก) AI แก้ได้ดี** | multimodal LLM อ่านภาพเอกสาร+ผลตรวจ แล้วสรุปเป็นภาษาคนได้ — ตัวนี้คือหัวใจของ review console |
| P7 | จัดลำดับคิวเคสตามความน่าจะอนุมัติ (G3) | **(ข) AI ช่วยได้บางส่วน** | เริ่มจาก rule-based scoring (ชนิดของ flag, ความครบของเอกสาร) → พอมี label จากผลอนุมัติจริงค่อย train ML classifier |
| P8 | การอนุมัติ/ปฏิเสธขั้นสุดท้าย (G3) | **(ค) ห้ามใช้ AI ตัดสิน** | ความเสี่ยงกำกับดูแลสูง — เกณฑ์ AML/ก.ล.ต. ต้องมีคนรับผิดชอบการตัดสินใจ AI ทำได้แค่ "เสนอ" พร้อมเหตุผล |
| P9 | Audit trail ทุกการตัดสินใจ | **(ค) ไม่ใช่งาน AI** | append-only log ใน database ธรรมดา |

> จุดสำคัญเชิงสถาปัตยกรรม: AI อยู่แค่ 3 จุด (P1, P5, P6+P7) ที่เหลือเป็น automation ธรรมดา
> ทำให้ต้นทุน LLM ต่อเคสต่ำและระบบส่วนใหญ่ deterministic — เหมาะกับงานสาย compliance

---

## 3. เครื่องมือรายส่วน

### ส่วน A — LLM สำหรับ P1 (แปลง reject → ข้อความไทย) และ P6 (สรุปเคสให้ reviewer)

ทั้งสองงานใช้ LLM ตัวเดียวกันได้ (P6 ต้องการ vision ด้วย)

#### ตัวเลือก 3 ตัว

**A1. Claude API (Anthropic)** — โมเดลหลัก `claude-opus-4-8` / งานเบา `claude-haiku-4-5`
ทำงาน: multimodal LLM รับทั้งข้อความ+ภาพเอกสาร (PDF/รูป) วิเคราะห์และตอบเป็นภาษาไทยได้ดี
มี structured outputs (`output_config.format`) บังคับ JSON schema — สำคัญมากสำหรับระบบที่
ต้อง parse ผลลัพธ์ต่อ [1][2]

**A2. OpenAI API** — `gpt-4.1` / `gpt-4o` (มี vision)
ทำงาน: เช่นเดียวกัน รองรับภาษาไทยดี มี structured outputs [5][6]

**A3. Typhoon (SCB 10X)** — Thai LLM แบบ open source (Apache 2.0) + มี API Pro
ทำงาน: โมเดลที่ pretrain เจาะภาษาไทยโดยเฉพาะ ดาวน์โหลด weight ฟรีจาก Hugging Face/Ollama
รัน self-host ได้ 100% (ข้อมูลไม่ออกนอกองค์กร) หรือใช้ API ผ่าน Together AI [7][8][9]

#### ตารางเปรียบเทียบ

| เกณฑ์ | Claude API | OpenAI API | Typhoon (self-host) |
|---|---|---|---|
| ราคา (ต่อ 1M token in/out) | Opus 4.8: $5/$25, Haiku 4.5: $1/$5, Batch API ลด 50% [1] | GPT-4.1: $2/$8, GPT-4o: $2.50/$10 [5][6] | ฟรี (จ่ายค่า GPU server เอง) หรือ API Pro per-token [7][8] |
| ภาษาไทย | ดีมาก (เขียนไทยธรรมชาติ) | ดี | ดีมาก (pretrain ไทยโดยเฉพาะ) แต่ตัวเล็ก (4B–12B) ความสามารถ reasoning ต่ำกว่า frontier model |
| Vision (อ่านภาพเอกสาร) | ✅ รวม PDF native, high-res 2576px [2] | ✅ (GPT-4o) | ⚠️ จำกัด — รุ่น vision ยังไม่เทียบเท่า |
| Data privacy | ไม่ train จาก API data, log ลบใน 7 วัน, เป็น Data Processor [10][11] | Business/API ไม่ train by default [5] | ดีที่สุด — ข้อมูลไม่ออกนอกองค์กรเลย |
| ความยากเริ่มใช้ | ต่ำ (SDK Python/TS) | ต่ำ | สูง (ต้องมี GPU + ops) |
| Structured output | ✅ json_schema enforce | ✅ | ⚠️ ต้อง prompt เอง |

#### ตัวอย่าง input → output (P1 — จากเคสจริงในรายงาน gap)

Input ที่ส่งให้ LLM (ผลจาก eKYC engine + system prompt กำหนด tone):
```json
{
  "rejection_code": "FACE_MATCH_FAILED_3X",
  "detail": "face similarity 0.62 < threshold 0.85, attempts: 3, glare detected on attempt 2-3",
  "customer_name": "คุณสมชาย",
  "channel": "LINE"
}
```
Output (ข้อความพร้อมส่งเข้า LINE OA):
```
สวัสดีครับคุณสมชาย 📋 การยืนยันตัวตนของคุณยังไม่สำเร็จ
เนื่องจากภาพถ่ายมีแสงสะท้อนบนใบหน้า ทำให้ระบบเทียบใบหน้ากับบัตรไม่ได้

วิธีแก้: ถ่ายใหม่ในที่แสงสว่างสม่ำเสมอ ไม่ย้อนแสง และถอดแว่นตาก่อนถ่าย
กดลิงก์นี้เพื่อยืนยันตัวตนอีกครั้งได้เลย (ใช้เวลา 2 นาที): https://...
ทีมงานพร้อมช่วยเหลือ พิมพ์ "ติดต่อเจ้าหน้าที่" ได้ตลอดครับ
```

#### ตัวอย่าง input → output (P6 — สรุปเคสให้ reviewer)

Input: ภาพบัตรประชาชน + ภาพ statement + ผลตรวจ engine (JSON) → Output (JSON เข้า review console):
```json
{
  "priority_score": 72,
  "summary_th": "เคสน่าจะอนุมัติได้ — เทียบหน้าไม่ผ่านเพราะคุณภาพภาพ ไม่ใช่คนละคน",
  "flags": [
    {"type": "face_match", "explanation_th": "คะแนนเทียบหน้า 0.62 ต่ำกว่าเกณฑ์ แต่ภาพ selfie ครั้งที่ 2-3 มีแสงสะท้อน แนะนำขอ selfie ใหม่แทนการปฏิเสธ", "evidence_region": {"page": 1, "bbox": [120, 80, 340, 300]}},
    {"type": "income_consistency", "explanation_th": "รายได้ใน statement (เฉลี่ย 52,000 บาท/เดือน) สอดคล้องกับที่กรอก (50,000 บาท)", "status": "pass"}
  ],
  "suggested_action": "REQUEST_NEW_SELFIE"
}
```

อ่านต่อ: [Claude API docs](https://platform.claude.com/docs/en/about-claude/models/overview) [1],
[Anthropic privacy — is my data used for training](https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training) [10],
[OpenAI pricing](https://developers.openai.com/api/docs/pricing) [5], [opentyphoon.ai](https://opentyphoon.ai/) [7]

---

### ส่วน B — Document AI สำหรับ P5 (อ่านเอกสารประกอบ + เทียบข้อมูล re-KYC)

งานนี้แยกจากส่วน A ได้ถ้าปริมาณเอกสารสูงมาก (OCR เฉพาะทางถูกกว่าต่อหน้า) แต่ทีมเล็ก
เริ่มจากใช้ multimodal LLM ตัวเดียวกับส่วน A ก่อนได้

| เกณฑ์ | Claude (multimodal LLM) | Azure AI Document Intelligence | GPT-4o vision |
|---|---|---|---|
| วิธีทำงาน | ส่งภาพ/PDF เข้า LLM โดยตรง สกัด+เปรียบเทียบ+ให้เหตุผลในคำขอเดียว [2] | Custom extraction model — train ด้วยตัวอย่างเอกสารของเราเอง ได้ field แบบ deterministic [12][13] | เช่นเดียวกับ Claude [6] |
| ราคา | ตามจำนวน token ภาพ (~1,600–4,784 token/ภาพ) [2] | Custom extraction $30/1,000 หน้า, free tier 500 หน้า/เดือน [13] | ตาม token |
| ภาษาไทย | อ่านเอกสารไทยได้รวมลายมือบางส่วน | รองรับ handwriting ภาษาไทยแล้ว [12] | อ่านได้ |
| จุดแข็ง | ยืดหยุ่นสุด — เอกสารชนิดใหม่ไม่ต้อง train, ให้เหตุผลเชิงเปรียบเทียบได้ | แม่นและถูกกว่าที่ปริมาณสูง, ผลลัพธ์คงที่ | ทีมที่ใช้ OpenAI อยู่แล้วไม่ต้องเพิ่ม vendor |
| จุดอ่อน | ต้นทุนต่อหน้าสูงกว่าที่ scale ใหญ่ | ต้อง train/maintain model ต่อชนิดเอกสาร, ไม่ให้เหตุผล | เหมือน Claude |

**คำแนะนำส่วนนี้:** MVP ใช้ multimodal LLM (ส่วน A) ทำ P5 ไปเลย — ไม่ต้องเพิ่มระบบ
พอปริมาณเกิน ~หลักหมื่นหน้า/เดือนค่อยประเมิน Azure DI สำหรับ extraction ขั้นแรก
แล้วส่งเฉพาะผลสรุปเข้า LLM

---

### ส่วน C — Delivery + Workflow สำหรับ P2, P3, P4 (ไม่ใช่ AI)

| เครื่องมือ | ทำอะไร | ราคา | หมายเหตุ |
|---|---|---|---|
| **LINE Messaging API** | ส่งข้อความสถานะ/เตือน re-KYC เข้า LINE OA ของ บล. | ไทย: Free 200 ข้อความ/เดือน, แผนเสียเงินตามปริมาณ (เรตปรับตามประกาศ LINE) [14][15] | ช่องทางหลักของลูกค้าไทย — นับข้อความตามผู้รับ ข้อความที่ส่งไม่ถึง (โดน block) ไม่คิดเงิน [14] |
| **n8n (self-host)** | workflow engine: cron ตรวจวันครบกำหนด re-KYC, ลำดับการยิงข้อความ, retry, เชื่อม API ต่าง ๆ | Community Edition ฟรี ไม่จำกัด execution (จ่ายแค่ VPS ~$5–7/เดือน) [16][17] | self-host = ข้อมูลไม่ออกนอกระบบ สอดคล้อง PDPA; ทางเลือก: เขียน worker เอง (ทีมมี dev อยู่แล้ว) |

ตัวอย่าง flow ใน n8n: `cron ทุกวัน 06:00 → query ลูกค้าที่ KYC หมดอายุใน 30 วัน →
เรียก Claude API สร้างข้อความเตือนเฉพาะบุคคล → ส่ง LINE push → บันทึก audit log →
ถ้าไม่ตอบใน 7 วัน ส่งซ้ำรอบ 2`

---

### ส่วน D — Priority scoring สำหรับ P7 (AI ช่วยบางส่วน)

- **เฟส 1 (MVP):** rule-based — คะแนนจากชนิด flag, จำนวนครั้งที่ fail, ความครบเอกสาร
  เขียนเป็นโค้ดธรรมดา ตรวจสอบได้ อธิบายให้ compliance ฟังได้
- **เฟส 2 (มี data 3–6 เดือน):** train classifier (scikit-learn/XGBoost — open source ฟรี)
  ด้วย label จากผลอนุมัติจริง เพื่อทำนาย "ความน่าจะอนุมัติ" แม่นกว่ากฎ
- **ไม่แนะนำ** ใช้ LLM ให้คะแนนตรง ๆ เป็น production score — ไม่ deterministic และแพงเกินจำเป็น
  (LLM ทำหน้าที่อธิบาย ไม่ใช่ตัดเกรด)

---

## 4. คำแนะนำ: Stack ที่เลือก

**Stack แนะนำสำหรับทีมเล็ก + privacy แบบ no-training cloud:**

| ชั้น | เลือก | เหตุผลเทียบข้อจำกัด |
|---|---|---|
| LLM หลัก (P1, P5, P6) | **Claude API — `claude-opus-4-8`** สำหรับ P6 (วิเคราะห์เคส ต้องแม่น) และ **`claude-haiku-4-5`** สำหรับ P1 (แปลงข้อความ งานเบา, $1/$5) | vision+PDF native, structured outputs enforce JSON, ไม่ train จาก API data + log 7 วัน [1][2][10][11] — ตอบโจทย์ privacy ที่ตั้งไว้; ใช้ Batch API กับงาน re-KYC ล่วงหน้า (ไม่ด่วน) ลดค่าใช้ 50% [1] |
| Delivery | **LINE Messaging API** | ช่องทางที่ลูกค้าไทยเปิดอ่านจริง [14] |
| Workflow | **n8n self-host** (หรือ worker เขียนเอง) | ฟรี, ข้อมูลอยู่ในระบบเรา [16] |
| Scoring | **rule-based → XGBoost** | อธิบายได้ต่อ compliance, ไม่ผูกค่าใช้จ่าย LLM กับทุกเคส |
| ทางหนีถ้า privacy เข้มขึ้น | **Typhoon self-host** แทน cloud LLM เฉพาะ P1 (งานข้อความล้วน) | โมเดลไทย open source รันในองค์กรได้ [7][9] — แต่ P6 ที่ต้องการ vision+reasoning ยังต้องพึ่ง frontier model |

**ประมาณการต้นทุน LLM ต่อเคส (คร่าว ๆ):** P1 ด้วย Haiku (~1K token in / 300 out) ≈ $0.0025;
P6 ด้วย Opus 4.8 (ภาพ 3 ภาพ + บริบท ~15K token in / 1K out) ≈ $0.10 —
เทียบกับต้นทุนคนตรวจ 1–2 วัน หรือลูกค้าหลุดหนึ่งราย ถือว่าต่ำมาก
(ตัวเลข token เป็นการประมาณจากขนาด input ที่ออกแบบ ควรวัดจริงด้วย count_tokens ก่อน production)

**ลำดับสร้าง MVP:** (1) P1+P2 ก่อน — เห็นผลเร็วสุด demo ง่ายสุด (LINE แจ้งเหตุผล reject ภาษาคน)
→ (2) P6 review console → (3) P4+P5 re-KYC flow → (4) P7 ML scoring ทีหลังสุด

---

## 5. แนวทางต่อยอด

- **Claude Batch API** — งาน re-KYC เป็น batch ล่วงหน้าโดยธรรมชาติ (รู้วันครบกำหนดก่อนเป็นเดือน)
  ส่งเข้า Batch API ได้ทั้งชุด ลดต้นทุน 50% [1]
- **Prompt caching** — system prompt + เกณฑ์การตรวจของแต่ละ บล. ยาวและคงที่
  ใส่ cache_control ลดต้นทุน input ที่ซ้ำได้ถึง ~90% [1]
- **Structured outputs → ต่อ dashboard ตรง** — ผลจาก P6 เป็น JSON schema คงที่
  เอาเข้า database ทำ drop-off funnel dashboard (metabase/superset ฟรี) ได้ทันที
- **ขยายจาก LINE → email/SMS** — n8n มี node สำเร็จรูปของ SendGrid/Twilio อยู่แล้ว [16]
- **Typhoon fine-tune** — ถ้าไปทาง self-host ในอนาคต weight เป็น Apache 2.0
  fine-tune กับข้อความ KYC ของเราเองได้ [9]
- **เก็บ label ตั้งแต่วันแรก** — ทุกการตัดสินใจของ reviewer (อนุมัติ/ปฏิเสธ/ขอเอกสารเพิ่ม)
  คือ training data ของ P7 เฟส 2 — ออกแบบ schema ให้เก็บตั้งแต่ MVP

---

## 6. แหล่งอ้างอิง (เข้าถึง 15 ก.ค. 2026)

### Claude API / Anthropic
- [1] https://platform.claude.com/docs/en/about-claude/models/overview — รุ่นและราคา (Opus 4.8 $5/$25, Haiku 4.5 $1/$5, Batch 50%, prompt caching)
- [2] https://platform.claude.com/docs/en/build-with-claude/vision — vision/PDF, ขนาดภาพ high-res
- [10] https://privacy.claude.com/en/articles/7996868-is-my-data-used-for-model-training — API/commercial ไม่ใช้ข้อมูล train
- [11] https://privacy.claude.com/en/articles/9267385-does-anthropic-act-as-a-data-processor-or-controller — สถานะ Data Processor

### OpenAI
- [5] https://developers.openai.com/api/docs/pricing — ราคา GPT-4.1 $2/$8, GPT-4o $2.50/$10; business data ไม่ใช้ train by default
- [6] https://openai.com/business/pricing/ — เงื่อนไข business privacy

### Typhoon (SCB 10X)
- [7] https://opentyphoon.ai/ — โมเดล + API
- [8] https://www.scb10x.com/en/blog/introducing-typhoon-2-thai-llm — Typhoon 2 / API Pro (ร่วมกับ Together AI)
- [9] https://huggingface.co/scb10x/typhoon-7b — weight Apache 2.0, self-host ได้

### Azure Document Intelligence
- [12] https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/language-support/custom — รองรับ handwriting ภาษาไทย
- [13] https://azure.microsoft.com/en-us/pricing/details/document-intelligence/ — custom extraction $30/1,000 หน้า, free tier 500 หน้า/เดือน

### Delivery / Workflow
- [14] https://developers.line.biz/en/docs/messaging-api/pricing/ — เกณฑ์คิดเงิน Messaging API (นับตามผู้รับ, ส่งไม่ถึงไม่คิด)
- [15] https://www.facebook.com/LINEDEVTH/posts/451637085681209 — ประกาศปรับแผนราคา LINE OA ไทย
- [16] https://n8n.io/pricing/ — Community Edition self-host ฟรีไม่จำกัด execution
- [17] https://openhosst.com/blog/n8n-self-hosted-pricing — ต้นทุน VPS ~$5–7/เดือน
