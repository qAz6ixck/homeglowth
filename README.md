# ข้อมูลฟุตบอลยุโรป · Euro Football Data

เว็บข้อมูลนักฟุตบอลใน 5 ลีก ได้แก่ พรีเมียร์ลีก, ลาลีกา, บุนเดสลีกา, เอเรอดีวีซี และลีกเอิง ครอบคลุม 10 ฤดูกาล (2016/17 – 2025/26) รองรับภาษาไทยและอังกฤษ

**Stack:** Next.js 16 (App Router), TypeScript, Tailwind CSS 4, Recharts, SQLite (built-in `node:sqlite`, ต้องใช้ Node.js 24+)

## เริ่มใช้งาน

```bash
npm install
npm run import   # สร้าง data/football.db จาก data/raw/*.csv.gz (~15 วินาที)
npm run dev      # http://localhost:3000  (จะ redirect ไป /th)
```

ถ้ายังไม่มีไฟล์ใน `data/raw/` ให้ดาวน์โหลดชุดข้อมูลจาก
[transfermarkt-datasets](https://github.com/dcaribou/transfermarkt-datasets)
(ไฟล์ zip: `https://pub-e682421888d945d684bcae8890b0ec20.r2.dev/data/transfermarkt-datasets.zip`)
แล้วแตกไฟล์ `*.csv.gz` มาไว้ในโฟลเดอร์ `data/raw/`

## หน้าเว็บ

| เส้นทาง | รายละเอียด |
| --- | --- |
| `/[th\|en]` | แดชบอร์ด: ตัวเลขภาพรวม, กราฟประตูรายฤดูกาล, สัญชาติ, ดาวซัลโว, แอสซิสต์, มูลค่าตลาด |
| `/[th\|en]/players` | ค้นหาและกรองตามลีก ทีม ตำแหน่ง สัญชาติ พร้อมการเรียงลำดับและแบ่งหน้า |
| `/[th\|en]/players/[id]` | โปรไฟล์: สถิติรายฤดูกาล, กราฟ, มูลค่าตลาดย้อนหลัง, ประวัติการย้ายทีม |
| `/[th\|en]/seasons` | สถิติตามฤดูกาลและลีก พร้อมผู้นำแต่ละด้าน |
| `/[th\|en]/compare?ids=1,2` | เปรียบเทียบนักเตะได้สูงสุด 4 คน (radar chart + ตาราง) |

## ทดสอบ

```bash
npm test                 # ตรวจความถูกต้องของข้อมูลในฐานข้อมูล
npm run lint && npm run build
npx next start -p 3123   # จากนั้นรันในอีกหน้าต่าง:
node scripts/smoke.mjs   # เรียกทุกหน้าทั้ง 2 ภาษาเพื่อตรวจสอบ
```

ข้อมูล: Transfermarkt ผ่าน transfermarkt-datasets (อัปเดตถึง ก.ค. 2026)
