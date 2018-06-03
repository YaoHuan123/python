```
class CapStr(str):
    def __new__(cls, string):
        string = string.upper()
        return str.__new__(cls,string)

a = CapStr("i love fashC.com")
print(a)
```

```
class C:
    def __init__(self):
        print("__init__")

    def __del__(self):
        print("__del__")

c1 = C()
c2 = c1
c3 = c2
del c1

print(".............")
del c2
print("...........")
del c3
```
