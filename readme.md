# 시작
: html_css 공부하긴 해야하는데 이참에 프로젝트 느낌으로 뭔가 만들면서 하면 재미있지 않을까...?
해서 시작하게 되었습니다.

<h3> 1. 기본 글씨체를 쓰려니 너무 페이지가 심심한거 같아서 일단 폰트를 적용하는것부터 도전의 시작입니다.</h3>
1. https://www.fonts.google.com 에 접속한다.
2. 원하는 폰트를 검색한다.
3. 원하는 폰트를 클릭해서 들어간뒤에 select를 통해 선택한다.
4. Selected families라고 바로 옆에 창이 나오는데, 안나오면 우측 상단 사각형 아이콘(Selected families)를 클릭.
5. 폰트를 직접 다운받을수도 있고, link나 @import 를 통해서 끌어올수 있는데 방법은 선택하면 된다.
6. 설명대로 폰트를 적용하고 결과를 확인하면 끝.

<h3> 2. 버튼과 modal을 사용해 알아야할 개념, 단어별로 나열한다.</h3>
- 모달을 넣었는데, 처음에 잘 작동하다가 갑자기 모달 창이 안뜨는 문제가 발생했다..
- 이것 저것 뒤져보다 다 안먹혀서 처음부터 다시 찬찬히 살펴본 결과
- bootstrap을 끌어오는 script의 닫는 태그부분이 <`/`scrip> 으로 바뀌어 있었다. (what???!?!?)
- 고치니까 바로 해결


<h3> 3. 버튼을 누르고 해당 개념을 이해하면 오른쪽 사이드에 암기 완료 목록에 저장되고 , 프로그레스 바로 진행률을 나타내는 기능을 만들어보자.</h3>
1. 먼저 프로그레스바 버튼을 만들어보자. 검색을 해보니 바로 나와서 복붙해봤다.
java 함수를 이용해서 버튼을 클릭하면 게이지가 올라가는 기능도 넣을 수 있는데 모달의 버튼과 연계하면 될듯하다.
> java 함수 모양을 보니 document.~~ 이런식으로 쓰이길래 어떤 녀석인가 싶어서 찾아 봤는데 html 문서 자기 자신을 뜻하는 녀석이고
이 녀석은 다양한 method를 가지고 있었다. 훑어보기만 하면서 당장 활용가능한것들은 써봐야겠다.

1-1. 모달에서 이해했음! 버튼을 누르면 프로그레스바 진도 1씩 상승시키기.
- 간단한 함수를 버튼 클릭시 이벤트로 넣어서 실행시켜서 구현
1-2. 프로그레스바 진도와 함께 화면 좌측 상단의 진도를 나타내는 text도 업데이트 하고싶다.
- String.format 을 이용해서 업데이트 하려고 했는데 안먹힌다.. 자세하게 할 시간은 없으니 다음에
- span을 여러개로 나눠 text를 넣고 변수를 직접할당해서 값을 바꿧다.
- 학습 완료시 축하 문구가 뜨도록 설정.
1-3. 한 keyword에서 "이해했다." 버튼을 계속 누를수 있다는 문제를 발견. 클릭하면 비활성화 되도록 변경해보자.
- 생각해보니 버튼의 기본상태가 "이해했니?" 였다가 비활성화시 "이해했다!"로 바꾸는게 더 나아보여서 바꿧다.
- 함수에 버튼 클릭을 발생한 객체 자신을 어떻게 인자로 보내줄까 엄청나게 구글링했는데 계속 못하다가
- 버튼의 onclick의 인자에 this를 넣으니 넘어가는것을 발견
- alert 이녀석이 python의 print 느낌으로 확인하기 좋은듯
- 각설하고, this를 통해 자기자신을 받아오고 e.disabled = true; 를 통해 비활성화 성공
- 그런데 여러 버튼을 만들고 id도 전부 다르게 설정했는데 버튼 전체가 비활성화됨...
- this를 자세히 살펴보니 type of global this 라고 써 있는것을 발견.
- 는 약간의 착각이 있었고 버튼을 전부 하나의 modal로 연결해놔서 전부 disabled되었던 것.
1-4. problem 모달 창이 열릴때 몇번째 열어서 보고있는지 기록하고 싶음.
- getElementsByClassName으로 class를 가져오고 addEventListner로 추가하려했으나 여러객체에 한번에 추가불가한것으로 보임. for문쓰면 될듯한데 pass
- 다른 방법을 찾다보니 $(id또는 클래스 등 ..).on('show.bs.modal',함수) 방법을 찾음.
- 참고:https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=sooni_&logNo=221455423015
- 각 problem 모달이 첫 번째 버튼 제외 나머지는 정상작동을 안해서 왜이러지 했는데 내용 업데이트를 1번 버튼에만 해둬서 함수 중간에 오류가 발생했던것
- 뭔가 잘 안되면 개발자도구로 오류가 없나 살펴보는게 중요하다!!
- 왜 java 함수들이 안먹히나 했더니 안불러와서 그랬던거였다. (일단은 쓸 수 있는것만 쓰자)
- span의 값을 변경하기위해 getattribute, setattribute method를 활용했다.
- 결국 jquery를 불러왔다. 진작 했으면 편했을텐데... each문을 활용해 각각에 모달이 열리면 값 갱신 성공






###### 참고자료
<!-- 형변환 -->
1. https://mine-it-record.tistory.com/330 
<!-- Each문 -->
2. https://webclub.tistory.com/455
<!-- modal 속성 -->
3. https://getbootstrap.com/docs/5.0/components/modal/
<!-- 이벤트의 종류 -->
4. https://jenny-daru.tistory.com/17
<!-- String indexing, slicing -->
5. https://coding-factory.tistory.com/126
<!-- 이벤트 리스터 예제 -->
6. https://kkk-kkk.tistory.com/entry/%EC%98%88%EC%A0%9C-9-5-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A6%AC%EC%8A%A4%EB%84%88%EC%97%90%EC%84%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EA%B0%9D%EC%B2%B4-%EC%A0%84%EB%8B%AC-%EB%B0%9B%EA%B8%B0
<!-- html, dom, form 등 간단 예제 -->
7. https://terianp.tistory.com/92
<!-- DOM 객체 목록 -->
8. http://www.tcpschool.com/javascript/js_dom_document
<!-- jump to java -->
9. http://www.tcpschool.com/javascript/js_dom_document
<!-- progress bar -->
10. https://www.codingfactory.net/11010
<!-- input 사용법 -->
11. https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input/button
<!-- form 작동방식의 이해 -->
https://www.nextree.co.kr/p8428/
<!-- 선택자 -->
https://www.google.com/search?q=%EC%84%A0%ED%83%9D%EC%9E%90+%ED%8F%AC%ED%95%A8%EA%B4%80%EA%B3%84&rlz=1C1SQJL_koKR786KR786&oq=%EC%84%A0%ED%83%9D%EC%9E%90+%ED%8F%AC%ED%95%A8%EA%B4%80%EA%B3%84&aqs=chrome..69i57j0i546l4.2561j0j4&sourceid=chrome&ie=UTF-8

https://code.tutsplus.com/ko/tutorials/the-30-css-selectors-you-must-memorize--net-16048

