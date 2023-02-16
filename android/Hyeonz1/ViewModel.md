# ViewModel

> #### 이 문서는 Android Developers의 공식 문서를 바탕으로 작성하였습니다. 
>[Android Kotlin Fundamentals: 5.1 ViewModel](https://developer.android.com/codelabs/kotlin-android-training-view-model?index=..%2F..android-kotlin-fundamentals#0)

<br>
<br>

## 📌 ViewModel의 필요성
---
### ViewModel의 필요성
**ViewModel이 없는 경우 발생하는 문제**
- 문제
    - device-configuration이 변했을 때, UI의 데이터가 보존되지 않는다.
- 예시
    - [Sleeper - LoginActivity](./img/sleeperLoginActivity.png)
    - 유저가 아이디를 입력하다가 화면을 회전하면 입력된 값이 사라진다.
<br>
<br>

**문제 발생 원인**
- [참고 - Activity Lifecycle](./img/activityLifeCycle.png)
- 화면 회전이 일어나면 Destroy후 다시 Create된다.
<br>
<br>

**ViewModel을 이용한 문제 해결**
- ViewModel을 이용하면 UI에 표시하는 것과 관련된 데이터를 저장 및 관리할 수 있다.
- ViewModelFactory는 ViewModel을 객체로 만들어 반환한다.


<br>
<br>

## 📌 App Architecture
---
- [UI Controller와 ViewModel의 관계](./img/relationshipBetweenUIcontrollerAndViewModel.png)

### 1. UI Controller
**UI Controller란?**
- Activity나 Fragment를 의미한다.

**UI Controller의 책임**
1. 화면 보여주기
2. 유저의 입력 받기

**UI Controller 활용 예시**
- [Sleeper - LoginActivity](./img/sleeperLoginActivity.png)
- LoginActivity에서는 로그인 화면을 보여주고, 유저의 입력을 받는 작업만 수행한다.
    - 자동 로그인 여부를 체크해도, LoginActivity는 자동 로그인 여부에 대한 데이터를 가지지 않는다.
    - LoginActivity는 자동 로그인 여부에 대한 데이터를 LoginViewModel에서 가져와서 UI에 보여준다.
        ~~~kotlin
        // Activity에서는 사용자의 입력을 받고, 이후의 정보 처리는 ViewModel에 맡긴다.
        // 사용자의 입력을 받아서 viewModel에 있는 setAuto함수를 실행시켰다. 
        binding.btnLoginAuto.setOnCheckedChangeListener { _, isChecked -> viewModel.setAuto(isChecked) }


        // 2. ViewModel의 isAutoLogin에 대한 데이터를 가져와서 UI를 보여준다.
        viewModel.isAutoLogin.observe(this, Observer { it ->
        binding.btnLoginAuto.isChecked = it })
        ~~~
<br>
<br>

### 2. ViewModel
**ViewModel의 책임**
1. UI Controller(fragment나 activity)가 사용자에게 보여주어야 하는 데이터를 가지고 있다.
    - 명명법: LoginViewModel은 LoginActivity와 관련된 데이터를 가지도록 작성한다.
2. 데이터의 계산 및 변형

**예시**
- LoginViewModel는 사용자의 이전 자동 로그인 설정 여부와 유저 아이디, 비밀번호에 대한 데이터를 가지고 있다.
    ~~~kotlin
    // setAuto함수는 LoginViewModel에 있는 isAutoLogin이라는 변수에 사용자 입력값을 넣는다.
    fun setAuto(isChecked : Boolean) {
        _isAutoLogin.value = isChecked
    }
    ~~~
<br>
<br>

### 3. ViewModelFactory
**ViewModelFactory의 책임**
- ViewModel 객체 생성

<br>
<br>

## 📌 결론
---
1. 사용자의 입력을 받은 내용이 UI에 직접 반영되지 않는다.
2. 사용자의 입력은 ViewModel의 Data에 반영된다.
3. UI Controller는 ViewModel의 데이터를 관찰하여 UI에 데이터를 표시한다.