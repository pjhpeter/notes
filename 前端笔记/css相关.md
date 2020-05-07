### 文字垂直居中
```
height: 20px;
line-height: 20px;
```
### 元素垂直居中
```
position: fixed/absolute;
top: 50%;
transform: translateY(50%)
```
### 好看的font-family设置
```
font-family: Avenir,Tahoma,Arial,PingFang SC,Lantinghei SC,Microsoft Yahei,Hiragino Sans GB,Microsoft Sans Serif,WenQuanYi Micro Hei,Helvetica,sans-serif;
```
### 单行文字过长用省略号代替
```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```
### 多行文字过长用省略号代替
```css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```