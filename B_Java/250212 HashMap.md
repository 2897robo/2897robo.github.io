# HashMap<K, V> 개념과 사용법

![Java Collections Framework](https://camo.githubusercontent.com/e9e790e3b06de82cd73140fe794d59a4c2c8ba461830853b019fb60074f53f86/68747470733a2f2f626c6f672e6b616b616f63646e2e6e65742f646e2f6d6a5646412f6274715a426350437435652f6977746355614f634942455169435258497671456a4b2f696d672e6a7067)

👉 `HashMap<K, V>`는 **Key-Value(키-값) 쌍**을 저장하는 자료구조로, **빠른 검색과 저장이 가능**한 Map 인터페이스의 대표적인 구현체다.

---

## **1️⃣ HashMap 개요**
✅ **Key를 기준으로 Value를 저장하는 자료구조**  
✅ **Key는 중복될 수 없으며, Value는 중복 가능**  
✅ 내부적으로 **해시 테이블(Hash Table)**을 사용하여 **빠른 검색과 삽입이 가능**  
✅ **Null 값 허용**
- Key는 **1개만 null 허용**
- Value는 **여러 개 null 허용**

---

## **2️⃣ HashMap 주요 특징**
| 특징 | 설명 |
|---|---|
| **빠른 검색 속도** | 평균적으로 `O(1)`에 조회 가능 (최악 `O(n)`) |
| **Key-Value 저장** | Key를 기준으로 데이터 저장 및 조회 |
| **순서 보장 X** | 데이터가 입력된 순서를 보장하지 않음 |
| **동기화 X** | 멀티쓰레드 환경에서 `ConcurrentHashMap`을 사용하는 것이 안전 |

---

## **3️⃣ HashMap 선언과 사용 예시**
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ HashMap 선언
        HashMap<String, Integer> map = new HashMap<>();

        // 2️⃣ 값 추가 (put)
        map.put("사과", 3);
        map.put("바나나", 5);
        map.put("오렌지", 2);
        
        // 3️⃣ 값 조회 (get)
        System.out.println("사과 개수: " + map.get("사과")); // 출력: 3
        
        // 4️⃣ Key 존재 여부 확인 (containsKey)
        System.out.println("키 '바나나' 존재 여부: " + map.containsKey("바나나")); // true

        // 5️⃣ Value 존재 여부 확인 (containsValue)
        System.out.println("값 5 존재 여부: " + map.containsValue(5)); // true

        // 6️⃣ Key-Value 삭제 (remove)
        map.remove("오렌지");
        System.out.println("오렌지 삭제 후: " + map);

        // 7️⃣ 전체 Key 확인 (keySet)
        System.out.println("Key 목록: " + map.keySet());

        // 8️⃣ 전체 Value 확인 (values)
        System.out.println("Value 목록: " + map.values());

        // 9️⃣ 전체 Key-Value 출력 (entrySet)
        for (var entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```

---

## **4️⃣ HashMap의 내부 동작 원리**
### **🔹 1. 해싱(Hashing)**
✅ `HashMap`은 **해시 함수를 이용하여 Key를 해시값(정수)으로 변환**  
✅ 해시값을 기반으로 **배열의 특정 위치에 데이터를 저장**  
✅ **해시 충돌(같은 해시값이 나오는 경우)** 발생 시 **LinkedList or Tree 구조로 처리**

### **🔹 2. 저장 과정**
1. **Key의 `hashCode()` 값을 이용하여 해시값 계산**
2. **배열의 적절한 위치(Bucket Index)에 저장**
3. **동일한 해시값을 가진 Key가 있다면 LinkedList로 연결**
4. **Java 8부터는 충돌이 많아지면 Tree 형태(레드-블랙 트리)로 변환**

```java
// Key의 해시값 계산 예시
String key = "사과";
int hash = key.hashCode(); // 해시값 계산
int index = hash % 배열크기; // 저장될 인덱스 계산
```

---

## **5️⃣ HashMap 주요 메서드 정리**
| 메서드 | 설명 |
|---|---|
| `put(K key, V value)` | Key-Value 추가 |
| `get(K key)` | Key에 해당하는 Value 반환 |
| `remove(K key)` | Key에 해당하는 값 삭제 |
| `containsKey(K key)` | Key 존재 여부 확인 |
| `containsValue(V value)` | Value 존재 여부 확인 |
| `size()` | 저장된 요소 개수 반환 |
| `keySet()` | 모든 Key 반환 |
| `values()` | 모든 Value 반환 |
| `entrySet()` | Key-Value 쌍을 `Set`으로 반환 |

---

## **6️⃣ HashMap vs LinkedHashMap vs TreeMap**
| 자료구조 | 검색 속도 | 저장 순서 유지 | 정렬 |
|---|---|---|---|
| **HashMap** | `O(1)` | ❌ | ❌ |
| **LinkedHashMap** | `O(1)` | ✅ (입력 순서 유지) | ❌ |
| **TreeMap** | `O(log n)` | ✅ (정렬 순서 유지) | ✅ (Key 기준 정렬) |

---

## **7️⃣ HashMap의 장점과 단점**
### **✅ 장점**
✔ **빠른 조회** (`O(1)`)  
✔ **Key 기반 데이터 저장 및 관리**  
✔ **넉넉한 용량을 미리 설정하면 성능 최적화 가능**

### **❌ 단점**
❌ **순서 보장 안됨**  
❌ **멀티스레드 환경에서 안전하지 않음** (`ConcurrentHashMap` 사용 필요)  
❌ **메모리 사용량이 많음** (LinkedList or Tree 사용으로 인한 오버헤드)

---

## **🔥 결론**
✅ `HashMap<K, V>`는 Key-Value 저장을 위한 **빠른 검색용 자료구조**  
✅ 내부적으로 **해시 테이블을 사용하여 평균 O(1)의 조회 속도** 제공  
✅ 하지만 **순서가 중요할 경우 `LinkedHashMap`, 정렬이 필요하면 `TreeMap`을 고려**  
✅ **멀티스레드 환경에서는 `ConcurrentHashMap`을 사용할 것!**

---
