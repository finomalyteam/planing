# Idea Deep Research: เครื่องมือวางแผนถอนเงินหลังเกษียณ (Decumulation Planning) สำหรับตลาดไทย

- **บริบท:** hackathon AI x finance (ทีม 5 คน, ~1 สัปดาห์)
- **ตลาดเป้าหมาย:** ไทย
- **วันที่ค้นคว้า:** 14 กรกฎาคม 2569 (2026-07-14) — วันที่เข้าถึงแหล่งอ้างอิงทุกรายการคือวันนี้
- **Hypothesis ที่ทดสอบ:** (1) คนไทยส่วนใหญ่ไม่วางแผนเกษียณ (2) คนสนใจ "การลงทุน" มากกว่า "ชีวิตหลังเกษียณ" (3) ตลาดไทยยังไม่มีเครื่องมือ decumulation

---

## บทสรุปผู้บริหาร

> **Verdict: CONDITIONAL GO — 21/30 คะแนน**
> ปัญหาใหญ่และมีหลักฐาน tier 1 รองรับหนักแน่น คู่แข่งตรงในไทยแทบไม่มี และมี "why now" ชัด (สังคมสูงวัยสุดยอดปี 2576 + เกณฑ์ Your Data ของ ธปท.) แต่ติดเงื่อนไขใหญ่คือ **ยังไม่มีหลักฐานว่าผู้บริโภคไทยยอมจ่าย (willingness to pay)** และ CAC ของ fintech app สูง — เส้นทางที่แนะนำคือเริ่มแบบ B2B2C (ขายผ่าน บลจ./นายจ้าง) และวางตัวเป็น education tool เพื่อเลี่ยงภาระ license ในช่วงแรก

ผล hypothesis: ข้อ (1) **ยืนยัน** — มีเพียง 16% ที่วางแผนและออมได้ตามแผน ข้อ (2) **ยืนยันบางส่วน** — 88% "คิดถึง" เรื่องเกษียณ แต่ action ต่ำมาก ขณะที่บัญชีลงทุนโตทำนิวไฮ ข้อ (3) **ยืนยันเกือบทั้งหมด** — มีแต่เครื่องคิดเลขฝั่งสะสม (accumulation) กับแอปวิชาการฟรี 1 ตัว ยังไม่มี decumulation orchestration เชิงพาณิชย์

---

## Module 1 — Problem & Demand

### 1.1 คนสนใจ "ชีวิตหลังเกษียณ" กี่ % เทียบกับสนใจ "การลงทุน"

