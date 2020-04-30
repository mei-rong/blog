# 正则表达式

## 普通正则(Regex)

### 标识符
^, $, [], (), {}...
```js
//匹配一个正整数，[1-9]设置第一个数字不是 0，[0-9]* 表示任意多个数字
/^[1-9][0-9]*$/
```
## 贪婪/非贪婪(Greedy/Lazy)

### 贪婪标识符
+，?，*，{n}，{n,}，{n,m}
```js
//贪婪模式，一直往后匹配，直到最后一个满足条件的b为止，因此匹配结果是aacbacb
'aacbacbc'.match(/a.*b/); // aacbacb
```

### 非贪婪标识符
+?，??，*?，{n}?，{n,}?，{n,m}?
```js
//非贪婪模式，匹配到了第一个b后，就匹配成功了，因此匹配结果是aacb
'aacbacbc'.match(/a.*?b/); // aacb
```

## 零宽断言(zero-width assertion)
零宽断言，零宽度的匹配，匹配到的内容不会保存到匹配结果中去，最终匹配结果是一个位置，用来给指定位置添加一个限定条件。

### (?=exp):零宽度正预测先行断言(zero-width positive lookahead assertion)，它断言自身出现的位置的后面能匹配表达式exp。
```js
//匹配后面为_path，结果为product
'product_path'.match(/product(?=_path)/) //product
'product_path'.match(/(product)(?=_path)/) //product, product
'product_path'.match(/produ(ct)(?=_path)/) //product, ct
```

### (?<=exp):零宽度正回顾后发断言(zero-width positive lookbehind assertion)，它断言自身出现的位置的前面能匹配表达式exp
```js
//匹配前面为name:的molly
'name:molly'.match(/(?<=name:)molly/)  //molly
```

### (?!exp):零宽度负预测先行断言(zero-width negative lookahead assertion)，断言此位置的后面不能匹配表达式exp。
```js
//匹配后面不是_path
'product_path'.match(/product(?!_path)/)   //nil
//匹配后面不是_url
'product_path'.match(/product(?!_url)/)   //product
```

### (?<!exp):零宽度负回顾后发断言(zero-width negative lookbehind assertion),断言此位置的前面不能匹配表达式exp
```js
//匹配前面不是name:
'name:molly'.match(/(?<!name:)molly/)   //nil
//匹配前面不是nick_name:
'name:molly'.match(/(?<!nick_name:)molly/)  //molly
```
