
# 1. Markdown 初体验
## 1.1 先试着写个标题
### 1.1.1 再来个小标题
- 试试项目符号
    - 符号会自动缩进吗
    - 会自动换行吗
    - **试试加粗字体**
- *这是斜着的*
- ***这是又粗又斜的***
- ~~这是被删掉的~~
- <u>这是带下划线的</u>
- 这个上面有脚注 [^Note]
[^Note]:Look Here!

## 2. 区块
> 创建一个区块
>> 套个娃   
>>> 继续套  
>>>> 还能套


## 3. 试着写一段代码
### 3.1 python
```python
# python
print('Hello World!')
```

### 3.2 java
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

### 3.3 C
```c
#include <stdio.h>
int main(){
    printf("%s","Hello World!")
    return 0;
}
```

## 4. 插入链接
这是一个链接
[世界三流大学.com](http://世界三流大学.com)


## 5. 插入图片

插张动图试试  
![learn](pikapi.gif "pikapi")


## 6. 插入表格
|   A  |   B  |   C  |   D  |  E   |
| ---- | ---- | ---- | ---- | ---- |
|   x  |   y  |   z  |   \  |  \   |
|   x  |   y  |   z  |   \  |  \   |
|   x  |   y  |   z  |   \  |  \   |


## 7. 插入公式
放弃这个了。

插个分割线
***
总结  
- 用jupyter notebook写markdown也挺方便的  
- markdown数学公式写起来一言难尽，学习成本一点也不低  
- 还是只用于纯文本编辑吧  
- 开sublime text  Shift + F11 沉浸模式写起来还是很爽的。（把网文作者关起来码字正好）
- 用sublime 直接打开Git仓库，修改后一次性commit，不需要打开命令行
