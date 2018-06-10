---
title: python finally知识点
date: 2018-04-18 20:33:19
categories:
- python编程/python填坑指南
tags:
---

```
def test():
    try:
        print "hellow"
        ret = "true"
        return "sssss"
    except Exception, e:
        print "======="
        return str(e)
    finally:
        print "end"

str = test()
print str
```

请看一下上面的代码，请思考一下finally 后的end是否会输出呢？

```
➜  ~ python finall.py
hellow
end
sssss
```

从结果中我们可以看出来，try 中的return并不影响finally后的语句执行，但是我们需要注意return并不是不执行，而是执行顺序变了，在try执行return前，先执行了finally的语句，然后在执行了try的return。


```
def test():
    try:
        print "hellow"
        int("true")
        return "sssss"
    except Exception, e:
        print "======="
        return str(e)
    finally:
        print "end"

str = test()
print str
```

```
➜  ~ python finall.py
hellow
=======
end
invalid literal for int() with base 10: 'true'
```

该程序也可以看出，except中的return依然不会影响finally的执行。执行的顺序依然是在except return之前，先执行finally语句，然后在执行except的return语句。


更多细节可以参考改文章：https://www.cnblogs.com/JohnABC/p/4065437.html