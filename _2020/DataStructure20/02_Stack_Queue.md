# Stack

스택 자료 구조는 마지막으로 들어간 item이 첫 번째로 나오는 item이 된다는 특징을 가지고 있다 (Last In Out First - LIFO).
스택은 가장 마지막에 쌓인 요소가 먼저 나오는 원리로 undo나 브라우저의 뒤로 가기와 같은 동작을 구현할 때 사용된다. 또한 서로 관계가 있는 여러 작업을 연달아 수행하면서 이전의 작업 내용을 저장해둘 필요가 있을 때 많이 사용된다. (ex. 포토샵 등)
스택 자료 구조가 실현되려면, 무엇이든 담아둘 수 있는 저장소(storage)가 필요하다. (배열 혹은 객체). 스택에서 가장 마지막에 쌓이 요소, 즉 가장 위에 위치하는 요소의 위치를 top이라고 표현한다.
구현할 수 있는 메소드로는

- 데이터를 추가하는 push(element)
- 데이터를 추출하는 pop()
- 마지막에 넣은 데이터를 확인하는 peek()
- 현재 스텍의 사이즈를 리턴하는 size()
- 스택이 비어 있는지 아닌지의 여부를 리턴하는 empty()
- 스택의 가장 top에 위치하는 데이터를 반환하는 top()
  ![](https://images.velog.io/images/gunwooko/post/954639eb-6b57-4827-90c1-0a328e949751/200px-Data_stack.svg.png)

# Queue

큐 자료구조는 첫 번째로 들어간 item이 첫 번째로 나오는 특징을 가지고 있다 (First In First Out - FIFO).
큐는 마치 놀이공원에 줄과 같이 작동하는데, 차례로 줄을 서고 맨 앞에서부터 놀이기구에 탑승하는 것과 같다.
구현할 수 있는 메소드로는

- 데이터를 추가하는 enqueue(element)
- 데이터를 삭제하는 dequeue()
- 큐의 현재 요소 개수를 리턴하는 size()
- 가장 처음에 있는 요소를 리턴하는 front()
- 데이터가 있는지 없는지를 리턴하는 isEmpty()
- 모든 값을 문자열로 concatenate되서 리턴하는 printQueue()

enqueue한 값, 즉 맨 뒤에 해당하는 요소를 rare라고 하고, 맨 앞의 값 즉, dequeue의 대상이 되는 요소를 front라고 한다.
![](https://images.velog.io/images/gunwooko/post/f7648698-d414-4566-a944-d0897c244cbe/200px-Data_Queue.svg.png)

## Priority Queue (우선순위 큐)

우선순위 큐는 마치 응급실과 같다. 환자가 여럿이 차례로 들어갔지만, 우선순위에(환자의 응급 순위에 따라) 따라 나온다.

# 참고

- [스택 관련 블로그1](https://medium.com/@nicolaisafai/what-are-stacks-useful-for-79668042e12b)
- [스택 관련 블로그2](https://initjs.org/data-structure-stack-in-javascript-714f45dbf889)
- [스택 관련 사이트1](https://www.oreilly.com/library/view/data-structures-and/9781449373931/ch04.html)
- [스택-큐 관련 블로그1](https://medium.com/@lyhlg0201/immersive-sprint-js-stack-queue-426ccfbdb602)
- [스택-큐 관련 블로그2](https://medium.com/@_jmoller/javascript-data-structures-stacks-and-queues-ea877d72a5f9)
- [스택-큐 관련 블로그3](https://velog.io/@ryu/JavaScript-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Stack-%EC%8A%A4%ED%83%9D)
- [스택-큐 관련 블로그4](https://velog.io/@nayeon/Data-Structure-Stack-Queue-in-JS)
- [스택-큐 관련 블로그5](https://helloworldjavascript.net/pages/282-data-structures.html)
- [큐 관련 블로그1](http://mythinkg.blogspot.com/2015/04/data-structure-javascript-queue.html)
- [큐 관련 블로그2](https://www.javascripttutorial.net/javascript-queue/)
- [큐 관련 블로그3](https://medium.com/@gwakhyoeun/data-structure-queue-javascript-e43719e3615f)
- [큐 관련 블로그4](https://hackernoon.com/the-little-guide-of-queue-in-javascript-4f67e79260d9)
- [우선순위 큐 관련1](https://www.geeksforgeeks.org/implementation-priority-queue-javascript/)
