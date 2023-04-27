https://webpack.js.org/guides/getting-started
npm init -y (выполняем данную команду в ТЕРМИНАЛЕ - она создаст файл package.json)
npm install webpack webpack-cli --save-dev (выполняем данную команду в ТЕРМИНАЛЕ - она установит webpack)
В корне проекта создаем файл: webpack.config.js со следующей конфигурацией:
const path = require('path')

// './src/index.js'
module.exports = {
  mode: 'development',
  entry: path.resolve(__dirname, `src`, `index.js`),
  output: {
    filename: 'main.js',
    path: path.resolve(__dirname, 'dist'),
    clean: true,
  },
}
npm install --save-dev html-webpack-plugin (выполняем данную команду в ТЕРМИНАЛЕ - упрощает создание html-файлов во время сборки и настраиваем его: переходим в файл webpack.config.js и импортируем его const HtmlWebpackPlugin = require('html-webpack-plugin') затем подключаем его  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, `index.html`)
    })
  ],
) 
npm install -D babel-loader @babel/core @babel/preset-env webpack (выполняем данную команду в ТЕРМИНАЛЕ - что бы код поддерживался старыми браузерами и подключаем его: переходим в файл webpack.config.js затем подключаем его: module: {
    rules: [
      {
        test: /\.(?:js|mjs|cjs)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [['@babel/preset-env', { targets: 'defaults' }]],
          },
        },
      },
    ],
  },
)
npm install --save-dev style-loader css-loader (выполняем данную команду в ТЕРМИНАЛЕ - для настройки стилей и подключения файлов css и настраиваем его: переходим в файл webpack.config.js и подключаем его в rules: [
     {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
  ],
  так же импортируем наши стили в файле index.js import '../index.css'
) 
для поддержки картинок: переходим в файл webpack.config.js и подключаем их поддержку в rules: [
  {
    test: /\.(png|svg|jpg|jpeg|gif)$/i,
    type: 'asset/resource',
  },  
],
  так же импортируем картинку в файле index.js import JS_IMAGE from '../assets/JavaScript.png' так же не забывая указать ее в src: 
  jsImageHTML.src = JS_IMAGE
npm install --save-dev webpack webpack-dev-server (выполняем данную команду в ТЕРМИНАЛЕ - для запуска проекта на локальном сервере и автоматического окрытия его на нем переходим в файл webpack.config.js и подключаем его в devServer: {
    static: path.resolve(__dirname, `dist`),
    port: 8080,
    open: true,
  },
) 
Облегчаем запуск для этого переходим в файл package.json и добавляем "scripts": {
    "start": "webpack serve"
  },
  для запуска в ТЕРМИНАЛЕ пишем: npm run start
  Остановить: Ctrl + C
