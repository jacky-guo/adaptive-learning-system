+ [前言](#前言)
+ [帳號](#帳號)
    + [登入](#登入)
    + [註冊](#註冊)
+ [單字](#單字)
    + [新增單字](#新增單字)
    + [刪除單字](#刪除單字)
    + [單字查詢](#單字查詢)
        + [相似搜尋](#相似搜尋)
        + [按年級或難易度查詢單字](#按年級或難易度查詢單字)
+ [教材](#教材)
    + [新增教材](#新增教材)
    + [刪除教材](#刪除教材)
    + [教材列表查詢](#教材列表查詢)
        + [按教材序號查詢](#按教材序號查詢)
        + [按年級或難易度查詢教材](#按年級或難易度查詢教材)
+ [考卷](#考卷)
+ [附錄](#附錄)
    + [錯誤碼列表](#錯誤碼列表)
    + [年級列表](#年級列表)
+ [更新日誌](#更新日誌)

## 前言

### 返回參數格式說明

調用方需判斷HTTP的響應碼：

* 200表調用成功
* 500,502表系統內部錯誤，可稍後再試
* 400Bad Request（例如：參數型態有誤）
* 401表未授權
* 403表禁止訪問
* 405表POST / GET模式請求錯誤

當HTTP響應200時，接口返回的數據格式如下

```
{"code": 错误码, "message": "success", "data":""}
```

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

請求參數

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
    "code": 40005,
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

請求參數

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
    "code": 40002,
    "msg": "帳號/密碼必填",
    "data": null
}

```

響應(錯誤)

```
{
    "code": 40006,
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

請求參數

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
    "code": 40002,
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

請求參數

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
    "code": 40004,
    "msg": "內容不存在",
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

請求參數

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
    "code": 40002,
    "msg": "參數不完整",
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
| grade | String | 欲查詢年級(grade和level不能同時為空)(default為3) | :o: |
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

請求參數

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
    "code": 40002,
    "msg": "參數不完整",
    "data": null
}
```

## 教材

### 新增教材

**URL**
```
POST /elearning/paragraph/insert
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| paragraphId | Int | 教材ID | :o: |
| paragraphLevel | Int | 教材難易度 | :o: | 
| paragraphContent | String | 教材內容 | :x: |
| paragraphHashtag | String | 教材標籤 | :o: |
| paragraphGrade | String | 教材所屬年級 | :x: |
| paragraphSource | String | 教材來源 | :o: |
| createBy | String | 創建帳號 | :o: |
| updateBy | String | 修改帳號 | :o: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| wordList | List<Word> | 新出現的單字列表[單字細節](#) |
| ParagraphId | Int | 教材ID |

**示例**

請求參數

```
paragraphId: 1
paragraphLevel: 600
paragraphContent: " Two Halloween fireballs ... in the night sky. "
paragraphHashtag: "Halloween fireballs"
paragraphGrade: "3"
paragraphSource: "第一单元"
createBy: "admin"
updateBy: "admin"
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "wordList": [
            {
                "wordId": null,
                "wordLevel": null,
                "wordLength": null,
                "wordContent": "Halloween",
                "wordPartofspeech": "adjective",
                "wordInterpretation": null,
                "wordGrade": 3,
                "wordSource": "第一单元",
                "createBy": "admin",
                "updateBy": null,
                "createTime": null,
                "updateTime": null
            },
            ...
            {
                "wordId": null,
                "wordLevel": null,
                "wordLength": null,
                "wordContent": "sky",
                "wordPartofspeech": "noun",
                "wordInterpretation": null,
                "wordGrade": 3,
                "wordSource": "第一单元",
                "createBy": "admin",
                "updateBy": null,
                "createTime": null,
                "updateTime": null
            }
        ],
        "ParagraphId": 1
    }
}
```

響應(錯誤)

```
{
    "code": 40002,
    "msg": "教材所屬年級必填",
    "data": null
}
```

### 刪除教材

**URL**
```
Delete /elearning/paragraph/delete
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| paragraphId | Int | 需要刪除的教材的ID | :x: |

**響應参数**

無

**示例**

請求參數

```
paragraphId: 1
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
    "code": 40004,
    "msg": "內容不存在",
    "data": null
}
```

### 教材列表查詢

#### 按教材序號查詢

**URL**
```
Get /elearning/paragraph/query
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| paragraphId | Int | 欲查詢的教材的ID | :x: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| paragraph | Paragraph |[教材細節](#) |

**示例**

請求參數

```
paragraphId: 1
```

響應(正確)

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "paragraphId": 1,
        "paragraphLevel": 300,
        "paragraphWordCount": 10,
        "paragraphSentenceLength": 1,
        "paragraphContent": "He sees all ... to the girl.",
        "paragraphHashtag": "1",
        "paragraphGrade": "3",
        "paragraphSource": "1",
        "createBy": "admin",
        "updateBy": null,
        "createTime": 1509549220000,
        "updateTime": 1509549220000
    },
}
```

響應(錯誤)

```
{
    "code": 40004,
    "msg": "內容不存在",
    "data": null
}
```

#### 按年級或難易度查詢教材

**URL**
```
Get /elearning/paragraph/list
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| grade | String | 欲查詢年級(grade和level不能同時為空)(default為3) | :o: |
| level | Int | 欲查詢難易度 | :o: |
| range | Int | 難易度範圍(default為5) | :o: |
| page | Int | 頁數(default為0) | :o: |
| size | Int | 每頁顯示數量(default為20) | :o: |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| paragraphList | List<Paragraph> | 教材列表[教材細節](#) |
| count | Int | 符合條件的教材個數 |

**示例**

請求參數

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
        "paragraphList": [
            {
                "paragraphId": 831,
                "paragraphLevel": 300,
                "paragraphWordCount": 1,
                "paragraphSentenceLength": 1,
                "paragraphContent": "He sees all ... to the girl.",
                "paragraphHashtag": "1",
                "paragraphGrade": "3",
                "paragraphSource": "1",
                "createBy": "admin",
                "updateBy": null,
                "createTime": 1509549220000,
                "updateTime": 1509549220000
            },
            ...
            {
                "paragraphId": 1853,
                "paragraphLevel": 300,
                "paragraphWordCount": 36,
                "paragraphSentenceLength": 7,
                "paragraphContent": "A man is ... will be fine.",
                "paragraphHashtag": "1",
                "paragraphGrade": "3",
                "paragraphSource": "1",
                "createBy": "admin",
                "updateBy": null,
                "createTime": 1509715215000,
                "updateTime": 1509715215000
            }
        ],
        "count": 10
    }
}
```

響應(錯誤)

```
{
    "code": 40002,
    "msg": "參數不完整",
    "data": null
}
```

## 附錄

### 錯誤碼列表

| 錯誤碼 | 錯誤描述 | 備註 |
| :-: | :-: | :-: |
| 0 | 成功 |  |
| 40001 | 參數不正確 |  |
| 40002 | 參數不完整 |  |
| 40003 | python服務器異常 |  |
| 40004 | 內容不存在 |  |
| 40005 | 帳號或密碼不正確 |  |
| 40006 | 帳號已被註冊 |  |

### 年級列表

| 代碼 | 所代表年級 |
| :-: | :-: |
| 0 | 課外 |
| 1 | 一年級 |
| 2 | 二年級 |
| 3 | 三年級 |
| 4 | 四年級 |
| 5 | 五年級 |
| 6 | 六年級 |


## 更新日誌

## 尚未上線部分

### 單字量分佈情況

**URL**
```
Get /elearning/word/pie
```

参数

```
null
```

返回

```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "grade6": 835,
        "grade5": 930,
        "grade4": 579,
        "grade3": 1353
    }
}
```

## 考卷
### 自動產生考卷

```
Get /elearning/exam/autoGenerateExam
```
参数
```
//examNumber default 3
grade: 3
examNumber: 3
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "examId": null,
        "examTitle": "AutoGenerateExam",
        "examLevel": 600,
        "examType": null,
        "examGrade": "3",
        "examNumber": 3,
        "examHashtag": "President...;Running...;LGBT;",
        "createBy": "AutoGenerate",
        "updateBy": null,
        "createTime": null,
        "updateTime": null,
        "questionDTOList": [
            {
                "questionId": null,
                "questionLevel": 600,
                "questionType": 2,
                "questionAutoCreate": 1,
                "questionParagraphId": 1868,
                "questionContent": " _1_ President ... from now!",
                "questionGrade": "6",
                "questionSource": "http ... level-1/",
                "questionHashtag": "President ... level 1",
                "createBy": "AutoGenerate",
                "updateBy": null,
                "createTime": null,
                "updateTime": null,
                "answerDTOList": [
                    {
                        "answerOrders": null,
                        "title": "1",
                        "rightvalue": "French",
                        "wrongvalue1": "wine",
                        "wrongvalue2": "win",
                        "wrongvalue3": "slow"
                    },
                    ...
                    {
                        "answerOrders": null,
                        "title": "11",
                        "rightvalue": "maybe",
                        "wrongvalue1": "whose",
                        "wrongvalue2": "die",
                        "wrongvalue3": "please"
                    }
                ]
            },
            ...
            {
                "questionId": null,
                "questionLevel": 600,
                "questionType": 2,
                "questionAutoCreate": 1,
                "questionParagraphId": 1875,
                "questionContent": " _1_ the USA ... have weapons.",
                "questionGrade": "6",
                "questionSource": "https ... level-1/",
                "questionHashtag": "LGBT Groups Take Up Weapons – level 1",
                "createBy": "AutoGenerate",
                "updateBy": null,
                "createTime": null,
                "updateTime": null,
                "answerDTOList": [
                    {
                        "answerOrders": null,
                        "title": "1",
                        "rightvalue": "in",
                        "wrongvalue1": "ago",
                        "wrongvalue2": "ready",
                        "wrongvalue3": "being"
                    },
                    ...
                    {
                        "answerOrders": null,
                        "title": "8",
                        "rightvalue": "so",
                        "wrongvalue1": "rose",
                        "wrongvalue2": "issue",
                        "wrongvalue3": "saw"
                    }
                ]
            }
        ]
    }
}
```

```
{
    "code": 400,
    "msg": "參數不正確",
    "data": null
}
```

### 新增考卷
