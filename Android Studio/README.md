![21.08.05 inflate에러](./img/21.08.05 inflate에러.PNG)
+ 문제 : 액티비티 내부 프래그먼트 화면 전환 부분 작성 중 `return inflater.inflate(R.layout.fragment_unused_surveyor_add, container, false);` 구문에서 에러 발생해서 화면 이동 x
+ 원인 : AppCompat은 예전소스라 parent에서 충돌이 일어 났거나 필요 SDK가 없어서 호환이 안된 것일 수도 있음
+ 해결 : res/values/themes/theme.xml에서 `parent="Theme.AppCompat.Light.NoActionBar`를 `parent="Theme.MaterialComponents.Light.NoActionBar"`로 변경


![21.08.10 radioButton 에러](./img/21.08.10 radioButton 에러.PNG)
+ 문제 : 라디오 버튼 클릭 시 switch 조건에 분기 해서 값은 가져간 후 죽어버림 
+ 원인 : 라디오 버튼 속성에 클릭기능을 쓸데없이 넣어놔서 프래그먼트화면에서 클릭 이벤트를 찾다가 없으니 앱이 죽은 것
+ 해결 : 레이아웃 파일의 라디오 버튼에서 `android:onClick="onRadioButtonClicked"` 삭제
+ 라디오 버튼은 라디오 그룹 차원에서 관리하니 따로 클릭 이벤트를 안 넣어도 된다
