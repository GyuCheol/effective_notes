# 규칙1
## 생성자 대신 static factory method를 고려하기

`요약`
```
static method를 통해 object를 반환하면 동적으로 개체 생성을 할 수 있다.
이를 통해 cache, singleton, subtype 반환 등을 할 수 있음.
```

- class를 통해 object를 생성하는 방법은 2가지
1. 생성자 (constructor)
2. public으로 선언된 static factory method

우리가 아는 Boolean Class는 이와 같은 방법으로도 객체를 반환한다.
```java
public static Boolean valueOf(boolean b) {
    return b ? Boolean.TRUE : Boolean.FALSE;
}
```

이것은 디자인 패턴의 factory method 와는 다르다. (일반적인 패턴은 아니다)

이것의 장점
1. 생성자는 class 이름 한정이지만, 이것은 method 고유 이름이 있다.
```
생성자 오버로딩은 API 사용자에게 명확한 동작을 예측하기 어렵다.
method을 통한다면 hint로서 method 이름을 가지고 동작을 기대할 수 있다.
```

2. 호출할 때마다 객체를 생성할 필요가 없다.
```
생성자는 호출이 되면 무조건 객체가 생성이 된다.
Boolean Class가 대표적인 예다.
다른 예로 cache 기법, multiton 기법, singleton 기법 등 객체 생성을 회피하고
객체를 반환할 수 있다는 점이다.
```

3. 반환 값의 subtype을 반환할 수 있다.
```
생성자는 그 class type만을 반환한다.
method는 하나의 함수이므로, 공변성 성질을 이용해 subtype을 반환할 수 있다.
즉, 어떤 개체를 만들지 동적으로 결정할 수 있다는 것.

jdbc의 url로 그것에 맞는 db connector 개체가 생성되는 것도 같은 원리이다.
```

이것의 단점
- 다른 static method와의 구분이 어려움.
```
그래서 주로 아래의 키워드의 용도만 사용한다.
valueOf, of, getInstance, newInstance, getType, newType
```