[帳號](#帳號)
    [登入](#登入)
    [註冊](#註冊)
[單字](#單字)
    [新增單字](#新增單字)
[教材](#教材)
[考卷](#考卷)
返回代碼: 0

## 單字

### 新增單字

**URL**
```
POST /elearning/word/insert
```

**請求参数**

| 參數名稱 | 參數類型 | 參數描述 | 可否為null |
| :-: | :-: | :-: | :-: |
| wordId | Int | 單字ID(需為空，自動添加) | 必須為null |
| wordLevel | Int | 單字難易度 | [x] |
| wordContent | String | 單字內容(需小於128字元) | :x: |
| wordPartofspeech | String | 單字詞性 | [x] |
| wordInterpretation | String | 單字解釋 | [x] |
| wordGrade | String | 單字所屬年級 | [x] | 
| createBy | String | 創建帳號 | [x] |
| updateBy | String | 修改帳號 | [x] |
| wordSource | String | 單字來源(尚未定義) | [x] |

**響應参数**

| 參數名稱 | 參數類型 | 參數描述 |
| :-: | :-: | :-: |
| wordId | Int | 單字ID |

**示例**

請求

```
//wordContent not null
//wordGrade not null
//wordPartofspeech not null
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

返回
```
{
    "code": 0,
    "msg": "成功",
    "data": 10947
}
```

```
{
    "code": 400,
    "msg": "年級必填",
    "data": null
}
```
### 刪除單字
```
Delete /elearning/word/delete
```
参数
```
wordId: 1
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

```
{
    "code": 403,
    "msg": "刪除內容不存在",
    "data": null
}
```

### 单字列表查询
```
Get /elearning/word/list
```
参数
```
//page default 0
//size default 20
//grade not null
grade: "3"
page: 0
size: 20
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "data": [
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

```
{
    "code": 400,
    "msg": "參數不正確",
    "data": null
}
```

### 單字量分佈情況
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

## 教材
### 新增教材
```
POST /elearning/paragraph/insert
```
参数
```
//paragraphContent not null
//paragraphGrade not null
paragraphId: 1
paragraphLevel: 600
paragraphContent: " Two Halloween fireballs ... in the night sky. "
paragraphHashtag: "Halloween fireballs"
paragraphGrade: "3"
paragraphSource: "第一单元"
createBy: "admin"
updateBy: "admin"
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "data": [
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

```
{
    "code": 400,
    "msg": "教材所屬年級必填",
    "data": null
}
```
### 刪除教材
```
Delete /elearning/paragraph/delete
```
参数
```
paragraphId: 1
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": null
}
```

```
{
    "code": 403,
    "msg": "刪除內容不存在",
    "data": null
}
```
### 教材列表查詢
```
Get /elearning/paragraph/list
```
参数
```
//page default 0
//size default 20
//grade not null
grade: "3"
page: 0
size: 20
```
返回
```
{
    "code": 0,
    "msg": "成功",
    "data": {
        "data": [
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

```
{
    "code": 400,
    "msg": "參數不正確",
    "data": null
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