| ตัวชี้วัด | ตัวเลข | ปี | แหล่ง | Confidence |
|---|---|---|---|---|
| คนไทยที่ "เริ่มคิดถึง" การวางแผนเกษียณ | 88% | 2566-67 | ผลสำรวจ อ้างใน [Workpoint Today](https://www.workpointtoday.com/super-aged-society-787576-2) | กลาง |
| วางแผนออมเพื่อเกษียณ **และทำได้ตามแผน** | 16% (ลดจาก 19% ปี 2561) | 2565 | สำรวจทักษะการเงิน สสช./ธปท. อ้างใน [PIER](https://www.pier.or.th/blog/2024/0801/) | สูง |
| ไม่ได้คิด/วางแผนเรื่องออมเพื่อเกษียณเลย | 19% (เพิ่มจาก 15% ปี 2563) | 2565 | [PIER](https://www.pier.or.th/blog/2024/0801/) | สูง |
| ดัชนีความพร้อมเกษียณ NRRI | 49.30/100 (ลดจาก 56.70 ปี 2563) | 2566 | Chulalongkorn Business School อ้างใน [PIER](https://www.pier.or.th/blog/2024/0801/) | สูง |
| บัญชีซื้อขายหลักทรัพย์ (ฝั่ง "ลงทุน") | 5.2 ล้านบัญชี — นิวไฮ | 2564 | [ตลท. อ้างใน กรุงเทพธุรกิจ](https://www.bangkokbiznews.com/business/993438) | สูง |

**การตีความ:** ความสนใจ "คิดถึง" เกษียณสูงถึง 88% แต่ conversion ไปสู่การวางแผนจริงเหลือ 16% — ช่องว่างระหว่าง intention กับ action คือ ~72 จุด ขณะที่ฝั่งการลงทุนคนแห่เปิดบัญชีทำนิวไฮ สะท้อนว่าพลังงานของคนไปลงที่ "ทำเงินโต" ไม่ใช่ "วางแผนใช้เงินให้พอ" (Confidence: กลาง — เป็นการเทียบ proxy คนละสำรวจ)

### 1.2 ผลลัพธ์จริงของคนที่ไม่วางแผน (cost of inaction)

- ผู้สูงอายุไทย **44% ไม่มีเงินออม** และ **42.7% มีหนี้** เฉลี่ย 130,505 บาท/คน (ภาระผ่อน ~2,208 บาท/เดือน) — [กรมกิจการผู้สูงอายุ](https://www.dop.go.th/th/know/15/465) (Confidence: สูง)
- ค่าใช้จ่ายเฉลี่ยผู้สูงอายุ ~8,125 บาท/เดือน ขณะที่เบี้ยยังชีพสูงสุด 1,000 บาท/เดือน — [กรมกิจการผู้สูงอายุ](https://www.dop.go.th/th/know/15/465) (Confidence: สูง)
- ผู้สูงอายุ >50% พึ่งรายได้จากลูกเป็นหลัก มีเพียง 4.4% ที่มีบำเหน็จบำนาญ — [กรมกิจการผู้สูงอายุ](https://www.dop.go.th/th/know/15/465) (Confidence: สูง)
- งานวิจัยชี้คนไทย **82% เสี่ยงมีเงินไม่พอใช้หลังเกษียณ** ทั้งที่อายุยืนขึ้น — [กรุงเทพธุรกิจ](https://www.bangkokbiznews.com/business/economic/1175834) (Confidence: กลาง)
- ผู้สูงอายุ ~88% ไม่เคยเตรียมการด้านสุขภาพ/การเงินอย่างเจาะจงก่อนวัยเกษียณ (โรงพยาบาล) — งานวิจัยอ้างใน [Thailand Business News](https://www.thailand-business-news.com/banking/151693-are-thai-people-ready-for-retirement) (Confidence: กลาง)
- ครึ่งหนึ่งของวัยทำงานไทยไม่พร้อมหยุดทำงานเมื่อถึงวัยเกษียณ — [Nation Thailand](https://www.nationthailand.com/thailand/general/40033964) (Confidence: กลาง)

### 1.3 อีกด้านของปัญหา: เกษียณแล้ว "ไม่กล้าใช้เงิน"

หลักฐานเชิงพฤติกรรมจากฟอรัม (tier 3 — ใช้เป็นหลักฐานพฤติกรรม ไม่ใช่ตัวเลขตลาด): กระทู้ Pantip จำนวนมากสะท้อนความกลัวเงินหมดหลังได้เงินก้อนสุดท้าย เช่น ["ผมควรทำยังไงกับเงินก้อนสุดท้ายของชีวิตดีครับ"](https://pantip.com/topic/38969747), ["ผมเป็นโรคกลัวการใช้เงิน"](https://pantip.com/topic/42325446), กรณีจำกัดตัวเองใช้ไม่เกิน 5,000 บาท/เดือนเพราะเคยลงทุนขาดทุน — decumulation มีปัญหา 2 ขั้ว: ใช้เปลืองจนหมด กับ กลัวจนไม่มีคุณภาพชีวิต ทั้งคู่คือ demand ของเครื่องมือนี้ (Confidence: กลาง — หลายแหล่งอิสระตรงกัน)

### 1.4 ปัจจัยที่ทำให้คนไม่โฟกัสเงินหลังเกษียณ

จาก [ThaiPFA](https://www.thaipfa.co.th/news/view/508) และ [TISCO Wealth](https://www.tiscowealth.com/trust-magazine/holistic-financial-advisory-63/): (1) ไม่รู้จะเริ่มยังไง / ขาดความรู้การเงิน (2) รู้สึกว่าซับซ้อนเกินไปจนไม่เริ่ม (3) present bias — "ยังหนุ่ม เดี๋ยวค่อยเก็บ" (4) มองอนาคตไม่ชัด รายได้ไม่แน่นอน ส่วน Gen Z มองการออมเกษียณเป็น "เรื่องไกลตัว" ให้ลำดับความสำคัญกับออมฉุกเฉินและท่องเที่ยวก่อน และเกือบครึ่งมี mindset "ใช้ตอนนี้สุขกว่าเก็บ" — [Spring News](https://www.springnews.co.th/lifestyle/spring-life/863392) (Confidence: กลาง)

---

## Module 2 — Market Size & Timing

### 2.1 ฐานประชากร (bottom-up, tier 1)

ทะเบียนราษฎร ณ มกราคม 2568 ([กรมการปกครอง](https://www.bora.dopa.go.th/wp-content/uploads/2025/02/pop_age_country_6801.pdf)):

| ช่วงอายุ | จำนวน (คน) |
|---|---|
| 51-55 ปี | 5,028,812 |
| 56-60 ปี | 4,842,737 |
| 61-65 ปี | 4,124,412 |
| **รวม 51-65 ปี (กลุ่มเป้าหมายหลัก)** | **~13.99 ล้านคน** |

ผู้สูงอายุ 60+ = 14.03 ล้านคน (20.0% ของประชากร) ปี 2567 — [สำรวจ สสช. อ้างผ่านผลค้นหา NSO](https://www.nso.go.th/nsoweb/storage/survey_detail/2025/20241209145003_27188.pdf) (Confidence: สูง)

### 2.2 TAM / SAM / SOM (ประมาณการ — แสดงวิธีคิด)

> ตัวเลขในส่วนนี้เป็น**การประมาณการของผู้วิเคราะห์** จาก input ที่มีอ้างอิง — Confidence: ต่ำ-กลาง ตามแหล่งที่อ่อนที่สุดในสูตร

- **TAM (B2C):** ประชากร 51-65 ปี ~14.0 ล้านคน × สมมติราคา subscription เทียบเคียง Boldin (~1,500-5,200 บาท/ปี — ดู Module 5) → เพดานทฤษฎี ~21,000-72,800 ล้านบาท/ปี แต่ตัวเลขนี้ไม่สมจริงเพราะ WTP ไทยต่ำกว่ามาก
- **SAM:** กลุ่มที่มีเงินก้อนให้บริหารจริง — สมาชิกกองทุนสำรองเลี้ยงชีพ ~3 ล้านคน, AUM ~1.1 ล้านล้านบาท ([World Bank FSAP Thailand](https://documents1.worldbank.org/curated/en/858671571260308391/pdf/Thailand-Financial-Sector-Assessment-Program-Technical-Note-Funded-Pension-System.pdf) — ข้อมูลปี 2019, Confidence: กลาง; ตัวเลขปัจจุบันดูได้ที่ [สถิติ ก.ล.ต.](https://market.sec.or.th/public/idisc/en/CapitalMarketReport/PP28)) + สมาชิก กบข. + ข้าราชการบำนาญ — คร่าว ๆ 4-5 ล้านคนที่มี "เงินก้อน + เงินงวด" ให้วางแผน
- **SOM (3-5 ปี, เส้นทาง B2B2C):** จับผ่าน บลจ./นายจ้าง — ถ้าได้พาร์ตเนอร์ บลจ. ที่ดูแล PVD 2-3 ราย เข้าถึงสมาชิกได้หลักแสนถึงล้านคน คิด revenue แบบ per-member-per-year 50-150 บาท → ~25-150 ล้านบาท/ปี (ประมาณการล้วน — Confidence: ต่ำ)

### 2.3 แนวโน้มระดับประเทศ + ประชากรศาสตร์

- ไทยเป็นสังคมสูงวัยสมบูรณ์แล้ว (60+ = 20%) และคาดเข้าสู่ **super-aged society (>30% ผู้สูงอายุ) ราวปี 2576**; ปี 2583 คาดสัดส่วน 31.3% — สศช. อ้างใน [Policy Watch Thai PBS](https://policywatch.thaipbs.or.th/article/life-100) และ [มส.ผส.](https://thaitgri.org/?p=39327) (Confidence: สูง)
- เด็กเกิดใหม่ **ต่ำสุดรอบ 75 ปี**: 461,421 คน (2567) → 416,574 คน (2568), TFR เหลือ ~0.86, ตายมากกว่าเกิดต่อเนื่องปีที่ 5 — [กรุงเทพธุรกิจ](https://www.bangkokbiznews.com/health/public-health/1215717), [The Prachakorn/IPSR มหิดล](https://www.theprachakorn.com/newsDetail.php?id=1085) (Confidence: สูง)
- **นัยต่อไอเดีย:** โครงสร้าง "ลูกเลี้ยงพ่อแม่" ที่วันนี้เป็นรายได้หลักของผู้สูงอายุ >50% กำลังพังลงเพราะรุ่นลูกมีจำนวนน้อยลงเรื่อย ๆ — คนรุ่นต่อไป **จำเป็น** ต้องพึ่งเงินก้อนตัวเองแบบมีระบบมากขึ้น นี่คือแรงลมหนุนเชิงโครงสร้างระยะ 10-20 ปี

### 2.4 Why now — catalyst

1. **เกณฑ์ Your Data ของ ธปท.** ออกแล้ว 30 ต.ค. 2568 — ประชาชนใช้สิทธิส่งข้อมูลเงินฝากของตัวเองให้ผู้ให้บริการอื่นได้ เริ่มใช้จริง**ปลายปี 2569** (เงินฝากบุคคลธรรมดาก่อน แล้วขยายสินเชื่อ/บัตร 2570-71) — [ธปท.](https://www.bot.or.th/th/news-and-media/news/news-20251110.html), [ThaiPublica](https://thaipublica.org/2025/11/bank-of-thailand-issued-regulations-under-your-data-project/) → เครื่องมือ decumulation จะดึงข้อมูลจริงได้แทนให้ผู้ใช้กรอกเอง (Confidence: สูง)
2. **กองทุนสงเคราะห์ลูกจ้าง** บังคับใช้ 1 ต.ค. 2569 และการผลักดัน กบช./การออมภาคบังคับ — [ศูนย์บริการข้อมูลภาครัฐ](https://gcc.go.th/2025/05/16/%E0%B8%81%E0%B8%AD%E0%B8%87%E0%B8%97%E0%B8%B8%E0%B8%99%E0%B8%AA%E0%B8%87%E0%B9%80%E0%B8%84%E0%B8%A3%E0%B8%B2%E0%B8%B0%E0%B8%AB%E0%B9%8C%E0%B8%A5%E0%B8%B9%E0%B8%81%E0%B8%88%E0%B9%89%E0%B8%B2%E0%B8%87/) → เงินก้อนตอนออกจากงานจะกลายเป็นเรื่องของแรงงานทุกคน (Confidence: สูง)
3. คลื่นคนเกษียณลูกใหญ่: กลุ่ม 51-60 ปี ~9.9 ล้านคนจะทยอยเกษียณใน 10 ปีข้างหน้า (คำนวณจากตาราง 2.1)

---

## Module 3 — Competition

### 3.1 ผู้เล่นในไทย

| ผู้เล่น | สิ่งที่ทำ | จุดอ่อนเทียบไอเดียเรา | แหล่ง |
|---|---|---|---|
| เครื่องคำนวณเกษียณของ SET ([Happy Money](https://www.set.or.th/th/education-research/education/happymoney/pre-retirement)), [กรุงศรี](https://www.krungsri.com/th/calculator/life-plan/plan-for-retirement), [ธ.กรุงเทพ](https://www.bangkokbank.com/th-TH/Personal/Save-And-Invest), [KAsset](https://assetallocation.kasikornasset.com/RetirementPlan), [GSB](https://oomtang.gsb.or.th/financial/retirement_plan_tool), [KTAM](https://smarttrade.ktam.co.th/smarttrade/pvdweb/index.php?page=retire_rich&sm=1) | เครื่องคิดเลข one-shot ฝั่ง **สะสม** ("ต้องออมเดือนละเท่าไหร่") | ไม่ทำ decumulation ต่อเนื่อง ไม่ track จริง ไม่ปรับตามตลาด/เงินเฟ้อรายปี | ตามลิงก์ |
| **Chula Wealth Plus** — แอปฟรีจากคณะบัญชีฯ จุฬาฯ | ประเมินความพอเพียงของเงินออม + **มี withdrawal rate planning** (ถอนได้เดือนละเท่าไหร่ อยู่ได้กี่ปี) | แอปวิชาการ ไม่มี business model, ไม่เชื่อมข้อมูลจริง, ไม่มี engagement ต่อเนื่อง — คู่แข่งใกล้เคียงที่สุดแต่ยังห่าง | [จุฬาฯ](https://www.chula.ac.th/highlight/81392/) |
| Robo-advisors: [Finnomena](https://www.finnomena.com/planet46/what-is-robo-advisor/) (แผน Goal, ไม่เก็บค่าบริการเพิ่ม), [StashAway](https://www.stashaway.co.th/), [odini](https://odiniapp.com/support/) (20 บาท/เดือน) | จัดพอร์ตอัตโนมัติฝั่งสะสม มีเป้าเกษียณ | โฟกัส accumulation; ไม่มีตัวไหนทำ "แผนถอน + ภาษี + ประกันสังคม/เบี้ยยังชีพ + ลำดับการถอนจากบัญชีไหนก่อน" | ตามลิงก์ |

**สรุป:** ยังไม่พบผู้เล่นไทยที่ทำ decumulation orchestration เชิงพาณิชย์ (แผนถอนรายเดือนต่อเนื่อง + ภาษี + แหล่งรายได้รัฐ) — ยืนยัน hypothesis ข้อ 3 โดยมีข้อแม้ว่า Chula Wealth Plus แตะเรื่องนี้แล้วแบบฟรี/วิชาการ (Confidence: กลาง — อาจมี product ใหม่ที่ยังไม่ index)

### 3.2 ผู้เล่นต่างประเทศ (best practice + ราคา)

- **Boldin (เดิม NewRetirement, สหรัฐฯ):** DIY planner ครบวงจร รวม decumulation, Roth conversion, ภาษี — ฟรี + PlannerPlus **$120-144/ปี** — [Boldin Pricing](https://www.boldin.com/retirement/pricing/) (Confidence: สูง)
- **IncomeLab (สหรัฐฯ):** แพลตฟอร์มสำหรับ retiree ฝั่ง decumulation โดยเฉพาะ (ขายที่ปรึกษาเป็นหลัก, personal license **$20/เดือน**) — [Rob Berger](https://robberger.com/best-retirement-calculators/) (Confidence: กลาง)
- **MaxiFi:** เด่นเรื่อง tax + decumulation phase — [White Coat Investor](https://www.whitecoatinvestor.com/best-retirement-calculators-2025/) (Confidence: กลาง)

### 3.3 Failure case ที่ต้องเรียนรู้

- **Kindur (สหรัฐฯ):** ระดมทุน >$10M ทำ decumulation B2C เต็มรูปแบบ (เงินเดือนหลังเกษียณ + ภาษี + RMD) → แข่ง B2C ไม่รอด **pivot เป็น Silvur ขาย B2B2C ผ่าน credit unions / สถาบันการเงิน** ในรูป white-label retirement education — [Forbes](https://www.forbes.com/sites/ashleaebeling/2019/07/30/make-it-last-fintech-firm-solves-number-one-retirement-fearoutliving-your-money/), [Silvur](https://www.silvur.com/), [Businesswire](https://www.businesswire.com/news/home/20210427005697/en/Silvur-Launches-First-of-its-Kind-Membership-for-the-Modern-Retiree-in-a-Post-Pension-World) (Confidence: กลาง)
- บทวิเคราะห์ [Nex Cubed](https://www.nex3.com/blog/2020/04/22/decumulation-fintechs-unsolved-challenge) ชี้ว่า decumulation คือ "โจทย์ที่ fintech ยังแก้ไม่ตก" เพราะ (1) ซับซ้อนกว่าฝั่งออมมาก (2) **AUM fee model ขัดแรงจูงใจ** — พอร์ตหดลงเรื่อย ๆ รายได้ที่ปรึกษาก็หด (3) ทุกโซลูชันมี trade-off ระหว่างกันเงินหมดกับพลาด upside (Confidence: กลาง)
- **บทเรียนเข้าทางเรา:** อย่าเริ่ม B2C ล้วน และอย่าคิดค่าบริการแบบ % AUM — flat fee / per-member B2B2C คือโครงสร้างที่รอดกว่า

### 3.4 Substitutes (คู่แข่งตัวจริง)

ถามกันเองใน Pantip, ฝากประจำ/สลาก, พึ่งพนักงานขายธนาคาร-ประกัน (มี conflict of interest เพราะขายของ), Excel ทำเอง, และ "ไม่ทำอะไรเลย" — จากหลักฐาน Module 1 คนกลุ่มใหญ่สุดคือกลุ่มสุดท้าย ประกันบำนาญ (annuity) ซึ่งเป็นโซลูชัน decumulation แบบดั้งเดิมมีสัดส่วนเล็กในตลาดประกันชีวิตไทย (เบี้ยประกันชีวิตรวม 3.5% ของ GDP) — [คปภ./SET Group](https://media.setgroup.or.th/setlink/Documents/2025/Apr/แนวโน้มธุรกิจกลุ่มบริษัทประกันภัย.pdf) (Confidence: ต่ำ — ไม่พบตัวเลข annuity แยกชัด; ค้นด้วย "ประกันบำนาญ ยอดขาย สัดส่วน คปภ." แล้วไม่พบสถิติจำเพาะ)

---

## Module 4 — Feasibility

### 4.1 Regulatory

- การให้ "คำแนะนำการลงทุน" เป็นธุรกิจต้องมี**ใบอนุญาตที่ปรึกษาการลงทุน (IA)** จาก ก.ล.ต. และ robo-advisor ต้องเปิดเผยหลักการของ algorithm, ขอบเขตคำแนะนำ — [ThaiPublica](https://thaipublica.org/2019/12/pises-robo-advisor-21/), [FAQ ก.ล.ต.](https://www.sec.or.th/TH/DOCUMENTS/INTERMEDIARIES/FAQ-INTERMEDIARIES.PDF) (Confidence: กลาง)
- ทางเลี่ยงช่วงแรก: วางตัวเป็น **เครื่องมือให้ความรู้/คำนวณ (financial education tool)** ที่ไม่แนะนำผลิตภัณฑ์เจาะจง — แบบเดียวกับเครื่องคำนวณของ SET/ธนาคาร และ Chula Wealth Plus ที่เปิดให้ใช้ฟรีโดยไม่ต้องมี license ที่ปรึกษาการลงทุน (Confidence: กลาง — ควรตรวจกับที่ปรึกษากฎหมายก่อนทำจริง)
- PDPA ใช้กับข้อมูลการเงินส่วนบุคคลเต็มรูปแบบ
- สำหรับ hackathon: ใช้ mock data → ไม่มีประเด็น regulatory ในเดโม แต่ต้องเล่าเส้นทาง license ให้กรรมการฟังได้

### 4.2 เทคโนโลยี

องค์ประกอบหลัก: (1) simulation engine (Monte Carlo / sequence-of-returns risk) — ไลบรารีเปิดมีพร้อม (2) กติกาภาษี+สิทธิรัฐไทย (ประกันสังคม บำนาญ/บำเหน็จ, เบี้ยยังชีพ, ภาษีถอน PVD/RMF) — เป็น rule-based เขียนเองได้ (3) LLM สำหรับอธิบายแผนเป็นภาษาคน/แชต — จุดขาย AI ที่เดโมง่ายใน 1 สัปดาห์ ไม่มีเทคโนโลยีที่ต้องรอใคร (Confidence: สูง — ประเมินเชิงวิศวกรรม)

### 4.3 Data availability

- **วันนี้:** ต้องให้ผู้ใช้กรอกเอง (ยอด PVD, เงินฝาก, ประกันสังคม) — friction สูง แต่ Chula Wealth Plus พิสูจน์แล้วว่า flow แบบกรอกเองใช้ได้ระดับหนึ่ง
- **ปลายปี 2569 เป็นต้นไป:** เกณฑ์ Your Data เปิดให้ดึงข้อมูลเงินฝากบุคคลธรรมดาข้ามสถาบันด้วย consent ของผู้ใช้ → roadmap ธรรมชาติของ product นี้ ([ธปท.](https://www.bot.or.th/th/news-and-media/news/news-20251110.html); Confidence: สูง)

### 4.4 Partnership ที่เป็นไปได้

บลจ. ที่บริหาร PVD (มี "moment ที่สมาชิกกำลังจะได้เงินก้อน" อยู่ในมือ), นายจ้าง/HR (สวัสดิการ pre-retirement), บริษัทประกัน (ขาย annuity ต่อท้ายแผน), กบข./กอช. — โมเดลเดียวกับที่ Silvur ทำกับ credit unions ในสหรัฐฯ

---

## Module 5 — Economics

### 5.1 Willingness to pay

- **ไม่พบผลสำรวจ WTP ตรง ๆ ของคนไทยต่อเครื่องมือวางแผนเกษียณ** (ค้น: "subscription willingness to pay financial app Thailand", "คนไทย ยอมจ่าย แอปการเงิน") — นี่คือความไม่แน่นอนหลักของไอเดีย (Confidence: —)
- Anchor ที่มี: CFP ไทยคิด **500-5,000 บาท/ครั้ง** หรือ 1,000-5,000 บาท/ชม. หรือ 0.5-1.0% AUM — [CMSK Academy](https://cmsk-academy.com/article/624/income-cfp) (Confidence: กลาง); odini เก็บเพียง 20 บาท/เดือน และยังต้อง waive — [odini FAQ](https://odiniapp.com/support/) (Confidence: กลาง); Boldin เก็บ $120-144/ปีในตลาดสหรัฐฯ ที่ WTP สูงกว่า
- **การตีความ:** B2C ไทยน่าจะจ่ายได้ระดับร้อยบาท/เดือนในกลุ่มแคบ — ไม่พอเลี้ยงธุรกิจถ้า CAC สูง → ชี้ไปทาง B2B2C

### 5.2 CAC / unit economics

- Marketing spend ของ financial apps ใน SEA เฉลี่ย **>$200 (~7,000 บาท) ต่อลูกค้า 1 คน** (AppsFlyer อ้างใน [Salesworks](https://salesworksgroup.com/sg/media-centre/blog/customer-acquisition-cost-in-southeast-asia-whats-a-good-benchmark/)) และ CAC สาย fintech เพิ่ม 40-60% ช่วงปี 2566-68 ([First Page Sage](https://firstpagesage.com/seo-blog/fintech-cac-benchmarks-report/)) (Confidence: กลาง)
- ถ้า B2C เก็บ 100 บาท/เดือน (1,200 บาท/ปี) ต้อง retain เกิน ~6 ปีถึงคุ้ม CAC 7,000 บาท → **B2C ล้วนไม่ผ่าน LTV/CAC ≥ 3** (ประมาณการ; Confidence: ต่ำ)
- B2B2C per-member fee ผ่าน บลจ./นายจ้าง ตัด CAC เกือบหมด — โครงสร้างเดียวที่ตัวเลขมีทางบวก และตรงกับบทเรียน Kindur→Silvur

---

## Module 6 — Strategy

### 6.1 Competitive advantage ที่สร้างได้

1. **ความซับซ้อนเฉพาะไทยคือ moat:** แผนถอนที่รวมประกันสังคม (บำนาญ/บำเหน็จ), เบี้ยยังชีพผู้สูงอายุ, ภาษีเงินก้อน PVD/RMF, กบข. — เครื่องมือ global ทำไม่ได้ และเครื่องคิดเลขธนาคารไทยยังไม่รวมทุกแหล่ง (SET รวมบางส่วน)
2. **AI conversational layer:** อธิบายแผนถอนเป็นภาษาคน ("เดือนนี้ถอนจากบัญชีไหน เท่าไหร่ เพราะอะไร") — แก้ pain "ซับซ้อนเกินไปจนไม่เริ่ม" จาก Module 1.4 โดยตรง และเป็นสิ่งที่เครื่องคิดเลข static ทำไม่ได้
3. **จังหวะ Your Data:** ผู้เล่นที่วางโครงรองรับ consent-based data ก่อนปลายปี 2569 จะได้เปรียบตอนเกณฑ์เปิดจริง

### 6.2 Beachhead segment

**พนักงานเอกชนอายุ 55-60 ที่เป็นสมาชิกกองทุนสำรองเลี้ยงชีพ** — กำลังจะได้เงินก้อนใหญ่ที่สุดในชีวิตภายใน 5 ปี, เข้าถึงได้เป็นกลุ่มก้อนผ่าน บลจ./นายจ้าง (ไม่ต้องจ่าย CAC รายคน), เจ็บจริง (กระทู้ Pantip ส่วนใหญ่คือคนกลุ่มนี้), และมีเงินให้วางแผนจริง (~3 ล้านคน)

### 6.3 ความเสี่ยงหลัก + mitigation

| ความเสี่ยง | ระดับ | Mitigation |
|---|---|---|
| WTP ฝั่ง B2C ต่ำ/ไม่มีหลักฐาน | สูง | ไป B2B2C ตั้งแต่แรก; B2C ใช้ freemium เป็น funnel |
| Trust — เรื่องเงินก้อนสุดท้าย คนไม่ไว้ใจ startup | สูง | ขายผ่านแบรนด์ที่คนไว้ใจอยู่แล้ว (บลจ./นายจ้าง) = ข้อดีอีกชั้นของ B2B2C |
| Regulatory — เส้นแบ่ง education vs investment advice | กลาง | เฟสแรก education-only ไม่แนะนำผลิตภัณฑ์เจาะจง; ปรึกษากฎหมายก่อน scale |
| Incumbent (บลจ./ธนาคาร) ทำเอง | กลาง | เร็วกว่า + ขายเป็น white-label ให้เขาเลย (เป็นพาร์ตเนอร์ ไม่ใช่คู่แข่ง) |
| ความแม่นของโมเดล (sequence risk, เงินเฟ้อ) ผิดแล้วคนเจ็บจริง | กลาง | แสดงช่วงความไม่แน่นอนเสมอ ไม่ฟันธงตัวเลขเดียว; disclaimers ชัด |

### 6.4 Positioning ที่แนะนำ

> "ผู้ช่วย AI ที่เปลี่ยนเงินก้อนสุดท้าย + สิทธิจากรัฐ ให้กลายเป็น 'เงินเดือนหลังเกษียณ' ที่ปลอดภัย — เริ่มจากสมาชิกกองทุนสำรองเลี้ยงชีพ ส่งมอบผ่าน บลจ. และนายจ้าง"

---

## ตารางคะแนน Rubric

| มิติ | คะแนน (1-5) | เหตุผลอิงหลักฐาน |
|---|---|---|
| 1. ขนาดปัญหา | **5** | ผู้ได้รับผลกระทบ ~14 ล้านคน (51-65 ปี), severity สูง (44% ผู้สูงอายุไม่มีเงินออม, ค่าใช้จ่าย 8 เท่าของเบี้ยยังชีพ), หลักฐาน tier 1 หลายชิ้น |
| 2. ขนาดตลาด | **3** | ฐานคนใหญ่และโตแน่ (super-aged 2576) แต่มูลค่าที่เก็บได้จริงถูกกดด้วย WTP; SOM ทาง B2B2C ระดับสิบ-ร้อยล้านบาท/ปี |
| 3. การแข่งขัน (กลับด้าน) | **4** | ไม่มีผู้เล่นเชิงพาณิชย์ตรงในไทย; ใกล้สุดคือแอปวิชาการฟรี + เครื่องคิดเลข static; substitutes อ่อน (ถามกันเอง/ไม่ทำอะไร) — หัก 1 เพราะ incumbent ลอกได้ |
| 4. Feasibility | **4** | เฟส education ไม่ติด license, เทคโนโลยีพร้อมหมด, demo ได้ใน 1 สัปดาห์; หัก 1 เพราะข้อมูลจริงต้องรอ Your Data ปลายปี 2569 |
| 5. Economics | **2** | ไม่มีหลักฐาน WTP ไทยตรง ๆ, CAC fintech SEA >$200 ทำให้ B2C ล้วนไม่ผ่าน LTV/CAC; ทางรอดเดียวคือ B2B2C ที่ยังต้องพิสูจน์ |
| 6. ความได้เปรียบ | **3** | ความซับซ้อนเฉพาะไทย + AI layer + จังหวะ Your Data เป็นแต้มต่อระยะสั้น แต่ยังไม่ใช่ moat ถาวร ต้องรีบสร้าง data/partnership lock-in |
| **รวม** | **21/30** | **Conditional Go** (เกณฑ์: 15-21) |

## Verdict: CONDITIONAL GO — เงื่อนไขที่ต้องแก้/พิสูจน์

1. **พิสูจน์เส้นทางรายได้ B2B2C** — ก่อนลงแรงเกิน hackathon ต้องคุยกับ บลจ./HR อย่างน้อย 2-3 ราย ว่ายอมจ่าย per-member fee ไหม (Kindur พิสูจน์แล้วว่า B2C ล้วนตาย)
2. **อยู่ฝั่ง education-only จนกว่าจะพร้อมขอ license** — ห้ามแนะนำผลิตภัณฑ์เจาะจงในเดโม/เฟสแรก
3. **สำหรับ hackathon: เดโมต้องเล่น "moment เงินก้อน PVD ออก"** — input ง่าย ๆ แล้วโชว์แผนถอนรายเดือน + AI อธิบายภาษาคน + กราฟเงินอยู่ได้ถึงอายุเท่าไหร่ พร้อมช่วงความไม่แน่นอน — นี่คือส่วนที่ยังไม่มีใครในไทยโชว์ได้

---

## แหล่งอ้างอิง (เข้าถึงทั้งหมดวันที่ 14 ก.ค. 2569)

### Tier 1 — หน่วยงานรัฐ / regulator / วิชาการ

1. PIER (สถาบันวิจัยเศรษฐกิจป๋วย อึ๊งภากรณ์) — คนไทยพร้อมแค่ไหนกับการเกษียณอายุ — https://www.pier.or.th/blog/2024/0801/
2. กรมการปกครอง — จำนวนประชากรไทยแบ่งช่วงอายุ ม.ค. 2568 — https://www.bora.dopa.go.th/wp-content/uploads/2025/02/pop_age_country_6801.pdf
3. กรมกิจการผู้สูงอายุ — ปัญหาใหญ่ของคนไทย "สูงวัยแต่ไม่รวย" — https://www.dop.go.th/th/know/15/465
4. สำนักงานสถิติแห่งชาติ — สำรวจประชากรสูงอายุ — https://www.nso.go.th/nsoweb/storage/survey_detail/2025/20241209145003_27188.pdf
5. ธปท. — ข่าวเกณฑ์ Your Data — https://www.bot.or.th/th/news-and-media/news/news-20251110.html
6. ธปท. — Open Data / Open Banking — https://www.bot.or.th/th/financial-innovation/digital-finance/open-data.html
7. ศูนย์บริการข้อมูลภาครัฐ — กองทุนสงเคราะห์ลูกจ้าง เริ่ม 1 ต.ค. 2569 — https://gcc.go.th/2025/05/16/กองทุนสงเคราะห์ลูกจ้าง/
8. ก.ล.ต. — FAQ เกณฑ์ประกอบธุรกิจตัวกลาง — https://www.sec.or.th/TH/DOCUMENTS/INTERMEDIARIES/FAQ-INTERMEDIARIES.PDF
9. ก.ล.ต. — สถิติกองทุนสำรองเลี้ยงชีพ — https://market.sec.or.th/public/idisc/en/CapitalMarketReport/PP28
10. World Bank — Thailand FSAP: Funded Pension System — https://documents1.worldbank.org/curated/en/858671571260308391/pdf/Thailand-Financial-Sector-Assessment-Program-Technical-Note-Funded-Pension-System.pdf
11. จุฬาลงกรณ์มหาวิทยาลัย — Chula Wealth Plus — https://www.chula.ac.th/highlight/81392/
12. มูลนิธิสถาบันวิจัยและพัฒนาผู้สูงอายุไทย (มส.ผส.) — คาดการณ์ผู้สูงอายุ 31% — https://thaitgri.org/?p=39327
13. สถาบันวิจัยประชากรและสังคม ม.มหิดล (The Prachakorn) — เด็กเกิด 6 เดือนแรกปี 2568 — https://www.theprachakorn.com/newsDetail.php?id=1085

### Tier 2 — research house / ข่าวธุรกิจ / บริษัท

14. Workpoint Today — ผลสำรวจ 88% คิดเรื่องเกษียณมากขึ้น — https://www.workpointtoday.com/super-aged-society-787576-2
15. กรุงเทพธุรกิจ — 82% เสี่ยงเงินไม่พอใช้หลังเกษียณ — https://www.bangkokbiznews.com/business/economic/1175834
16. กรุงเทพธุรกิจ — เด็กเกิดใหม่ต่ำสุดรอบ 75 ปี — https://www.bangkokbiznews.com/health/public-health/1215717
17. กรุงเทพธุรกิจ — บัญชีหุ้นนิวไฮ 5.2 ล้านบัญชี ปี 2564 — https://www.bangkokbiznews.com/business/993438
18. Policy Watch Thai PBS — โฉมหน้าสังคมสูงวัยอย่างสมบูรณ์ — https://policywatch.thaipbs.or.th/article/life-100
19. Nation Thailand — 50% ของวัยทำงานไม่พร้อมเกษียณ — https://www.nationthailand.com/thailand/general/40033964
20. Thailand Business News — Are Thai people ready for retirement? — https://www.thailand-business-news.com/banking/151693-are-thai-people-ready-for-retirement
21. ThaiPublica — Robo-advisor กับกฎหมาย — https://thaipublica.org/2019/12/pises-robo-advisor-21/
22. ThaiPublica — ธปท. ประกาศเกณฑ์ Your Data — https://thaipublica.org/2025/11/bank-of-thailand-issued-regulations-under-your-data-project/
23. Spring News — Gen Z มองออมเกษียณเป็นเรื่องไกลตัว — https://www.springnews.co.th/lifestyle/spring-life/863392
24. Forbes — Kindur solves retirement fear — https://www.forbes.com/sites/ashleaebeling/2019/07/30/make-it-last-fintech-firm-solves-number-one-retirement-fearoutliving-your-money/
25. Boldin — Pricing — https://www.boldin.com/retirement/pricing/
26. Businesswire — Silvur membership launch — https://www.businesswire.com/news/home/20210427005697/en/Silvur-Launches-First-of-its-Kind-Membership-for-the-Modern-Retiree-in-a-Post-Pension-World
27. First Page Sage — Fintech CAC Benchmarks — https://firstpagesage.com/seo-blog/fintech-cac-benchmarks-report/
28. Salesworks — CAC in Southeast Asia (อ้าง AppsFlyer) — https://salesworksgroup.com/sg/media-centre/blog/customer-acquisition-cost-in-southeast-asia-whats-a-good-benchmark/
29. CMSK Academy — รายได้/ค่าบริการ CFP ไทย — https://cmsk-academy.com/article/624/income-cfp
30. SET Group / คปภ. — แนวโน้มธุรกิจกลุ่มบริษัทประกันภัย — https://media.setgroup.or.th/setlink/Documents/2025/Apr/แนวโน้มธุรกิจกลุ่มบริษัทประกันภัย.pdf
31. เครื่องมือคำนวณเกษียณ: SET Happy Money — https://www.set.or.th/th/education-research/education/happymoney/pre-retirement · กรุงศรี — https://www.krungsri.com/th/calculator/life-plan/plan-for-retirement · KAsset — https://assetallocation.kasikornasset.com/RetirementPlan · GSB — https://oomtang.gsb.or.th/financial/retirement_plan_tool · KTAM — https://smarttrade.ktam.co.th/smarttrade/pvdweb/index.php?page=retire_rich&sm=1 · ธ.กรุงเทพ — https://www.bangkokbank.com/th-TH/Personal/Save-And-Invest

### Tier 3 — ฟอรัม / blog / บทวิเคราะห์เอกชน (ใช้เป็นหลักฐานพฤติกรรม/บริบท)

32. Nex Cubed — Decumulation: FinTech's Unsolved Challenge — https://www.nex3.com/blog/2020/04/22/decumulation-fintechs-unsolved-challenge
33. Pantip — เงินก้อนสุดท้ายของชีวิต — https://pantip.com/topic/38969747 · โรคกลัวการใช้เงิน — https://pantip.com/topic/42325446 · รายได้หลังเกษียณ — https://pantip.com/topic/42285384
34. ThaiPFA — สาเหตุที่คนไม่วางแผนเกษียณ — https://www.thaipfa.co.th/news/view/508
35. TISCO Wealth — ทำไมคนไทยวางแผนเกษียณผิดพลาด — https://www.tiscowealth.com/trust-magazine/holistic-financial-advisory-63/
36. odini — FAQ ค่าธรรมเนียม — https://odiniapp.com/support/
37. Rob Berger — Best Retirement Calculators (IncomeLab pricing) — https://robberger.com/best-retirement-calculators/
38. White Coat Investor — DIY Retirement Calculators 2025 — https://www.whitecoatinvestor.com/best-retirement-calculators-2025/
39. Silvur — เว็บไซต์ทางการ — https://www.silvur.com/

*หมายเหตุ: ตัวเลข TAM/SAM/SOM และ unit economics ใน Module 2.2 และ 5.2 เป็นการประมาณการของผู้วิเคราะห์จาก input ข้างต้น ไม่ใช่ตัวเลขจากแหล่งใดแหล่งหนึ่งโดยตรง*
