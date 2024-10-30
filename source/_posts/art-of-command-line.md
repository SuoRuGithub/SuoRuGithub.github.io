---
title: The art of command line
tags: 
categories:
    accumulation
date: 2024-10-13
mathjax: true
---


本篇笔记属于accumulation的category下，用来积累一些使用命令行的技巧。

**设置`PYTHONPATH`**

- 什么是`PYTHONPATH`？

- `PYTHONPATH`环境变量告诉Python去哪里寻找模块，所以当下次出现了找不到模块的问题，可以想想是否应该正确设置`PYTHONPATH`

- 在当前的环境中设置`PYTHONPATH`

```bash
export PYTHONPATH=/path/to/module:$PYTHONPATH   // 这样可以将选择的路径添加到目前的PYTHONPATH而不是替代它
```

- 全局设置`PYTHONPATH`

将上述语句写入`~/.bashrc`或者`~/.zshrc`即可

思考：上面的方法设置`PYTHONPATH`时，一个范围太小，另一个范围又太大。前者，每次我新建终端执行程序时都要进行`export`操作；后者，全局的`PYTHONPATH`都被更改。如果我只希望在指定的虚拟环境下，`PYTHONPATH`是指定路径呢？


