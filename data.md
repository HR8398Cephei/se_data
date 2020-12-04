# 学生查看某门课程自己的历史比赛列表

```json
{
  matches: [
    {
      matchId,
      constestId,
      timeStamp,
      courseId,
      title,
      participantNumber,
      startTime,
      endTime,
      chapter,
      description
      rank,
      score
    }
  ]
}
```

# 学生查看某门课程自己某场比赛详情

```json
{
  match: {
    userId,
    matchId,
    contestId,
    courseId,
    title，
    chapter,
    participantNumber
    description,
    publisherId,
    startTime,
    endTime,
    timeStamp,
    score,
    participators: [
      {
        userId,
        nickname,           // 随机生成的比赛昵称
        avatar,             // 随机生成的头像
        rank
      }
    ],
    questions: [
      {
        questionId / question_uuid,
        questionType,
        answer,             // 用户所选答案
        question_chapter,
        question_content,
        question_answer     // 题目答案
        question_choice_a_content,
        question_choice_b_content,
        question_choice_c_content,
        question_choice_d_content,
      }
    ]
  }
}
```

# 学生参加某门课程的比赛页面，显示比赛基础信息

```json
{
  match: {
    contestId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description
  }
}
```

# 学生匹配



## 开始匹配 

**接收数据**

```json
{
  type: 'MATCHING'                  // 1 或 2 或 3 或 4， 1代表加入比赛，2代表退出比赛，3代表准备，4代表取消准备
  match: {
    contetstId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description
    participator: [         // 房间内的人，包括我自己
      {
        userId,
        nickname,           // 随机生成的比赛昵称，若type为 3 或 4，可没有此项
        avatar,             // 随机生成的头像，若type为 3 或 4，可没有此项
        ready: false        // 该对手是否准备
      }
    ]
  }
}
```

**发送数据**

```json
{
  type: 'START_MATCHING',
  userId,
  courseId,
  contestId
}
```

## 对手信息变化 

**接收数据**

```json
{
  type: 'COMPETITOR_INFO_CHANGE'                  // 1 或 2 或 3 或 4， 1代表加入比赛，2代表退出比赛，3代表准备，4代表取消准备
  match: {
    contetstId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description
    participator: [         // 房间内的人，包括我自己
      {
        userId,
        nickname,           // 随机生成的比赛昵称，若type为 3 或 4，可没有此项
        avatar,             // 随机生成的头像，若type为 3 或 4，可没有此项
        ready: false        // 该对手是否准备
      }
    ]
  }
}
```

## 比赛开始 

**接收数据**

```json
{
  type: 5             // 5 代表比赛正式开始，此处必须是5
  match: {
    matchId,
    contestId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description，
    participators: [
      {
        userId,
        nickname,           // 随机生成的比赛昵称
        avatar,             // 随机生成的头像
      }
    ]
  }
}
```

## 某人提交 

**接收数据**

```json
{
  type: 6                  // 6 代表有人提交，此处必须是 6
  match: {
    contetstId,
    matchId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description
    participator: {
      userId,
      nickname,           // 随机生成的比赛昵称，若type为 3 或 4，可没有此项
      avatar,             // 随机生成的头像，若type为 3 或 4，可没有此项
    }
  }
}
```

## 比赛结束 

**接收数据**

```json
{
  type: 7                   // 7 代表比赛时间到，此处必须是7
  match：{
    contetstId,
    matchId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description
  }
}
```


## 取消准备 

**发送数据**

```json
{
  type: 4,
  userId,
  courseId,
  contestId，
  matchId
}
```

## 提交 

**发送数据**

```json
{
  type: 6,
  userId,
  courseId,
  contestId,
  matchId,
  answers: [
    {
      questionId,
      answer                // 和 question_ansewr 格式相同
    }
  ]
}
```

# 老师查看某门课程题库

```json
{
  courseId,
  questions: [
    {
      questionId / question_uuid,
      question_capter,
      quetion_content,
      quetionType,
    }
  ]
}
```

# 老师查看某门课程的题库中某一题详情

```json
{
  courseId,
  question: {
    questionId / question_uuid,
    question_capter,
    question_content,
    question_choice_a_content,
    question_choice_b_content,
    question_choice_c_content,
    question_choice_d_content,
    question_answer,
    quetionType,
  }
}
```


```json
{
  courseId,
  students: {
    userId,
    personal_id,
    realname,
    email,
    nickname,
    avatar,
    universityId,
    schoolId
  },
  matches: [
    {
      contestId,
      courseId,
      publisherId,
      title,
      participantNumber,
      startTime,
      endTime,
      chapter,
      description,
      matchId,
      timeStamp,        // 比赛的开始时间
      rank,
      score
    }
  ]
}
```

# 老师发布某门课程的比赛

## requestData

### post data

```json
{
  userId,
  title
  participantNumber,
  startTime
  endTime,
  chapter
  description,
  randomQuestions: bool， // 是否随机出题
  questions: [            // 选择的题目Id，若randomQuestions为true，则没有此项
    123
  ]
}
```

### params

```json
{
  contestId,
}
```

## returnData

```json
{
  contest: {
    contestId,
    courseId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description,
    questions: [
      {
        questionId / question_uuid,
        questionType,
        question_chapter,
        question_content,
        question_answer     // 题目答案
        question_choice_a_content,
        question_choice_b_content,
        question_choice_c_content,
        question_choice_d_content,
      }
    ]
  }
}
```

# 老师增加题目

## requestData

### post data

```json
{
  userId,
  questionType,
  question_chapter,
  question_content,
  question_choice_a_content,
  question_choice_b_content,
  question_choice_c_content,
  question_choice_d_content,
  question_answer
}
```

### params

```json
{
  courseId,
}
```

## returnData

```json
{
  question: {
    questionId,
    questionType,
    question_chapter,
    question_content,
    question_choice_a_content,
    question_choice_b_content,
    question_choice_c_content,
    question_choice_d_content,
    question_answer,
  }
}
```

# 老师修改题目

## requestData

### patch data

```json
{
  userId,
  courseId,
  questionType,
  question_chapter,
  question_content,
  question_choice_a_content,
  question_choice_b_content,
  question_choice_c_content,
  question_choice_d_content,
  question_answer
}
```

### params

```json
{
  courseId
}
```

## return data

```json
{
  question: {
    questionId,
    questionType,
    question_chapter,
    question_content,
    question_choice_a_content,
    question_choice_b_content,
    question_choice_c_content,
    question_choice_d_content,
    question_answer,
  }
}
```

# 老师修改题目

## requestData

### delete data

```json
{
  userId,
}
```

### params

```json
{
  courseId,
  questionId,
}
```

## return data

```json
{
  question: {
    questionId,
    questionType,
    question_chapter,
    question_content,
    question_choice_a_content,
    question_choice_b_content,
    question_choice_c_content,
    question_choice_d_content,
    question_answer,
  }
}
```