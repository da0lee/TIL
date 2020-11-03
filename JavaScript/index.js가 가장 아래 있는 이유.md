> 소스코드 : prgrms-devjs3-practice

> index.html

<br/>

# src/main.js 가 가장 아래 있는 이유
앞선 utility들을 실행하고 마지막에 main.js 실행하라는 의미

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <link rel="stylesheet" href="src/style.css" />
    <title>Cat Search</title>
  </head>
  <body>
    <div id="App"></div>
    <script src="src/utils/validator.js"></script>
    <script src="src/api.js"></script>
    <script src="src/ImageInfo.js"></script>
    <script src="src/DarkLightBtn.js"></script>
    <script src="src/SearchInput.js"></script>
    <script src="src/SearchResult.js"></script>
    <script src="src/App.js"></script>
    <script src="src/main.js"></script>
  </body>
</html>
```