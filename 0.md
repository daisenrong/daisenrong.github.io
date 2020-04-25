# 相关面试题

## 1.你说你懂i++跟++i的区别，那你知道下面这段代码的运行结果吗?

```java
public static void main(String[] args) {
    int j = 0;
    for (int i = 0; i < 10; i++) {
        j = (j++);
    }
    System.out.println(j);
}
```

### 两个方面进行解释：

#### 1.从jvm层面进行解释

​	这个直接看这个文章就行了，

[jvm层面解释问题](https://blog.csdn.net/qq_41907991/article/details/105337049)

#### 2.从代码层面进行解释

上面 `j=j++`我们可以拆分一下

```java
public static void main(String[] args) {
    int j = 0;
    for (int i = 0; i < 10; i++) {
        int tmp=j;
      	j=j+1;
      	j=tmp;
    }
    System.out.println(j);
}
```

这样就能理解为什么是 0了



#### ==注意==

**上面的两个解释看似是对的，但实际上是存在一定的问题的**

我们看class反编译之后的代码

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by Fernflower decompiler)
//

package com.lazydsr.study.test;

public class Test007 {
    public Test007() {
    }

    public static void main(String[] args) {
        int j = 0;

        for(int i = 0; i < 10; ++i) {
          	// 这里idea给我们做了优化
            int var3 = j + 1;
            j = j;
        }

        System.out.println(j);
    }
}

```

从代码中就很清楚的可以看到，结果必然为0

