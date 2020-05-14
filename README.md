# C++ coding style guideline

Google C++ Style Guideline을 참고함.

### A. Naming
1. **Type Names**은 **파스칼 표기법**을 따른다.
```
// Class ans structs
Class NetworkLibrary{
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
