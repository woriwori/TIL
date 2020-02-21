# Webpack Config Issue1

class 내부의 property를 읽지 못하는 에러 발생
```
ERROR in ./board.js 4:7
Module parse failed: Unexpected token (4:7)
You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file. See https://webpack.js.org/concepts#loaders
| import { COLS, ROWS } from './constants';
| class Board {
>   grid = null;
|   reset() {
|     // 게임 시작전 보드 초기화
 @ ./main.js 3:0-32 15:16-21
```

확인해보니, webpack 설정이 잘못됐었음. <br>
webpack 설정을 구글링해서 나온 블로그 따라하면서 복붙해왔더니, 
웹팩에서 babel loader로 컴파일하는 경로를 include로 지정하는 부분이
내 프로젝트에 없는 폴더였음.<br>
즉 내 프로젝트의 파일들이 전부 babel로 컴파일이 안되고 있었음.<br>
그래서 babel loader의 옵션으로 class property를 컴파일해주는 게 안되가지고 에러났던거임. 

``` javascript
module: {
    rules: [
      {
        test: /\.js$/,
        // 아래 include를 지우거나, /src/js를 내 프로젝트에 맞게 설정해야함. 
        //include: [path.resolve(__dirname, '/src/js')],
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
```