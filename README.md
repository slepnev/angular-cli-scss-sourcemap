# Angular CLI 1.7.4 scss sourcemap fix

##### npm
`npm install --save css-loader exports-loader`

`npm install --save-dev gulp gulp-inject gulp-inject-string gulp-sass gulp-sourcemaps map-stream`

##### ./node_modules/@angular/cli/models/webpack-configs/styles.js
`in line 180`
```javascript
// const commonLoaders = [
//     { loader: 'raw-loader' },
// ];
// new code
const commonLoaders = [
    {
        loader: 'css-loader',
        options: {
            sourceMap: cssSourceMap,
            import: false,
        }
    }
];
// load component css as raw strings
const rules = baseRules.map(({ test, use }) => ({
    exclude: globalStylePaths, test, use: [
        'exports-loader?module.exports.toString()', // <- new
        ...commonLoaders,
        {
            loader: 'postcss-loader',
            options: {
                ident: 'embedded',
                plugins: postcssPluginCreator,
                sourceMap: cssSourceMap
            }
        },
        ...use
    ]
}));
```

##### package.json
`ng serve --sourcemap --extractCss   // has sourcemap ` 
