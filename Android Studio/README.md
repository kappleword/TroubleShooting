![21.08.05 inflate에러](./img/Trouble Shooting/21.08.05 inflate에러.PNG)
+ 문제 : 액티비티 내부 프래그먼트 화면 전환 부분 작성 중 `return inflater.inflate(R.layout.fragment_unused_surveyor_add, container, false);` 구문에서 에러 발생해서 화면 이동 x
+ 원인 : AppCompat은 예전소스라 parent에서 충돌이 일어 났거나 필요 SDK가 없어서 호환이 안된 것일 수도 있음
+ 해결 : res/values/themes/theme.xml에서 `parent="Theme.AppCompat.Light.NoActionBar`를 `parent="Theme.MaterialComponents.Light.NoActionBar"`로 변경
