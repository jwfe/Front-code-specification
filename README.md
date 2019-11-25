# 0. 前言

高质量的代码就是对程序自己最好的注释。当你打算要添加注释时，问问自己，“我如何能改进编码以至于根本不需要添加注释？”改进你的代码，然后才是用注释使它更清楚。                                                  
———  Steve McConnell, 软件工程师，作家, 出自 《Code Complete》

### 1. 为什么要有团队代码规范？

虽然代码代码规范只是细节的小事，不会影响性能与业务。但是却体现了一个coder和团队的专业程度。

所以不管团队有多少人，代码风格都应该统一标准。

规范的制定是我们长期以来对工作的积累与沉淀的产物，帮助我们更快、更好、更高效的完成繁重、复杂、多样化的任务，我们制作规范的主要目的在于：

- 降低每个组员介入项目的门槛成本；
- 提高工作效率及协同开发的便捷性；
- 高度统一的代码风格；
- 整合一整套HTML、CSS解决方案，来帮助开发人员快速做出高质量的符合要求的页面。

## 基本信息

规范名称 | 前端规范
--------|------|
当前版本 | v0.1 alpha
规范发起 | [bikedawuwang](https://github.com/bikedawuwang)
参与人群 | [JWFE](https://github.com/jwfe)
最后更新 | 2019.11.25


## 目录

[toc]

## 1. 通用约定

### 1.1. <a name="intro"></a>目录结构

目录划分目标:

- 项目的学习成本更低 (想要满足此条件，则需要让所有项目的目录划分保持一致)
- 目录之间的关系更加清晰
- 保持目录层级扁平
- 项目更加的容易被重构
- 文件检索更简单
- 模块和展示组件可以无痛抽离
- 将有副作用的代码划分在固定目录中

```
    /project
        /docs           文档目录
        /utils          工具类函数目录
        /build          编译输出目录
        /config         webpack配置目录
        /public         静态资源目录
        /scripts        npm脚本目录
        /src            业务代码目录
        /tests          单元测试目录
        jsconfig.json   alias 声明
        package.json    npm 包说明
        README.md       工程说明
```

### 1.2. <a name="separate"></a>分离

结构（HTML）、表现（CSS）、行为分离（JavaScript）

> 将结构与表现、行为分离，保证它们之间的最小耦合，这对前期开发和后期维护都至关重要。

### 1.3. <a name="file-name"></a>文件命名

* CSS模块文件，其文件名必须与模块名一致；

假定有这样一个模块：

> .bs-detail { sRules; }
> .bs-detail-hd { sRules; }
> .bs-detail-bd { sRules; }
> .bs-detail-ft { sRules; }

> 那么该模块的文件名应该为：`bs-detail.css || bs-detail.less `

* CSS页面文件，其文件名必须与HTML文件名一致；

> 假定有一个HTML页面叫 `bs-component.html || bs-component.jsx`，那么其相对应的CSS页面文件名应该为：`bs-component.css || bs-component.less`

### 1.4. <a name="indentation"></a>缩进

使用4个空格宽度来进行缩进。

### 1.5. <a name="encoding"></a>编码

* 以 UTF-8 无 BOM 编码作为文件格式；
* 在HTML中文档中用 `<meta charset="utf-8" />` 来指定编码；
* 为每个CSS文档显示的定义编码，在文档首行定义 `@charset "utf-8";`

> 在 Sass 中，如果文档中出现中文，却未显示定义编码，将会编译出错，为了统一各种写法，且提前规避错误几率，统一要求每个CSS文档都需要定义编码



### 1.6. <a name="comment"></a>注释

尽可能的为你的代码写上注释。解释为什么要这样写，它是新鲜的方案还是解决了什么问题。

### 1.7. <a name="todo"></a>待办事项

用 TODO 标示待办事项和正在开发的条目

	<!-- TODO: 遗漏某些业务逻辑 || 遗漏某些已知BUG -->
	<div class="bs-ucenter"></div>
	...


### 1.8. <a name="end-line-space"></a>行尾空格

删除行尾空格，这些空格没有必要存在。

### 1.9. <a name="protocol-relative-url"></a>省略嵌入式资源协议头

省略图像、媒体文件、样式表和脚本等URL协议头部声明 ( http: , https: )。如果不是这两个声明的URL则不省略。

省略协议声明，使URL成相对地址，防止内容混淆问题和导致小文件重复下载（这个主要是指http和https交杂的场景中）。

不推荐：

	<script src="http://unpkg.com/react@16/umd/react.production.min.js"></script>

推荐：

    <script src="//unpkg.com/react@16/umd/react.production.min.js"></script>

不推荐：

```
.example {
  background: url(http://www.google.com/images/example);
}
```

推荐：

```
.example {
  background: url(//www.google.com/images/example);
}
```

> 注：省略协议头在IE7-8下会有一点小问题，外部CSS文件（link和@import）会被下载两遍。



### 1.10. <a name="validator"></a>代码有效性

* 使用 [W3C HTML Validator](http://validator.w3.org/) 来验证你的HTML代码有效性；
* 使用 [W3C CSS Validator](http://jigsaw.w3.org/css-validator/) 来验证你的CSS代码有效性。

> 代码验证不是最终目的，真的目的在于让开发者在经过多次的这种验证过程后，能够深刻理解到怎样的语法或写法是非标准和不推荐的，即使在某些场景下被迫要使用非标准写法，也可以做到心中有数，以后找到其他解决方案后，替换为其他解决方案。

## 2.样式规范

CSS in JS 现在还没有特别成熟稳定的方案, 不合适进行长期投入, 较为热门的 [styled-components](https://www.styled-components.com/) 等方案需要投入学习时间, 并且收益不确定, 也不建议使用. 我们只讨论 CSS 预处理 方案的规范:

### 2.1. <a name='SASSLESS'></a>SASS/LESS 约定

- 降低依赖
  - 全局变量文件只有 1 个
  - 每个样式文件的样式在当前文件内闭环, 不引用其他样式文件
  - 使用 BEM,防止样式污染, 组件样式以组件名作为 BEM 前缀

- 提高可读性
  - 组件引用的样式文件始终保持在该组件的文件夹内, 并且名称一致 (方便查询)
  - 样式嵌套控制在 3 层以内, **如无必要, 最好不使用嵌套**


```less
    // Case A 使用嵌套
    .bs-button {
        &-open {
            font-size: 16px;
            &-hight {
            color: #f00;
            }
            &-disable {
            color: #888;
            }
        }
        &-close {
            font-size: 24px;
        }
    }
```

```less
    // Case B 不使用嵌套
    .bs-button-open {
        font-size: 16px;
    }

    .bs-button-open-hight {
        color: #f00;
    }

    .bs-button-open-disable {
        color: #f00;
    }

    .bs-button-open {
        font-size: 24px;
    }
```

Case A 对于我们来讲，确实简化了，但是往往解决一个问题就会带来多个新的问题。

在可读性上 Case B 相对 Case A 可读性更高。也方便后续维护时全局检索。

### 2.2.  <a name='global'></a>全局变量

 整个项目只有一个 `global.(sass|less)` 文件, 下表区分了全局变量及局部变量的分布(注意, 局部变量只可在当前样式文件中使用):

| 类型                        | 全局变量 | 局部变量 | 说明                                                                                                        |
| --------------------------- | -------- | -------- | ----------------------------------------------------------------------------------------------------------- |
| 颜色                        | O        |          | 整个项目的颜色应该基于几个基色进行变化                                                                      |
| 字体\字号                   | O        |          | 字体应该统一                                                                                                |
| 导航栏\工具栏 宽高          | O        |          | 此类宽高应该固定, 并且全局可读                                                                              |
| 栅格间隙                    | O        |          | 栅格间隙应该统一                                                                                            |
| 颜色混合                    |          | O        | 颜色视情况而产生的 加深\减淡\透明度 等效果应该写在组件样式中                                                |
| 组件宽高                    |          | O        | 基于组件上下文而定                                                                                          |
| 组件盒模型 (margin\padding) |          | O        | 基于组件上下文而定                                                                                          |
| 常用样式组合                |          | O        | 类似 flex 的 column, row 等等, 不应该有默认的预设, 使用基础的样式进行组合, 我们不应该去记忆不必要记忆的变量 |

## 3. 工程结构

### 3.1.1. <a name='alias'></a>工程 alias

alias 的引入有利有弊, 其中最大的优点是方便重构目录结构:

如果移动该文件，会导致引用关系被打破

```js
    import React from "react";
    import Button from "../Components/Button";

    export default () => {
        return <div>be move this file</div>;
    };
```
设置 Components 为 alias 移动该文件不会导致引用关系被打破

```js
    import React from "react";
    import Button from "Components/Button";

    export default () => {
        return <div>be move this file</div>;
    };
```

alias 的弊端:

- 滥用 （可能导致无法分辨 `node_modules` 还是 `alias`）
- 路径识别 （不方便找到引用文件位置）

### 3.1.2. <a name='npm'></a>导入 npm 包

尽量不要随意引入新包, 并且尽量少的引用第三方包

使用一些较大的包我们需要按需引入, 不必要的不需要引入:

```js
// 虽然增加 lodash-webpack-plugin 同样可以按需引入, 但是我们还是更建议直接按需引入, 养成习惯

// bad
import { isArray } from "lodash";

// good
import isArray from "lodash/isArray";

// best
function isArray(target) {
  return Object.prototype.toString.call(target) === "[object Array]";
}
```

