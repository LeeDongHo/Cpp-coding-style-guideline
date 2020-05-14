# C++ coding style guideline

Google C++ Style Guideline을 참고함.

### A. Naming
1. **Type Names**은 **파스칼 표기법**을 따른다.
```
// Class ans structs
class NetworkLibrary{
...
};

struct PacketHeader{
...
};

```

2. **Variable Names**은 **카멜 표기법**을 따른다.
```
std::string newString;
```

변수명을 작성할 때에는 줄임말을 사용하지 않습니다.
예외에는 반복문에서 쓰는 i,j이 있습니다.


3. **Macro Names**는 **대문자**로만 쓴다.
```
#define SQUARED(x) x*x
```


4. **Const**는 **접두어로 k**를 붙인다.
```
const int kWidth = 3;
```

### B. 중괄호
1. 클래스, 구조체의 경우 중괄호를 붙여서 사용합니다.
```
class NetworkLibrary{

}
```

2. 그 외의 경우에는 중괄호를 띄어서 사용합니다. (함수, if-else 등)
```
int Sum(int a, int b)
{
  return a+b;
}
```
