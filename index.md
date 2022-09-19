<!DOCTYPE html>
<html>
<head>
   <meta charset="UTF-8">
   <meta http-equiv="X-UA-Compatible" content="IE=edge">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <title>Test Telegram WebApps API</title>
   <script src="https://telegram.org/js/telegram-web-app.js"></script> <!--Подключаем скрипт от телеграм-->

   <style>
    * {
   box-sizing: border-box;
}
body {
   background: #f69a73;
}
.decor {
   position: relative;
   max-width: 400px;
   margin: 50px auto 0;
   background: white;
   border-radius: 30px;
}
.form-left-decoration, .form-right-decoration {
   content: "";
   position: absolute;
   width: 50px;
   height: 20px;
   background: #f69a73;
   border-radius: 20px;
}
.form-left-decoration {
   bottom: 60px;
   left: -30px;
}
.form-right-decoration {
   top: 60px;
   right: -30px;
}
.form-left-decoration:before, .form-left-decoration:after, .form-right-decoration:before, .form-right-decoration:after {
   content: "";
   position: absolute;
   width: 50px;
   height: 20px;
   border-radius: 30px;
   background: white;
}
.form-left-decoration:before {
   top: -20px;
}
.form-left-decoration:after {
   top: 20px;
   left: 10px;
}
.form-right-decoration:before {
   top: -20px;
   right: 0;
}
.form-right-decoration:after {
   top: 20px;
   right: 10px;
}
.circle {
   position: absolute;
   bottom: 80px;
   left: -55px;
   width: 20px;
   height: 20px;
   border-radius: 50%;
   background: white;
}
.form-inner {
   padding: 50px;
}
.form-inner input, .form-inner textarea {
   display: block;
   width: 100%;
   padding: 0 20px;
   margin-bottom: 10px;
   background: #E9EFF6;
   line-height: 40px;
   border-width: 0;
   border-radius: 20px;
   font-family: 'Roboto', sans-serif;
}
.form-inner input[type="submit"] {
   margin-top: 30px;
   background: #f69a73;
   border-bottom: 4px solid #d87d56;
   color: white;
   font-size: 14px;
}
.form-inner textarea {
   resize: none;
}
.form-inner h3 {
   margin-top: 0;
   font-family: 'Roboto', sans-serif;
   font-weight: 500;
   font-size: 24px;
   color: #707981;
}
   </style>
</head>

<body>
  
    <form class="decor">
        <div class="form-left-decoration"></div>
        <div class="form-right-decoration"></div>
        <div class="circle"></div>
        <div class="form-inner">
        <h3>Написать нам</h3>
        <input id="name" type="text" placeholder="Имя">
        <input id="phone" type="tel" pattern="\+7\s?[\(]{0,1}9[0-9]{2}[\)]{0,1}\s?\d{3}[-]{0,1}\d{2}[-]{0,1}\d{2}" placeholder="+7(___)___-__-__">
        <textarea id="message" placeholder="Сообщение..." rows="3"></textarea>
        </div>
        </form>
</body>

<script>
     function setCursorPosition(pos, e) {
    e.focus();
    if (e.setSelectionRange) e.setSelectionRange(pos, pos);
    else if (e.createTextRange) {
      var range = e.createTextRange();
      range.collapse(true);
      range.moveEnd("character", pos);
      range.moveStart("character", pos);
      range.select()
    }
  }

  function mask(e) {
    //console.log('mask',e);
    var matrix = this.placeholder,// .defaultValue
        i = 0,
        def = matrix.replace(/\D/g, ""),
        val = this.value.replace(/\D/g, "");
    def.length >= val.length && (val = def);
    matrix = matrix.replace(/[_\d]/g, function(a) {
      return val.charAt(i++) || "_"
    });
    this.value = matrix;
    i = matrix.lastIndexOf(val.substr(-1));
    i < matrix.length && matrix != this.placeholder ? i++ : i = matrix.indexOf("_");
    setCursorPosition(i, this)
  }
  window.addEventListener("DOMContentLoaded", function() {
    var input = document.querySelector("#phone");
    input.addEventListener("input", mask, false);
    input.focus();
    setCursorPosition(3, input);
  });
   let tg = window.Telegram.WebApp; //получаем объект webapp телеграма 

   tg.expand(); //расширяем на все окно  

   tg.MainButton.text = "Отправить"; //изменяем текст кнопки 
   
   tg.MainButton.textColor = "#white"; //изменяем цвет текста кнопки
   tg.MainButton.color = "##f69a73"; //изменяем цвет бэкграунда кнопки


 

 

   Telegram.WebApp.onEvent('mainButtonClicked', function(){
      tg.sendData("some string that we need to send"); 
      //при клике на основную кнопку отправляем данные в строковом виде
   });


</script>
</html>
