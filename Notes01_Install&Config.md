# react native开发环境搭建
- 这篇文章参考教程：https://www.react-native.cn/docs/environment-setup
- 参考视频教程：https://www.bilibili.com/video/BV1E22UYfEsx/
- 以Windows平台配置Android开发为例
## 安装依赖
使用react native开发必须安装的依赖：
- Node.js：是JavaScript的运行时环境，用于打包js代码（官网下载）
- JDK：运行java代码（https://www.oracle.com/java/technologies/downloads/#java17）
- Yarn：JavaScript包管理工具，用于替代npm
- Android Studio：Android虚拟机和Android SDK

### 切换淘宝源
```bash
# 使用nrm工具切换淘宝源
npx nrm use taobao

# 如果之后需要切换回官方源可使用
npx nrm use npm
```
### 安装Android SDK
图形化安装工具中需要配置代理
代理地址：http://mirrors.aliyun.com:80

### 配置ANDROID_HOME环境变量
1. 在环境变量设置中讲Android SDK的目录添加到环境变量  
2. 将Android SDK添加到PATH：
```bash
%ANDROID_HOME%\platform-tools
```

## 创建新项目
用react native的初始化命令创建新项目
```bash
npx @react-native-community/cli init AwesomeProject
```
### 配置Android studio虚拟机并用虚拟机调试
```bash
cd AwesomeProject
yarn android
# 或者
yarn react-native run-android
```
若配置正确，模拟器会打开并启动项目，第一次启动会比较慢
此时可以在项目中的`App.tsx`随意改上几行并查看效果了

## 项目结构
- .bundle：这个文件夹通常用于存储打包后的 JavaScript 代码。在 React Native 项目中，使用 react-native bundle 命令时，生成的 JavaScript 代码会被打包成 .bundle 文件，供生产环境使用。
- android：这个文件夹包含了 Android 平台的特定代码和配置，类似于一个原生的 Android 项目。里面包含 build.gradle、AndroidManifest.xml 等文件，供构建和配置 Android 应用时使用。
- ios：这个文件夹包含了 iOS 平台的特定代码和配置，类似于一个原生的 iOS 项目。它包含 Xcode 项目文件（.xcodeproj 或 .xcworkspace），配置和构建脚本，供构建和配置 iOS 应用时使用。
- node_modules：这个文件夹包含了项目的所有依赖包。在运行 yarn install 或 npm install 时，所有的第三方库和模块都会被下载并安装到这里。
- tests：这个文件夹通常包含了项目的测试文件。React Native 项目中，通常使用 Jest 作为测试框架，__tests__ 文件夹里放置的是测试脚本。
文件：
- .eslintrc.js：这是 ESLint 配置文件，控制代码的静态分析规则。ESLint 用于查找和修复 JavaScript 代码中的问题，比如代码风格问题、潜在的错误等。
- .gitignore：该文件指定了哪些文件或文件夹应该被 Git 忽略，避免将临时文件、构建文件、依赖文件等不需要版本控制的内容加入到 Git 仓库中。
- .prettierrc.js：这是 Prettier 配置文件，Prettier 是一个代码格式化工具，用于自动格式化代码，确保代码风格的一致性。
- .watchmanconfig：这个文件是 Watchman 的配置文件。Watchman 是一个由 Facebook 开发的工具，用于监视文件系统的变化。React Native 使用它来监控源代码的变化并触发构建和重新加载。
- app.json：这是 React Native 项目的配置文件，包含了一些应用的元数据，如名称、图标、启动画面等。React Native 会从这个文件读取配置。
- App.tsx：这是 React Native 项目的入口文件，包含了应用的主要组件。你在这里定义了应用的初始布局和主要组件。
- babel.config.js：这是 Babel 配置文件，Babel 是一个 JavaScript 编译器，它将 ES6+ 和 JSX 转换为兼容的 JavaScript 代码。这个文件用于配置 Babel 如何处理代码。
- Gemfile：这个文件通常与 Ruby 环境相关，React Native 中的 iOS 项目通常依赖于 CocoaPods，它是通过 Ruby gem 来管理的。因此，Gemfile 用于指定项目所需的 Ruby gem。
- index.js：这是应用的入口文件。在 React Native 项目中，index.js 用于注册根组件并挂载到设备或模拟器上。
- jest.config.js：这是 Jest 测试框架的配置文件，Jest 用于运行单元测试和集成测试。该文件定义了 Jest 的运行环境和测试设置。
- metro.config.js：这是 Metro Bundler 的配置文件，Metro 是 React Native 使用的 JavaScript 打包工具。metro.config.js 用于配置打包过程中的一些选项，如自定义缓存、模块解析等。
- package-lock.json：这是 npm 自动生成的文件，记录了项目依赖的确切版本。它确保项目中的每个开发者使用的依赖版本完全相同。
- package.json：这是项目的核心配置文件，包含了项目的元数据（如项目名称、版本、描述等），以及项目所依赖的 npm 包（依赖、开发依赖）、脚本命令等。
- README.md：这是项目的说明文件，通常包含了项目的描述、安装指南、使用方法、贡献方式等信息。
- tsconfig.json：这是 TypeScript 配置文件，定义了 TypeScript 编译器的行为和项目的编译选项。在使用 TypeScript 时，React Native 项目会用这个文件来配置如何处理 TypeScript 代码。

## 安装ES7插件
安装vscode插件：ES7 React/Redux/GraphQL/React-Native snippets  
该插件可以实现快速代码补全，如输入rsc即可得到一段和class有关的代码  
## 调试工具
### 真机调试
链接usb并启动调试模式（不同手机方式不一样）
### 模拟器调试
- ctrl + m打开开发者菜单
- open dev tools即可按照开发网页的方式开发
```js
console.log("hello, react")
```
打印到终端