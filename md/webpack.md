# webpack简单服务器配置
1. 全局安装webpack <br/>
`cnpm install webpack -g`
2. 本项目安装webpack <br/>
`cnpm install webpack --save`
3. 本项目安装webpack-cli、webpack-dev-server <br/>
`cnpm install webpack-cli webpack-dev-server --save`
4. 配置webpack.config.js文件
```js
//引入node内置模块
const path = require('path');

module.exports = {
  //设置入口文件路径
  entry: './src/index.js',
  //设置出口文件路径
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  //设置服务器
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    compress: true,
    port: 9000
  }
};
```
5. 命令行 <br/>
`webpack-dev-server`
