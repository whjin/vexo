---
title: jQuery选择器
date: 2019-05-08 16:17:24
category: ["技术"]
tags: ["前端","jQuery"]
comments:
---

# 基本选择器 Basics #

- `*`选择所有元素
- `.class`选择`class`，如：`$('.mybox')`
- `element`选择`element`，如：`$('p')`
- `#id`选择`id`，如：`$('#box')`
- `selector1,selectorN`可以同时选择多个元素，如：`$('div, p.box, #phone')`

<!--more-->

# 层级选择器 Hierarchy #

- `parent > child`选择指定元素下的指定子元素，如：`$('ul.tonav > li')`
- `ancestor descendant`选择一个元素里所有的后代元素，如：`$('form input')`
- `prev + next`选择所有指定元素后紧跟着的元素，如：`$('label + input')`
- `prev ~ siblings`选择与指定元素之后有相同父级的同级选择器，如：`$('#prev ~ div')`

# 基本过滤器 Basic Filters #

- `:animated`选择动画进行中的所有元素。如：`$('div:animated)`
- `:eq(n)`选取第`n`个元素，如：`$('ul.tonav li:eq(n)')`
- `:even`选取偶数个元素，如：`$('li:even')`
- `:odd`选取奇数个元素，如：`$('li.odd')`
- `:first`选取奇数个元素，如：`$('li:first')`
- `:gt(n)`选取结果集中索引大于`n`的元素，`n`可以为负值，如：`$(':gt(3)')`
- `:lt(n)`选取结果集中索引小于`n`的元素，`n`可以为负值，如：`$(':lt(3)')`
- `:header`选取所有的标题元素，例如`h1`、`h2`、`h3`...，如：`$(':header')`
- `:lang()`选取指定语言的所有元素，，如：`$('div:lang(zh-cn)')`
- `:last`选取最后一个符合的元素，如：`$('li:last')`
- `:not`选取不符合的所有元素，如：`$('input:not(:checked) + span')`
- `:root`选取作为文档根目录的元素
- `:target`选取由文档的图片、视频、音频指示的目标元素

# 内容过滤器 Content Filters #

- `:contains()`选择包含指定文本的所有元素，如：`$("div:containers('home')")`
- `:empty`选择没有子元素或内容文字的元素，如：`$("td:empty"))`
- `:has()`选择包含至少一个匹配指定选择器的元素的元素，如：`$("div:has(p)"))`
- `:parent`选择至少有一个子节点（元素或文本）的所有元素

# 可视选择器 Visibility Filters #

- `:hidden`选择所有隐藏的元素，如：`$("div:hidden").show(3000));`
- `:visible`选择所有隐藏的元素，如：
    `$("div:visible").click(function() {$(this).css("background", "yellow");});`

# 属性选择器 Attribute #

- `[name]`选择具有指定属性的元素（使用任何值都可以）。如：`$("div[id]")`
- `[name|="value"]`选择具有指定属性的元素，其值等于给定的字符串，或者以该字符串开头，后跟连字符（`-`）。

    ```javascript
    $('a[href="about.html"]');  //选择 a 链接的 href 属性包含 'about.html' 的元素
    ```

- `[name*="value"]`选择具有包含给定子字符串的值得指定属性的元素。

    ```javascript
    $('input[name*="man"]');  //选择所有的 name 属性包含 'man' 的 input 元素
    ```

- `[name~="value"]`选择具有指定属性的元素，其中包含由空格分隔的给定单词的值。

    ```html
    <input name="man-news">
    <input name="milk man">
    <input name="letter">
    ```
    ```javascript
    $('input[name~="man"]');  //会选择到前两个 input 元素
    ```

- `[name$="value"]`选择具有指定属性的元素，其值与给定字符串精确匹配，要区分大小写。如：`$("input[name$='letter']")`
- `[name="value"]`选择具有指定属性的元素，其值恰好等于特定值，如：`$("input[value='Hot Fuzz']")`会选到`value`等于`Hot Fuzz`的`input`
- `[name!="value"]`选择不具有指定属性的元素，或者具有指定苏醒但不具有特定值的元素。如：`$("input[name!='newsletter']")`，`name`属性值为`newsletter`的不选。
- `[name^="value"]`选择具有指定属性的元素，其值与给定字符串完全一致。

    ```html
    <input name="newsletter">
    <input name="milkman">
    <input name="news">
    ```
    ```javascript
    $('input[name^="news"]');  //会选择到第三个 input
    ```

- `[name="value"][name2="value2"]`符合所有指定的属性过滤器的元素。如：`$("input[id][name$='man']")`

# 子代过滤器 Child Filters #

- `:first-child`选择同父代的第一个子代元素。
- `:first-of-type`选择同一元素名称的兄弟中的第一个元素。
- `:last-child`选择同父代的最后一个子代元素。
- `:last-of-type`选择同一元素名称的兄弟中的最后一个元素。
- `:nth-child()`选择同父代的第`n`个子代元素。
- `:nth-last-child()`选择同父代的倒数第`n`个子代元素。
- `:nth-last-of-type()`选择同父代的倒数第`n`个子代元素。
- `:nth-of-type()`选择同父代的第`n`个子代元素。
- `:only-child`选择只有一个子代的元素。
- `:only-of-type()`选择所有没有同名元素的兄弟元素。如：`$("div.button:only-child")`选择只有一个`button`的`div`

# 表单选择器 #

- `:button`选择所有按钮元素和按钮类型的元素。
- `:checkbox`选择所有得可取块的元素。
- `:checked`选择所有选中的元素。
- `:disabled`选择所有被禁用的元素。
- `:enabled`选择所有已启用的元素。
- `:focus`选择当下被`focus`的元素。
- `:file`选择`file`类型的元素。
- `:image`选择图像类型的所有的元素。
- `:input`选择所有`input`、`textarea`、`select`和`button`元素。
- `:password`选择所有密码类型的元素。
- `:radio`选择所有选项按钮的元素。
- `:reset`选择所有清除按钮（复位按钮）的元素。
- `:selected`选择所有选中的元素。
- `:submit`选择所有提交类型的元素。
- `:text`选择所有文本输入框的元素。