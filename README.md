<!DOCTYPE html>
<html lang="en">

<head>
    <!-- تعريف مجموعة البيانات والترميز المستخدم في الصفحة -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🥳 Online Store to Display Custom Products 🛒🎉</title>
    
    <!-- ربط ملف الأنماط (CSS) الخاص بالصفحة -->
    <link rel="stylesheet" href="styles.css">

    <!-- تضمين أنماط CSS الخاصة بمكتبة DataTables -->
    <link rel="stylesheet" href="https://cdn.datatables.net/1.11.5/css/jquery.dataTables.min.css">
    <link rel="stylesheet" href="https://cdn.datatables.net/buttons/1.7.1/css/buttons.dataTables.min.css">

    <!-- تضمين أنماط CSS لمكتبة Bulma -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bulma/0.9.3/css/bulma.min.css">
    
    <!-- تضمين أنماط CSS لأيقونات FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <!-- تضمين أحدث نسخة من أنماط Bootstrap -->
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/5.3.0/css/bootstrap.min.css">

    <!-- تضمين خط Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap" rel="stylesheet">

    <!-- تضمين أنماط CSS لمكتبة SweetAlert2 -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/sweetalert2@11/dist/sweetalert2.min.css">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fancyapps/fancybox@3/dist/jquery.fancybox.min.css">

</head>

<body>
  
    <!-- المحتوى الخاص بك هنا -->

    <!-- تضمين مكتبات JavaScript -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>

    <!-- تضمين حزمة Bootstrap مع Popper -->
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/5.3.0/js/bootstrap.bundle.min.js"></script>

    <!-- تضمين مكتبات JavaScript الخاصة بمكتبة DataTables -->
    <script src="https://cdn.datatables.net/1.11.5/js/jquery.dataTables.min.js"></script>
    <script src="https://cdn.datatables.net/buttons/1.7.1/js/dataTables.buttons.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.1.3/jszip.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdfmake/0.1.53/pdfmake.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdfmake/0.1.53/vfs_fonts.js"></script>
    <script src="https://cdn.datatables.net/buttons/1.7.1/js/buttons.html5.min.js"></script>
    <script src="https://cdn.datatables.net/buttons/1.7.1/js/buttons.print.min.js"></script>
    <script src="https://cdn.datatables.net/buttons/1.7.1/js/buttons.colVis.min.js"></script>

    <!-- تضمين مكتبة SweetAlert2 -->
    <script src="https://cdn.jsdelivr.net/npm/sweetalert2@11/dist/sweetalert2.all.min.js"></script>

    <!-- سكربتاتك المخصصة هنا -->
