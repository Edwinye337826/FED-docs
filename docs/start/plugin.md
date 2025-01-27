# 默认插件

初始项目内部，是通过`@w6s/cli-script`进行构建处理，其中会内含以下插件，并设以默认配置。其外，你也可以通过`w6s.config.js`进行自定义配置。

## babel

bable 使用的是`@vue/cli-plugin-babel`，相关配置请查看`babel.config.js`。其中针对不同项目模板的 UI 库，默认支持按需引入。

## eslint

eslint 使用的是`@vue/cli-plugin-eslint`，相关配置请查看`.eslintrc.js`，当前使用的规范是`@w6s/eslint-config`。

```js
module.exports = {
  root: true,
  extends: ['@w6s'],
  rules: {
    ...
  },
};
```

## stylelint

stylelint 使用的是`@w6s/stylelint-plugin`，相关配置请查看`stylelint.config.js`，当前使用的规范是`@w6s/stylelint-config`。

```js
module.exports = {
  "extends": ["@w6s/stylelint-config"],
};
```

## typescript

相关配置请查看`tsconfig.json`。

## mock

API mock 服务功能，是通过`@w6s/mock-plugin`实现的。依赖于 webpack 的 dev-server，通过 express 中间件的方式来达到模拟请求的效果，所有请求都可以在调试器的 network 一栏查看。插件的默认配置在`w6s.config.js`里，如果不需要，可以将`disable`设置为`true`。

API 的模拟，默认放置在`/mock/index.js`里，`@w6s/mock-plugin`会监听文件的变化，并自动重置所有请求配置。

> 模拟接口的配置文件，必须按 node.js 的模块规范来导出，暂不支持以 es 的模块导出。

## vConsole

[vConsole](https://github.com/Tencent/vConsole) 是腾讯开源的一个轻量、可拓展、针对手机网页的前端开发者调试面板。

通过`@w6s/vconsole-plugin`插件，会自动判断当前环境，只会在开发模式下，也就是`process.env.NODE_ENV === 'development'`时，自动为项目引入 vConsole，便于在移动设备调试。

当前该插件默认在 H5 项目模版启用。

## Sentry

Sentry 是一个实时的事件日志记录和聚合平台。当前我们团队也私有化部署了一套，可以通过[https://sentry.workplus.io/sentry/](https://sentry.workplus.io/sentry/)访问。

而该插件的功能由`@w6s/sentry-plugin`插件提供，主要是用于在项目打包后，上传前端资源文件，例如 js 的`sourcemap`文件。

想了解更多使用 Sentry 的知识，请访问 [使用 Sentry](/DevOps/sentry.html)。

## i18n

该插件使用的是一个叫[vue-cli-plugin-i18n](https://github.com/kazupon/vue-cli-plugin-i18n)的第三方 vue-cli 插件，该插件会注册一个名为`i18n:report`的`command`命令，该命令的主要作用就是检测当前的国际化配置中，哪些属性有遗漏或未被使用。有利于检测国际化配置的完整性，避免不必要的低级错误。

国际化文件，默认存放到`src/locales/`内，为保证统一性，请勿随意修改目录。

## style-resources-loader

该插件是通过`@w6s/style-resources-loader-plugin`实现。主要是依赖了[style-resources-loader](https://github.com/yenshih/style-resources-loader)模块。

该 loader 主要用于：

* 在所有样式文件中共享变量，mixin，函数，因此您无需手动 @import 它们；
* 覆盖其他库提供的样式文件中的变量（例如 element-ui），并自定义您自己的主题。
