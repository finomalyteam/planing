# Research Modules — checklist, query patterns, source tiers, rubric

ไฟล์นี้คือรายละเอียดของ 6 module ที่ SKILL.md อ้างถึง อ่านก่อนเริ่ม search ทุกครั้ง

## สารบัญ

1. [เกณฑ์ tier คุณภาพแหล่งข้อมูล + confidence level](#source-tiers)
2. [Module 1 — Problem & Demand](#module-1)
3. [Module 2 — Market Size & Timing](#module-2)
4. [Module 3 — Competition](#module-3)
5. [Module 4 — Feasibility](#module-4)
6. [Module 5 — Economics](#module-5)
7. [Module 6 — Strategy](#module-6)
8. [Rubric ให้คะแนนละเอียด](#rubric)
9. [ตัวอย่าง query pattern เต็มเคส (decumulation ตลาดไทย)](#example)

---

## <a id="source-tiers"></a>1. เกณฑ์ tier คุณภาพแหล่งข้อมูล + confidence level

| Tier | แหล่ง | ตัวอย่าง |
|---|---|---|
| Tier 1 | หน่วยงานรัฐ, regulator, งานวิจัยวิชาการ, สถิติทางการ | ธปท., ก.ล.ต., คปภ., สศช., สำนักงานสถิติแห่งชาติ, กบข./กอช., World Bank, OECD, paper ที่ peer-reviewed |
| Tier 2 | research house, บริษัทที่ปรึกษา, ข่าวธุรกิจที่อ้างแหล่งชัด, รายงานประจำปีบริษัท | SCB EIC, KKP Research, Krungsri Research, McKinsey/BCG, Bangkok Post, กรุงเทพธุรกิจ, annual report |
| Tier 3 | blog, ฟอรัม, social media, PR ของบริษัทขายของ, market research ที่ไม่เปิดวิธีคำนวณ | Pantip, Reddit, Medium, press release, "XX market to reach $YB by 2030" |

การติด confidence level ต่อ finding:

- **สูง** — มีแหล่ง tier 1 ยืนยัน หรือ tier 2 อย่างน้อย 2 แหล่งอิสระตรงกัน
- **กลาง** — tier 2 แหล่งเดียว หรือ tier 3 หลายแหล่งตรงกัน
- **ต่ำ** — tier 3 แหล่งเดียว, ข้อมูลเก่าเกิน 3 ปี, หรือเป็นการประมาณการของเราเอง

ตัวเลขที่คำนวณต่อจากหลายแหล่ง (เช่น SAM = TAM × สัดส่วน) ให้ติด confidence
ตามแหล่งที่อ่อนที่สุดในสูตร และแสดงสูตรคำนวณในรายงานเสมอ

ข้อมูลฟอรัม/social (tier 3) ยังมีค่าใน Module 1 และ 3 ในฐานะ "หลักฐานเชิงพฤติกรรม"
(คนบ่นอะไร ใช้อะไรแทน) — ใช้ได้แต่ห้ามใช้เป็นแหล่งตัวเลขตลาด

---

## <a id="module-1"></a>2. Module 1 — Problem & Demand

เป้าหมาย: พิสูจน์ว่าปัญหามีจริง ใหญ่จริง และคนรู้สึกถึงมัน (หรือยังไม่รู้สึก — ซึ่งก็คือ insight)

Checklist คำถามย่อย:

- [ ] กลุ่มเป้าหมายสนใจเรื่องนี้กี่ % — เทียบกับความสนใจเรื่องข้างเคียงที่ใหญ่กว่า
      (เช่น สนใจ "ชีวิตหลังเกษียณ" vs สนใจ "การลงทุน" เฉย ๆ)
- [ ] ระดับ awareness ปัจจุบัน — คนรู้ว่าตัวเองมีปัญหานี้ไหม หรือต้อง educate ก่อน
- [ ] Cost of inaction — คนที่ไม่มี/ไม่ใช้โซลูชันนี้ เจอผลลัพธ์อะไรจริง ๆ
      (หาเป็นตัวเลข เช่น % ที่เงินไม่พอ, มูลค่าความเสียหาย, คุณภาพชีวิต)
- [ ] ปัจจัยเชิงพฤติกรรม — ทำไมคนไม่ทำ/ไม่ซื้อ ทั้งที่ควร
      (present bias, ความรู้ไม่พอ, ไม่ไว้ใจ, ราคา, เข้าไม่ถึง)
- [ ] สถิติระดับประเทศของตลาดเป้าหมาย — % ประชากรที่อยู่ในปัญหานี้

Query pattern (แทน {topic} ด้วยหัวข้อไอเดีย):

- `สำรวจ {topic} คนไทย เปอร์เซ็นต์ 2567 2568`
- `{topic} survey Thailand statistics`
- `ผลกระทบ ไม่มี {topic} / consequences of not {doing X}`
- `ทำไมคนไทยไม่ {do X} สาเหตุ อุปสรรค` + `behavioral barriers {topic}`
- ค้นชื่อหน่วยงานที่น่าจะเคยสำรวจตรง ๆ เช่น `site:bot.or.th`, `สำนักงานสถิติแห่งชาติ {topic}`

## <a id="module-2"></a>3. Module 2 — Market Size & Timing

เป้าหมาย: แปลงความสนใจเป็นมูลค่าตลาดที่จับต้องได้ และตอบว่า "ทำไมต้องตอนนี้"

Checklist:

- [ ] TAM — มูลค่าตลาดรวมถ้าทุกคนที่มีปัญหาจ่าย (แสดงสูตร: จำนวนคน × ราคา/ปี)
- [ ] SAM — ส่วนที่เข้าถึงได้จริงด้วย model ของเรา (ตัดด้วยข้อจำกัดช่องทาง/segment)
- [ ] SOM — ส่วนที่ชิงได้จริงใน 3-5 ปี (เทียบ market share ของผู้เล่นใหม่ในตลาดใกล้เคียง)
- [ ] แนวโน้มโครงสร้าง — ประชากรศาสตร์ (สังคมสูงวัย, อัตราเกิด), รายได้, พฤติกรรมดิจิทัล
- [ ] "Why now" — catalyst อะไรทำให้ตอนนี้คือจังหวะ (กฎใหม่, เทคโนโลยีใหม่,
      พฤติกรรมเปลี่ยนหลังเหตุการณ์ใหญ่, โครงสร้างประชากรถึงจุดเปลี่ยน)

ข้อระวัง: อย่ารายงาน TAM จาก market research PR โดด ๆ — สร้าง TAM แบบ bottom-up
จากสถิติ tier 1 ควบคู่เสมอ แล้วรายงานทั้งสองค่าถ้าต่างกันมาก

Query pattern:

- `{topic} market size Thailand / Southeast Asia`
- `จำนวนประชากร {segment} ไทย สถิติ` (สร้าง bottom-up)
- `Thailand aging society projection สศช. / birth rate decline impact`
- `{topic} regulation change 2024 2025 2026` (หา why-now catalyst)

## <a id="module-3"></a>4. Module 3 — Competition

เป้าหมาย: รู้ว่าใครทำอยู่แล้ว ทำได้แค่ไหน คนใช้อะไรแทน และใครเคยตายเพราะอะไร

Checklist:

- [ ] ผู้เล่นตรงในไทย — ชื่อ, feature, ราคา, จำนวนผู้ใช้ (ถ้าหาได้)
- [ ] ผู้เล่นต่างประเทศที่เป็น best practice — เอาไว้เทียบว่าของไทยห่างแค่ไหน
- [ ] Substitutes — สิ่งที่คนใช้แทนจริง ๆ ตอนนี้ (Excel, ที่ปรึกษา, LINE group,
      "ไม่ทำอะไรเลย") — นี่คือคู่แข่งตัวจริงของ product ใหม่
- [ ] Pricing ของแต่ละเจ้า — model อะไร (subscription, AUM fee, freemium, ครั้งเดียว)
- [ ] ช่องทาง GTM ที่คู่แข่งใช้ — ขายผ่านธนาคาร, app store, ตัวแทน, B2B2C
- [ ] Failure cases — ใครเคยทำแล้วปิด/pivot และเพราะอะไร
      (ค้น: `{competitor} shut down`, `{topic} startup failed`, ข่าวปิดบริการ)
- [ ] รีวิว/complaint ของผู้ใช้จริงต่อเจ้าที่มีอยู่ — จุดอ่อนที่เราเสียบได้

## <a id="module-4"></a>5. Module 4 — Feasibility

เป้าหมาย: ตอบว่าสร้างได้จริงไหมใน constraint ของกฎหมาย เทคโนโลยี และข้อมูล

Checklist:

- [ ] Regulatory — license ที่ต้องมี, กฎที่คุมการให้คำแนะนำ/ตัวเงิน
      (ไทย: ก.ล.ต. เรื่อง investment advice/robo, ธปท. เรื่อง lending/payment,
      คปภ. เรื่องประกัน, PDPA เรื่องข้อมูลส่วนบุคคล — เลือกตามบริบทไอเดีย)
- [ ] มีทางเลี่ยง/sandbox ไหม — regulatory sandbox ของ ธปท./ก.ล.ต.,
      โครงสร้างแบบ education-only ที่ไม่ต้องขอ license
- [ ] เทคโนโลยี/แพลตฟอร์มที่ต้องใช้ — build vs buy, API ที่มีให้ต่อ
- [ ] Data availability — ข้อมูลที่โซลูชันต้องกินมีให้ใช้จริงไหมในตลาดนั้น
      (open data, API ธนาคาร, ต้องให้ผู้ใช้กรอกเอง?) ไอเดีย AI จำนวนมากตายตรงนี้
- [ ] Partnership — ใครมีลูกค้า/ข้อมูล/license อยู่แล้วที่เราเกาะได้
      (ธนาคาร, บลจ., บริษัทประกัน, นายจ้าง/HR platform)

## <a id="module-5"></a>6. Module 5 — Economics

เป้าหมาย: ตอบว่าคนยอมจ่ายไหม และ business model ยืนได้ไหม

Checklist:

- [ ] Willingness to pay — หลักฐานว่ากลุ่มเป้าหมายจ่ายเงินกับเรื่องนี้
      (ยอดขาย product ใกล้เคียง, ราคาที่จ่ายให้ที่ปรึกษา/คอร์ส, survey WTP)
- [ ] Pricing benchmark — ช่วงราคาที่ตลาดคุ้นเคยจาก Module 3
- [ ] CAC benchmark ของอุตสาหกรรม — fintech/สาย consumer มัก CAC สูง
      หาตัวเลขอ้างอิง (เช่น CAC ของ fintech app ใน SEA)
- [ ] LTV คร่าว ๆ — ราคา × retention ที่สมเหตุผล เทียบ CAC (เป้าหมาย LTV/CAC ≥ 3)
- [ ] Revenue model ทางเลือก — ถ้า B2C จ่ายยาก มี B2B/B2B2C ไหม
      (ขายให้ธนาคาร/นายจ้างแทนขายให้ผู้ใช้ตรง)

ตัวเลขฝั่ง economics มักเป็นการประมาณการ — แสดงสูตรและ assumption ทุกตัว
และติด confidence "ต่ำ" ถ้า input มาจาก tier 3

## <a id="module-6"></a>7. Module 6 — Strategy

เป้าหมาย: สังเคราะห์ทุก module เป็นคำตอบว่า "ถ้าจะทำ ต้องทำยังไงถึงชนะ"

Checklist:

- [ ] Competitive advantage ที่เป็นไปได้ — อะไรที่คู่แข่งเดิมทำตามยาก
      (data ที่เข้าถึงได้คนเดียว, segment ที่เจ้าใหญ่ไม่คุ้มจะลง, UX/ภาษา local,
      cost structure ที่ AI ทำให้ถูกกว่า 10 เท่า)
- [ ] Beachhead segment — กลุ่มแรกที่ควรตี: เจ็บที่สุด + เข้าถึงง่ายที่สุด + จ่ายไหว
      ระบุให้แคบพอที่จะทำ GTM ได้จริง
- [ ] ความเสี่ยงหลัก + mitigation — อย่างน้อย: trust (เรื่องเงินคนไม่ไว้ใจ startup),
      regulatory (กฎเปลี่ยน/ต้อง license), CAC สูงเกิน, incumbent ลอกได้เร็ว,
      data ไม่พอ — เลือกที่ relevant กับไอเดีย + ที่เจอเพิ่มจาก research
- [ ] Positioning ที่แนะนำ — หนึ่งประโยค: ขายอะไร ให้ใคร ต่างจากคู่แข่งยังไง

## <a id="rubric"></a>8. Rubric ให้คะแนนละเอียด

ทุกมิติให้ 1-5 อิงหลักฐานจาก module ที่เกี่ยว ห้ามให้คะแนนโดยไม่อ้างหลักฐาน

| มิติ | 1 | 3 | 5 |
|---|---|---|---|
| ขนาดปัญหา (M1) | ปัญหา niche คนเจ็บน้อย/ไม่รู้สึก | คนเจ็บจำนวนมากแต่ severity ปานกลาง | คนเจ็บมาก + severity สูง + มีสถิติยืนยัน |
| ขนาดตลาด (M2) | SOM เล็กจนไม่คุ้มสร้าง | SOM พอเลี้ยงธุรกิจขนาดกลาง | TAM ใหญ่ + โครงสร้างหนุนให้โตต่อ |
| การแข่งขัน-กลับด้าน (M3) | ตลาดแดงเดือด เจ้าใหญ่ครบ feature | มีผู้เล่นแต่ยังมีจุดอ่อนชัด | แทบไม่มีผู้เล่นตรง + substitutes อ่อน |
| Feasibility (M4) | ต้อง license หนัก + data ไม่มี | ทำได้แต่มีด่าน regulatory/data ที่ต้องแก้ | สร้างได้เลย ไม่ติด license + data หาได้ |
| Economics (M5) | ไม่มีหลักฐานว่าใครยอมจ่าย | จ่ายไหวแต่ CAC/LTV ตึง | WTP ชัด + LTV/CAC ≥ 3 มีทางไปได้ |
| ความได้เปรียบ (M6) | ไม่มีอะไรที่คู่แข่งลอกไม่ได้ | ได้เปรียบระยะสั้น ต้องรีบสร้าง moat | มี moat ชัด (data/ช่องทาง/cost) |

Verdict (รวม 30):

- **Go** — รวม ≥ 22 และไม่มีมิติไหนได้ 1
- **Conditional Go** — รวม 15-21 หรือรวม ≥ 22 แต่มีมิติที่ได้ 1
  → ระบุเงื่อนไขที่ต้องพิสูจน์/แก้ให้ชัดเป็นข้อ ๆ
- **No-Go** — รวม < 15 → ระบุว่าอะไรคือ dealbreaker และไอเดียข้างเคียงที่น่าไปดูแทน

## <a id="example"></a>9. ตัวอย่าง query pattern เต็มเคส (decumulation ตลาดไทย)

ตัวอย่างการแปลงไอเดีย "เครื่องมือวางแผนถอนเงินหลังเกษียณ (decumulation planning)
สำหรับตลาดไทย" เป็น query จริง — ใช้เป็นแบบเทียบเคียงเวลา map ไอเดียอื่น:

- M1: `สำรวจ คนไทย วางแผนเกษียณ เปอร์เซ็นต์`, `Thai retirement readiness survey`,
  `คนไทย เงินไม่พอใช้หลังเกษียณ สถิติ`, `ทำไมคนไทยไม่วางแผนเกษียณ`,
  `retirement planning vs investment interest survey`
- M2: `Thailand aging society 2030 projection สศช.`, `อัตราเกิดไทย ลดลง ผลกระทบ`,
  `retirement planning app market size`, จำนวนคนไทยอายุ 50-65 × ค่าบริการ/ปี
  (bottom-up TAM), `กองทุนสำรองเลี้ยงชีพ สมาชิก จำนวน` (proxy กลุ่มมีเงินก้อน)
- M3: `retirement planning app ไทย`, `robo-advisor ไทย เปรียบเทียบ`,
  `decumulation software Boldin NewRetirement pricing`, `Pantip วางแผนเกษียณ ใช้อะไร`
  (หา substitutes), `retirement app startup shut down`
- M4: `ก.ล.ต. investment advice license robo advisor`, `PDPA ข้อมูลการเงิน`,
  `กบข. API / open banking Thailand ข้อมูลบัญชี`
- M5: `ค่าบริการ นักวางแผนการเงิน CFP ไทย ราคา`, `fintech app CAC Southeast Asia`,
  `subscription willingness to pay financial app Thailand`
- M6: สังเคราะห์จาก M1-M5 — เช่น beachhead = พนักงานบริษัทอายุ 50+ ที่มี
  กองทุนสำรองเลี้ยงชีพ, ช่องทาง = ขายผ่าน HR/นายจ้าง (B2B2C) เลี่ยง CAC สูง
