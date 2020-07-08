### 文字垂直居中
```css
height: 20px;
line-height: 20px;
```
### 元素垂直居中
```css
position: fixed/absolute;
top: 50%;
transform: translateY(50%)
```
### 好看的font-family设置
```css
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
### 纵向布局动态加列
```css
display: flex;
flex-flow: column wrap;
align-content: flex-start;
```
### 自定义滚动条样式（chrome）
```css
/*滚动条整体样式*/
    .box::-webkit-scrollbar {
        width: 10px;
        height: 1px;
    }
    /*滚动条滑块*/
    .box::-webkit-scrollbar-thumb {
        border-radius: 10px;
        -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.2);
        background: #535353;
    }
    /*滚动条轨道*/
    .box::-webkit-scrollbar-track {
        -webkit-box-shadow: inset 0 0 1px rgba(0,0,0,0);
        border-radius: 10px;
        background: #ccc;
    }
```