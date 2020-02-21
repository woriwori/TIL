# VanilaJS 프로젝트에 Babel, Webpack 세팅하기

1. npm 프로젝트로 선언
   - npm init -y
   - package.json이 생성됨
2. babel 설치
   - npm i -D @babel/core @babel/cli @babel/preset-env
   - Babel 프리셋 : 함께 사용되어야하는 Babel 플러그인을 모아둔 것. 필요한 플러그인들을 프로젝트 지원환경에 맞게 동적으로 결정해줌.
   - .babelrc 파일을 생성하고 아래 코드를 넣자.

```
{
    "presets": ["@babel/preset-env"]
}
```

3. webpack 설치
   - npm i -D webpack webpack-cli babel-loader
4. package.json의 script 수정
   - "build": "webpack -w"
   - w 옵션은 watch 옵션으로, webpack 커맨드 실행 후 계속 프로젝트 변경사항을 확인해서, 변경이 발생할 때마다 직접 recompile 해줌. -w 없으면 직접 매번 다시 webpack 커맨드치면 됨.
5. webpack.config.js 파일 추가

   ```javascript
   const path = require('path');

    module.exports = {
    entry: './main.js', // 최초 루트 파일

    // 컴파일 + 번들링된 js 파일이 저장될 경로와 이름 지정
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'bundle.js'
    },
    module: {
        rules: [
        {
            test: /\.js$/,
            include: [
            path.resolve(__dirname, 'src/js')
            ],
            exclude: /node_modules/,
            use: {
            loader: 'babel-loader',
            options: {
                presets: ['@babel/preset-env']
            }
            }
        }
        ]
    },
    devtool: 'source-map',
    // https://webpack.js.org/concepts/mode/#mode-development
    mode: 'development'
    };
   ```

6. index.html에 bundle.js를 참조하는 코드 추가
   ```html
   <script src="./dist/bundle.js"></script>
   ```
7. npm run build 실행
8. live server extension으로 index.html 을 띄운 결과물 확인

출처 : https://poiemaweb.com/es6-babel-webpack-1