</body>
</html>
  <script>
    // قائمة الاقتباسات العشوائية
    const quotes = [
        "The only way to do great work is to love what you do. – Steve Jobs 💖✨",
        "Success is not final, failure is not fatal: It is the courage to continue that counts. – Winston Churchill 🏆🚀",
    ];

    // دالة للحصول على اقتباس عشوائي
    function getRandomQuote() {
        const randomIndex = Math.floor(Math.random() * quotes.length);
        return quotes[randomIndex];
    }

    // دالة لتحديث التاريخ والوقت كل ثانية
    function updateDateTime() {
        const now = new Date();
        const date = now.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
        const time = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
        document.getElementById('date-time').textContent = `${date} ${time}`;
    }

    // دالة لتحديث الاقتباس العشوائي كل 7 ثواني
    function updateQuote() {
        document.getElementById('quote').textContent = getRandomQuote();
    }

    // دالة لتحديث وقت آخر تحديث
    function updateLastUpdate() {
        var now = new Date();
        now.setMinutes(now.getMinutes() - 15); // طرح 15 دقيقة
        var formattedDate = now.toLocaleDateString('en-US', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });
        var formattedTime = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' });
        $('#last-update').text('Last updated: ' + formattedDate + ' ' + formattedTime);
    }

    // عند تحميل الوثيقة
    $(document).ready(function() {
    // تهيئة جدول البيانات
    var table = $('#data-table').DataTable({
        data: [], // بيانات مبدئية، سيتم استبدالها ببيانات من Google Sheets
        columns: [
            { "title": "NO 📦", "className": "column-NO"  }, // العمود الأول: رمز UPC
            { "title": "Brand 🏬", "className": "column-Brand"  }, // العمود الثاني: اسم المتجر
            { "title": "ASIN 🔍", "className": "column-ASIN"  }, // العمود الثالث: رمز ASIN
            { "title": "Reviews 🔢", "className": "column-Reviews"  }, // العمود الرابع: رمز NIN
            {
                "title": "Image 🖼️","className": "column-image",// العمود الخامس: الصورة
                "data": function(row) {
                    var imageUrl = row[4]; // افتراض أن رابط الصورة في العمود الخامس
                    return '<div class="img-container"><img src="' + imageUrl + '" class="img-thumbnail" style="max-width: 100px; max-height: 90px;"></div>';
                },
                "orderable": false // إلغاء ترتيب العمود (الصورة)
            },
            { "title": "sellers on Amazon 🗂️", "className": "column-sellers on Amazon"  }, // العمود السادس: الفئة
            { "title": "discount 📈", "className": "column-discount"  }, // العمود السابع: العلامة التجارية
            { "title": "User 🔢", "className": "column-User"  }, // العمود الثامن: SKU
            { "title": "Title 🏷️", "className": "column-Title"  }, // العمود التاسع: العنوان
            {
                "title": "global ratings 👥", "className": "column-global ratings"  , // العمود العاشر: المخزون
                "data": function(row) {
                    return parseInt(row[9], 10); // افتراض أن المخزون في العمود العاشر
                }
            },
            {
                "title": "Cost 💵", "className": "column-Cost"  , // العمود الحادي عشر: التكلفة
                "data": function(row) {
                    return 'EGP ' + parseFloat(row[10]).toFixed(2); // افتراض أن التكلفة في العمود الحادي عشر
                }
            },
            {
                "title": "Price B 💲", "className": "column-Price B"  , // العمود الثاني عشر: السعر B
                "data": function(row) {
                    return 'EGP ' + parseFloat(row[11]).toFixed(2); // افتراض أن السعر B في العمود الثاني عشر
                }
            },
            {
                "title": "URL 🌐", "className": "column-URL"  , // العمود الثالث عشر: الرابط
                "data": function(row) {
                    var url = row[12]; // افتراض أن الرابط في العمود الثالث عشر
                    return '<a href="' + url + '" target="_blank">Buy on Amazon 🛒🛍️</a>'; // رابط لفتح الرابط في نافذة جديدة
                },
                "orderable": true // تمكين ترتيب العمود (الرابط)
            }
        ],
        columnDefs: [
            { "width": "10%", "targets": '_all' } // تحديد عرض الأعمدة لجميع الأعمدة
        ],

        columnDefs: [
            {
                "targets": [1, 11, 12,], // أعمدة مخفية عند تحميل الصفحة
                "visible": false // إخفاء الأعمدة
            }
        ],
 
        responsive: true, // تمكين التفاعل مع حجم الشاشة
        paging: true, // تمكين الترقيم الصفحات
        searching: true, // تمكين البحث
        info: true, // تمكين معلومات الصفحات
        pageLength: 10, // عدد السجلات في الصفحة
        lengthMenu: [10, 25, 50, 100], // خيارات عرض السجلات في الصفحة
        dom: 'Bfrtip', // عناصر الترتيب (زر التصدير، البحث، إلخ.)
        buttons: [
            {
                extend: 'copy',
                text: '<i class="fas fa-copy"></i> Copy 📋📄', // زر لنسخ البيانات إلى الحافظة
                className: 'btn btn-outline-primary', // تنسيق الزر
                exportOptions: {
                    columns: ':visible' // تصدير الأعمدة المعروضة فقط
                }
            },
            {
                extend: 'csv',
                text: '<i class="fas fa-file-csv"></i> CSV 📂🗂️', // زر لتصدير البيانات إلى ملف CSV
                className: 'btn btn-outline-primary',
                filename: function() {
                    return 'data_export_' + new Date().toISOString().slice(0,10); // تعيين اسم ملف التصدير مع التاريخ
                },
                exportOptions: {
                    columns: ':visible'
                },
                charset: 'utf-8',
                title: 'Exported Data',
                extension: '.csv'
            },
            {
                extend: 'excel',
                text: '<i class="fas fa-file-excel"></i> Excel 📊🗂️', // زر لتصدير البيانات إلى ملف Excel
                className: 'btn btn-outline-primary',
                filename: function() {
                    return 'data_export_' + new Date().toISOString().slice(0,10); // تعيين اسم ملف التصدير مع التاريخ
                },
                exportOptions: {
                    columns: ':visible'
                },
                title: 'Exported Data',
                sheetName: 'Sheet1'
            },
            {
                extend: 'pdf',
                text: '<i class="fas fa-file-pdf"></i> PDF 📄🖨️', // زر لتصدير البيانات إلى ملف PDF
                className: 'btn btn-outline-primary',
                orientation: 'landscape', // اتجاه الصفحة
                pageSize: 'A4', // حجم الصفحة
                exportOptions: {
                    columns: ':visible'
                }
            },
          
          {
    extend: 'print',
    text: '<i class="fas fa-print"></i> Print 🖨️',
    className: 'btn btn-outline-primary',
    title: 'My Data Records 🔍📝:',
    orientation: 'portrait',
    pageSize: 'A4',
    exportOptions: {
        columns: ':visible'
    },
    messageTop: '✨ Hello! Thank you for using our services. Enjoy your printing experience! ✨',
    messageBottom: 'Page generated on ' + new Date().toLocaleDateString(),
    customize: function(win) {
        // تخصيص استايل الطباعة
        $(win.document.body).css({
            'font-size': '12pt',
            'font-family': 'Arial, sans-serif',
            'color': '#333',
            'background-color': '#fff'
        });

        // تخصيص الجدول (أنيق وأوسع)
        $(win.document.body).find('table').css({
            'width': '100%',
            'border-collapse': 'collapse',
            'margin': '20px 0'
        });

        // تخصيص العناوين والصفوف
        $(win.document.body).find('th').css({
            'background-color': '#f0f0f0',
            'font-weight': 'bold',
            'padding': '8px',
            'border': '1px solid #ddd',
            'text-align': 'center'
        });
        $(win.document.body).find('td').css({
            'padding': '8px',
            'border': '1px solid #ddd',
            'text-align': 'center'
        });

        // تخصيص الصفوف ذات الخلفية المتبادلة
        $(win.document.body).find('tr:nth-child(even)').css({
            'background-color': '#f9f9f9'
        });
        $(win.document.body).find('tr:nth-child(odd)').css({
            'background-color': '#ffffff'
        });

        // إضافة الشعار في أعلى الصفحة
        $(win.document.body).prepend('<img src="https://via.placeholder.com/150" style="width:150px; display:block; margin: 0 auto 20px;">');

        // تخصيص الطباعة باستخدام media query
        $(win.document).find('style').append(`
            @media print {
                body {
                    font-family: Arial, sans-serif;
                    color: #333;
                    background-color: #fff;
                }
                table {
                    width: 100%;
                    border-collapse: collapse;
                }
                th, td {
                    padding: 8px;
                    text-align: center;
                    border: 1px solid #ddd;
                }
                th {
                    background-color: #f0f0f0;
                }
                tr:nth-child(even) {
                    background-color: #f9f9f9;
                }
                tr:nth-child(odd) {
                    background-color: #ffffff;
                }
                img {
                    max-width: 100px;
                    max-height: 100px;
                    display: block;
                    margin: 0 auto;
                    border: 1px solid #ddd;
                    padding: 5px;
                    border-radius: 5px;
                }
            }
        `);

        // تخصيص عمود الصور
        var imageColumnIndex = -1;
        $(win.document.body).find('table thead th').each(function(index) {
            if ($(this).text().trim() === 'Image 🖼️') {
                imageColumnIndex = index; // العثور على عمود الصور
            }
        });

        // تخصيص الصفوف لعرض الصور داخل العمود "Image 🖼️"
        if (imageColumnIndex !== -1) {
            $(win.document.body).find('table tbody tr').each(function() {
                var imageUrl = $(this).find('td').eq(imageColumnIndex).find('img').attr('src');
                if (imageUrl) {
                    var imgTag = '<img src="' + imageUrl + '" style="width: 100px; height: 100px; margin: 0 auto; display: block; border: 1px solid #ddd; padding: 5px; border-radius: 5px;" />';
                    $(this).find('td').eq(imageColumnIndex).html(imgTag);
                }
            });
        }

        // تأكيد تحميل الصور أولاً
        var images = $(win.document.body).find('img');
        var imagesLoaded = 0;
        var totalImages = images.length;

        // تأكد من أن جميع الصور قد تم تحميلها قبل الطباعة
        images.each(function() {
            var img = new Image();
            img.src = $(this).attr('src');
            img.onload = function() {
                imagesLoaded++;
                if (imagesLoaded === totalImages) {
                    // عندما يتم تحميل جميع الصور، تنفيذ الطباعة
                    setTimeout(function() {
                        win.print();
                    }, 500);
                }
            };
        });

        // في حالة عدم وجود صور، اطبع فوراً
        if (totalImages === 0) {
            setTimeout(function() {
                win.print();
            }, 500);
        }
    }
},


            {
                extend: 'colvis',
                text: '<i class="fas fa-columns"></i> Toggle Columns 🌟', // زر لتبديل رؤية الأعمدة
                className: 'btn btn-outline-secondary btn-colvis-custom',
                titleAttr: 'Click to show/hide columns with a cool effect!', // عنوان التلميح عند التمرير
                collectionLayout: 'fixed', // تخطيط قائمة التبديل
                collectionTitle: 'Select Columns', // عنوان القائمة
                buttonText: '<i class="fas fa-columns"></i> Toggle Columns',
                buttonClassName: 'btn btn-outline-secondary',
                collectionLayout: 'fixed'
            },
            {
                extend: 'colvisRestore',
                text: '<i class="fas fa-undo"></i> Restore Defaults 🔄', // زر لاستعادة الإعدادات الافتراضية للأعمدة
                className: 'btn btn-outline-danger btn-colvis-restore',
                titleAttr: 'Restore column visibility to default', // عنوان التلميح عند التمرير
                buttonText: '<i class="fas fa-undo"></i> Restore Defaults'
            }
        ],
        order: [], // عدم تطبيق ترتيب افتراضي
        language: {
            search: "Search records 🔍📝:", // نص البحث
            lengthMenu: "Display _MENU_ records per page 📄", // نص عدد السجلات في الصفحة
            info: "Showing page _PAGE_ of _PAGES_ 📑", // نص معلومات الصفحة
            infoEmpty: "No records available 🚫", // نص عندما لا تكون هناك سجلات
            infoFiltered: "(filtered from _MAX_ total records 🔍)", // نص معلومات التصفية
            paginate: {
                first: "First ⏮️", // نص للزر الأول
                last: "Last ⏭️", // نص للزر الأخير
                next: "Next ▶️", // نص للزر التالي
                previous: "Previous ◀️" // نص للزر السابق
            }
        }
    });


        // نقل الأزرار إلى رأس الجدول
        var buttons = table.buttons().container();
        $('#datatable-buttons').append(buttons);

        // ملء قائمة اختيار الأعمدة
        var columnSelector = $('#column-select');
        table.columns().every(function () {
            var column = this;
            var columnTitle = $(column.header()).text();
            columnSelector.append('<option value="' + column.index() + '">' + columnTitle + '</option>');
        });

        // التعامل مع تغيير طول الصفحة
        $('#length-select').on('change', function () {
            var length = $(this).val();
            table.page.len(length).draw();
        });

        // التعامل مع بحث الأعمدة
        $('#search-input').on('keyup', function () {
            var searchTerms = $(this).val().split('\n').map(term => term.trim()).filter(term => term.length > 0);
            var selectedColumn = $('#column-select').val();

            table.columns().every(function () {
                var column = this;
                column.search('');
                if (column.index() == selectedColumn) {
                    var searchRegex = searchTerms.join('|');
                    column.search(searchRegex, true, false).draw();
                }
            });

            updateFilteredCount(); // تحديث العد بعد البحث
        });

        // التعامل مع تغيير اختيار الأعمدة
        $('#column-select').change(function () {
            var selectedColumn = $(this).val();
            var searchTerm = $('#search-input').val();

            table.columns().every(function () {
                var column = this;
                column.search('');
                if (column.index() == selectedColumn) {
                    column.search(searchTerm).draw();
                }
            });
        });

        // تحديث عدد السجلات المفلترة
        function updateFilteredCount() {
            var filteredCount = table.rows({ filter: 'applied' }).count();
            $('#filtered-count').text('Number of filtered records: ' + filteredCount);
        }

        table.on('draw', function () {
            updateFilteredCount(); // تحديث العد عند إعادة رسم الجدول
        });

        // تحديث التاريخ والوقت كل ثانية
        setInterval(updateDateTime, 1000);
        updateDateTime(); // استدعاء أولي

        // عرض اقتباس عشوائي وتغييره كل 7 ثواني
        setInterval(updateQuote, 7000);
        updateQuote(); // استدعاء أولي

        // تحديث آخر تحديث
        updateLastUpdate(); // استدعاء أولي

        // رسالة ترحيب خاصة للمستخدم
        var isSpecialUser = true; // تحديث بناءً على شرطك
        if (isSpecialUser) {
            Swal.fire({
                title: '🎉 Welcome, Special User! 🌟 Server(P@2).H🫰A',
                text: 'We are thrilled to have you here. Enjoy exploring the 🥳 Online Store to Display Custom Products 🛒🎉!',
                icon: 'success',
                confirmButtonText: 'Thank you! 😊',
                position: 'top-end',
                toast: true,
                showConfirmButton: true,
                timer: 0, // الرسالة ستبقى حتى ينقر المستخدم على الزر
                timerProgressBar: false
            });
        }
    });

    // دالة لعرض دائرة التحميل
    function showLoading() {
        document.getElementById('loading').style.display = 'block';
    }

    // دالة لإخفاء دائرة التحميل
    function hideLoading() {
        document.getElementById('loading').style.display = 'none';
    }

    // دالة لتحميل البيانات من Google Sheets
    function loadData() {
        showLoading(); // عرض دائرة التحميل

        google.script.run.withSuccessHandler(function(data) {
            hideLoading(); // إخفاء دائرة التحميل
            var table = $('#data-table').DataTable();
            table.clear().rows.add(data).draw(); // تحديث البيانات في DataTable
        }).getData(); // افتراض أن getData هي دالة في Google Apps Script التي تعيد البيانات
    }

    // دالة للتحقق من التحديثات
    function checkForUpdates() {
        Swal.fire({
            title: 'Important Update Available! 🔔',
            text: 'The prices and quantities in the warehouse need to be updated. Do you want to refresh the data from the Server P@2.HA 🕸️ now?',
            icon: 'warning',
            showCancelButton: true,
            confirmButtonColor: '#3085d6',
            cancelButtonColor: '#d33',
            confirmButtonText: 'Yes, Refresh Now! 🔄',
            cancelButtonText: 'No, Keep Current Data 🚫',
            customClass: {
                title: 'alert-title',
                content: 'alert-content'
            }
        }).then((result) => {
            if (result.isConfirmed) {
                loadData(); // تحديث البيانات إذا تم التأكيد
            }
        });
    }

    // دالة لتحديث بيانات الجدول
    function updateTable() {
        showLoading(); // عرض دائرة التحميل

        $.ajax({
            url: 'https://docs.google.com/spreadsheets/d/13HDICoHo5wvh5jSWangpWPE3krbCi__Y2TXsaSEIzb8/edit?usp=sharing', // استبدل برابط مصدر بياناتك
            method: 'GET',
            dataType: 'json',
            success: function(data) {
                hideLoading(); // إخفاء دائرة التحميل
                var table = $('#data-table').DataTable();
                table.clear().rows.add(data).draw();
            },
            error: function() {
                hideLoading(); // إخفاء دائرة التحميل
                Swal.fire({
                    icon: 'error',
                    title: 'Failed to load data',
                    text: 'There was an error while updating the table data.'
                });
            }
        });
    }

    // تهيئة DataTable وتحميل البيانات عند تحميل الوثيقة
    $(document).ready(function() {
        $('#data-table').DataTable(); // تهيئة DataTable
        loadData(); // تحميل البيانات الأولية

        // التحقق من التحديثات كل 60 ثانية
        setInterval(checkForUpdates, 600000);
    });

