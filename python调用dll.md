##### 如果是64位的python，要是用64位的DLL

- 参考https://blog.csdn.net/jethai/article/details/52345083生成64位的DLL！


```
from ctypes import *

import time
# 这两种方法都可以
#dll = cdll.LoadLibrary("makeDLL.dll")
#dll = CDLL("makeDLL.dll")

#dll = WinDLL("makeDLL.dll")
#dll = windll.LoadLibrary("makeDLL.dll")

# python3之后  bytes和string分离了！


class A(Structure):
    _fields_=[("a1",c_int)]

from ctypes import *
class SimpStruct(Structure):
    _fields_ = [ ("nNo", c_int),
              ("fVirus", c_float),
              ("szBuffer", c_char * 512)]

dll = CDLL("makeDLL.dll")
simple = SimpStruct();
simple.nNo = 16
simple.fVirus = 3.1415926
simple.szBuffer = b"magicTong/0"
print(dll.PrintStruct(byref(simple)))
print(simple.nNo)
print(simple.fVirus)

a = A()
dll.ChangeValue(byref(a))
print("a is :",a.a1)
```

```
#include "stdafx.h"
#include <stdio.h>

#define DLLEXPORT extern "C" __declspec(dllexport)

typedef struct A{
	int a1;
	float a2;
};

DLLEXPORT int sum(int a, int b) {
	return a + b;
}

DLLEXPORT int PrintInfo(char* p, int len) {
	printf("%s\n",p);
	return len;
}

DLLEXPORT int ChangeValue(A* p) {
	p->a1 = 100;
	p->a2 = 200;
	printf("a1 is %d\n",p->a1);
	printf("a2 is %f\n",p->a2);
	return p->a2;
}

typedef struct _SimpleStruct
{
	int    nNo;
	float  fVirus;
	char   szBuffer[512];
} SimpleStruct, *PSimpleStruct;
typedef const SimpleStruct*  PCSimpleStruct;

extern "C"int  __declspec(dllexport) PrintStruct(PSimpleStruct simp);
int PrintStruct(PSimpleStruct simp)
{
	printf("nMaxNum=%f, szContent=%s", simp->fVirus, simp->szBuffer);
	simp->nNo = 333333;
	simp->fVirus = 0.00001234;
	return simp->nNo;
}
```
