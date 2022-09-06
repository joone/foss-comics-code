hello_v1과  hello_v2 디렉토리에는 같은 hello.c라는 파일이 있지만, hello_v2에는 변경한 코드가 있습니다.

```  
~/foss-comics-code/47.git/diff$ cat hello_v1/hello.c 
```

```c
/* gcc hello.c -o hello */
  
#include <stdio.h>
  
int main() {

    printf("Hello World");
  
    return 0;
}
```

```
~/foss-comics-code/47.git/diff$ cat hello_v2/hello.c 
```

```c
/* gcc hello.c -o hello */
  
#include <stdio.h>
  
int main() {

    printf("Hello World %s\n");
  
    return 0;
}
```

두 hello.c파일을 비교할 때, diff라는 툴을 사용합니다.
```
~/foss-comics-code/47.git$ diff hello_v1 hello_v2
diff hello_v1/hello.c hello_v2/hello.c
7c7
<     printf("Hello World");
---
>     printf("Hello World %s\n");
```

위와 같이 두 파일을 차이를 쉽게 볼 수 있습니다. 자, 이제 이를 파일로 만들어서 hello.c를 만든 사람에 전달해봅시다.
```
~/my-git/foss-comics-code/47.git/diff$ diff -u hello_v1 hello_v2 > diff.patch
~/my-git/foss-comics-code/47.git/diff$ cat diff.patch 
diff -u hello_v1/hello.c hello_v2/hello.c
--- hello_v1/hello.c	2022-09-05 17:25:53.992894733 -0700
+++ hello_v2/hello.c	2022-09-05 17:27:51.091147715 -0700
@@ -4,7 +4,7 @@
   
 int main() {
 
-    printf("Hello World");
+    printf("Hello World %s\n");
   
     return 0;
 }
```

Diff.patch라는 파일이 만들어졌습니다. 이제 이를 hello_v1/hello.c에 적용해봅니다.

```
~/my-git/foss-comics-code/47.git/diff$ patch -d hello_v1/ -p1 < diff.patch 
patching file hello.c
```

이렇게 하면 hello_v1/hello.c와 hello_v2/hello.c이 같아야 합니다. 확인해보겠습니다.

```
joone@cube:~/my-git/foss-comics-code/47.git/diff$ diff -u hello_v1 hello_v2
joone@cube:~/my-git/foss-comics-code/47.git/diff$ 
```

Diff명령어 결과가 없는 것으로 보아 두 파일이 같다는 것을 알 수 있습니다.


