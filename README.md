# new-promiseify #
---

  本工具可以让异步函数promise化，未满足nodejs回调函数规范的异步函数也可以使用。

---

### 适用范围 ###

+ 仍然在使用回调函数流程的异步函数
+ 遵守nodejs回调函数规范的异步函数
+ 不遵守nodejs回调函数规范的异步函数

---

### 使用方法 ###

       安装：npm install new-promiseify --save-dev

       const promiseify = require('new-promiseify');

       //可以只转换一个函数
       const rmdir = promiseify(fs.rmdir);

       //也可以是多个函数
       const [rdFile, wtFile, mkdir] = promiseify(fs.readFile, fs.writeFile, fs.mkdir);

       //可以满足nodejs回调函数规范
       const [rdFile, wtFile] = promiseify(fs.readFile, fs.writeFile);

       //也可以不满足nodejs回调函数规范
       const [timer, inter] = promiseify([setTimeout, 0, 1], [setInterval, 0, 1]);

       //对于不满足nodejs回调函数规范的参数结构[method, callbackIndex, errorIndex]，需要配置回调函数的索引，error在回调函数参数中的索引
       //如果回调函数参数中不包含error，errorIndex应该配置为大于回调函数参数的最大索引