</script>

  <style>

/* عام */
body {
     background: linear-gradient(135deg, #0f0c29, #302b63, #24243e); /* Space-like gradient */
background-size: 400% 400%;
animation: gradientAnimation 15s ease infinite;
}
@keyframes gradientAnimation {
    0% { background-position: 0% 0%; }
    50% { background-position: 100% 100%; }
    100% { background-position: 0% 0%; }
}




/* تثبيت الرسالة على الشاشة */
#loading {
    position: fixed;
    margin: 12px 0;
   background: linear-gradient(45deg, #1d2671, #c33764); /* تدرج لوني جريء */
    top: 0;
    left: 0;
     font-size: 0.75rem;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.8);
    text-align: center;
    z-index: 9999;
    display: flex;
    justify-content: center;
      font-weight: bold;
    align-items: center;
     
}

#spinner {
    margin: 0 auto;
    border: 8px solid rgba(0,0,0,0.1); /* Light grey */
    border-radius: 50%;
    border-top: 8px solid #000; /* Black */
    width: 60px;
    height: 60px;
    animation: spin 5s linear infinite;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
       25% { transform: rotate(90deg); }
        50% { transform: rotate(180deg); }
    100% { transform: rotate(360deg); }
}

/* إخفاء الرسالة عند الضغط على الزر */
#close-btn {
    display: inline-block;
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

