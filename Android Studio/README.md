![image](https://github.com/kappleword/TroubleShooting/blob/main/img/22.04.25%20%EB%A6%AC%EC%82%AC%EC%9D%B4%ED%81%B4%EB%9F%AC%EB%B7%B0%20SparseBooleanArray%20%EC%A0%91%EA%B3%A0%ED%8E%BC%EC%B9%98%EA%B8%B0%20%EC%97%90%EB%9F%AC.jpg?raw=true)
+ 문제 : 리사이클러뷰를 SparseBooleanArray를 사용해서 접고 펼치기 가능하게 만들었는데 2번 항목이 펼쳐진 상태에서 1번 항목을 펼치면 1번 항목 내용이 정상 출력X
+ 원인 : 1번 항목의 리사이클러뷰를 전역변수로 선언해서 항목 변경할 때 초기화되고 no attached가 나온 듯
+ 해결 : 어댑터 선언할 때 `planList_recyclerView = holder.itemView.findViewById(R.id.rv_list_plan);` 추가해서 해결
------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://github.com/kappleword/TroubleShooting/blob/main/img/21.10.16%20Fragment%20already%20added%20%EC%97%90%EB%9F%AC.PNG?raw=true
)
+ 문제 : 저장 후 onFragmentChange로 화면 이동 시 Fragment already added 에러 발생 
+ 원인 : 안드로이드 앱에서 동일한 프래그먼트 객체로 beginTransaction.add() 메소드를 2번째 호출 시 아래와 같은 오류가 발생하는 듯
+ 해결 : 프래그먼트가 추가되어 있으면 삭제 후 새롭게 생성해서 해결
```java
            //모든 프래그먼트 초기화
            getSupportFragmentManager().popBackStack(null, FragmentManager.POP_BACK_STACK_INCLUSIVE);

            //프래그먼트가 이미 추가되있으면 삭제 후 새로운 프래그먼트를 생성한다
            if(resourceSurveyListFragment.isAdded()){
                getSupportFragmentManager().beginTransaction().remove(resourceSurveyListFragment);
                resourceSurveyListFragment = new ResourceSurveyListFragment();
            }

            resourceSurveyListFragment.setArguments(bundle);
            getSupportFragmentManager().beginTransaction().replace(R.id.resourceSurveyContainer, resourceSurveyListFragment,      ResourceSurveyListFragment.TAG).addToBackStack(null).commit();

```
------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://github.com/kappleword/TroubleShooting/blob/main/img/21.10.08%20setText%20%EC%97%90%EB%9F%AC.png?raw=true)
+ 문제 : 상세페이지로 이동 시 Resources$NotFoundException 에러 발생 후 앱이 죽음 
+ 원인 : setText(int)를 호출하면 해당하는 숫자의 리소스를 찾게 되게 됩니다. 이 해당하는 리소스가 없기때문에 익셉션이 발생한다
+ 해결 : setText(myInt) 와 같이 소스구성이 되어있다면 setText(Integer.toString(myInt)) 로 변경하시면 해결
+ 출처 : https://m.blog.naver.com/kkson50/221081639597
------------------------------------------------------------------------------------------------------------------------------------------------------------
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
