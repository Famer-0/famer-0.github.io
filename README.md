<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Мастер-класс по созданию сайтов</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css"  rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script> 
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/flatpickr/dist/flatpickr.min.css"> 
    <style>
        body {
            background: #f8f9fa;
            padding: 20px;
            font-family: 'Segoe UI', sans-serif;
        }
        .card {
            border-radius: 15px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .btn-gradient {
            background: linear-gradient(45deg, #6a11cb, #2575fc);
            color: white;
            border: none;
            transition: all 0.3s ease;
        }
        .btn-gradient:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(38, 76, 160, 0.3);
        }
        .success-message {
            display: none;
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from {opacity: 0;} 
            to {opacity: 1;}
        }
    </style>
</head>
<body>
    <div class="container py-5">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card p-4">
                    <h2 class="text-center mb-4">Регистрация на мастер-класс</h2>
                    <p class="text-center text-muted mb-4">Научитесь создавать современные сайты за 3 часа</p>
                    
                    <form id="registrationForm" class="needs-validation" novalidate>
                        <div class="mb-3">
                            <label for="name" class="form-label">Имя</label>
                            <input type="text" class="form-control" id="name" required>
                            <div class="invalid-feedback">Введите ваше имя</div>
                        </div>

                        <div class="mb-3">
                            <label for="email" class="form-label">Email</label>
                            <input type="email" class="form-control" id="email" required>
                            <div class="invalid-feedback">Введите корректный email</div>
                        </div>

                        <div class="mb-3">
                            <label for="datetime" class="form-label">Выберите дату и время</label>
                            <input type="text" class="form-control" id="datetime" required>
                            <div class="invalid-feedback">Выберите дату и время</div>
                        </div>

                        <div class="d-grid">
                            <button type="submit" class="btn btn-gradient btn-lg">
                                Записаться
                            </button>
                        </div>
                    </form>

                    <div id="successMessage" class="success-message mt-4 text-center text-success">
                        ✅ Вы успешно записались! Подробности придут на ваш email.
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Telegram WebApp SDK -->
    <script src="https://telegram.org/js/telegram-web-app.js"></script> 

    <script>
        // Инициализация календаря
        flatpickr("#datetime", {
            enableTime: true,
            dateFormat: "Y-m-d H:i",
            minDate: "today",
            time_24hr: true,
            locale: {
                firstDayOfWeek: 1
            }
        });

        // Валидация формы
        const form = document.getElementById('registrationForm');
        const successMessage = document.getElementById('successMessage');
        
        form.addEventListener('submit', function(e) {
            e.preventDefault();
            if (form.checkValidity()) {
                // Имитация отправки данных
                document.querySelectorAll('.form-control').forEach(input => {
                    input.disabled = true;
                });
                form.querySelector('button').disabled = true;
                
                // Анимация успеха
                setTimeout(() => {
                    form.style.display = 'none';
                    successMessage.style.display = 'block';
                    
                    // Для Telegram Mini App - отправка данных в Telegram
                    if (window.Telegram && window.Telegram.WebApp) {
                        window.Telegram.WebApp.sendData(JSON.stringify({
                            action: 'registration',
                            name: document.getElementById('name').value,
                            email: document.getElementById('email').value,
                            datetime: document.getElementById('datetime').value
                        }));
                    }
                }, 1000);
            }
            form.classList.add('was-validated');
        });
    </script>
</body>
</html>
