![image](https://github.com/kappleword/TroubleShooting/blob/main/img/21.09.30%20spinner%20%EC%9D%B4%EB%B2%A4%ED%8A%B8%20%EC%97%90%EB%9F%AC.PNG?raw=true)
+ 문제 : Spinner 항목 선택 시 숨겨둔 텍스트 박스가 보이게끔 만들었는데 해당 페이지 이동 시 앱이 죽었다 
+ 원인 : Spinner에 맞지 않는 `setOnClickListener`를 사용해서 발생한 듯 
+ 해결 : `setOnClickListener`을 `setOnItemSelectedListener`으로 변경해서 만드니 제대로 동작
------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://user-images.githubusercontent.com/45361543/131081906-291cd5f2-967f-40c1-a2d5-439e89d8e11d.png)
+ 문제 : 액티비티 내부 프래그먼트 화면 전환 부분 작성 중 `return inflater.inflate(R.layout.fragment_unused_surveyor_add, container, false);` 구문에서 에러 발생해서 화면 이동 x
+ 원인 : AppCompat은 예전소스라 parent에서 충돌이 일어 났거나 필요 SDK가 없어서 호환이 안된 것일 수도 있음
+ 해결 : res/values/themes/theme.xml에서 `parent="Theme.AppCompat.Light.NoActionBar`를 `parent="Theme.MaterialComponents.Light.NoActionBar"`로 변경  
------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://user-images.githubusercontent.com/45361543/131081953-74c4b17a-7e7c-47bf-9b28-cc8e1242f5fa.png)
+ 문제 : 라디오 버튼 클릭 시 switch 조건에 분기 해서 값은 가져간 후 죽어버림 
+ 원인 : 라디오 버튼 속성에 클릭기능을 쓸데없이 넣어놔서 프래그먼트화면에서 클릭 이벤트를 찾다가 없으니 앱이 죽은 것
+ 해결 : 레이아웃 파일의 라디오 버튼에서 `android:onClick="onRadioButtonClicked"` 삭제
+ 라디오 버튼은 라디오 그룹 차원에서 관리하니 따로 클릭 이벤트를 안 넣어도 된다  
------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://user-images.githubusercontent.com/45361543/131081972-bb0de2f8-7bd4-4298-826e-a3a595609a39.png)
+ 문제 : 화면 이동시 널포인터 에러빔맞고 앱 죽음
+ 원인 : 중복되는 부분 코드를 복붙해놓고 버튼의 findViewById의 id값을 제대로 안 바꾼 것
+ 해결 : 올바른 버튼의 id값들로 변경해줘서 해결
+ 버튼 id는 btn_버튼명으로 통일!
