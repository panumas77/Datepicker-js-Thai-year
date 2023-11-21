# Datepicker-js-Thai-year
Date Picker เปลี่ยนจากปี ค.ศ เป็น พ.ศ.

## วัตถุประสงค์
เนื่องจากโปรเจ็คที่ทำผู้ใช้งานต้องการใช้ภาษาไทยทั้งหมด รวมทั้งหน่วยและวันเดือนปีต่างๆ ด้วย ในส่วนของ วันเดือนปี ผมได้เลือกให้ JQuery library date picker ตัวนี้ [pickadate.js](https://amsul.ca/pickadate.js/). เพราะดีไซล์ทันสมัย, responsive, ขนาดเล็กเบา. 

## Dependencies
- [JQuery](https://jquery.com/)
- [pickadate.js](https://amsul.ca/pickadate.js/)


## การติดตั้ง
```html
<!-- JQuery -->
<script src="Your_Path_To/jquery-3.7.0.min.js"></script>

<!-- Pickadate -->
<!-- CSS -->
    <link rel="stylesheet" href="Your_Path_To/pickadate/lib/themes/default.css">
    <link rel="stylesheet" href="Your_Path_To/pickadate/lib/themes/default.date.css">

<!-- JavaScript -->
    <script src="Your_Path_To/pickadate/lib/picker.js"></script>
    <script src="Your_Path_To/pickadate/lib/picker.date.js"></script>
```

## การเรียกใช้
```html
<script>
    $('.datepicker').pickadate({
        max: true, //ไม่สามารถเลือกวันเดือนปี เกินวันที่ปัจจุบันได้
        monthsFull: ['มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน', 'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม'],
        monthsShort: ['ม.ค.', 'ก.พ.', 'มี.ค.', 'เม.ย.', 'พ.ค.', 'มิ.ย.', 'ก.ค.', 'ส.ค.', 'ก.ย.', 'ต.ค.', 'พ.ย.', 'ธ.ค.'],
        weekdaysFull: ['อาทิตย์', 'จันทร์', 'อังคาร', 'พุธ', 'พฤหัสบดี', 'ศุกร์', 'เสาร์'],
        weekdaysShort: ['อา.', 'จ.', 'อ.', 'พ.', 'พฤ.', 'ศ.', 'ส.'],
        today: 'วันนี้',
        clear: 'ลบ',
        format: 'dd-mm-yyyy',
        formatSubmit: 'dd-mm-yyyy',
        selectMonths: true, //เลือกเดือนได้
        selectYears: 5, //เลือกปีได้ 5ปี (true, ค่าเริ่มต้น 10ปี )
        onRender: function () {
            var yearDropdown = this.$root.find('.picker__select--year');
            if (yearDropdown.length > 0) {
                yearDropdown.find('option').each(function () {
                    var westernYear = parseInt($(this).text());
                    var buddhistYear = westernYear + 543; // แปลงเป็น พ.ศ.
                    $(this).text(buddhistYear);
                });
            }
        },
        onClose: function () {
            // จัดรูปแบบค่าฟิลด์อินพุตหลังจากที่ตัวเลือกปิด
            var selectedDate = this.get('select', 'dd-mm-yyyy'); // รับวันที่เลือก
            var parts = selectedDate.split('-'); // แยกส่วนวันที่
            var buddhistYear = parseInt(parts[2]) + 543; // แปลงเป็น พ.ศ. (เนื่องจากค่าใน input จะยังเป็น ค.ศ. จึงต้องแปลงอีกรอบ)
            var formattedDate = parts[0] + '-' + parts[1] + '-' + buddhistYear; // จัดวันที่ใหม่
            this.$node.val(formattedDate); // อัปเดตค่าอินพุต
        }
    });
    
</script>

```

## หมายเหตุ
สำหรับฐานข้อมูล ส่วนตัวแล้ว ฟิลต์วันเดือนปี ผมจะเก็บในรูปแบบตัวอักษรนะครับ varchar(10) dd-mm-yyyy (เฉพาะโปรเจ็คที่ต้องการรูปแบบไทยแบบนี้ครับ) เพราะสามารถเรียกมาแสดงผลได้โดยตรงไม่ต้องแปลงอีกทีครับ. อีกส่วนที่ผมใช้คือ เอามาคำนวนอายุก็ยังสามารถทำได้ไม่มีปัญหาอะไรครับ.
ขอบคุณครับ
