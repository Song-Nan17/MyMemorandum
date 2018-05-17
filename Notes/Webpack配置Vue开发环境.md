# ����Webpack�Vue��������

## һ����ʼ����Ŀ�ļ���

�½�һ���ļ��У�·�����������⣩��Ȼ���Terminal���л�·�������ļ��У�ͨ�����������ʼ����

    npm init -y

`-y`�Ǽ򻯵ĳ�ʼ�����̣�����`package.json`���������Զ�ʹ��Ĭ��ֵ��

����Ŀ�ļ������½��ļ��У�`/dist`��`/src`��

��`/src`�ļ������½��ļ���`main.js`��`index.html`��`main.js`�Ǵ��������ļ���

## ������װWebpack��Webpack-cli

ͨ���������װ��

    npm install -D webpack webpack-cli

## ���������������Webpack

ͨ���������װ����ģ�飺

    npm install -D style-loader css-loader webpack-merge vue-loader babel-loader babel-preset-env babel-polyfill html-webpack-plugin clean-webpack-plugin webpack-dev-server vue-template-compiler vue-style-loader

����Ŀ�ļ��еĸ�Ŀ¼���½������ļ���`webpack.dev.conf.js`��`webpack.base.conf.js`��`webpack.prod.conf.js`��

���ݷֱ����£�

**webpack.base.conf.js**

    const path = require('path');
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const CleanWebpackPlugin = require('clean-webpack-plugin');

    module.exports = {
        entry: './src/main.js',
        output: {
            filename: 'bundle.[hash].js',
            path: path.join(__dirname, './dist')
        },
        module: {
            rules: [
                {
                    test: /\.css$/,
                    use: ['style-loader', 'css-loader']
                },
                {
                    test: /\.js$/,
                    use: 'babel-loader',
                    exclude: /node_modules/
                }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
                template: './src/index.html'
            }),
            new CleanWebpackPlugin(['dist'])
        ]
    };

**webpack.dev.conf.js**

    const merge = require('webpack-merge');
    const baseConfig = require('./webpack.base.conf.js');

    module.exports = merge(baseConfig, {
        mode: 'development',
        devtool: 'inline-source-map',
        devServer: {
            port: 3000,
            contentBase: './dist'
        }
    });

**webpack.prod.conf.js**

    const merge = require('webpack-merge');
    const baseConfig = require('./webpack.base.conf.js');

    module.exports = merge(baseConfig, {
        mode: 'production'
    });

## �ġ�����`npm scripts`

�޸�`package.json`����scripts�������¼����������

    // package.json
    {
        "scripts": {
            "start": "webpack-dev-server --open --config webpack.dev.conf.js",
            "build": "webpack --config webpack.prod.conf.js"
        }
    }

���ڿ��Բ���webpack�Ļ������ã�

�޸�ҳ���ļ������ݷֱ����£�

**index.html**

    <html>
        <head>
            <meta charset="utf-8"/>
            <title>Vue & Webpack</title>
        </head>
        <body>
            <div id="app">
                <h1>Hello Vue & Webpack!</h1>
            </div>
        </body>
    </html>

**main.js**

    console.log('Yes!');

��������`npm run start`��`npm run build`���ֱ�鿴Ч����

## �塢����Vue��������

ͨ���������װVueģ�飺

    npm install --save vue

��`webpack.base.conf.js`��`module.rules`�����£���**js��css�Ĺ���֮ǰ**�¼�һ�������޸�֮��`webpack.base.conf.js`�������£�

    const path = require('path');
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const CleanWebpackPlugin = require('clean-webpack-plugin');

    module.exports = {
        entry: './src/main.js',
        output: {
            filename: 'bundle.[hash].js',
            path: path.join(__dirname, './dist')
        },
        module: {
            rules: [
                {
                    test: /\.vue$/,
                    use: 'vue-loader'
                },
                {
                    test: /\.css$/,
                    use: ['style-loader', 'css-loader']
                },
                {
                    test: /\.js$/,
                    use: 'babel-loader',
                    exclude: /node_modules/
                }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
                template: './src/index.html'
            }),
            new CleanWebpackPlugin(['dist'])
        ]
    };