#close-btn:hover {
    background-color: #0056b3;
}

.form-select:focus {
    border-color: #007bff;
    box-shadow: 0 0 0 0.2rem rgba(38, 143, 255, 0.25);
}

/* تحسين التنسيق عند التمرير */
.form-select option {
    padding: 0.5rem;
}

/* ترويسة الصفحة */
header {
    background: linear-gradient(45deg, #1d2671, #c33764); /* تدرج لوني جريء */
    color: #ffffff;
    padding: 10px 0; /* تباعد أكبر */
    text-align: center;
    position: relative;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.5); /* ظل عميق */
 
    justify-content: space-between;
    align-items: left;
    flex-wrap: wrap;
    animation: pulse 25s infinite; /* تأثير النبض */
}

/* حركة النبض */
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
}

/* محتوى الترويسة */
.header-content {
    flex: 1;
    background: linear-gradient(135deg, #6b2e91, #f05661);
    color: #ffffff;
    font-size: 0.875rem;
       font-weight: bold;
    padding: 15px;
    border-radius: 10px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    position: relative;
    overflow: hidden;
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
    transition: transform 0.3s ease, box-shadow 0.3s ease, background-position 0.6s ease;
    background-size: 200% 200%;
        align-items: left;
    
}

.header-content::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, rgba(255, 255, 255, 0.2), transparent);
    border-radius: 10px;
    opacity: 0;
    transition: opacity 0.3s ease;
       font-weight: bold;
           align-items: left;
             color: #ffffff;
}

.header-content:hover {
    transform: scale(1.05);
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
    background-position: 100% 100%;
       font-weight: bold;
           align-items: left;
             color: #ffffff;
}

.header-content:hover::before {
    opacity: 0.3;
    text-align: right;
       font-weight: bold;
           align-items: left;
             color: #ffffff;
}

/* تنسيق التاريخ والوقت والاقتباسات */
.date-time, .quote {
    font-size: 1.2rem; /* زيادة حجم الخط */
    font-style: italic;
    font-weight: bold;
    text-align: left;
    padding: 10px;
    border-radius: 8px;
    position: relative;
    overflow: hidden;
}

/* تأثيرات على التاريخ والوقت */
.date-time {
    background: linear-gradient(45deg, #ff0066, #ffcc00, #00ffcc, #ff66ff); /* تدرج ألوان زاهي */
    background-size: 400% 400%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: gradientAnimation 4s ease infinite; /* حركة تدرج الألوان */
    text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3); /* ظل للنص */
    margin-bottom: 12px;
    line-height: 1.5;
}

