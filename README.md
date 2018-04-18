# Angular CLI 1.7.4 SCSS sourcemap fix

`./node_modules/@angular/cli/models/webpack-configs/styles.js`

**in line 180**

```javascript
// const commonLoaders = [
//     { loader: 'raw-loader' },
// ];
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
        'exports-loader?module.exports.toString()',
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

`ng serve --sourcemap --extractCss   // has sourcemap ` 
