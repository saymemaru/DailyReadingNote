# MarkdownJ基础语法

## 目录

- [标题](#标题)  
- [段落](#段落)  
- [换行](#换行)  
- [语义标记](#语义标记)

---

## 标题

### Markdoawn标题2

#### Markdoawn标题3

<h1>HTML标题h1</h2>
<h2>HTML标题h2</h2>
<h3>HTML标题h3</h2>

---

## 段落

隔开一行  
I really like using Markdown.

I think I'll use it to format all of my documents from now on.

``</p>``
<p>I really like using Markdown.</p>

<p>I think I'll use it to format all of my documents from now on.</p>

---

## 换行

结尾两个空格  
This is the first line.  
And this is the second line.

``<br>``  
<p>This is the first line.<br>
And this is the second line.</p>

---

## 语义标记

### Markdoawn

*斜体1* *斜体2*  
**加粗1** **加粗2** ``ctrl + B``  
***加粗+斜体1*** ***加粗+斜体2***  ***加粗+斜体3***  
~~删除线~~  
$\underline{下划线}$  
\*转义*


### HTML

<i>斜体1</i>  <em>斜体2</em>
<b>加粗1</b> <strong>加粗2</strong>  
<strong><em>加粗+斜体</em></strong>  
<u>下划线1</u> <ins>下划线2</ins>  
<del>删除线</del>  
上标<sup>a</sup>  
下标<sub>a</sub>  
<kbd>Ctrl</kbd>

<p style="text-align:center">居中显示</p>

<font color="red">蓝色 Blue</font>
<p style="color:blue">红色 Red</p>

---

## 引用

> Dorothy followed her through many of the beautiful rooms in her castle.
>
>> The Witch bade her clean the pots and kettles and sweep the floor and keep the fire fed with wood.

---

## 公式

$$ x \href{why-equal.html}{=} y^2 + 1 $$

---

## 代码

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "age": 25
}
```

正文中的代码``Console.WriteLine("Hello")``

---

## 列表

- [x] Write the press release
- [ ] Update the website
- [ ] Contact the media

1. 动物
2. 植物
3. 水果
   1. 西瓜
      1. 西瓜皮
         1. 西瓜籽

- 欧洲  
   >缩进
- 非洲
- 亚洲
  - 赛里斯
    - 苏联

- This is the first list item.
- Here's the second list item.

   I need to add another paragraph below the second list item.

- And here's the third list item.

---

## 表格

This is a regular paragraph.

<table>
    <tr>
        <td>11</td>
        <td>12</td>
    </tr>
    <tr>
        <td>21</td>
        <td>22</td>
    </tr>
</table>

This is another regular paragraph.

| 左对齐      | 居中对齐     | 右对齐        |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text   |<ul><li>项目一</li><li>项目二</li></ul>|

---

## 表情

插件：:emojisense，Markdown Emoji  
输入":"或 ctrl + I

✋😊✋

---

## 链接

[这是连接](https://markdown.com.cn)  
[有标题的链接](https://markdown.com.cn "最好的markdown教程")  
<https://markdown.com.cn>  
<fake@example.com>

### 引用类型链接  

建立文本内联系

[引用链接][1]

[1]: https://markdown.com.cn

---

## 图片

![图片](MarkDown语法_Image/image.png "Magic Gardens")

[![带链接的图片](MarkDown语法_Image/image-1.png "Shiprock")](https://markdown.com.cn)

html设置图片大小
<figure>
    <img src="MarkDown语法_Image/image.png" width="200" height="100" alt="描述文本">
    <figcaption>这是一张描述图片。</figcaption>
</figure>

---

## 导出为PDF等

插件：markdown PDF  
ctrl + shift + p 输入 Export

---

## 特殊符号

版权 (©) — &copy;  
注册商标 (®) — &reg;  
商标 (™) — &trade;  
欧元 (€) — &euro;  
左箭头 (←) — &larr;  
上箭头 (↑) — &uarr;  
右箭头 (→) — &rarr;  
下箭头 (↓) — &darr;  
度数 (°) — &#176;  
圆周率 (π) — &#960;  

