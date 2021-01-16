## 이진탐색

### 정의
- 탐색 알고리즘 종류 중 하나.
- 탐색 범위를 절반씩 나눠가면서 찾고자 하는 데이터를 탐색해나가는 알고리즘.
- 이미 정렬돼있는 자료구조에서 탐색해야 한다.

### 시간 복잡도
- 순차탐색: O(N)
- 이분탐색  O(logN)

### 구현
1. 정렬
2. 양끝점을 left, right으로 지정하고 mid를 찾는다.
3. 찾는 값과 mid를 비교한다.
4. 비교 결과,
- mid < target 이라면 left = mid + 1로 대입한 후 다시 탐색
- mid > target이라면 right = mid -1로 대입한 후 다시 탐색
- mid = target이라면 종료
- right <= left가 되면 없는 것이므로 종료.


### 구현 코드
```java
package Study;

import java.util.Arrays;

/**
 * created by victory_woo on 2020/04/30
 */
public class BinarySearch {
    public static void main(String[] args) {
        int[] arr = {2, 13, 6, 5, 12, 15, 23, 17, 19, 10,};
        System.out.println(solution(17, arr));
    }

    private static int solution(int target, int[] arr) {
        Arrays.sort(arr);
        int left = 0, right = arr.length - 1, mid = 0;

        while (left < right) {
            mid = (left + right) / 2;

            if (target == arr[mid]) {
                System.out.println("Find Target : " + target + ", Value : " + arr[mid]);
                return arr[mid];
            }

            if (target < arr[mid]) right = mid - 1;
            else left = mid + 1;
        }

        return -1;
    }
}
```
## Reference
- 