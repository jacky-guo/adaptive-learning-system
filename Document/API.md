+ [帳號](#帳號)
    + [登入](#登入)
    + [註冊](#註冊)
+ [單字](#單字)
    + [新增單字](#新增單字)
    + [刪除單字](#刪除單字)
    + [單字查詢](#單字查詢)
+ [教材](#教材)
+ [考卷](#考卷)

返回代碼: 0

## 帳號

### 登入

**URL**

```
POST /elearning/auth/login
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| username | String | 用戶帳號 | :x: |
| password | String | 用戶密碼 | :x: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| userId | String | 用戶ID |
| userAccount | String | 用戶帳號 |
| userName | String | 用戶姓名 |
| userEmail | String | 郵箱 |
| userGrade | String | 年級碼 [細節](#) |
| userSchool | String | 學校 |
| userRank | Int | 排名 |
| userLevel | Int | 程度 |
| userIdentity | Tinyint | 身份碼 [細節](#) |
| lastloginTime | Timestamp | 最後登入時間 |

**示例**

請求

```
username: "admin"
password: "admin"
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": [
        {
            "userId": "123456",
            "userAccount": "admin",
            "userName": "管理员",
            "userEmail": "xxx@email.com",
            "userGrade": "6",
            "userSchool": "ntu",
            "userRank": "1",
            "userLevel": 600,
            "userIdentity": 0,
            "lastloginTime": 1509617737000
        }]
}
```

響應(錯誤)

```
{
    "code": 401,
    "msg": "賬號或密碼不正確",
    "data" null
}
```

### 註冊

**URL**

```
POST /elearning/auth/register
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| username | String | 用戶帳號 | :x: |
| password | String | 用戶密碼 | :x: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| userId | String | 用戶ID |
| userAccount | String | 用戶帳號 |
| userName | String | 用戶姓名 |
| userEmail | String | 郵箱 |
| userGrade | String | 年級碼 [細節](#) |
| userSchool | String | 學校 |
| userRank | Int | 排名 |
| userLevel | Int | 程度 |
| userIdentity | Tinyint | 身份碼 [細節](#) |
| lastloginTime | Timestamp | 最後登入時間 |

**示例**

請求

```
username: "admin"
password: "admin"
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "userId": "1510633838654296565",
        "userAccount": "teacher01",
        "userName": null,
        "userEmail": null,
        "userGrade": null,
        "userSchool": null,
        "userRank": null,
        "userLevel": 600,
        "userIdentity": 1,
        "lastloginTime": null
    }
}
```

響應(錯誤)

```
{
    "code": 400,
    "msg": "帳號/密碼必填",
    "data": null
}

```

響應(錯誤)

```
{
    "code": 403,
    "msg": "賬號已被註冊",
    "data" null
}
```

## 單字

### 新增單字

**URL**
```
POST /elearning/word/insert
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| wordContent | String | 單字內容(需小於128字元) | :x: |
| wordGrade | String | 單字所屬年級 | :x: | 
| wordPartofspeech | String | 單字詞性 | :x: |
| wordLevel | Int | 單字難易度 | :o: |
| wordInterpretation | String | 單字解釋 | :o: |
| createBy | String | 創建帳號 | :o: |
| updateBy | String | 修改帳號 | :o: |
| wordSource | String | 單字來源(尚未定義) | :o: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| wordId | Int | 單字ID |

**示例**

請求

```
wordId: 10943
wordLevel: 300
wordContent: "apple"
wordPartofspeech: "noun"
wordInterpretation: "苹果"
wordGrade: "3"
createBy: "admin"
updateBy: "admin"
wordSource: "第一单元"
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": 10947
}
```

響應(錯誤)

```
{
    "code": 400,
    "msg": "年級必填",
    "data": null
}
```

### 刪除單字

**URL**
```
Delete /elearning/word/delete
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| wordId | Int | 需要刪除的單字的ID | :x: |

**響應参数**

無

**示例**

請求

```
wordId: 1
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

響應(錯誤)

```
{
    "code": 403,
    "msg": "刪除內容不存在",
    "data": null
}
```

### 單字查詢

#### 相似搜尋

**URL**
```
Get /elearning/word/query
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| wordContent | String | 欲查詢的單字或以此開頭的單字 | :x: |
| page | Int | 頁數(default為0) | :o: |
| size | Int | 每頁顯示數量(default為20) | :o: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| wordList | List<Word> | 單字列表[單字細節](#) |
| count | Int | 符合條件的單字個數 |

**示例**

請求

```
wordContent: "like"
page: 0
size: 20
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "wordList": [
            {
                "wordId": 1,
                "wordLevel": 326,
                "wordLength": 4,
                "wordContent": "like",
                "wordPartofspeech": "verb",
                "wordInterpretation": "喜歡",
                "wordGrade": "3",
                "wordSource": "",
                "createBy": "admin",
                "updateBy": "",
                "createTime": 1507029667000,
                "updateTime": 1507205646000
            },
            ...
            {
                "wordId": 4,
                "wordLevel": 526,
                "wordLength": 10,
                "wordContent": "likelihood",
                "wordPartofspeech": "noun",
                "wordInterpretation": "可能",
                "wordGrade": "5",
                "wordSource": "",
                "createBy": "admin",
                "updateBy": "",
                "createTime": 1507029667000,
                "updateTime": 1507205646000
            }
        ],
        "count": 4
    }            
}
```

響應(錯誤)

```
{
    "code": 400,
    "msg": "參數不正確",
    "data": null
}
```

#### 按年級或難易度查詢單字

**URL**
```
Get /elearning/word/list
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| grade | String | 欲查詢年級(grade和level不能同時為空) | :o: |
| level | Int | 欲查詢難易度 | :o: |
| range | Int | 難易度範圍(default為5) | :o: |
| page | Int | 頁數(default為0) | :o: |
| size | Int | 每頁顯示數量(default為20) | :o: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| wordList | List<Word> | 單字列表[單字細節](#) |
| count | Int | 符合條件的單字個數 |

**示例**

請求

```
grade: "3"
page: 0
size: 20
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "wordList": [
            {
                "wordId": 1,
                "wordLevel": 326,
                "wordLength": 4,
                "wordContent": "able",
                "wordPartofspeech": "adjective",
                "wordInterpretation": "能;有能力的",
                "wordGrade": "3",
                "wordSource": "",
                "createBy": "admin",
                "updateBy": "",
                "createTime": 1507029667000,
                "updateTime": 1507205646000
            },
            ...
            {
                "wordId": 4,
                "wordLevel": 326,
                "wordLength": 5,
                "wordContent": "above",
                "wordPartofspeech": "adjective",
                "wordInterpretation": "上文的,前述的",
                "wordGrade": "3",
                "wordSource": "",
                "createBy": "admin",
                "updateBy": "",
                "createTime": 1507029667000,
                "updateTime": 1507205646000
            }
        ],
        "count": 1792
    }            
}
```

響應(錯誤)

```
{
    "code": 400,
    "msg": "參數不正確",
    "data": null
}
```
