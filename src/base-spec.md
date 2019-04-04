## 基本原则

> from w3cschool https://www.w3cschool.cn/webdevelopment/q3k8wozt.html

## 结构、样式、行为分离

尽量确保文档和模板只包含  `HTML`  结构，样式都放到样式表里，行为都放到脚本里。

## 缩进

统一**两个空格**缩进（总之缩进统一即可），不要使用  `Tab`  或者  `Tab`和空格混搭。
原因一：IDE snippets工具生成代码是2个缩进的
原因二：现有项目代码大多数使用2个缩进

## 文件编码

**使用不带  `BOM`  的 UTF-8 编码。**

- 在 HTML 中指定编码  `<meta charset="utf-8">` ；
- 无需使用  `@charset`  指定样式表的编码，它默认为  `UTF-8` （参考  [@charset](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset)）；

## 一律使用小写字母

    <!-- 推荐 -->
    <img src="google.png" alt="Google">

    <!-- 不推荐 -->
    <A HREF="/">Home</A>

    /* 推荐 */
    color: #e5e5e5;

    /* 不推荐 */
    color: #E5E5E5;

## 省略外链资源 URL 协议部分

省略外链资源（图片及其它媒体资源）URL 中的  `http` / `https`  协议，使 URL 成为相对地址，避免[Mixed Content](https://developer.mozilla.org/en-US/docs/Security/MixedContent)  问题，减小文件字节数。

**其它协议（`ftp`  等）的 URL 不省略。**

    <!-- 推荐 -->
    <script src="//www.w3cschool.cn/statics/js/autotrack.js"></script>

    <!-- 不推荐 -->
    <script src="http://www.w3cschool.cn/statics/js/autotrack.js"></script>

    /* 推荐 */
    .example {
      background: url(//www.google.com/images/example);
    }

    /* 不推荐 */
    .example {
      background: url(http://www.google.com/images/example);
    }

## 文件与代码结尾
javascript语句用;结尾
文件末尾用一个换行结尾

## 统一注释

通过配置编辑器，可以提供快捷键来输出一致认可的注释模式。

vscode
单行注释 ctrl+/,可定制
多行注释 alt+shift+a,可定制
方法与函数注释： Document This 插件, alt+ctrl+d 重复两次

单行注释必须独占一行。`//`  后跟一个空格
缩进与下一行被注释说明的代码一致

### HTML 注释

- 单行注释

      <!-- 文章列表列表模块 -->
      <div class="article-list">
      ...
      </div>

- 模块注释

      <!--制作内容弹窗-结业考试 - begin-->
      <div class="article-list">
      ...
      </div>
      <!--制作内容弹窗-结业考试 - end-->

### CSS 注释

- 单行注释

      /* 注释title */
      .title {
        background-color: #fff;
      }

- 模块注释

      /* 没有任何配套资料 - begin */
      .not-cover-content-box {
        background-color: #fff;
        padding-bottom: 30px;
        text-align: center;
      }

      .not-cover-content-box .title {
        margin: 0 auto;
        color: #4f4f4f;
      }
      /* 没有任何配套资料 - end */

### SCSS注释

- 单行注释

      // 注释title
      .title {
        background-color: #fff;
      }

- 模块注释

      /* 没有任何配套资料 - begin*/
      .not-cover-content-box {
        background-color: #fff;
        padding-bottom: 30px;
        text-align: center;
      }

      .not-cover-content-box2 .title {
        margin: 0 auto;
        color: #4f4f4f;
      }
      /* 没有任何配套资料 - end*/

### JavaScript 注释

- 单行注释

      // 单行注释
      javacript code

- 多行注释

避免使用  `/*...*/`  这样的多行注释。有多行注释内容时，使用多个单行注释。

      // 推荐
      // if(!this.acceptFileSuffix.includes(file.name.split('.').pop().toUpperCase())) {
      //   return CommonUtils.toast('不支持上传该种文件格式')
      // }
      // if(file.size > 3221225472) {
      //   return CommonUtils.toast('单个视频文件大小不能超过3G')
      // }

      // 不推荐
      /* if(!this.acceptFileSuffix.includes(file.name.split('.').pop().toUpperCase())) {
        return CommonUtils.toast('不支持上传该种文件格式')
      }
      if(file.size > 3221225472) {
        return CommonUtils.toast('单个视频文件大小不能超过3G')
      } */

- 模块注释

      /* js 模块注释 - begin*/
      if(!this.acceptFileSuffix.includes(file.name.split('.').pop().toUpperCase())) {
        return CommonUtils.toast('不支持上传该种文件格式')
      }
      if(file.size > 3221225472) {
        return CommonUtils.toast('单个视频文件大小不能超过3G')
      }
      /* js 模块注释 - end*/

- 函数/方法注释
函数/方法注释必须包含函数说明，有参数和返回值时必须使用注释标识。；
参数和返回值注释必须包含类型信息和说明；
当函数是内部函数，外部不可访问时，可以使用 @inner 标识；

  /\*\*
  函数描述
  
  @param {string} p1 参数 1 的说明
  @param {string} p2 参数 2 的说明，比较长
      那就换行了.
  @param {number=} p3 参数 3 的说明（可选）
  @return {Object} 返回值描述
  \*/
  function foo(p1, p2, p3) {
    var p3 = p3 || 10;
    return {
      p1: p1,
      p2: p2,
      p3: p3
    };
  }

- 文件注释

文件注释用于告诉不熟悉这份文件的读者这个文件中包含哪些东西。 应该提供文件的大体内容、作者、依赖关系和兼容性信息。如下:

    /**
     * @fileoverview Description of file, its uses and information
     * about its dependencies.
     * @author user@meizu.com (Firstname Lastname)
     * Copyright 2015 Meizu Inc. All Rights Reserved.
     */
