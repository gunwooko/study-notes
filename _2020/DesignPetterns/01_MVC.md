# MVC(Model-View-Controller)

소프트웨어를 설계하는 디자인 패턴이다. 각 기능의 역활로 코드를 나눠주는데 이렇게 해줌으로 가독성과 관리 또한 편리해진다.
![](https://images.velog.io/images/gunwooko/post/34f1518c-b3ae-4272-af80-4120be04c703/600px-Router-MVC-DB.svg.png)
여러 웹 프레인워크에서 다양한 MVC 컨셉을 사용하는데:

- Ruby on Rails (Ruby)
- Laravel (PHP)
  -Codeigniter (PHP)
- Django (Python)
- Flask (Python)
- Express (JS)
- Backbone (JS)
- Angular (JS)

## Model

데이터의 정보를 가지고 있다. 자신이 데이터를 가지고 있다던지 혹은 데이터베이스로부터 값을 가져올 수 있다. 즉, 데이터베이스와 관계를 가지고, Controller와 관계를 맺고서 데이터베이스의 값을 Controller로 전해준다.

## View

유저가 보는 화면을 보여주게 하는 역활을 담당한다(UI). Controller하고만 관계를 맺는다.

## Controller

일반적으로 View로 부터 액션과 이벤트에 관한 인풋값을 받는다. 그러면 받은 값을 모델에 넘겨주기 전에 가동할 수도 있다. 또한 모델로부터 다시 돌려받은 값을 가동해서 view로 보내준다.

## 참고

- [Traversy Media(youtube)](https://www.youtube.com/watch?v=pCvZtjoRq1I)
- [생활코딩](https://opentutorials.org/course/3883)
- Atom's Network
- [라우팅 모듈화를 통한 MVC 패턴 ](https://mygumi.tistory.com/105)
- [Node : MVC 패턴 뼈대 만들기](https://blog.naver.com/PostView.nhn?blogId=psj9102&logNo=221282415870&categoryNo=40&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=postView) -[What Is Wrong With Model-View-Controller](https://cocoacasts.com/what-is-wrong-with-model-view-controller)
