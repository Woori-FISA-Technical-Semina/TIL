# sed 실습

날짜: 2024년 1월 12일

![Untitled](sed%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%20b8886f9e6e4f48cc8ee00ea737796d73/Untitled.png)

```bash
Drink List
+-------+----+---------------------------+----------------------+
| price | id | name                      | img_link             |
+-------+----+---------------------------+----------------------+
|   100 |  1 | 아이스 아메리카노         | images/americano.jpg |
|  2900 |  2 | 신타6 쉐이크              | images/shake.jpg     |
|  1900 |  3 | XTEND BCAA 자몽           | images/ade.png       |
|  1900 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
+-------+----+---------------------------+----------------------+
```

![Untitled](sed%20%E1%84%89%E1%85%B5%E1%86%AF%E1%84%89%E1%85%B3%E1%86%B8%20b8886f9e6e4f48cc8ee00ea737796d73/Untitled%201.png)

```bash
Activist List
+-------------+-----------+----------+-------------+
| activist_id | name      | password | major       |
+-------------+-----------+----------+-------------+
| giver1      | 나의사    | gp1      | dermatology |
| giver2      | 오드리    | gp2      | culture     |
| giver3      | 키다리    | gp3      | mentor      |
+-------------+-----------+----------+-------------+
```

1. Drink List에서 img_link의 링크를 image에서 resources로 바꾸세요.

```bash
username@servername:~/sedtest$ vi cloud.txt
username@servername:~/sedtest$ sed 's/images/resources/' cloud.txt
Drink List
+-------+----+---------------------------+----------------------+
| price | id | name                      | img_link             |
+-------+----+---------------------------+----------------------+
|   100 |  1 | 아이스 아메리카노         | resources/americano.jpg |
|  2900 |  2 | 신타6 쉐이크              | resources/shake.jpg     |
|  1900 |  3 | XTEND BCAA 자몽           | resources/ade.png       |
|  1900 |  4 | 셀렉스 프로틴             | resources/profit.jpg    |
+-------+----+---------------------------+----------------------+
```

1. 모든 파일에서 | 를 느낌표로 바꾸세요.

```bash
username@servername:~/sedtest$ sed -i 's/|/!/g' *.txt
username@servername:~/sedtest$ cat cloud.txt
Drink List
+-------+----+---------------------------+----------------------+
! price ! id ! name                      ! img_link             !
+-------+----+---------------------------+----------------------+
!   100 !  1 ! 아이스 아메리카노         ! images/americano.jpg !
!  2900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
+-------+----+---------------------------+----------------------+

username@servername:~/sedtest$ cat engineering.txt
Activist List
+-------------+-----------+----------+-------------+
! activist_id ! name      ! password ! major       !
+-------------+-----------+----------+-------------+
! giver1      ! 나의사    ! gp1      ! dermatology !
! giver2      ! 오드리    ! gp2      ! culture     !
! giver3      ! 키다리    ! gp3      ! mentor      !
+-------------+-----------+----------+-------------+
username@servername:~/sedtest$
```

1. cloud.txt 파일에서 ‘신타’가 나오는 행과 ‘셀렉스’가 나오는 행 사이의 모든 행을 출력하세요.

```bash
username@servername:~/sedtest$ sed -n '/신타/,/셀렉스/p' cloud.txt
!  2900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
```

1. 모든 파일에서 숫자 세자리수 이상은 세자리수마다 쉼표로 구분하세요.

```bash
username@servername:~/sedtest$ sed -E ':L;s=\B[0-9]{3}\b=,&=;t L' *.txt
Drink List
+-------+----+---------------------------+----------------------+
! price ! id ! name                      ! img_link             !
+-------+----+---------------------------+----------------------+
!   100 !  1 ! 아이스 아메리카노         ! images/americano.jpg !
!  2,900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1,900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1,900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
+-------+----+---------------------------+----------------------+
Activist List
+-------------+-----------+----------+-------------+
! activist_id ! name      ! password ! major       !
+-------------+-----------+----------+-------------+
! giver1      ! 나의사    ! gp1      ! dermatology !
! giver2      ! 오드리    ! gp2      ! culture     !
! giver3      ! 키다리    ! gp3      ! mentor      !
+-------------+-----------+----------+-------------+
username@servername:~/sedtest$
```

1. cloud.txt 파일에서 공백을 모두 제거 후 new_cloud.txt라는 새 파일에 저장하세요.

```bash
username@servername:~/sedtest$ sed '/^ *$/d' cloud.txt > new_cloud.txt
username@servername:~/sedtest$ ls
cloud.txt  engineering.txt  new_cloud.txt
username@servername:~/sedtest$ cat new_cloud.txt
Drink List
+-------+----+---------------------------+----------------------+
! price ! id ! name                      ! img_link             !
+-------+----+---------------------------+----------------------+
!   100 !  1 ! 아이스 아메리카노         ! images/americano.jpg !
!  2900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
+-------+----+---------------------------+----------------------+
```
