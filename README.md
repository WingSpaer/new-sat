<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Магазин</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;500&display=swap');
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Montserrat', sans-serif;
            font-weight: 200;
            --tg-theme-text-color: black;
            --tg-theme-bg-color: white;
            --tg-theme-button-text-color: white;
            --tg-theme-secondary-bg-color: #007BFF;
            color: var(--tg-theme-text-color);
            background: var(--tg-theme-bg-color);
        }
        #main {
            width: 100%;
            padding: 20px;
            text-align: center;
        }
        h1 {
            margin-top: 50px;
            margin-bottom: 10px;
        }
        img {
            width: 70px;
            margin: 30px auto;
        }
        p {
            width: 70px;
            margin: 0 auto;
        }
        button {
            border: 0;
            border-radius: 5px;
            margin-top: 50px;
            height: 60px;
            width: 200px;
            font-size: 20px;
            font-weight: 500;
            cursor: pointer;
            transition: all 500ms ease;
            color: var(--tg-theme-button-text-color);
            background: var(--tg-theme-secondary-bg-color);
        }
        button:hover {
            background: #0056b3;
        }
        form {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }
        input {
            margin-bottom: 10px;
            padding: 10px;
            width: 300px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        #order {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Онлайн магазин</h1>
    </header>
    <main>
        <div id="main">
            <img src="https://cdn-icons-png.flaticon.com/512/3595/3595455.png" alt="Логотип магазина">
            <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusantium ipsum magni, molestias</p>
            <button id="buy">Купить</button>
        </div>
        <form id="form">
            <input type="text" placeholder="Имя" id="user_name" required>
            <input type="email" placeholder="Email" id="user_email" required>
            <input type="tel" placeholder="Телефон" id="user_phone" required>
            <div id="error"></div>
            <button id="order">Оформить</button>
        </form>
    </main>
    <script src="https://telegram.org/js/telegram-web-app.js"></script>
    <script>
        let tg = window.Telegram.WebApp;
        let buy = document.getElementById("buy")
        let order = document.getElementById("order")
        tg.expand();
        buy.addEventListener("click", () => {
            document.getElementById("main").style.display = "none"
            document.getElementById("form").style.display = "block"
            document.getElementById("user_name").value = tg.initDataUnsafe.user.first_name + " " + tg.initDataUnsafe.last_name
        });
        order.addEventListener("click", () => {
            document.getElementById("error").innerText = '';
            let name = document.getElementById("user_name").value
            let email = document.getElementById("user_email").value
            let phone = document.getElementById("user_phone").value
            if(name.length < 5){
                document.getElementById("error").innerText = "ошибка в имени";
                return;
            }
            if(email.length < 5){
                document.getElementById("error").innerText = "ошибка в email";
                return;
            }
            if(phone.length < 5){
                document.getElementById("error").innerText = "ошибка в номере телефона";
                return;
            }

            let data = {
                name: name,
                email: email,
                phone: phone
            }
            tg.sendData(JSON.stringify(data));

            tg.close()
        })
    </script>
</body>
</html>
