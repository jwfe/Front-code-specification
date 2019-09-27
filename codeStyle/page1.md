# 1.1.1 缩进

```text
// bad
function() {
   const name
}

// bad
function() {
 const name
}

// good
function() {
    const name
}

// good
function() {
  const name
}
```

关于空格为4个或者2个网络上有很多版本，个人认为2个空格与4个空格均可，切记请勿使用3个空格与1个空格或者tab键缩进，因为在不同编辑器下tab键的距离不同，可能会导致代码难以阅读。我个人倾向于使用4个空格，代码缩进明显，更方便阅读。

