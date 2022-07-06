# subject-220706

### 更新前
![image](https://user-images.githubusercontent.com/1501327/177440360-33809ea0-8f2d-41df-9040-c5fd926423db.png)

### 入力
![image](https://user-images.githubusercontent.com/1501327/177440437-d828cb65-f0e1-4915-9ea1-8da3676185a0.png)

### 更新後表示
![image](https://user-images.githubusercontent.com/1501327/177440555-19515bca-58df-4fb4-be53-ae12286805e1.png)

![image](https://user-images.githubusercontent.com/1501327/177448043-f1cb6fb2-bc43-4887-a5e6-3fd5b245e8ab.png)

### 新規入力
![image](https://user-images.githubusercontent.com/1501327/177456257-dcd98d59-b183-4dfb-acc6-dc44f039ec3d.png)


### 商品マスタメンテ
- scode
- sname
- ztanka
- htanka
- stype
- skbn
- biko


```javascript
$(".form-control").each( function( index ){ console.log(this.name) })
```

![image](https://user-images.githubusercontent.com/1501327/177472638-b4647971-0e87-440c-8143-177e739ef7e9.png)


### 問い合わせ用 SQL
```SQL
select
    社員コード,
    氏名,
    フリガナ,
    所属,

    case 性別
        when 1 then '男'
        when 0 then '女'
    end as 性別,

    DATE_FORMAT(作成日,'%Y/%m/%d') as 作成日,
    DATE_FORMAT(更新日,'%Y/%m/%d') as 更新日,
    給与,
    手当,
    管理者,
    DATE_FORMAT(生年月日,'%Y/%m/%d') as 生年月日
from 社員マスタ
where 氏名 like :name
order by 社員コード
```

```sql
select 
    社員マスタ.社員コード,
    社員マスタ.氏名,
    社員マスタ.フリガナ,
    社員マスタ.所属,

    case 社員マスタ.性別
        when 1 then '男'
        when 0 then '女'
    end as 性別,

    DATE_FORMAT(社員マスタ.作成日,'%Y/%m/%d') as 作成日,
    DATE_FORMAT(社員マスタ.更新日,'%Y/%m/%d') as 更新日,
    社員マスタ.給与,
    社員マスタ.手当,
    社員マスタ.管理者,
    DATE_FORMAT(社員マスタ.生年月日,'%Y/%m/%d') as 生年月日
   ,コード名称マスタ.名称
 from 社員マスタ
 left outer join コード名称マスタ
 on  社員マスタ.所属 = コード名称マスタ.コード
 and 2 = コード名称マスタ.区分
where 社員マスタ.氏名 like :name
order by 社員マスタ.社員コード
```
