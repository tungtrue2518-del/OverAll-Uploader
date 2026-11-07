# OverAll Uploader

A Windows desktop app for an IT team's routine emails. It opens ready-to-check drafts in
Thunderbird or Outlook, so nothing is sent without a person looking at it first.

Built with Python and pywebview (Python backend, HTML/CSS/JS interface). Thai user interface.

## What it does

- **Standby notice**: end-of-day "IT is not on standby after HH:MM" email, with the cut-off time
  rounded to the next half hour and the next business day filled in.
- **Vendor quotation flow, 2 steps**:
  1. Request a quotation: attaches the newest PDF from the step-1 folder and reads the quotation
     number from the file name, or from the PDF text (with OCR as a fallback).
  2. Approve and request delivery: opens a real threaded reply to the vendor's original email
     (through a small Thunderbird extension and native messaging), attaches the signed PDF,
     then copies it into a dated archive folder (`<year>\<month>\<number>.pdf`).
- **Auto-rename of scanned PDFs**: watches the step-3 folder and renames new scans to their
  document number.
- **Custom categories**: your own templates with recipients, subject and body.
- **Scheduled sends** and a **send log** with search.
- **Outlook leave notice**, opened through Outlook COM.
- **Digital signature** editor with a live HTML preview.
- **Status tab** for a separate scheduled import tool (reads its log files, can start a manual run).

## Requirements

- Windows 10/11, Python 3.11+
- `pip install pywebview pymupdf pytesseract pywin32`
- Thunderbird and/or Outlook. Tesseract OCR is optional (for scanned PDFs).

## Run

```bash
python mail_app.py
```

Build a single exe:

```bash
pyinstaller "OverAll Uploader.spec"
```

Then run `install.ps1` to copy it to `%LOCALAPPDATA%\Programs` and add Desktop / Start Menu shortcuts.

## Settings

All site-specific values live in Settings and are saved to `config.json` (git-ignored):
vendor To/CC, the quotation folder, and the signature. Paths can also come from environment
variables: `PO_ARCHIVE_ROOT` (archive share) and `FG_STOCK_DIR` (the import tool's folder).

The addresses, company name and phone numbers in the source are placeholders
(`example.com`, `080-000-000x`).

## Real reply for step 2 (optional)

`thunderbird_extension/` is a MailExtension that finds the vendor's original email and opens a
reply on it. Zip the folder's contents into an `.xpi`, install it in Thunderbird, then turn on
"Reply จริงสำหรับขั้นตอนที่ 2" in Settings. That registers the native-messaging host.

---

# OverAll Uploader (ภาษาไทย)

โปรแกรมบน Windows สำหรับอีเมลงานประจำของฝ่าย IT โปรแกรมเปิดร่างอีเมลใน Thunderbird หรือ Outlook ให้ตรวจก่อนกดส่งเองทุกครั้ง

- อีเมลแจ้ง Standby ตอนเลิกงาน คำนวณเวลาและวันทำการถัดไปให้
- ขอใบเสนอราคาและแจ้งอนุมัติพร้อมจัดส่งกับผู้ขาย 2 ขั้นตอน อ่านเลขเอกสารจาก PDF ได้ (มี OCR) และ Reply บนอีเมลเดิมได้จริง
- เปลี่ยนชื่อไฟล์สแกนเป็นเลขเอกสารให้อัตโนมัติ และเก็บสำเนาเข้าโฟลเดอร์ตามปีและเดือน
- สร้างหมวดอีเมลเอง ตั้งเวลาส่ง และดูประวัติการส่งได้
- ข้อมูลของแต่ละที่ (ผู้รับ โฟลเดอร์ ลายเซ็น) ตั้งค่าในหน้า "ตั้งค่า" และเก็บไว้ใน `config.json` ซึ่งไม่ขึ้น GitHub

ข้อมูลบริษัท อีเมล และเบอร์โทรในโค้ดเป็นตัวอย่างทั้งหมด
