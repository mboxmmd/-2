<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>محاسبه سود اقساطی</title>
    <!-- اضافه کردن لینک CDN فونت Yekan -->
    <link href="https://cdn.jsdelivr.net/gh/google/fonts@main/legacy-fonts/Yekan.css" rel="stylesheet">
    <style>
        body {
            font-family: 'Yekan', sans-serif; /* استفاده از فونت Yekan */
            background: #f5f5f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            padding: 10px;
        }

        .calculator {
            background: #fff;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            padding: 30px;
            width: 100%;
            max-width: 500px;
            animation: fadeIn 1s ease-out;
            box-sizing: border-box;
        }

        @keyframes fadeIn {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            100% {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .calculator h2 {
            text-align: center;
            font-size: 24px;
            color: #333;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-size: 16px;
            color: #444;
            font-weight: 600;
        }

        .form-group input {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #ddd;
            background-color: #f9f9f9;
            font-size: 16px;
            transition: all 0.3s ease;
            box-sizing: border-box;
        }

        .form-group input:focus {
            border-color: #007BFF;
            background-color: #fff;
            outline: none;
        }

        .form-group button {
            width: 100%;
            padding: 14px;
            background: #007BFF;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .form-group button:hover {
            background: #0056b3;
            transform: translateY(-2px);
        }

        /* بخش نتایج */
        .result {
            margin-top: 20px;
            background: linear-gradient(135deg, #e3f2fd, #bbdefb);
            padding: 25px;
            border-radius: 10px;
            color: #333;
            font-weight: bold;
            text-align: center;
            display: none;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
            animation: slideIn 1s ease-out;
            box-sizing: border-box;
        }

        @keyframes slideIn {
            0% {
                opacity: 0;
                transform: translateX(50px);
            }
            100% {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .result p {
            margin: 15px 0;
            font-size: 18px;
            line-height: 1.6;
        }

        .result .amount {
            font-size: 22px;
            color: #1b5e20;
            font-weight: bold;
        }

        /* استایل برای آیکن‌ها */
        .result i {
            font-size: 24px;
            margin-left: 10px;
            color: #007BFF;
        }

        .logo {
            display: block;
            margin-top: 30px;
            max-width: 200px; /* اندازه جدید لوگو */
            height: auto;
            margin-left: auto;
            margin-right: auto;
            animation: zoomIn 1.2s ease;
        }

        @keyframes zoomIn {
            0% {
                transform: scale(0.7);
                opacity: 0;
            }
            100% {
                transform: scale(1);
                opacity: 1;
            }
        }

    </style>
</head>
<body>
    <div class="calculator">
        <h2>محاسبه سود اقساطی</h2>
        <div class="form-group">
            <label for="capital">سرمایه اولیه (تومان):</label>
            <input type="text" id="capital" placeholder="مبلغ سرمایه اولیه را وارد کنید" oninput="formatInput(this)" inputmode="decimal">
        </div>
        <div class="form-group">
            <label for="rate">نرخ سود ماهانه (%):</label>
            <input type="number" id="rate" placeholder="نرخ سود ماهانه را وارد کنید">
        </div>
        <div class="form-group">
            <label for="months">تعداد ماه:</label>
            <input type="number" id="months" placeholder="تعداد ماه را وارد کنید">
        </div>
        <div class="form-group">
            <button onclick="calculateProfit()">محاسبه</button>
        </div>
        <div id="result" class="result">
            <p>سود ماهانه شما: <span class="amount" id="monthly-profit"></span> <i class="fas fa-dollar-sign"></i></p>
            <p>سود کل (ماهانه): <span class="amount" id="total-profit"></span> <i class="fas fa-piggy-bank"></i></p>
            <p>مبلغ کل بازپرداخت: <span class="amount" id="total-amount"></span> <i class="fas fa-money-bill-wave"></i></p>
            <p>مبلغ هر قسط: <span class="amount" id="installment"></span> <i class="fas fa-credit-card"></i></p>
        </div>
        <img class="logo" src="https://s32.picofile.com/file/8481556242/%D9%84%D9%88%DA%AF%D9%88_%D8%B3%D8%A7%DB%8C%D8%AA.png" alt="لوگو سایت">
    </div>

    <script>
        function formatToToman(amount) {
            return amount.toLocaleString('fa-IR') + ' تومان';
        }

        function formatInput(input) {
            const value = input.value.replace(/,/g, '').replace(/[^0-9.]/g, '');
            if (!isNaN(value) && value !== '') {
                const parts = value.split('.');
                parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ',');
                input.value = parts.join('.');
            } else {
                input.value = '';
            }
        }

        function calculateProfit() {
            const capitalInput = document.getElementById('capital').value.replace(/,/g, '');
            const capital = parseFloat(capitalInput);
            const rate = parseFloat(document.getElementById('rate').value);
            const months = parseInt(document.getElementById('months').value);

            if (isNaN(capital) || isNaN(rate) || isNaN(months) || capital <= 0 || rate <= 0 || months <= 0) {
                alert('لطفاً اعداد معتبر و مثبت وارد کنید.');
                return;
            }

            const monthlyProfit = (capital * rate) / 100;
            const totalProfit = monthlyProfit * months;
            const totalAmount = capital + totalProfit;
            const installment = Math.round(totalAmount / months);

            const resultDiv = document.getElementById('result');
            document.getElementById('monthly-profit').innerText = formatToToman(monthlyProfit);
            document.getElementById('total-profit').innerText = formatToToman(totalProfit);
            document.getElementById('total-amount').innerText = formatToToman(totalAmount);
            document.getElementById('installment').innerText = formatToToman(installment);
            resultDiv.style.display = 'block';
        }
    </script>
</body>
</html>
