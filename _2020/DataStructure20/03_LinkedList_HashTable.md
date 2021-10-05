# Linked List (연결 리스트)

연결 리스트는 노드(node)라는 요소들의 연결로 이뤄진 자료 구조인다.(혹은 vertex 라고도 불린다.) 배열과는 다르게 노드는 노드와(data) 다음 노드를 가리키는 포인터로(pointer to next node) 이뤄져있다. 그리고 마지막 노드가 가리키는 값은 `null`이다. `head` property가 있는데 `head`는 항상 첫 번째 노드를 가리킨다(연결의 시작). `tail`은 항상 마지막 노드를 가리킨다. 연결리스트의 장점은 데이터를 추가하고 삭제하는데 있어서 O(1) constante time의 시간 복잡도를 가진다. 다만, 연결 리스트의 각 노드는 인덱스를 갖지 않아, 어떤 특정 데이터를 연결 리스트에서 찾고자 할 경우, 처음부터 전체 연결 리스트를 훓어야 하며,이는 O(n)의 linear time의 시간 복잡도를 필요로 한다. 또한, 연결 메모리 공간을 낭비하지 않고, 프로그램이 수행되는 동안 크기가 커지거나 작아질 수 있다.

## Single Linked List

![](https://images.velog.io/images/gunwooko/post/0a84691f-f184-4fef-b31f-f46e845ddf12/43154574-2615-11e3-8e29-43cf74e25b10.png)

## Double Linked List (이중 연결 리스트)

연결 리스트에서 특정 노드를 검색하기 위해서는 앞에서부터 탐색할 수 밖에 없는데, 포인터가 바로 다음 노드의 정보만을 가지고 있기 때문이다. 이와 같은 문제를 보안한 것이 한 방향이 아닌 양 방향을 모두 가리키는 Double Linked List다. 여기서 한가지 추가된 것은 `prev` property가 추가되서 이전 노드를 가리킨다.
![](https://images.velog.io/images/gunwooko/post/90e693c0-6a1e-462a-87c0-32f9f5c1b47c/doubly_linked_list_1.png)

## 참고 - Linked List

- [연결 리스트 관련 블로그 1](https://medium.com/journey-of-one-thousand-apps/data-structures-in-the-real-world-508f5968545a)
- [연결 리스트 관련 블로그 2](https://codeburst.io/linked-lists-in-javascript-es6-code-part-1-6dd349c3dcc3)
- [연결 리스트 관련 블로그 3](https://boycoding.tistory.com/33)
- [연결 리스트 관련 블로그 4](https://velog.io/@760kry/JS-Linked-List-vs-Array-List-data-structor#deletion--o1-%EC%82%AD%EC%A0%9C)
- [연결 리스트 관련 블로그 5](https://im-developer.tistory.com/125)
- [연결 리스트 관련 블로그 6](https://medium.com/@lyhlg0201/immersive-sprint-js-linkedlist-4edcb5928a9e)
- [이중 연결 리스트 관련 블로그 1](https://boycoding.tistory.com/34)
- [생활코딩 - Linked List](https://opentutorials.org/module/1335/8821)

# Hash Table

해시 테이블은 키-값 쌍을 저장하는 자료 구조인데, 특이한 점은 값을 해시 함수에 통과 시켜 나온 인덱스에 저장한다. 해시 코드를 만드는 것을 해싱이라 부르는데 이것은 암호화하는 것과 같다. 어떤 특정 값을 해시 함수에 통과시키면 나오는 결과 값은 항상 같아야 하고, 나온 인덱스 값으로는 해싱 전에 어떤 값이었는지 알 수 없다. 한 가지 주의할 점은 키값이 달라도 해시 함수에 의해 나온 인덱스 값이 같을 수 있다. 이것을 해시 충돌(hash collision)이라고 부른다. 이런 충돌이 일어날 수 있음에도 사용하는 이유는 적은 리소스로 많은 데이터를 효율적으로 관리할 수 있기 때문이다. 해시테이블의 장점은 탐색하고, 값을 삽입하고, 삭제하는 것이 빠르다.
![](https://images.velog.io/images/gunwooko/post/a86e1acc-64b1-437a-839f-e4a4b6764cd6/236B1A4C56B4DE1F12.png)
해시 테이블에서 해시 충돌을 해결하는 방법은 여러 가지가 있다.

- Separate chaining: 충돌이 일어나면 linked list를 이용해 노드를 추가하여 값을 추가한다. 또한, tree 구조를 사용하기도 한다.
- Open Addressing: 여기서도 여러 방법이 있지만, linear probing 방식은 충돌이 일어나면 인덱스 뒤에 있는 버킷 중 빈 곳을 찾아 데이터를 저장하는 방식이다.

보통 해시 테이블이 잘 실행되려면 값이 저장되는 tuple(데이터 키-값쌍)의 스토리지 길이가 25%-75%로 유지해주는 것이 좋다. 사이즈가 넘어가면 두 배로 다시 리사이징을 해주어야 한다. 리사이징 후 저장되어 있던 값을 전부 다시 해싱해줘야 한다. 또한 아무래도 해시 충돌을 최소한 하려면, 잘 짜인 해시 함수를 사용해야 한다.
![](https://images.velog.io/images/gunwooko/post/550fc0d4-9d81-4549-a64e-bcc2bcc815d9/IMG-7175.jpg)

## 참고 - Hash Table

- [해시테이블 관련 블로그 1](https://medium.com/javascript-in-plain-english/algorithm-in-javascript-hash-table-7b0464d2b81b)
- [해시테이블 관련 블로그 2](https://jeongw00.tistory.com/168)
- [해시테이블 관련 블로그 3](https://evan-moon.github.io/2019/06/25/hashtable-with-js/)
- [해시테이블 관련 블로그 4](https://velog.io/@riceintheramen/hash-Table#%ED%95%B4%EC%8B%9C-%EC%B6%A9%EB%8F%8C%EC%9D%84-%EB%8F%8C%ED%8C%8C%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)
- [해시테이블 관련 블로그 5](https://bcho.tistory.com/1072)
- [해시테이블 관련 블로그 6](https://velog.io/@760kry/JS-hash-table-javascript-hash-table-%EA%B5%AC%ED%98%84-45k5i3f0gw)
- [해시테이블 관련 블로그 7](https://soldonii.tistory.com/72?category=862199)
- [해시테이블 관련 블로그 8](https://medium.com/@songjaeyoung92/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-javascript-hash-table-%EC%9D%B4%EB%9E%80-5f5345623dab)
- [해시테이블 관련 영상](https://www.youtube.com/watch?v=Vi0hauJemxA&feature=youtu.be)
