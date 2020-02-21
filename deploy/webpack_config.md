# Webpack

웹팩(Webpack) = Javascript Module Bundler

webpack.config.js = 웹팩 설정파일

### 웹팩이 필요한 이유?
기존에 외부 라이브러리를 연동할때에는 HTML 파일에 script로 불러와서 HTML 파일과 의존성이 생김.

또한 HTTP 로 필요한 컨텐츠를 각각 요청하는게 비효율적이라, import, require등으로 js 파일들을 합치고, 모듈화해서 요청하는 개념이 생김.
그래서 이러한 점들을 극복할 수 있는 번들러가 나왔고, webpack은 그중 하나.
(그외에 gulp, grunt 등이 있다고함)


### 웹팩 설정 파일 
1. entry 부터 파일을 읽어들임.
2. module.rules 를 거쳐서 test 에 부합하는 파일들을 loader에  지정한 로더가 컴파일 해줌. options는 로더에 대한 옵션임. exclude는 컴파일 안할 파일들이고, include는 컴파일할 파일을 지정하는것. 
3. output으로 내보낼 파일의 이름, 경로등을 설정.

```javascript
const path = require('path');

module.exports = {
  entry: './main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        include: [path.resolve(__dirname, '/src/js')],
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
            plugins: ['@babel/plugin-proposal-class-properties'],
          },
        },
      },
    ],
  },
  devtool: 'source-map',
  mode: 'development',
};

```
<br>
<br>


참고
- https://www.zerocho.com/category/Webpack/post/58aa916d745ca90018e5301d
- https://www.daleseo.com/webpack-basics/