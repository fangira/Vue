# async/await

- [以 async/await 为例，说明 babel 插件怎么搭](https://segmentfault.com/a/1190000009673642)

webpack的babel本身不支持async/await

需要安装
```
npm install --save-dev babel-plugin-transform-runtime
npm install --save babel-runtime // `babel-plugin-transform-runtime` 插件本身其实是依赖于 `babel-runtime` 的，但为了适应 `npm install --production` 强烈建议添加该依赖。
```

在`webpack`文件夹目录新增一个`. babelrc`,这份是`babel`配置文件

然后在里面写入
```json
{
  "plugins": ["transform-runtime", "babel-plugin-transform-regenerator", "babel-plugin-transform-es2015-modules-commonjs"]
}
```

把`webpack`的use里面的options注释掉
```js
{
    test: /\.js$/,
    // 除了node_modules|bower_components所有的js文件都用babel-loader处理
    exclude: /(node_modules|bower_components)/,
    use: {
        loader: 'babel-loader',
        // options: {
        //     presets: ['@babel/preset-env']
        // }
    }
}
```
