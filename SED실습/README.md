# 💡 sed 실습

날짜: 2024년 1월 12일
## 📝 예시 데이터
### 1. drinks.txt
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
### 2. engineering.txt
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

## 📝 문제
### 1. '프로틴'이라는 단어가 포함된 모든 라인 출력

```bash
$ sed -n '/프로틴/p' drinks.txt
```

```bash
|  1900 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
```

### 2. 아이스 아메리카노' 항목을 삭제

```bash
$ sed '/아이스 아메리카노/d' drinks.txt
```

```bash
Drink List
+-------+----+---------------------------+----------------------+
| price | id | name                      | img_link             |
+-------+----+---------------------------+----------------------+
|  2900 |  2 | 신타6 쉐이크              | images/shake.jpg     |
|  1900 |  3 | XTEND BCAA 자몽           | images/ade.png       |
|  1900 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
+-------+----+---------------------------+----------------------+
```

### 3. 모든 가격 앞에 '$' 기호 추가

```bash
$ sed '/|/s/\([0-9]\{1,\}\)/\$\1/' drinks.txt
```

```bash
Drink List
+-------+----+---------------------------+----------------------+
| price | id | name                      | img_link             |
+-------+----+---------------------------+----------------------+
|   $100 |  1 | 아이스 아메리카노         | images/americano.jpg |
|  $2900 |  2 | 신타6 쉐이크              | images/shake.jpg     |
|  $1900 
|  3 | XTEND BCAA 자몽           | images/ade.png       |
|  $1900 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
+-------+----+---------------------------+----------------------+
```

### 4. 테이블 헤더 제거

```bash
$ sed '1,3d' drinks.txt
```

```bash
+-------+----+---------------------------+----------------------+
|   100 |  1 | 아이스 아메리카노         | images/americano.jpg |
|  2900 |  2 | 신타6 쉐이크              | images/shake.jpg     |
|  1900 |  3 | XTEND BCAA 자몽           | images/ade.png       |
|  1900 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
+-------+----+---------------------------+----------------------+
```

### 5. Drink List에서 img_link의 링크를 image에서 resources로 바꾸기

```bash
$ vi cloud.txt
$ sed 's/images/resources/' cloud.txt
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

### 6. 모든 파일에서 | 를 느낌표로 바꾸기

```bash
$ sed -i 's/|/!/g' *.txt
$ cat cloud.txt
Drink List
+-------+----+---------------------------+----------------------+
! price ! id ! name                      ! img_link             !
+-------+----+---------------------------+----------------------+
!   100 !  1 ! 아이스 아메리카노         ! images/americano.jpg !
!  2900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
+-------+----+---------------------------+----------------------+

$ cat engineering.txt
Activist List
+-------------+-----------+----------+-------------+
! activist_id ! name      ! password ! major       !
+-------------+-----------+----------+-------------+
! giver1      ! 나의사    ! gp1      ! dermatology !
! giver2      ! 오드리    ! gp2      ! culture     !
! giver3      ! 키다리    ! gp3      ! mentor      !
+-------------+-----------+----------+-------------+
```

### 7. cloud.txt 파일에서 ‘신타’가 나오는 행과 ‘셀렉스’가 나오는 행 사이의 모든 행을 출력하기

```bash
$ sed -n '/신타/,/셀렉스/p' cloud.txt
!  2900 !  2 ! 신타6 쉐이크              ! images/shake.jpg     !
!  1900 !  3 ! XTEND BCAA 자몽           ! images/ade.png       !
!  1900 !  4 ! 셀렉스 프로틴             ! images/profit.jpg    !
```

### 8. 모든 파일에서 숫자 세자리수 이상은 세자리수마다 쉼표로 구분하기

```bash
$ sed -E ':L;s=\B[0-9]{3}\b=,&=;t L' *.txt
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
```

### 9. cloud.txt 파일에서 공백을 모두 제거 후 new_cloud.txt라는 새 파일에 저장하기

```bash
$ sed '/^ *$/d' cloud.txt > new_cloud.txt
$ ls
cloud.txt  engineering.txt  new_cloud.txt
$ cat new_cloud.txt
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

### 10. '셀렉스 프로틴'의 가격을 2000으로 변경
```
$ sed '/셀렉스 프로틴/s/1900/2000/' drinks.txt
```
```
Drink List
+-------+----+---------------------------+----------------------+
| price | id | name                      | img_link             |
+-------+----+---------------------------+----------------------+
|   100 |  1 | 아이스 아메리카노         | images/americano.jpg |
|  2900 |  2 | 신타6 쉐이크              | images/shake.jpg     |
|  1900 |  3 | XTEND BCAA 자몽           | images/ade.png       |
|  2000 |  4 | 셀렉스 프로틴             | images/profit.jpg    |
+-------+----+---------------------------+----------------------+
```
