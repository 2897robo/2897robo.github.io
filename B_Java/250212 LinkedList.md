### **📌 LinkedList in Java**
![Java Collection Framework](https://camo.githubusercontent.com/e9e790e3b06de82cd73140fe794d59a4c2c8ba461830853b019fb60074f53f86/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f6d6a5646412f6274715a426350437435652f6977746355614f634942455169435258497671456a4b2f696d672e6a7067)

---

## **1️⃣ LinkedList란?**
`LinkedList`는 **이중 연결 리스트(Doubly Linked List)**로 구현된 `List` 인터페이스의 한 구현체이다.  
데이터가 **노드(Node) 단위로 저장**되며, 각 노드는 **이전 노드와 다음 노드를 가리키는 참조(포인터)**를 가진다.

---

## **2️⃣ LinkedList의 구조**
- **각 요소(Node)는 다음과 같은 구조를 가짐**
  ```
  [prev | data | next]
  ```
    - `prev`: 이전 노드를 가리키는 참조
    - `data`: 실제 저장된 데이터
    - `next`: 다음 노드를 가리키는 참조

---

## **3️⃣ LinkedList의 주요 특징**
| 특징 | 설명 |
|------|------|
| **연결 리스트 구조** | 내부적으로 **이중 연결 리스트(Doubly Linked List)**로 구현됨 |
| **O(1) 삽입/삭제** | 리스트의 **중간에서 요소 추가/삭제**가 빠름 |
| **O(n) 접근 속도** | 인덱스로 접근하려면 **처음부터 순차 탐색**해야 하므로 `ArrayList`보다 느림 |
| **순차적 접근에 최적화** | `Iterator`나 `for-each` 루프를 사용할 때 효율적 |
| **메모리 오버헤드** | 각 요소가 **이전/다음 노드 참조(포인터)를 추가로 저장**해야 하므로 메모리를 더 많이 사용 |

---

## **4️⃣ LinkedList vs ArrayList 비교**
| 비교 항목 | **LinkedList** | **ArrayList** |
|----------|--------------|--------------|
| **내부 구조** | 이중 연결 리스트 | 동적 배열 |
| **삽입/삭제 속도** | **O(1)** (중간 삽입/삭제가 빠름) | **O(n)** (중간 삽입/삭제가 느림) |
| **조회 속도** | **O(n)** (순차 탐색) | **O(1)** (인덱스로 직접 접근 가능) |
| **메모리 사용량** | 추가적인 포인터 저장 필요 (더 큼) | 포인터 저장 필요 없음 (더 적음) |
| **적합한 경우** | **빈번한 삽입/삭제가 필요할 때** | **랜덤 접근이 많을 때** |

---

## **5️⃣ LinkedList 사용법**
### **(1) 기본적인 사용**
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // LinkedList 생성
        LinkedList<String> list = new LinkedList<>();

        // 요소 추가 (add)
        list.add("A");
        list.add("B");
        list.add("C");

        System.out.println(list); // [A, B, C]

        // 특정 위치에 요소 삽입 (add(index, element))
        list.add(1, "X");
        System.out.println(list); // [A, X, B, C]

        // 요소 제거 (remove)
        list.remove("X");
        System.out.println(list); // [A, B, C]

        // 첫 번째 요소 접근 (getFirst)
        System.out.println(list.getFirst()); // A

        // 마지막 요소 접근 (getLast)
        System.out.println(list.getLast()); // C
    }
}
```

---

### **(2) `Deque`(양방향 큐)로 사용하기**
- `LinkedList`는 `Deque` 인터페이스를 구현하고 있어서 **스택(Stack)이나 큐(Queue)로 사용 가능**하다.

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> queue = new LinkedList<>();

        // 큐 (Queue) 기능 활용
        queue.offer(1);  // enqueue (addLast와 동일)
        queue.offer(2);
        queue.offer(3);

        System.out.println(queue); // [1, 2, 3]

        System.out.println(queue.poll()); // 1 (dequeue)
        System.out.println(queue); // [2, 3]

        // 스택 (Stack) 기능 활용
        queue.push(10);  // push (addFirst와 동일)
        System.out.println(queue); // [10, 2, 3]

        System.out.println(queue.pop()); // 10 (pop)
        System.out.println(queue); // [2, 3]
    }
}
```

---

## **6️⃣ LinkedList의 시간 복잡도**
| 연산 | **시간 복잡도** | 설명 |
|------|--------------|------|
| **삽입 (add, addFirst, addLast)** | **O(1)** | 링크 조정만 수행하므로 빠름 |
| **삭제 (remove, removeFirst, removeLast)** | **O(1)** | 노드를 찾아서 링크 변경 |
| **조회 (get, indexOf, contains)** | **O(n)** | 첫 번째 노드부터 순차 탐색 |
| **정렬 (sort)** | **O(n log n)** | 병합 정렬(TimSort) 사용 |

---

## **7️⃣ LinkedList가 적합한 경우**
✅ **삽입과 삭제가 자주 발생하는 경우**  
✅ **Queue(큐) 또는 Stack(스택)처럼 사용할 때**  
✅ **리스트의 크기가 자주 변경될 때**

---

## **8️⃣ LinkedList가 부적합한 경우**
❌ **인덱스를 자주 조회해야 하는 경우 (`get(index)`)**  
❌ **메모리 사용이 중요한 경우 (포인터 추가 저장 필요)**  
❌ **정렬이 빈번히 발생하는 경우 (느림)**

---

## **📌 결론**
- `LinkedList`는 **이중 연결 리스트**를 기반으로 구현되어 있음.
- **삽입/삭제는 빠르지만 (`O(1)`) 조회는 느림 (`O(n)`)**.
- **Queue/Stack처럼 사용할 때 유용**하지만, **랜덤 접근이 많은 경우 `ArrayList`가 더 적합**.