/* تأثيرات على الاقتباسات */
.quote {
    background: linear-gradient(135deg, #ff3399, #00ccff, #ff9900, #33cc33); /* تدرج ألوان زاهي */
    background-size: 300% 300%;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    animation: gradientAnimation 5s ease infinite; /* حركة تدرج الألوان */
    text-shadow: 3px 3px 8px rgba(0, 0, 0, 0.5); /* ظل للنص */
    border: 2px dashed #ffffff; /* إطار متقطع */
    margin-bottom: 15px;
    line-height: 1.5;
}

/* حركة تدرج الألوان */
@keyframes gradientAnimation {
    0% { background-position: 0% 0%; }
    50% { background-position: 100% 100%; }
    100% { background-position: 0% 0%; }
}
 

.quote {
    background: linear-gradient(45deg, #ffdf00, #ff3df0);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    font-size: 0.875rem;
    margin-bottom: 10px;
    font-weight: bold;
    text-align: center;
        align-items: left;
}

/* تنسيق الحاويات */
.container {
    margin-top: 1px;
  
    flex-direction: column;

    color: #ffffff;

    /* تحديد الأبعاد بشكل تلقائي */
    width: auto; /* عرض تلقائي يتكيف مع المحتوى أو العنصر الأب */
    max-width: 100%; /* أقصى عرض للحاوية هو 100% من العنصر الأب */
    min-width: 0; /* الحد الأدنى للعرض هو 0 ليتكيف مع المحتوى */

    height: auto; /* الارتفاع التلقائي يتكيف مع المحتوى */
    max-height: none; /* لا يوجد حد أقصى للارتفاع، يتكيف مع المحتوى */
    min-height: 0; /* الحد الأدنى للارتفاع هو 0 ليتكيف مع المحتوى */

    /* تخصيص الحاوية */
  max-width: fit-content; /* العرض يتكيف مع المحتوى */
    padding: 1px; /* إضافة حشو حول المحتوى */
    border-radius: 1px; /* زوايا دائرية للحاوية */
}

/* تنسيق حاوية النموذج */
.form-wrapper {
    display: flex;
    flex-wrap: wrap; /* يسمح بتغليف العناصر عند الحاجة */
    gap: 60px; /* المسافة بين العناصر لتكون أكثر وضوحًا */
    color: #ffffff; /* لون النصوص داخل الحاوية */
   
 
    max-width: fit-content; /* العرض يتكيف مع المحتوى */
    width: auto; /* العرض التلقائي للحاوية */
    box-sizing: border-box; /* يشمل الحشو والإطار في العرض والارتفاع */
}

/* تنسيق مجموعة النموذج */
.form-group {
    display: flex;
    flex-direction: column; /* الترتيب الرأسي للعناصر داخل .form-group */
    align-items: center
    flex: 2 2 auto; /* السماح للعناصر بالتوسع والنقصان حسب الحاجة */
    min-width: 210px; /* تحديد الحد الأدنى للعرض لضمان وضوح العناصر */
}
 align-items: left;
/* تنسيق العناصر داخل مجموعة النموذج */
.form-group label,
.form-group select,
.form-group textarea,
.form-group input {
    width: 100%; /* جعل العناصر تمتد على كامل عرض الحاوية */
    margin-bottom: 100px; /* إضافة مسافة بين العناصر */
}

/* تنسيق التسمية */
.form-label {
    font-size: 1rem;
    font-weight: bold;
    text-align: left; /* محاذاة النصوص إلى اليسار */
    margin-bottom: 1px; /* مسافة أسفل التسمية لجعلها أكثر وضوحًا */
}

/* تنسيق عناصر الإدخال (اختيارات ونصوص) */
.form-select, 
.form-control {
    width: 100%; /* تمديد العناصر لتأخذ العرض الكامل للحاوية */
    max-width: 100%; /* تحديد أقصى عرض ليأخذ العرض الكامل للحاوية */
    margin-top: 1px; /* تقليل المسافة العلوية لتكون أقرب إلى التسمية */
    padding: 8px; /* إضافة حشو داخل عناصر الإدخال لتحسين التباعد */
    border: 1px solid #ccc; /* إضافة إطار خفيف لعناصر الإدخال */
    border-radius: 4px; /* إضافة زوايا دائرية لعناصر الإدخال */
    background-color: #fff; /* خلفية بيضاء لعناصر الإدخال */
}

/* تنسيق التعدادات */
#filtered-count {
    font-size: 1rem;
    font-weight: bold;
    color: white;
    margin: 5px 0; /* المسافة من الأعلى والأسفل */
    text-align: center; /* توسيط النصوص */
}

/* تنسيق النصوص الكبيرة */
textarea {
    resize: vertical;
    padding: 10px;
    border-radius: 4px;
    border: 1px solid #ced4da;
      text-align: left;
}

/* تنسيق الجدول */
.table {
   text-align: center;
     font-weight: bold;
    width: 99%;
    border-collapse: collapse;
    font-family: Helvetica, sans-serif; /* خط غير تقليدي */
    border: 3px solid #ff00ff; /* لون نيون زاهي */
    background: linear-gradient(45deg, #f0ff00, #ff007f); /* تدرج خلفية مبهر */
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.5); /* ظل عميق */
}

.table thead th {
    position: sticky;
    top: 0;
    z-index: 10; /* تأكد من أن الرأس فوق المحتوى */
    background: #ff007f; /* نفس لون الخلفية لرأس الجدول لتجنب مشاكل التراكب */
    color: #ffffff;
        font-size: 12px; /* حجم أكبر */
        font-weight: bold;
}
.table tbody td {
    background-color: #e0e0e0; /* لون خلفية خفيف */
    font-weight: normal;
    vertical-align: middle;
    text-align: center;
    font-weight: bold;
    height: 90px; /* ارتفاع أكبر */
    font-size: 13px; /* حجم أكبر */
    padding: 15px;
    border-bottom: 2px solid #ff007f; /* لون زاهي */
    transition: background-color 0.3s, transform 0.3s, box-shadow 0.3s; /* تأثيرات تفاعلية */
    border-radius: 5px; /* حواف مدورة */
    
}
/* تخصيص محاذاة النصوص لكل عمود بناءً على الفئة */
table#data-table td.column-upc {
    text-align: left; /* محاذاة النص في عمود UPC إلى الوسط */
}
table#data-table td.column-store {
    text-align: center; /* محاذاة النص في عمود Store إلى اليسار */
}
table#data-table td.column-asin {
    text-align: left; /* محاذاة النص في عمود ASIN إلى اليمين */
}
table#data-table td.column-nin {
    text-align: left; /* محاذاة النص في عمود NIN إلى الوسط */
}
table#data-table td.column-image {
    text-align: center; /* محاذاة النص في عمود Image إلى اليسار */
}
table#data-table td.column-Title {
    text-align: left; /* محاذاة النص في عمود Title إلى اليمين */
}
.table tbody td:hover {
    background-color: #ffecb3; /* لون خلفية عند المرور */
    transform: scale(1.05); /* تكبير عند المرور */
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.6); /* ظل متقدم */
}

