## Object of type ‘datetime‘ is not JSON 日期序列化问题

重写构造json类，遇到日期特殊处理，其余的用内置的就行

```python
from datetime import date, datetime

class ComplexEncoder(json.JSONEncoder):
    def default(self, obj):
        if isinstance(obj, datetime):
            return obj.strftime('%Y-%m-%d %H:%M:%S')
        elif isinstance(obj, date):
            return obj.strftime('%Y-%m-%d')
        else:
            return json.JSONEncoder.default(self, obj)
```

在使用时，json.dumps时需要调用上面定义的类，指定cls参数为ComplexEncoder

```python
json.dumps(your_data, cls=ComplexEncoder)
```

