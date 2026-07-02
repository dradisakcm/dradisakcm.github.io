# คลินิกรักษ์สมองหมออดิศักดิ์ — Website Project

## ไฟล์หลัก
ไฟล์ที่ใช้งานจริงอยู่ที่ **root ของโปรเจกต์** (deploy ผ่าน GitHub Pages จาก repo `dradisakcm/dradisakcm.github.io` โดย serve ตรงจาก root ของ branch main — ไม่มี build process):
- **หน้าเว็บหลัก**: `index.html` (ที่ root) — ไฟล์เดียว single-page website ทั้งหมด
- **คลังความรู้**: `knowledge/` — บทความทั้งหมด (38 บทความ ใน `knowledge/dementia/`)
- **หน้าแบบทดสอบสมอง (Thai AZQ)**: `thaiazq/index.html`
- **Admin Analytics**: `admin-analytics.html` (ที่ root) — dashboard ดูสถิติผู้เยี่ยมชม (localStorage)
- **sitemap.xml / robots.txt**: อยู่ที่ root
- **Preview server config**: `.claude/launch.json` — รัน `npx serve -p 4200`

⚠️ **อย่าแก้ไฟล์ใน `dist/`** — เคยมีโฟลเดอร์ `dist/` ที่เป็นสำเนาเก่า/ไม่ได้ใช้งานจริง (ลบไปแล้ว) ถ้าเจอโฟลเดอร์แบบนี้กลับมาอีกให้ระวัง ของจริงคือไฟล์ที่ root เท่านั้น

## วิธีรัน preview
เปิด preview server ชื่อ `taq-app` ผ่าน Claude Code preview tools
URL: `http://localhost:4200/index.html`

## โครงสร้างเว็บ
- **ภาษา**: รองรับ TH / EN / ZH / JA / DE — ใช้ `data-lang` attribute + `html[lang]` CSS selector
- **CSS custom properties**: `--teal`, `--gold`, `--ink`, `--paper`, `--teal-deep` ฯลฯ
- **Section หลัก (ตามลำดับ)**: Hero → Philosophy → Services (9 cards) → Doctor → Visit → Contact → Articles → FAQ → Footer

## CSS ที่เพิ่มเข้ามา (อยู่ท้าย `<style>` ก่อน media query สุดท้าย)
- `.philosophy-tagline` — ประโยคแรกในส่วนปรัชญา
- `.svc-card-hdr` + `.svc-knowledge-btn` — ปุ่มคลังความรู้ใน service card (top-right)
- `.map-gmap-wrap` + `.map-gmap` — แผนที่ flex layout ใน contact section
- `.azq-map-vid` — strip ปุ่มวิดีโอใต้แผนที่

## HTML โครงสร้าง Service Card
```html
<article class="svc-card">
  <div class="svc-card-hdr">
    <div class="svc-ic"><!-- icon SVG --></div>
    <a href="/articles/SLUG" class="svc-knowledge-btn"><!-- ปุ่มคลังความรู้ --></a>
  </div>
  <h3 data-lang="th">ชื่อโรค</h3>
  <p data-lang="th">คำอธิบาย</p>
</article>
```

## HTML โครงสร้าง Map Section (contact)
```html
<div class="map reveal">
  <div class="map-gmap-wrap">
    <iframe class="map-gmap" src="Google Maps embed"></iframe>
    <a class="map-cta" href="Google Maps link">เปิดใน Google Maps</a>
  </div>
  <div class="azq-map-vid">
    <a href="YouTube link" class="azq-visit-btn azq-visit-btn-sm">วิดีโอแนะนำการเดินทาง</a>
  </div>
</div>
```

## Analytics Tracking
Tracking script อยู่ก่อน `</body>` ใน `index.html`
เก็บข้อมูลใน localStorage key `azq_analytics`:
- `views` — page views รายวัน
- `sessions` — duration แต่ละ session
- `clicks` — นับ clicks รายปุ่ม/ลิงก์

## หมายเหตุสำคัญ
- ไฟล์ใหญ่มาก (~1900+ บรรทัด) ใช้ `grep -n` หรือ `Read` แบบ offset+limit แทน Read ทั้งไฟล์
- CSS บางอันต้องใช้ `!important` เพราะ selector `.map iframe` มี specificity สูงกว่า
- ไม่มี build process — แก้ไฟล์ HTML โดยตรงแล้ว refresh browser ได้เลย
