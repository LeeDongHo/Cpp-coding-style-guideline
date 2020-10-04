# C++ coding style guideline

Google C++ Style Guideline을 참고함.

## 명명 규칙 (Naming)

### A. 일반 명명 규칙 (General Naming Rules)
다른 팀 사람이 일기 쉽게 이름을 지으세요.
오브젝트의 목적이나 의도를 설명하는 이름을 사용하세요. 코드의 가로 길이가 늘어나는 것 보다 다른 사용자가 읽었을 때 바로 이해되는게 더 중요합니다. 프로젝트 외 인원이 알지 못하는 약어 (특히 두문자어) 사용은 최소화합니다. 단어 중간을 삭제한 약어(Message -> msg)를 사용하지 않습니다. 위키피디아에서 사용되는 약어는 허용합니다. 일반적으로 묘사(설명)은 이름의 범위와 비례해야합니다. 예를 들면 n 이라는 변수는 5줄 이내 함수에서는 적합하지만 클래스 변수명으로는 적합하지 않습니다.

```
class MyClass {
  public:
    int CountFooErrors(const std::vector<Foo>& foos) {
      int n = 0;  //  Clear meaning given limited scope and context
      for (const auto& foo : foos) {
        ...
        ++n;
      }
      return n;
    }
    void DoSomethingImportant() {
      std::string fqdn = ...;   // Well-known abbreviation for Fully Qualified Domain Name
    }
  private:
    const int kMaxAllowedConnections = ...;   // Clear meaning within context
}
```
```
class MyClass {
  public:
    int CountFooErrors(const std::vector<Foo>& foos) {
      int total_number_of_foo_errors = 0;  //  Overly verbose given limited scope and context
      for (int foo_index = 0; foo_index < foos.size() ; ++foo_index) {  // Use idiomatic 'i'
        ...
        ++total_number_of_foo_errors;
      }
      return total_number_of_foo_errors;
    }
    void DoSomethingImportant() {
      int cstmr_id = ...;   // Deletes internal letters
    }
  private:
    const int kNum = ...;   // Unclear meaning within board scope
}
```
iterator로 사용하는 i, template parameter로 사용하는 T 같이 일반적으로 사용되는 약어는 허용됩니다.
앞으로 말할 "단어"는 단어 사이에 공백이 없이 영어로 작성한 것을 말합니다. 단어에는 약어와 두문자어도 포함됩니다. 파스칼 표기법이나 카멜 표기법같이 첫 글자를 대문자로 표기하는 방법으로 작성된 단어의 경우 약어를 단일 단어로 취급합니다. 예를 들어 StartRPC() 라면 StartRpc()로 표기합니다.

Template parameters는 해당 카테고리의 명명법을 따릅니다. type template parameters는 type names 규칙을 따라야하며 non-type template parameters는 variable names 규칙을 따라야 합니다.

### B. 파일명 (File Names)

파일 이름은 소문자로 작성하고 언더스코어(_), 대시(-)를 포함할 수 있습니다. 소속된 프로젝트의 규칙을 따르세요. 따로 정해진 규칙이 없다면 언더스코어를 권장합니다.
```
my_useful_class.cc
my-useful-class.cc
myusefulclass.cc
myusefulclass_test.cc // _unittest and _regtest are deprecated.
```
C++ 파일 확장자는 .cc, 헤더는 .h를 사용해야합니다. 특정지점에 텍스트 파일로 포함되는 것은 .inc로 끝나야 합니다. (자세한 내용은 #self-contained headers 참고)

db.h처럼 /user/include에 존재하는 파일 이름은 사용하지 마세요.
logs.h 대신 http_server_logs.h 같이 명시적인 파일 이름을 사용하세요. 클래스는 같은 이름을 사용하세요. 예를 들면 FooBar 클래스는 foo_bar.h, foo_bar.cc를 사용해야합니다.

### C. 타입명 (Type Names)
타입명은 대문자로 시작하고 새로운 단어가 나올 때 언더스코어 대신 대문자를 사용합니다. MyExcitingClass, MyExcitingEnum.
모든 타입들(클래스, 구조체, type aliases, enums, template parameters)은 같은 명명규칙을 사용합니다. 
```
// classes and structs
class UrlTable { ... 
class UrlTableTester { ...
struct UrlTableProperties { ...

// typedefs
typedef hash_map<UrlTableProperties *, std::string> PropertiesMap;

// using aliases
using PropertiesMap = hash_map<UrlTableProperties *, std::string>;

// enums
enum class UrlTableError { ...
```

### D. 변수명 (Variable Names)
변수(함수 파라미터 포함), 멤버 변수의 이름은 모두 소문자와 언더스코어를 사용합니다. 구조체 변수는 해당하지 않고 클래스의 멤버 변수는 이름 끝에 언더스코어를 붙입니다.

#### **공통 변수명**
```
std::string tableName;    // BAD
std::string table_name;   // OK
```

#### **클래스 멤버 변수**
정적 혹은 비정적인 클래스 멤버 변수들은 일반 변수 명명 규칙을 따르지만 *끝에 언더스코어를 붙여줘야합니다*.
```
class TableInfo{
  ...
  private:
    std::string table_name_;      // OK
    static Pool<TableInfo>* pool_ // OK
}
```

#### **구조체 변수**
정적이거나 비정적인 구조체 변수들은 일반 변수 명명 규칙을 따릅니다. *클래스 처럼 끝에 언더스코어를 붙이지 않습니다.*
```
struct UrlTableProperties {
  std::string anme;
  int num_entries;
  static Pool<UrlTableProperties>* pool;
}
```

### E. 상수명 (Constant Names)
constexpr 또는 const로 선언됐고 프로그램 동작 중 값이 고정된 변수들 이름 앞에 k를 붙입니다. 단어를 구분할 때 대문자를 쓸 수 없는 경우 언더스코어를 사용할 수 있습니다.
```
const int kDaysInAWeek = 7;
const int kAndroid8_0_0 = 24;   //  Android 8.0.0
```
정적으로 저장되는 모든 변수(static, 전역 변수)는 상수 명명 규칙을 사용해야합니다. 이 규칙은 다른 저장 범위 변수(Automatic 변수)들에게는 선택사항 입니다.
[[정적 저장 변수 범위]](https://en.cppreference.com/w/cpp/language/storage_duration#Storage_duration)

### F. 함수명 (Function Names)
보통 함수명에는 대소문자가 혼합되어있습니다. 