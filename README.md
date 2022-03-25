# YAML

**YAML**（[/ˈjæməl/](https://zh.wikipedia.org/wiki/Help:英語國際音標)，尾音类似*camel*骆驼）是一个可读性高，用来表达资料[序列化](https://zh.wikipedia.org/wiki/序列化)的格式。

*YAML*是"YAML Ain't a Markup Language"（YAML不是一种[标记语言](https://zh.wikipedia.org/wiki/标记语言)）的[递归缩写](https://zh.wikipedia.org/wiki/遞迴縮寫)。在开发的这种语言时，*YAML* 的意思其实是："Yet Another Markup Language"（仍是一种[标记语言](https://zh.wikipedia.org/wiki/标记语言)）[[3\]](https://zh.wikipedia.org/wiki/YAML#cite_note-YAML_spec_2001_08_01-3)，但为了强调这种语言以数据为中心，而不是以标记语言为重点，而用反向缩略语重命名。

### 文件

```yaml
---
receipt:     Oz-Ware Purchase Invoice
date:        2012-08-06
customer:
    given:   Dorothy
    family:  Gale
   
items:
    - part_no:   A4786
      descrip:   Water Bucket (Filled)
      price:     1.47
      quantity:  4

    - part_no:   E1628
      descrip:   High Heeled "Ruby" Slippers
      size:      8
      price:     133.7
      quantity:  1

bill-to:  &id001
    street: | 
            123 Tornado Alley
            Suite 16
    city:   East Centerville
    state:  KS

ship-to:  *id001   

specialDelivery:  >
    Follow the Yellow Brick
    Road to the Emerald City.
    Pay no attention to the
    man behind the curtain.
...
```

字符串不一定要用双引号标示

在缩进中空白字符的数目并不是非常重要，只要相同层次结构的元素左侧对齐就可以了（不过不能使用TAB字符）。

在一个文件中，可同时包含多个文件，并用"`---`"分隔。选择性的符号"`...`"可以用来表示文件结尾（在利用流的通信中，这非常有用，可以在不关闭流的情况下，发送结束信号）。

### 数据类型

YAML 支持以下几种数据类型：

- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hashes） / 字典（dictionary）
- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）
- 纯量（scalars）：单个的、不可再分的值



#### 对象

```yaml
key: 
    child-key: value
    child-key2: value2
?  
    - complexkey1
    - complexkey2
:
    - complexvalue1
    - complexvalue2
person: {name: John Smith, age: 33}
```

问号加一个空格代表一个复杂的 key，配合一个冒号加一个空格代表一个 value；意思即对象的属性是一个数组 [complexkey1,complexkey2]，对应的值也是一个数组 [complexvalue1,complexvalue2]



#### 数组

```yaml
--- # 最喜爱的电影 区块格式（block format）短杠+空白字符作为起始
 - Casablanca
 - North by Northwest
 - Notorious
...

--- # 购物清单 内置格式（inline format）可以选择──用方括号围住，并用逗号+空白区隔（类似JSON的语法）
 [milk, pumpkin pie, eggs, juice]
```



#### 复合结构

```yaml
languages:
  - Ruby
  - Perl
  - Python 
websites:
  YAML: yaml.org 
  Ruby: ruby-lang.org 
  Python: python.org 
  Perl: use.perl.org
```



#### 纯量

```yaml
boolean: 
    - TRUE  #true,True都可以
    - FALSE  #false，False都可以
float:
    - 3.14
    - 6.8523015e+5  #可以使用科学计数法
int:
    - 123
    - 0b1010_0111_0100_1010_1110    #二进制表示
null:
    nodeName: 'node'
    parent: ~  #使用~表示null
string:
    - 哈哈
    - 'Hello world'  #可以使用双引号或者单引号包裹特殊字符
    - newline
      newline2    #字符串可以拆成多行，每一行会被转化成一个空格
date:
    - 2018-02-17    #日期必须使用ISO 8601格式，即yyyy-MM-dd
datetime: 
    -  2018-02-17T15:02:31+08:00    #时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区
```



#### 引用

```yaml
defaults: &defaults
  adapter:  postgres
  host:     localhost

development:
  database: myapp_development
  <<: *defaults

test:
  database: myapp_test
  <<: *defaults
```

**&** 用来建立锚点（defaults），**<<** 表示合并到当前数据，***** 用来引用锚点。



#### 字符串详解

```yam
- str: 这是一行字符串 # 默认不加引号
- str: '这是一行特殊的: 字符串' # 包含空格和特殊字符需要引号
- str: 'it''s good day' # 单引号中存在单引号，连续使用两个单引号转义
- str: 第一段 # 可以多行，另起一行需空格隔开，换行符会转换为空格
 第二段
 第三段
- str: | # 保留换行符\n第二段
 保留换行符
 第二段
- str: > # 折叠换行  第二段\n
 折叠换行
 第二段
- str: |+ # 保留字串末尾的换行\n\n\n
 保留字串末尾的换行
 
 
- str: |- # 删除字串末尾的换行
 删除字串末尾的换行
 
 
 
```



