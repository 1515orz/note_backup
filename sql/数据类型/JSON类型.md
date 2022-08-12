__# JSON类型

    在MySQL中我们同样可以储存JSON文档,它基本上是一种通过网络储存和传输数据的"轻量级格式"
    在网络和移动客户端中被大量使用,大多数时候,你的移动应用程序通过把JSON将你的数据发送到后端


## JSON
* JSON会使用大括号定义一个对象
* 大括号里可以有一个或多个键值对
* 键就是字符串,所以要*带上引号*
* 值可以是任意值,字符串,布尔值,数组,其他对象等
* JSON可以很轻松地储存每个对象的多个属性
_插入一个JSON数据_**标准插入**
```MySQL
UPDATE products
SET properties = '
{
	"dimensions": [1,2,3],
    "weight": 10,
    "manufacturer": { "name": "sony" }
}
'
WHERE product_id = 1
```

_插入一个JSON数据_**调用MySQL函数** **JSON_OBJECT&JSON_ARRAY**
```MySQL
UPDATE products
SET properties = JSON_OBJECT(  # 插入JSON对象
	'weight',10,
    'dimensions', JSON_ARRAY(1, 2, 3),  # 插入JSON数组
    'manufacturer', JSON_OBJECT('name','sony')  # 插入套娃JSON对象
)
WHERE product_id = 1  
```

### JSON 提取
* 我们可以从JSON对象中提取单独的键值对,这就是比起VARCHAR数据类型的好处
* 对于字符串来说,在JSON对象中提取单独的键值对真的很难

_提取JSON数据中的值 _**JSON_EXTRACT**
```MySQL
# 使用JSON_EXTRACT函数提取JSON中的值
SELECT product_id, JSON_EXTRACT(properties, '$.weight') AS weight
# $ 符号代表properties(self) "."代表引用对象的属性(键),注意加引号
FROM products
WHERE product_id = 1;
```

_提起JSON中的值_ **列路径运算符(指针) ->>**
```MySQL
# "->"代表列路径运算符,指向JSON的键  "$."代表引用
SELECT product_id, properties -> '$.weight'
FROM products
WHERE product_id = 1;
```

#### 使用指针访问JSON值下的值
_访问数组_ 
`SELECT product_id, properties -> '$.dimensions[1]`
 ++[]方括号中的值代表索引值,类似指针,从 0 开始++
_访问值下的对象_
`SELECT product_id, properties -> '$.manufacturer.name'`
==会返回带双引号的字符串==
++使用 ‘.’ 访问对象下的属性,可以向下访问++
==不返回双引号==
_可以将“->” 替换为“->>_”_
`SELECT product_id, properties ->> '$.manufacturer.name'`

### 更新 JSON 数据
我们可以使用`JSON_SET()`来更新或添加新属性**JSON_SET()**
```MySQL
UPDATE products
SET properties = JSON_SET(
	properties,  # 选择对象,可以用$表示
    '$.weight',20,  # 更新键值对,类似字典
    '$.age', 10  # 插入新的键值对也是可以的
)
WHERE product_id = 1  
```
  也可以使用`JSON_REMOVE()`  来移除属性**JSON_REMOVE()**
```MySQL
UPDATE products
SET properties = JSON_REMOVE( # 移除属性
	properties, 
    '$.age'  # 选择键进行移除
)
WHERE product_id = 1  
```

* 对JSON的更新操作实质上就是覆盖更新
