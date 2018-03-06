###### dict
- dict的key必须是不可变对象
- 判断key的存在
  `'Thmous' in d` 或 `d.get('Thmous')`
- 默认情况下，dict迭代的是key 如果要迭代value，可以用for value in d.values()，如果要同时迭代key和value，可以用for k, v in d.items()。
