# Code Convention

<aside>
| 💡 추가나 수정이 필요한 부분에 대해서 Contribute 해주세요!

</aside>

## binding 생성 관련

```kotlin

lateinit var binding: ActivityMainBinding

override fun onCreate(...) {
		binding = ActivityMainBinding.inflate(layoutInflater)
		setContentView(binding.root)
}
```

## 중복코드
중복된 코드가 있으면 추후 유지보수가 어렵고, 변경 시 실수할 가능성이 커지므로 피하는 것이 좋습니다. 공통된 로직은 Util 클래스로 빼서 재사용성을 높이는 것이 좋습니다. 또한 메소드의 길이는 너무 길면 가독성이 떨어지므로, 10~20라인 정도로 유지하는 것이 좋습니다.

- 중복코드 제거 전
    ```kotlin
    fun showErrorDialog(context: Context) {
        AlertDialog.Builder(context)
            .setTitle("Error")
            .setMessage("An error occurred.")
            .setPositiveButton("OK") { dialog, _ -> dialog.dismiss() }
            .show()
    }

    fun showSuccessDialog(context: Context) {
        AlertDialog.Builder(context)
            .setTitle("Success")
            .setMessage("Operation completed successfully.")
            .setPositiveButton("OK") { dialog, _ -> dialog.dismiss() }
            .show()
    }
    ```

- 중복코드 제거 후(use util)
    ```kotlin
    fun showDialog(
        context: Context,
        title: String,
        message: String,
        positiveButtonText: String = "OK"
    ) {
        AlertDialog.Builder(context)
            .setTitle(title)
            .setMessage(message)
            .setPositiveButton(positiveButtonText) { dialog, _ -> dialog.dismiss() }
            .show()
    }

    fun showErrorDialog(context: Context) {
        showDialog(context, title = "Error", message = "An error occurred.")
    }

    fun showSuccessDialog(context: Context) {
        showDialog(context, title = "Success", message = "Operation completed successfully.")
    }
    ```

## Scope 함수
Scope 함수(let, apply, run, also, with)는 객체나 로직을 간결하게 처리하고, 가독성을 높일 수 있도록 도와줍니다. 적절한 Scope 함수를 사용하는 것이 중요하며, 코드 가독성 및 명확성을 유지해야 합니다.
```kotlin
// let 예시
val user = api.getUser()
user?.let {
    // it을 통해 user 객체를 안전하게 사용
    println(it.name)
}

// apply 예시
val view = TextView(context).apply {
    text = "Hello"
    textSize = 20f
    setTextColor(Color.BLACK)
}

// run 예시
val result = run {
    val x = 10
    val y = 20
    x + y // 마지막 라인이 반환값
}
```


## 상수
하드코딩된 값은 의도를 파악하기 어렵고, 유지보수가 어려울 수 있으므로 상수로 정의해서 관리하는 것이 좋습니다. 또한, 의미 있는 이름을 부여해 코드 가독성을 높일 수 있습니다.

- 하드코딩된 상수:
    ```
    kotlin
    fun setTextSize(textView: TextView) {
        textView.textSize = 16f  // 하드코딩된 숫자
    }
    ```

- 상수화된 코드
    ```kotlin
    const val DEFAULT_TEXT_SIZE = 16f

    fun setTextSize(textView: TextView) {
        textView.textSize = DEFAULT_TEXT_SIZE  // 상수 사용
    }
    ```

## 주석의 위치

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

## 함수 파라미터

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

## 함수 파라미터의 우선순위 

- 1순위: 기본값이 없는 파라미터
- 2순위: Modifier (+modifer는 기본값을 넣어주기)

```kotlin
fun Switch(
    onToggle: (SwitchState) -> Unit,
    modifier: Modifier = Modifier,
    switchState: SwitchState = SwitchState.Unselected
)
```

## 🚨 많은 파라미터 vs 객체 자체를 넘기기
- 논의가 필요합니다!

## 중괄호

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


## 표현식

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



## reference
- https://it-techtree.tistory.com/entry/codesmell-refactoring
- https://github.com/PRNDcompany/android-style-guide