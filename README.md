<font face="微软雅黑">
# FrontEndLearning
前端学习项目
-创建于2018-09-20

https://webpack.js.org/guides/installation/ webpack学习笔记(第一次写markdown 丑的一比)
---
1. ## 不用自己编写index.html
```
    plugins: [  
        new HtmlWebpackPlugin({  
            title: 'Output Management'  
        })  
    ],  
```
---
2. # 自动清理目录
```
    new CleanWebpackPlugin(['dist']),  
```
---
3. ## 生产环境源码打断点
```
    devtool: 'inline-source-map',  
```
---
4. ## 本地server
```
    "start": "webpack-dev-server --open",  
    devServer: {  
        contentBase: './dist'  
    },  
```
---
5. ## 热模块更换Hot Module Replacement (or HMR)
```
    devServer: {  
        contentBase: './dist',  
        hot: true  
    },  
    new webpack.HotModuleReplacementPlugin() 
``` 
---
6. ## Tree Shaking 不使用的模块不打包 类似修剪树枝
```
    mode: 'development'
```
---
7. ## 区分环境配置
```
    const merge = require('webpack-merge');  
    "start": "webpack-dev-server --open --config webpack.dev.js",  
```
---
8. ## 模块公共引用的部分不重复打包
```
    optimization: {  
        splitChunks: {  
            chunks: 'all'  
        }  
    }  

    async function getComponent() {  
        var element = document.createElement('div');  
        const { default: _ } = await import(/* webpackChunkName: "lodash" */ 'lodash');  
        element.innerHTML = _.join(['Hello', 'webpack'], ' ');  
        return element;  
    } 
``` 
---
9. ## 文件名控制cache
```
    filename: '[name].[contenthash].js',  
  
    optimization: {  
        runtimeChunk: 'single',  
        splitChunks: {  
            cacheGroups: {  
                vendor: {  
                test: /[\\/]node_modules[\\/]/,  
                name: 'vendors',  
                chunks: 'all'  
            }  
        }  
    }  
 ```

---
10. ## Shimming(垫片) 某些lib在代码里使用了$ 之类的全局对象
```
    plugins: [  
         new webpack.ProvidePlugin({  
            _: 'lodash'  
        })  
    ]  
```
---
11. ## Progressive Web Applications (or PWAs) 渐进式网站应用??
```
    yarn add http-server --save-dev  
    "start": "http-server dist"  
```
---
</font>