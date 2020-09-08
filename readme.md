# 1. Настройка webpack и окружения проекта:

## 1.1 npm init

## 1.2 npm install --save-dev webpack webpack-cli webpack-dev-server

или
npm install -D webpack webpack-cli webpack-dev-server

## 1.3 Создаем файл webpack.config.js

Данный файл будет запускаться на платформе node.js и после он будет собирать наш проект и с ним взаимодействовать. Учитывая что это node.js здесь можно пользоваться конструкциями которые доступны в node.js.
Задача этого файла в том чтобы из него экспортировался обычный js объект, который является объектом конфигурации. И минимальный набор конфигураций для webpack это точка входа в проект, файл с которого все начинается и далее он тащит за собой список зависимостей.
Создаем папку src и файл index.js.
webpack.config.js:

```js
const path = require("path");
module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
};
```

## 1.4 Создаем script в package.json:

"scripts": {
"build": "webpack --mode production"
}
запустив команду: npm run build - получим готовый минифицированный проект.
Если хотим увидеть не минифицированный проект, меняем флаг на development:
"build": "webpack --mode development"

## 1.5 Создаем настройку в файл webpack.config.js для webpack-dev-server:

```js
const path = require("path");
module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  devServer: {
    port: 3000,
  },
};
```

## 1.5 Создаем script в package.json для webpack-dev-server:

"serve": "webpack-dev-server --mode development"

## 1.6 Теперь настраиваем работу с html:

### 1.6.1 по документации работы с webpack:

https://webpack.js.org/plugins/html-webpack-plugin/
устанавливаем пакет:
npm install --save-dev html-webpack-plugin

### 1.6.2 В src создаем index.html и его базовую разметку, а также

### 1.6.3 В webpack.config.js подключаем этот плагин:

const HtmlWebpackPlugin = require('html-webpack-plugin');

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "dist"),
  },
  devServer: {
    port: 3000,
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html",
    }),
  ],
};
```

### 1.6.4 Запустив команду npm run build, в dist появятся минифицированные index.html, а также bundle.js

Можно запустить index.html и убедиться что все работает.

### 1.6.5 Запустив команду npm run serve, проект запуститься на http://localhost:3000/ и также можна проверить что все работает.
