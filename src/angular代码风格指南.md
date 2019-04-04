## 官方指南
> https://angular.cn/guide/styleguide

## 单一职责
- 单一规则
一个文件定义一样东西，比如一个组件、一个服务、一个管道、一个指令
每个文件最多不要超过400行
- 小函数
定义功能单一的函数
一个函数最多不要超过75行

## 代码规范

### 同类代码写在一块

#### 将变量、@Input、@Output、生命周期钩子写在一块
顺序为：
const类型变量
let类型变量
Subject变量
@Input
@Output
construct
生命周期钩子
其他方法

#### import顺序

- angular库在第一层
- 第三方库在第二层
- 教学项目公共库在第三层
- 模块内项目本身文件在第四层
各层之间用空一行的方式来区分
```ts

import { Component, EventEmitter, Input, OnDestroy, OnInit, Output } from '@angular/core';

import { Subject, BehaviorSubject } from "rxjs";
import { debounceTime } from 'rxjs/operators';
import { DragulaService } from "ng2-dragula/ng2-dragula";

import { HttpService, CommonUtils } from "../../../../../http.service";

import { CCourseWare, CCourseWareCatalog } from "../../../../model/CCourseWare";
import { REQUEST_URL } from "../../../banke-content-manage.api";
import { CATALOG_TYPES, CONTENT_TYPES } from "../../../../banke-constant";
import { REQUEST_BANKE_URL } from '../../../../ban-ke.api';

```


### scss文件

_color.scss无法自动import，且切换目录层级的时候会报错，所以不建议引入

## 项目结构
好的项目结构的准则就是快速定位，快速识别，尽可能保持扁平，不要写冗余／重复代码
把所有项目代码放入src文件夹，为每个特性创建文件夹
第三方库放在src外的一个文件夹
每个组件、服务、管道、指令都独成一个文件
当组件有多个附属文件时（htm，css，ts，spec.ts），建议创建一个独立的文件夹

## 模块
在src/app下创建根模块，建议命名为app.module.ts
为每个特性创建一个模块，并且保持文件夹命名和模块命名一致
共享模块建议用SharedModule命名，放在app/shared/shared.module.ts中
在共享模块中定义复用的组件、指令和管道，避免在共享模块中定义服务
在共享模块中导入所有必需的模块，比如CommonModule和FormsModule，导出所有复用的模块、组件、指令、管道
考虑将只用一次的类放在核心特性模块中，并且仅在根模块中导入，建议写guard.ts来保证
核心特性模块建议用CoreModule命名，放在app/core/core.module.ts中
将单例服务放在核心特性模块中，比如ExceptionService和LoggerService
在核心特性模块中导入所有必需的模块，比如CommonModule和FormsModule，导出所有定义的组件，服务等
将全局仅用一次的组件放在核心特性模块，然后只在AppModule中导入，比如NavComponent和SpinnerComponent
独立的特性模块可以做成懒加载模块，避免在任何地方导入懒加载模块，不然模块就会直接加载

## 组件
当模板／样式超过3行时，写成单独文件
删除无样式定义的样式文件
模板／样式的定义与组件命名保持一致
导入时使用相对路径
用装饰器@Input和@Output来修改输入输出数据，而不是使用元数据中的inputs和outputs属性
不推荐重命名输入输出数据
按照变量，构造器，生命周期函数，一般方法的顺序定义；一般方法按页面的功能模块放一起，被调用的方法写在后面；变量和方法均先公有后私有排列；
组件中只写跟视图相关的逻辑，把其他的业务逻辑放在服务中
将可复用的业务逻辑放在服务中
不推荐事件命名加上on前缀
将展示逻辑放在组件的类中，而不是在模板中

## 指令
当有跟模板无关的展示逻辑时，使用属性指令，比如[highlight]指令
推荐使用@HostListener和@HostBinding，而不是元数据的host属性

## 服务
保持单例服务的使用规则，服务用来在特性模块或者应用中共享数据和方法
跟函数一样，一个服务只有一个目的
把服务注入在最高层的组件／模块中，使得该单例服务能在子组件、子模块中共享
使用@Injectable装饰服务类，而不是@Inject装饰参数
跟数据相关的操作，比如xhr请求，本地储存等抽象成服务

## 生命周期
需要生命周期钩子时，实现相关的接口，可有效防止错误
