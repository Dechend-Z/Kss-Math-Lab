# หลักคิด — เว็บไซต์คอร์สเรียน

## โครงสร้างไฟล์
```
/
├── index.html          หน้าแรก (landing page)
├── gate.html            หน้าตรวจสอบสิทธิ์ + dashboard 9 บท (ลิงก์จากอีเมล magic link มาที่นี่)
├── robots.txt            กันไม่ให้ search engine เข้าถึงหน้าที่มี token
├── chapters/
│   ├── chapter1.html     เนื้อหาบทที่ 1 (ทำเสร็จแล้ว)
│   ├── chapter2.html     ...9  (ยังเป็น placeholder รอใส่เนื้อหาจริง)
└── assets/                ไว้เก็บโลโก้/รูปภาพร่วมที่ใช้หลายหน้า (ว่างไว้ก่อน)
```

## ขึ้น GitHub
```bash
cd หลักคิด-website
git init
git add .
git commit -m "โครงสร้างเว็บไซต์เริ่มต้น"
git branch -M main
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin main
```
ถ้ายังไม่มี repo บน GitHub: เข้า github.com → New repository → ตั้งชื่อ → **ห้าม**ติ๊ก "Add README" (จะชนกับที่มีอยู่แล้ว) → Create

## Host บน Hostinger — วิธีที่ 1: เชื่อม Git โดยตรง (แนะนำ)
1. เข้า **hPanel** ของ Hostinger → เลือกเว็บไซต์ที่จะใช้
2. ไปที่เมนู **Advanced > Git**
3. วาง URL ของ GitHub repo (เช่น `https://github.com/username/repo.git`)
4. Branch ใส่ `main`
5. Directory to install ใส่ `public_html` (หรือ subfolder ถ้าจะขึ้นใต้ subdomain)
6. กด **Create** — Hostinger จะดึงไฟล์มา deploy ให้ทันที
7. ครั้งต่อไปที่แก้โค้ดแล้ว push ขึ้น GitHub ใหม่ กลับมาหน้านี้กด **Pull/Deploy** อีกครั้ง (บางแพ็กเกจมี auto-deploy ผ่าน webhook ให้เปิดใช้ได้เลย)

> ฟีเจอร์ Git ใน hPanel มีเฉพาะบางแพ็กเกจ (Business ขึ้นไป) ถ้าไม่มีเมนูนี้ ให้ใช้วิธีที่ 2

## Host บน Hostinger — วิธีที่ 2: อัปโหลดไฟล์ตรง (ใช้ได้ทุกแพ็กเกจ)
1. ดาวน์โหลดโค้ดจาก GitHub เป็น ZIP (หน้า repo → Code → Download ZIP)
   หรือ `git clone` แล้ว zip โฟลเดอร์เอง
2. เข้า hPanel → **Files > File Manager**
3. เข้าไปที่โฟลเดอร์ `public_html` (หรือโฟลเดอร์ของ domain/subdomain ที่จะใช้)
4. อัปโหลด ZIP แล้วกด **Extract** ให้ไฟล์ทั้งหมดออกมาอยู่ระดับเดียวกับ `public_html` โดยตรง (ไม่ใช่ซ้อนอยู่ในโฟลเดอร์ย่อยอีกชั้น)
5. ตรวจว่าเปิด `https://โดเมนของคุณ/` แล้วเจอหน้า index.html ทันที

หรือใช้ **FTP** (FileZilla) แทนก็ได้ — ดึง FTP host/username/password จาก hPanel > Files > FTP Accounts

## หลัง deploy แล้วต้องแก้อะไรบ้าง
- `gate.html`: แก้ `APPS_SCRIPT_URL` ให้เป็น URL จริงจาก Apps Script, แก้ `buyUrl` ทั้ง 9 บทให้เป็น Stripe Payment Link จริง
- Apps Script: แก้ `GATE_BASE_URL` ให้ตรงกับโดเมนจริงที่ deploy (เช่น `https://หลักคิด.com/gate.html`)
- เปิด **SSL ฟรี** ใน hPanel (Security > SSL) ให้เป็น `https://` เสมอ ก่อนใช้งานจริง เพราะลิงก์ที่มี token ไม่ควรวิ่งผ่าน http ธรรมดา
- ทดสอบว่า `robots.txt` โหลดได้ที่ `https://โดเมนของคุณ/robots.txt`

## เพิ่มเนื้อหาบทที่ 2–9
แทนที่ไฟล์ `chapters/chapterN.html` (ตอนนี้เป็น placeholder) ด้วยไฟล์เกม/บทเรียนจริงที่สร้างในแต่ละบท โดยใช้โครงสร้างเดียวกับ `chapter1.html` ได้เลย
