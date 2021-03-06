---
layout: post
title: golang import包前的字母和符号
category: go
tags: go
keywords: go
description: go
---

转载自 [link](https://blog.csdn.net/qq_33875256/article/details/83378192 "With a Title"). 


> 像例子里面的cb就是后面要引用的包的别名（防止冲突）

> 格式：别名+空格+引用的包名（包名加双引号）
```bash
import (
	"fmt"
	"strings"
 
	cb "github.com/hyperledger/fabric/protos/common"
 
	"github.com/golang/protobuf/proto"
)
```



> 前面加下划线，只调用包里面的init函数。无法调用包中别的函数。
```bash
import (
	"fmt"
	"strings"
 
	_ "github.com/hyperledger/fabric/protos/common"
 
	"github.com/golang/protobuf/proto"
)
```


> fmt前面加点，调用函数时可以省略包的名字。即：fmt.println()可以写成println()
```bash
import (
	. "fmt"
	"strings"
 
	"github.com/hyperledger/fabric/protos/common"
 
	"github.com/golang/protobuf/proto"
)
```