.dataTables_wrapper .dataTables_paginate .paginate_button {
    padding: 0.75rem 1.25rem;
    font-weight: bold;
    margin: 0.3rem;
    border: 2px solid #ff00ff; /* لون نيون */
    border-radius: 1rem; /* حواف مدورة كبيرة */
    background-color: #ffffff;
    color: #ff00ff;
    transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease; /* تأثيرات تفاعلية */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); /* ظل خفيف */
}

.dataTables_wrapper .dataTables_paginate .paginate_button:hover {
    background-color: #ff00ff;
    color: #ffffff;
    transform: scale(1.1); /* تكبير معتدل عند المرور */
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4); /* ظل أعمق */
}

.dataTables_wrapper .dataTables_paginate .paginate_button.current {
    background-color: #00ffff; /* لون نيون */
    color: #000000;
    border: 2px solid #00ffff; /* لون نيون */
}

.dataTables_wrapper .dataTables_filter input {
    margin-left: 1rem;
    padding: 0.75rem;
    border-radius: 1rem; /* حواف مدورة كبيرة */
    border: 2px solid #ff00ff; /* لون نيون */
    font-size: 14px; /* حجم أكبر */
    transition: border-color 0.3s ease, box-shadow 0.3s ease; /* تأثير التفاعل */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* ظل خفيف */
}

.dataTables_wrapper .dataTables_filter input:focus {
    border-color: #00ffff; /* لون نيون عند التركيز */
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4); /* ظل أعمق */
}

.dataTables_wrapper .dataTables_info {
    margin-top: 1rem;
    color: #ff00ff; /* لون زاهي */
    font-size: 14px; /* حجم أكبر */
    font-weight: bold;
}

/* تأثير نبضي */
@keyframes pulse {
    0% {
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4);
    }
    50% {
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.6);
    }
    100% {
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.4);
    }
}

.dataTables_wrapper .dataTables_paginate .paginate_button {
    animation: pulse 1.5s infinite; /* إضافة تأثير نبضي للزر */
}

/* أزرار جنونية */
.btn-outline-primary {
    margin: 0.75rem;
    font-size: 1.1rem;
    border-radius: 1rem; /* حواف دائرية عملاقة */
    background: linear-gradient(135deg, #ff0081, #ff8c00, #ff00a8, #ff6f61); /* تدرج لوني متغير */
    border: none;
    color: white;
    padding: 1rem 2.5rem; /* تباعد أكبر */
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.6); /* ظل أكثر عمقًا */
    transition: background 0.5s, transform 0.5s, color 0.5s, box-shadow 0.5s, filter 0.5s; /* تأثيرات تفاعل متعددة */
    position: relative;
    overflow: hidden;
    font-family: 'Comic Sans MS', cursive; /* خط مميز */
}

.btn-outline-primary::before {
    content: "";
    position: absolute;
    top: 50%;
    left: 50%;
    width: 400%;
    height: 400%;
    background: rgba(255, 255, 255, 0.3);
    transform: translate(-50%, -50%) scale(0);
    border-radius: 50%;
    z-index: 0;
    transition: transform 0.6s ease, background 0.6s ease;
}

.btn-outline-primary:hover::before {
    transform: translate(50%, -50%) scale(1.2);
    background: rgba(255, 255, 255, 0.5); /* تغيير الخلفية عند التمرير */
}

.btn-outline-primary:hover {
    background: linear-gradient(135deg, #ff6f61, #ff00a8, #ff8c00, #ff0081); /* تدرج نابض */
    color: #ffffff;
    transform: rotate(10deg) scale(1.15); /* تدوير وتكبير عند التمرير */
    box-shadow: 0 25px 50px rgba(0, 0, 0, 0.8); /* ظل أعمق وأوسع */
    filter: brightness(1.3) contrast(1.2); /* زيادة الإضاءة والتباين */
    animation: shake 0.5s ease; /* تأثير الاهتزاز */
}

/* تأثير الاهتزاز */
@keyframes shake {
    0% { transform: rotate(10deg) translateX(0); }
    25% { transform: rotate(10deg) translateX(-10px); }
    50% { transform: rotate(10deg) translateX(10px); }
    75% { transform: rotate(10deg) translateX(-10px); }
    100% { transform: rotate(10deg) translateX(0); }
}

/* تنسيق الصور */
.table img {
    width: 300px; /* عرض ثابت للصورة */
    height: 300px; /* ارتفاع ثابت للصورة */
    border-radius: 5%; /* حواف دائرية للصورة */
    border: 1px solid #ddd; /* حدود خفيفة حول الصورة */
    transition: transform 0.5s ease, box-shadow 0.5s ease; /* تأثيرات تفاعلية للصورة */
}

.table img:hover {
    transform: scale(3.3); /* تكبير خفيف عند المرور */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* ظل خفيف عند المرور */
}
/* تنسيق أزرار التصفح */
.dataTables_wrapper .dataTables_paginate .paginate_button {
    padding: 0.75rem 1.5rem;
    font-weight: 600; /* زيادة سمك الخط */
    margin: 0.25rem;
    border: 2px solid #4caf50; /* حدود ملونة بلون أخضر مميز */
    border-radius: 1rem; /* حواف مدورة أكثر عصرية */
    background-color: #ffffff; /* خلفية بيضاء */
    color: #4caf50; /* نص بلون أخضر */
    transition: background-color 0.3s ease, color 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease; /* تأثيرات تفاعلية سلسة */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* ظل خفيف */
}

.dataTables_wrapper .dataTables_paginate .paginate_button:hover {
    background-color: #4caf50; /* خلفية خضراء عند المرور */
    color: #ffffff; /* نص أبيض عند المرور */
    transform: scale(1.05); /* تكبير خفيف عند المرور */
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2); /* ظل أعمق */
}

.dataTables_wrapper .dataTables_paginate .paginate_button.current {
    background-color: #388e3c; /* خلفية زاهية للحالة الحالية */
    color: #ffffff; /* نص أبيض */
    border: 2px solid #388e3c; /* حدود ملونة */
}

/* تنسيق فلتر البحث */
.dataTables_wrapper .dataTables_filter input {
    margin-left: 1rem;
    padding: 0.75rem 1rem; /* تحسين الحشو */
    border-radius: 0.75rem; /* حواف مدورة بشكل عصري */
    border: 2px solid #4caf50; /* حدود ملونة بلون أخضر */
    font-size: 16px; /* حجم خط أكبر */
    transition: border-color 0.3s ease, box-shadow 0.3s ease; /* تأثيرات تفاعلية سلسة */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* ظل أخف */
    color: #333; /* نص داكن للتباين */
    background-color: #ffffff; /* خلفية بيضاء */
    text-align: left;
}

