# 什么是 CSS hack？
```
由于不同厂商的流览器或某浏览器的不同版本（如IE6-IE11,Firefox/Safari/Opera/Chrome等），对CSS的支持、解析不一样，导致在不同浏览器的环境中呈现出不一致的页面展现效果。这时，为了获得统一的页面效果，就需要针对不同的浏览器或不同版本写特定的CSS样式，把这个针对不同的浏览器/不同版本写相应的CSS code的过程，叫做CSS hack。其原理是由于不同的浏览器和浏览器各版本对CSS的支持及解析结果不一样，以及CSS优先级对浏览器展现效果的影响，我们可以据此针对不同的浏览器情景来应用不同的CSS。CSS hack有3种表现形式，CSS属性前缀法、选择器前缀法以及IE条件注释法（即HTML头部引用if IE）Hack，实际项目中CSS Hack大部分是针对IE浏览器不同版本之间的表现差异而引入的。
 a. 属性前缀法(即类内部Hack)：例如 IE6能识别下划线"_"和星号" * "，IE7能识别星号" * "，但不能识别下划线""，IE6~IE10都认识"\9"，但Firefox前述三个都不认识。
b. 选择器前缀法(即选择器Hack)
c. IE条件注释法(即HTML条件注释Hack)：针对所有IE(注：IE10+已经不再支持条件注释)： ，针对IE6及以下版本：。这类Hack不仅对CSS生效，对写在判断语句里面的所有代码都会生效
```
# 处理浏览器兼容问题的思路
```
（1）要不要做：产品的角度（产品的受众人群，受众的浏览器比例，效果优先还是功能优先），是否有必要为小部分人群兼容；成本的角度（有没有必要做某件事情）
（2）做到什么程度：要让哪些浏览器支持哪些效果；
（3）如何做：
 a. 根据兼容需求选择兼容技术框架\库和兼容工具（JQuery,css reset,normalizr,respond.js ,html5shiv)
 b. 使用条件注释，css hack，js能力检测做一些修补
```
# 列举5种以上浏览器兼容的写法

1. [html5shiv.js](https://github.com/aFarkas/html5shiv)让IE等浏览器支持HTML5。

2. 条件注释法

|项目|   范例|   说明|
|----|----|----|
|！|   [if !IE]|   非IE|
|It|   [if It IE 5.5]|   小于IE5.5|
|Ite|   [if Ite IE 6]|    小于等于IE6|
|gt|   [if gt IE 5]|   大于 IE5|
|gte|   [if gte IE7]|    大于等于IE7|
|I|  [if(IE6)I(IE7)]|   IE6或者IE7|

3. 选择器前缀法
```
*html  *前缀只对IE6生效
*+html *+前缀只对IE7生效
@media screen\9{...}只对IE6/7生效
@media \0screen {body { background: red; }}只对IE8有效
@media \0screen\,screen\9{body { background: blue; }}只对IE6/7/8有效
@media screen\0 {body { background: green; }} 只对IE8/9/10有效
@media screen and (min-width:0\0) {body { background: gray; }} 只对IE9/10有效
@media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {body { background: orange; }} 只对IE10有效
```
4. 属性前缀法
```
.box{
color: red;
_color: blue; /*ie6*/
*color: pink; /*ie67*/
color: yellow\9;  /*ie/edge 6-8*/
}
```
5. 使用Modernizr。Modernizr运行时会在html元素上添加一批CSS的class名称，这些class名称标记当前浏览器支持哪些特性和不支持哪些特性，支持的特性就直接使用该特性的名称作为一个class，不支持的特性显示的class是“no-特性名称”。
可以直接使用Modernizr在元素里生成的class名称，在你的css文件里定义相应的属性以便支持当前浏览器
# 以下工具/名词是做什么的
```
条件注释：HTML源码中被IE有条件解释的语句。条件注释可被用来向IE提供及隐藏代码。
IE Hack：使用特殊的符号或者方式写出只有IE浏览器可以解析的代码，如CSS属性前缀法、选择器前缀法以及IE条件注释法
js 能力检测：能力检测的目标是识别浏览器的能力。使用这种方式无需顾及浏览器如何如何，只需确定浏览器是否支持特定的能力，就可以给出相关的方案。
html5shiv.js：解决一些浏览器不支持html5的一些新特性和标签的问题。
respond.js：解决在做响应式网页的时候一些浏览器不支持媒体查询的问题。
css reset：重新定义样式属性，将浏览器默认样式覆盖掉。
normalize.css：保护有用的浏览器默认样式而不是完全去掉它们，修复浏览器自身的bug并保证各浏览器的一致性，用一些小技巧优化CSS可用性。相比于传统的CSS reset，Normalize.css是一种现代的、为HTML5准备的优质替代方案。
Modernizr：Modernizr会在页面加载时自动检测浏览器的特性，并html元素上添加一批CSS的class名称，这些class名称标记当前浏览器支持哪些特性和不支持哪些特性。
postCSS：postCSS是一款通过JS插件来转换CSS的工具。这些插件能帮你校验你的CSS代码、转换未来的CSS语法、支持变量和混写、以及内联图片等等。
```
# 在哪个网站查询属性兼容性？
http://caniuse.com/
