# Regex-collection
## 1.分割命令行
> 首先把命令行字符串按**不在双引号范围之内**的空格分割，其中**双引号不能被转义（\\"）**，若双引号被转义则当成普通字符

版本v1：
```
\S*?(?<!\\)".*?(?<!\\)"\S*|\S+
```
版本v2：（修复了多个连续的、用双引号引用的字符串会错误按照空格分割的bug）
```
(?:\S*?(?<!\\)".*?(?<!\\)"(?:[^"\s]*(?:\\"))*|\S)+
```
最后版本的预览图：  
![](./resources/01.png)  
![](./resources/02.png)

## 2.提取首字母
> 首先把一句英文按空格分割，然后提取每个子串的第一个字母（不区分大小写）

版本v1：
```
(?<=(?:^|\s)[^A-Z|a-z]{0,}?)[A-Z|a-z]
```
最后版本的预览图：
![](./resources/03.png)

## 3.多行trim
> 有一个字符串，但是包含换行符，相当于有好几行，要求匹配这个字符串每一行中，左右两边的所有空白字符

版本v1：
```
(?<!.)\s+|\s+(?!.)
```
最后版本的预览图：
![](./resources/04.png)

## 4.匹配所有英文特殊符号
> 匹配所有英文特殊符号

版本v1：
```
[\x21-\x2f\x3a-\x40\x5b-\x60\x7b-\x7e]+
```
最后版本的预览图：  
![](./resources/05.png)

## 5.JSON、INI等配置文件通用的非注释匹配
> 使用“#”作为注释关键字，匹配每一行文本“#”第一次出现之前的字符串，**但如果“#”本身在双引号里面则当成普通字符**

版本v1：
```
(?<!.)(?:[^"#\n]*(?:(?<!\\)".*?(?<!\\)"[^"#\n]*)+|[^"#\n]+)
```
最后版本的预览图：  
![](./resources/06.png)
