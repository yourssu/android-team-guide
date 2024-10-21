# Code Convention

<aside>
| 💡 수정이 필요한 부분에 대해서 Contribute 해주세요!

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