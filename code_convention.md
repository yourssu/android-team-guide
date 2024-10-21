# Code Convention

<aside>
| 💡 추가나 수정이 필요한 부분에 대해서 Contribute 해주세요!

</aside>

## 1. binding 생성 관련

```kotlin

lateinit var binding: ActivityMainBinding

override fun onCreate(...) {
		binding = ActivityMainBinding.inflate(layoutInflater)
		setContentView(binding.root)
}
```



## 4. 주석의 위치

함수 주석의 위치

```kotlin
// 모든 주석은 함수 선언 바로 위에
fun foo(f: Any) {
	...
}

/**
 * 여러 줄일 경우에는 
 * 이 형식으로
 */
fun bar(b: Bar) {
	..
}
```

## 5. 함수 파라미터

2개 이하일 경우 한 줄에

```kotlin
fun foo(a: Int, t: List<Int>) {
	...
}
```

3개 이상일 경우 여러 줄로 split

```kotlin
fun bar(
	b: Float,
	a: List<List<Int>>,
	c: Context, // trailing comma 넣기
) {
	...
}
```

## 6. 함수 파라미터의 우선순위 

- 1순위: 기본값이 없는 파라미터
- 2순위: Modifier (+modifer는 기본값을 넣어주기)

```kotlin
fun Switch(
    onToggle: (SwitchState) -> Unit,
    modifier: Modifier = Modifier,
    switchState: SwitchState = SwitchState.Unselected
)
```

## 7. 중괄호

if, for, when 브랜치, do 및 while 문과 표현식의 경우 본문이 비어 있거나 단일 구문만 포함하는 경우에도 중괄호가 필요합니다.

```kotlin
if (string.isEmpty())
    return  // WRONG!

if (string.isEmpty()) {
    return  // Okay
}

if (string.isEmpty()) return  // WRONG
else doLotsOfProcessingOn(string, otherParametersHere)

if (string.isEmpty()) {
    return  // Okay
} else {
    doLotsOfProcessingOn(string, otherParametersHere)
}
```

빈블럭도 중괄호 이후에는 enter해야합니다.

```kotlin
try {
    doSomething()
} catch (e: Exception) {} // WRONG!

try {
    doSomething()
} catch (e: Exception) {
} // Okay
```


## 8. 표현식

표현식으로 사용되는 if/else 조건문에서는 전체 표현식이 한 줄에 들어가는 경우에만 중괄호를 생략할 수 있습니다.

```kotlin
val value = if (string.isEmpty()) 0 else 1  // Okay

val value = if (string.isEmpty())  // WRONG!
    0
else
    1

val value = if (string.isEmpty()) { // Okay
    0
} else {
    1
}
```