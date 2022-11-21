要想实现aside侧边框高度占满整页需要设置下面几个地方：

index.css中：
```
html,body {
      margin: 0;
      height: 100%;
    }
```
vue文件中，最外层<el-container>标签设置高度：

```

.container{
    height: 100%
}

```

<el-menu>标签设置高度：

```

.menu {
  height: 100%;
}

```
通过上述三处高度设置，即可实现占满整页的效果