.dataTables_wrapper .dataTables_filter input:focus {
    border-color: #388e3c; /* لون عند التركيز */
    box-shadow: 0 4px 12px rgba(56, 142, 54, 0.3); /* ظل أخضر عند التركيز */
}

/* تنسيق معلومات الجدول */
.dataTables_wrapper .dataTables_info {
    margin-top: 1rem;
    color: #ffffff; /* لون داكن */
    font-size: 18px; /* حجم مناسب */
    font-weight: 600; /* سمك خط عريض */
    color: #f456fff; /* نص أبيض */
}

/* تنسيق الميديا */
@media (max-width: 768px) {
    .table thead th {
        font-size: 14px;
        padding: 12px;
    }
    .table tbody td {
        font-size: 12px;
        padding: 10px;
    }
    .table img {
        width: 70px;
        height: 70px;
    }
}

@media (max-width: 576px) {
    .table thead th {
        font-size: 12px;
        padding: 10px;
    }
    .table tbody td {
        font-size: 10px;
        padding: 8px;
    }
    .table img {
        width: 60px;
        height: 60px;
    }
}

/* تنسيق التحديدات */
textarea.form-control {
    resize: vertical;
    font-size: 0.875rem;
    line-height: 1.5;
    padding: 0.5rem; /* حشو أفضل */
    border: 1px solid #4caf50; /* حدود بلون أخضر */
    border-radius: 0.75rem; /* حواف مدورة */
    background-color: #ffffff; /* خلفية بيضاء */
}

.form-select {
    width: 100%;
    max-width: 250px; /* اتساع أكبر */
    height: auto;
    border: 2px solid #4caf50; /* حدود ملونة */
    border-radius: 0.75rem; /* حواف مدورة */
    background-color: #ffffff; /* خلفية بيضاء */
    padding: 1rem; /* تحسين الحشو */
}

.dropdown-menu {
    max-height: 200px; /* ارتفاع أكبر للتمرير */
    overflow-y: auto;
    border: 1px solid #4caf50; /* حدود ملونة */
    border-radius: 0.75rem; /* حواف مدورة */
    
}

.dropdown-item {
    max-height: 60px; /* ارتفاع العنصر */
    overflow-y: auto;
    padding: 0.75rem; /* حشو إضافي */
}

/* Footer Styling */
.footer {
    background: linear-gradient(135deg, #0f0c29, #302b63, #24243e); /* Space-like gradient */
    color: #ffffff; /* White text */
    border-top: 1px solid #4b4b4b; /* Slightly lighter border */
    padding: 20px 0; /* Ample padding */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.5); /* Soft shadow */
}

.footer a {
    color: #00d2ff; /* Neon blue links */
    text-decoration: none;
    font-size: 0.875rem; /* Slightly smaller font size for links */
    transition: color 0.3s ease; /* Smooth color transition */
}

.footer a:hover {
    color: #ff0081; /* Neon pink on hover */
    text-decoration: underline; /* Underline on hover */
}

.footer p {
    font-size: 0.875rem; /* Slightly larger font size for text */
    margin-bottom: 5px; /* Reduced margin */
    font-family: 'Arial', sans-serif; /* Clean font */
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .footer p {
        font-size: 0.75rem; /* Smaller font size on mobile */
    }
}
    /* تخصيص زر تبديل الأعمدة */
    .btn-colvis-custom {
        background-color: #ff5733; /* لون خلفية زاهي */
        color: white; /* نص باللون الأبيض */
        border: 2px solid #c70039; /* إطار ملون */
        border-radius: 30px; /* زوايا دائرية */
        font-weight: bold; /* نص عريض */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* ظل خلفي */
        transition: all 0.3s ease; /* تأثير الانتقال */
    }
    .btn-colvis-custom:hover {
        background-color: #c70039; /* تغيير اللون عند التمرير بالماوس */
        border-color: #fd7333; /* تغيير لون الإطار عند التمرير */
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3); /* تحسين الظل عند التمرير */
        transform: scale(1.05); /* تكبير الزر عند التمرير */
    }
    
    /* تخصيص زر استعادة الأعمدة */
    .btn-colvis-restore {
        background-color: #007bff; /* لون خلفية زاهي */
        color: white; /* نص باللون الأبيض */
        border: 2px solid #0056b3; /* إطار ملون */
        border-radius: 30px; /* زوايا دائرية */
        font-weight: bold; /* نص عريض */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* ظل خلفي */
        transition: all 0.3s ease; /* تأثير الانتقال */
    }
    .btn-colvis-restore:hover {
        background-color: #0056b3; /* تغيير اللون عند التمرير بالماوس */
        border-color: #007bff; /* تغيير لون الإطار عند التمرير */
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3); /* تحسين الظل عند التمرير */
        transform: scale(1.05); /* تكبير الزر عند التمرير */
    }

            .logo {
            width: 600px; /* يمكنك تعديل الحجم حسب الحاجة */
            height: auto;
            display: block;
            margin: 0 auto;
        }
/* تنسيق الرسالة الترحيبية */
.welcome-message {
    position: relative; /* لتحديد موضع الـ tooltip */
    background-color: #f4f4f9;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 20px;
    margin: 20px;
    font-family: Arial, sans-serif;
    color: #333;
}

/* تنسيق الـ tooltip */
.tooltip {
    visibility: hidden; /* مخفي بشكل افتراضي */
    width: 350px; /* عرض الـ tooltip */
    background-color: #ff5722; /* خلفية زاهية */
    color: #fff; /* لون النصوص */
    text-align: center; /* محاذاة النصوص إلى الوسط */
    border-radius: 10px; /* زوايا دائرية */
    padding: 15px; /* حشو داخلي */
    position: absolute; /* تحديد موضع الـ tooltip */
    bottom: 120%; /* وضع الـ tooltip فوق العنصر */
    left: 50%; /* محاذاة الـ tooltip إلى الوسط أفقيًا */
    margin-left: -175px; /* تعويض العرض لجعل الـ tooltip في المركز */
    opacity: 0; /* إخفاء الـ tooltip */
    transition: opacity 0.3s, transform 0.3s; /* تأثير الانتقال */
    transform: scale(0.8); /* تصغير الـ tooltip بشكل افتراضي */
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3); /* ظل خلفي للـ tooltip */
}

