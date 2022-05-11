```java
class Solution {
    static int dy[] = {1, 0, -1};
    static int dx[] = {0, 1, -1};
    static int arr[][] = new int[1001][10001];
    static int endKey = -1;
    static int N = -1;

    public static void goNumber(int n, int nowY, int nowX, int number) {

        for(int i=0; i<n; i++) {
            if(arr[nowY][nowX] != 0 || endKey < number || nowY > N) {
                return;
            }
            arr[nowY++][nowX] = number++;
        }
        nowY--;
        for(int i=1; i<n; i++) {
            if(arr[nowY][nowX+1] != 0 || endKey < number|| nowX+1 > N) {
                return;
            }
            arr[nowY][++nowX] = number++;
        }

        while(nowY>0 && nowX >0 && arr[nowY-1][nowX-1] == 0) {
            arr[--nowY][--nowX] = number++;
        }

        if(endKey < number) {
            return;
        } else {
            goNumber(n-3, nowY+1, nowX, number);
        }

    }

    public int[] solution(int n) {
        init(n);
        N = n;
        endKey = 0;
        for(int i=1; i<=n; i++) {
            endKey += i;
        }
        int[] answer = new int[endKey];
        goNumber(n, 1, 1, 1);
        int index = 0;
        for(int i=1; i<=n; i++) {
            for(int j=1; j<=i; j++) {
                answer[index++] = arr[i][j];
            }
        }
        return answer;
    }
    static public void init(int n) {
        for(int i=0; i<=n; i++) {
            for(int j=0; j<=n; j++) {
                arr[i][j] = 0;
            }
        }
    }
}
```
