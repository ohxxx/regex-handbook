<h1 align="center">
  <samp>正则手册</samp>
</h1>

## 量词
|   模式   |                 说明                 |                 示例                 |
| :------: | :----------------------------------: | :----------------------------------- |
|   `*`    |      重复 0 次或更多次，等价于 `{0,}`。 `贪婪模式`      |      表达式：`你好.*`<br />测试文本：<br />1：`你好`<br />2：`你好，世界`      |
|   `*?`    |      重复 0 次或更多次，等价于 `{0,}?`。 `惰性模式`      |      表达式：`你好.*?`<br />测试文本：<br />1：`你好`<br />2：`你好`，世界      |
|   `+`    |      重复 1 次或更多次，等价于 `{1,}`。 `贪婪模式`      |      表达式：`你好.+`<br />测试文本：<br />1：你好<br />2：`你好，世界`      |
|   `+?`    |      重复 1 次或更多次，等价于 `{1,}?`。 `惰性模式`      | 表达式：`你好.+?`<br />测试文本：<br />1：你好<br />2：`你好，`世界 |
|   `?`    |     重复 0 次或 1 次，等价于 `{0,1}` 。 `贪婪模式`     |     表达式：`你好.?`<br />测试文本：<br />1：`你好`<br />2：`你好，`世界     |
|   `??`    |     重复 0 次 或 1 次，等价于 `{0,1}?` 。 `惰性模式`     | 表达式：`你好.??`<br />测试文本：<br />1：`你好`<br />2：`你好`，世界 |
|  `{n}`   |     重复出现 `n` 次。 `贪婪模式`，匹配指定 `n` 次     | 表达式：`0\d{2}-\d{8}`<br />测试文本：<br />1：012-123456<br />2：`012-12345678`9 |
|  `{n}?`   |     重复出现 `n` 次。 `惰性模式`，与 `{n}` 一样，没啥区别     | 表达式：`0\d{2}-\d{8}?`<br />测试文本：<br />1：012-123456<br />2å：`012-12345678`9 |
|  `{n,}`  |  至少重复出现 `n` 次。 `贪婪模式` ，优先匹配 `, >>> 更多次`  | 表达式：`0\d{2}-\d{7,}`<br />测试文本：<br />1：012-123456<br />2：`012-123456789` |
|  `{n,}?`  |   至少重复出现 `n` 次。 `惰性模式`，优先匹配 `n`   | 表达式：``0\d{2}-\d{7,}?`<br />测试文本：<br />1：012-123456<br />2：`012-1234567`89 |
| `{n,m}`  | 重复出现 `n` 到 `m`  次。 `贪婪模式` ，优先匹配 `m` | 表达式：`0\d{2}-\d{7,8}`<br />测试文本：<br />1：012-123456<br />2：`012-12345678`9 |
| `{n,m}?`  | 重复出现 `n` 到 `m`  次。 `惰性模式` ，优先匹配 `n`  | 表达式：``0\d{2}-\d{7,8}?`<br />测试文本：<br />1：012-123456<br />2：`012-1234567`89 |



## 位置


## 括号


## 字符组


## 字面量


## 修饰符
| 符号 |                             说明                             | 示例                                                         |
| :--: | :----------------------------------------------------------: | ------------------------------------------------------------ |
| `g`  |         `global - 全局匹配` ，找到所有满足匹配的子串         | 表达式：`/你好/g`<br />测试文本：<br />1：`你好`，世界，`你好`我好大家好 |
| `i`  |     `ignore - 忽略大小写` , 匹配过程中 `忽略字母大小写`      | 表达式：`/halo/gi`<br />测试文本：<br />1：`halo`，world、`HaLo`，`HALO`，WORLD |
| `m`  | `multi line - 多行匹配` ，把 `^` 和 `$` 变成  行开头  和  行结尾 | 表达式：`/halo/gm`<br />测试文本：<br />1：`halo`<br/>`halo`，world<br/>world，`halo` |
| `s`  | `single line - 单行匹配` ，更改 `.` 的含义，使它与每一个字符匹配（包括换行符 \n ） | 表达式：`/halo./gs`<br />测试文本：<br />1：`halo`<br/>world |
| `d`  |   `indices - 指数`，返回正则表达式在目标字符串中匹配的索引   | 表达式：`/halo./gd`<br />测试文本：world，`halo`<br/><br />使用 `exec` 会返回一个 `indices` 的数组，代表正则表达式在目标字符串中开始到结束的索引 |
| `y`  |       `sticky - 粘性`，匹配从目标字符串的当前位置开始        | 表达式#1：`/x+/y`<br />测试文本#1：`xxx`_xx_x<br /><br />表达式#2：`/x+/g`<br />测试文本#2：`xxx`_`xx`_`x` |
| `u`  |          `unicode ` ，使用 unicode 码的模式进行匹配          | 表达式#1：`/^\uD83D/.test('\uD83D\uDC2A')` // >>> true <br /><br />表达式#2：`/^\uD83D/.test('\uD83D\uDC2A')` // >>> false |