/* إظهار الـ tooltip عند التمرير فوق العنصر */
.welcome-message:hover .tooltip {
    visibility: visible; /* إظهار الـ tooltip */
    opacity: 1; /* جعل الـ tooltip مرئيًا */
    transform: scale(1.1); /* تكبير الـ tooltip عند التمرير */
    background-color: #ff7043; /* تغيير لون الخلفية */
}


   </style>

<body>
    <!-- شريط التحميل -->
    <div id="loading">
        <!-- عنصر يمثل الدائرة المتحركة في شريط التحميل -->
        <div id="spinner"></div>
        <!-- رسالة توضح أن البيانات قيد التحميل من الخادم -->
        <p>Loading data...Server P@2.HA 🕸️</p>
        
        <!-- نص ترحيبي يعرض معلومات عن الخادم والمستودع مع Tooltip مخصص -->
        <div class="welcome-message">
            <h1>🚀 Welcome to Server P@2.HA 🕸️</h1>
            <p>We are excited to have you here! Our server is designed to provide seamless and efficient management for your needs. Here’s a quick overview of what we offer:</p>
            <ul>
                <li>**Warehouse Management**: Efficiently manage and track your inventory with ease.</li>
                <li>**Dragon**: Integrated solutions for resource planning and management.</li>
                <li>**Acc-Shop**: Cutting-edge tools for comprehensive inventory management.</li>
                <li>**Hub**: A centralized platform for managing your brand assets and strategies.</li>
            </ul>
            <p>Explore our features and make the most of our advanced tools to streamline your operations. If you have any questions or need assistance, feel free to contact our support team.</p>
            <p>Happy managing!</p>
            <!-- Tooltip يعرض رسالة ترحيب عند المرور فوق العنصر -->
            <div class="tooltip">
                مرحبا بك ! نحن متحمسون لأنك هنا. خادمنا مصمم لتقديم إدارة سلسة وفعالة لاحتياجاتك. فيما يلي نظرة سريعة على ما نقدمه: إدارة المستودعات، رامكو، Acc-Shop، مركز العلامات التجارية. استكشف ميزاتنا واستفد من أدواتنا المتقدمة لتبسيط عملياتك. إذا كان لديك أي أسئلة أو تحتاج إلى مساعدة، لا تتردد في الاتصال بفريق الدعم لدينا.
            </div>
        </div>

        <!-- إضافة ساعة حية من خدمة خارجية -->
        <script src="https://cdn.logwork.com/widget/clock.js"></script>
        <a href="https://logwork.com/current-time-in-cairo-egypt-al-qahirah" class="clock-time" data-style="greenv5" data-size="100" data-timezone="Africa/Cairo">.</a>
    </div>

    <header>
        <!-- عرض التاريخ والوقت في ترويسة الصفحة -->
        <div class="date-time" id="date-time"></div>

        <!-- نص ترحيبي يعرض معلومات عن الخادم والمستودع -->
        🚀 Welcome to Server P@2.HA 🕸️... 🥳 Online Store to Display Custom Products 🛒🎉  
        Dragon, Acc-Shop, Hub 🏢📦

        <!-- حاوية لعرض الاقتباسات أو الرسائل الأخرى -->
        <div class="quote" id="quote">
            <!-- عرض التاريخ والوقت -->
        </div>
           
             <!-- حاوية للأزرار الخاصة بجدول البيانات -->
        <div id="datatable-buttons" class="btn-group"></div>
    </header>

    <div class="header-text">
   
                <!-- حاوية المحتوى الرئيسي للترويسة -->
        <div class="header-content">
            <div class="container">
                <div class="form-wrapper">
                    <!-- نموذج البحث والفلترة -->
                    <div class="form-group">
                        <label for="column-select" class="form-label">Search Column 🔍:</label>
                        <select id="column-select" class="form-select mb-3">
                            <!-- الخيارات سيتم إضافتها بواسطة JavaScript -->
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="search-input" class="form-label">Search Query 🔎:</label>
                        <textarea id="search-input" class="form-control" rows="2" placeholder="Product name or product ID... 🔎"></textarea>
                    </div>
                    <div class="form-group">
                        <label for="length-select" class="form-label">Records Per Page:</label>
                        <select id="length-select" class="form-select mb-3">
                            <option value="10">10 records per page</option>
                            <option value="25">25 records per page</option>
                            <option value="50">50 records per page</option>
                            <option value="100">100 records per page</option>
                            <option value="-1">Show all records</option>
                        </select>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- عدد السجلات المفلترة سيتم عرضه هنا -->
    <div class="row">
        <div class="col">
            <h1 class="mb-4">
                <!-- لعرض تاريخ آخر تحديث -->
                <div id="filtered-count" class="mb-3"></div>
            </h1>
            <p id="last-update" class="text-center text-light" style="color: white;"></p>
            <!-- عنوان يمكن استخدامه للجدول -->
            <table id="data-table" class="table table-striped table-bordered table-hover" style="width:100%"></table>
            <!-- جدول البيانات المعروض -->
        </div>
    </div>

    <!-- قسم التذييل (الذيل) -->
    <footer class="footer bg-dark text-light py-4">
        <div class="container text-center">
            <p class="mb-1">&copy; 2024 Warehouse 🥳 Online Store to Display Custom Products 🛒🎉 Management.</p>
            <!-- حقوق النشر لصفحة الويب -->
            <p class="mb-1">Powered by <a href="https://script.google.com/macros/s/AKfycbx7RK7Uj5SmOetKmXsm85JTfYvA8fOlZfPmfzAWAw5kVSriW8vWwUd-ialVP21PLdML/exec" target="_blank" class="text-light">Your Server(P@2).H🫰A</a></p>
            <!-- رابط للخادم الخاص بالموقع -->
            <p class="mb-0">
                <a href="https://wa.me/01114566656" class="text-light" target="_blank">
                    Contact us on WhatsApp 📲
                </a>
                <!-- رابط للتواصل عبر WhatsApp -->
            </p>
               <!-- إضافة ساعة حية من خدمة خارجية -->
        <script src="https://cdn.logwork.com/widget/clock.js"></script>
        <a href="https://logwork.com/current-time-in-cairo-egypt-al-qahirah" class="clock-time" data-style="greenv5" data-size="100" data-timezone="Africa/Cairo">.</a>
        </div>
    </footer>
</body>
</body>
</html>
