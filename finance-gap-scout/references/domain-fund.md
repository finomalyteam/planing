# Domain: Fund — กองทุนรวม, Asset Management, Fund Operations

## ขอบเขตสายงาน

- ธุรกิจ บลจ. (asset management company): ออกกองทุน, บริหารกองทุน, ขายผ่านตัวแทน
- Fund operations: NAV calculation, fund accounting, compliance monitoring,
  รายงาน regulator
- ช่องทางขาย: ธนาคาร, บล., แพลตฟอร์มกองทุน (fund supermarket)
- เอกสารกองทุน: fund fact sheet, หนังสือชี้ชวน, รายงานประจำปี

## ผู้เล่นที่ควรสำรวจ

- ไทย: บลจ.ใหญ่ (KAsset, SCBAM, BBLAM, Krungsri Asset, Eastspring ฯลฯ),
  แพลตฟอร์มขาย (Finnomena Funds, FinVest, ธนาคารทุกแห่ง)
- Global: fund admin/ops vendors — SS&C, State Street, BNY, Clearwater,
  FundApps (compliance), fund data — Morningstar, Lipper
- AI ใน fund ops: startup ด้าน reconciliation อัตโนมัติ, NAV oversight,
  document automation

## Regulator และกรอบกฎหมาย

- ก.ล.ต. — เกณฑ์จัดตั้ง/บริหารกองทุน, การเปิดเผยข้อมูล, การโฆษณากองทุน
  (ข้อความโฆษณาต้องผ่านเกณฑ์ — เป็นงาน manual review ที่หนัก)
- สมาคมบริษัทจัดการลงทุน (AIMC) — มาตรฐานอุตสาหกรรม, การจัดกลุ่มกองทุน
- กติกากับ prototype: ห้ามสร้างระบบที่ชี้นำให้ซื้อกองทุนจริง — ใช้ข้อมูลจำลอง
  หรือข้อมูลสาธารณะ + disclaimer

## Query set เฉพาะสาย

- "fund operations automation AI 2025 2026"
- "NAV calculation error cases asset management" (ความเสี่ยง ops ที่แพง)
- "fund fact sheet generation automation"
- "กองทุนรวม เปรียบเทียบ ยาก pantip" (pain point นักลงทุนรายย่อย)
- "fund selector platform Thailand รีวิว"
- "mutual fund fee Thailand เทียบ ต่างประเทศ" (cost gap)
- "asset management middle office cost benchmark"
- "compliance monitoring investment mandate automation"
- "AIMC fund classification data API" (ข้อมูลกองทุนไทยเข้าถึงยากแค่ไหน)

## จุดที่มักเป็น gap ในสายนี้ (hypothesis ให้ไป verify)

- การเปรียบเทียบกองทุนข้าม บลจ. สำหรับรายย่อยยังยาก — ข้อมูล fee/performance
  กระจัดกระจาย, fact sheet เป็น PDF ที่เครื่องอ่านยาก
- งานผลิตเอกสาร (fact sheet, รายงาน, ข้อความการตลาดที่ต้องผ่าน compliance)
  ยัง manual สูง — LLM ช่วย draft + pre-check เกณฑ์โฆษณาได้
- Reconciliation ระหว่างระบบ (custodian/registrar/บลจ.) ยังใช้คนไล่ diff
- ไม่มีเครื่องมือช่วยผู้ลงทุนตรวจว่าพอร์ตกองทุนที่ถืออยู่ซ้ำซ้อนกันเอง
  (หลายกองถือหุ้นเดียวกัน)

## ตัวเลขที่ควรหาให้เจอ (สำหรับ cost story)

- ขนาด AUM อุตสาหกรรมกองทุนรวมไทย และจำนวนกองทุน
- ค่าธรรมเนียมเฉลี่ย (TER) กองทุนไทยเทียบต่างประเทศ
- ต้นทุน fund ops (ต่อกองทุน/ต่อ AUM) หรือค่า fund admin ที่ outsource กัน
- เวลาที่ใช้ผลิต/ตรวจเอกสารหนึ่งชุด (ถ้าหาได้จาก case study vendor)
