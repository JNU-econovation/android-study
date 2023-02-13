# 코틀린 프로그래밍 쿡북 2장

### if 키워드를 활용한 값 할당
```kotlin
fun main()(args: Array<String>) {
    var buyCoffee: Boolean
    var money: Int = 500
    buyCoffee = if (money > 2100) true else false
}
```

### when과 함께 범위 사용
----
- 범위를 사용할 수 있는 점
- 데이터 클래스를 조건문으로 활용할 수 있는 점
```kotlin
fun main(args: Array<String>) {
    val diaryLength = 10

    when(diaryLength) {
        in (0..5) -> println("내일은 좋은 일이 있을거야!")
        !in (0..5) -> println("Zzz")
    }
}
```
```kotlin
fun main(args: Array<String>) {
    data class character (var level: Int, var status: String, var experience: Int)

    var hyeonjiCharacter = character(1, awake, 30)
    when (character.experience) {
        40 -> println("레벨업이 얼마 남지 않았어요!")
        50 -> println("레벨이 올랐습니다. 현재 레벨 : ${character.level}")
    }
}
```

<br>

### 사용자 정의 오브젝트와 when
----
 - 정의 오브젝트끼리 비교가 가능
 ```kotlin
fun main(args: Array<String>) {
    data class character (var level: Int, var status: String, var experience: Int)

    var hyeonjiCharacter = character(1, awake, 30)
    var sumiCharacter = character(3, sleep, 280)

    when(hyeonjiCharacter) {
        sumiCharacter -> println("두 캐릭터의 정보가 동일합니다.")
    }
}
```

<br>

### 표현식으로서의 try-catch
----
- 코틀린과 자바의 예외 처리 차이
  - 코틀린은 예외를 던지더라도 원하지 않는다면 try-catch문을 작성하지 않아도 된다.
  - 자바는 컴파일 오류가 발생한다.
<br>

### also 함수를 이용한 swap 함수 만들기
----
```kotlin
var a = 1
var b = 2

a = b.also { b = a }
```

<br>

### 사용자 정의 예외
----

<br>

### 다중 조건 반복문
----
```kotlin
val numbers = arrayOf(5, 6, 7, 1, 3, 4, 5, 7, 12, 1)

(0..9).asSequence().takeWhile {
    it < numbers[it]
}.forEach {
    println("$it - ${numbers[it]}")
}
```
- `takeWhile`은 특정 조건을 만족하기 이전까지의 요소 그룹을 반환한다.
```kotlin
data class Record(val date: Int, val isRecoreded: Boolean)

fun main() {
    val datesOnJan2023 = arrayOf(
        Record(1, true),
        Record(2, false),
        Record(3, true),
        ...,
        Record(31, false)
    )
    val today: String = 23
    
    (0..datesOnJan2023.length()-1).takeWhile {
        today > datesOnJan2023[it]
    }.forEach {
        //젤리 표시
    }
}

```

<br>