## RegExp

|  属性  |                        说明                        | 示例                                                         |
| :----: | :------------------------------------------------: | ------------------------------------------------------------ |
| `test` |    检索目标字符串中指定的值，返回 true 或 false    | /halo/g.test('world,halo.')<br/><br />// >>> true            |
| `exec` | 检索目标字符串中指定值，返回找到的值，并确定其位置 | /halo/g.exec('world,halo.')<br/><br />// >>> ['halo', index: 6, input: 'world,halo.', groups: undefined] |


## String
|    方法    |                             说明                             | 示例                                                         |
| :--------: | :----------------------------------------------------------: | ------------------------------------------------------------ |
|  `search`  |      返回匹配到的第一个子串在目标字符串中的 `位置索引`       | const str = 'world,halo'<br/>str.search(/halo/)<br /><br />// >>> 6 |
|  `split`   |    以匹配到的子串，对目标字符串 `进行切分` 。返回一个数组    | const str = 'world,halo.'<br/>str.split(/halo/)<br /><br />// >>> ['world,', '.'] |
|  `match`   |      返回匹配到的子串的结果数组，其中包含具体的匹配信息      | const str = 'world,halo.'<br/>str.match(/halo/)<br /><br />// >>> ['halo', index: 6, input: 'world,halo.', groups: undefined] |
| `matchAll` | 返回匹配到的所有子串的结果数组，其中包含具体的匹配信息，返回值是一个迭代器 | [...'world,halo.halo,world'.matchAll(/halo/g)]<br /><br />// >>> [<br />['halo', index: 6, input: 'world,halo.halo,world', groups: undefined],['halo', index: 11, input: 'world,halo.halo,world', groups: undefined]<br />] |
| `replace`  | 对目标字符串进行 `替换操作` 。正则是其第一个参数。返回替换后的字符串 | const str = 'world,halo.'<br/>str.replace(/halo/, 'hello')<br /><br />// >>> 'world,hello.' |

## Replace

> 这里是对第二个参数的说明汇总


|      字符      |             说明             |             示例             |
| :-------------: | :--------------------------: | ---------------------------- |
| `$1,$2,...,$99` | 匹配第1-99个分组里捕获的文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$1_xxx_")<br/><br />// >>> 'halo_xxx_.world,hello' |
|      `$&`       | 匹配到的子串文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$&_xxx_")<br/><br />// >>> 'world,halo_xxx_.world,hello' |
|      `$`\`      | 匹配到的子串的左边文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$`_xxx_")<br/><br />// >>> '_xxx_.world,hello' |
|       `$'`        | 匹配到子串的右边文本 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$'_xxx_")<br/><br />// >>> '.world,hello_xxx_.world,hello' |
|       `$$`        | 美元符号 | const str = 'world,halo.world,hello'<br/>str.replace(/.*?(halo)/g, "$$")<br/><br />// >>> '$.world,hello' |

### 参考
- [Regexp Tutorial](https://www.runoob.com/regexp/regexp-tutorial.html)
- [MDN Regexp](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
- [Regular 30-minute tutorial](https://deerchao.cn/tutorials/regex/regex.htm#howtouse)
- [JS Regex Mini Book](https://github.com/qdlaoyao/js-regex-mini-book)