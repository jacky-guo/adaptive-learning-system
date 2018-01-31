[帳號](#帳號)
    [登入](#登入)
    [註冊](#註冊)
[單字](#單字)
    [新增單字](#新增單字)
[教材](#教材)
[考卷](#考卷)
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
