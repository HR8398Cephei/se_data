# 学生查看某门课程自己的历史比赛列表

```json
{
  matches: [
    {
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
    participants: [
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
  },
  bParticipated: bool    // 是否参与过
  bIsParticipating: bool // 是否正在进行该场比赛的某场对抗
}
```

# 学生匹配

## 开始匹配 

**发送数据**

// TODO

```json
{

}
```

**接收数据**

```json
{
  type: 'MATCHING'              // 0 代表开始匹配，此处必须是0
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
    participants: [
      {
        userId,
        nickname,
        avatar,
        ready: bool   // 是否准备
      }
    ]
  },
  timeStamp 
}
```

## 对手信息变化

**接收数据**

```json
{
  type: 'MATCHING'              // 0 代表开始匹配，此处必须是0
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
    participants: [
      {
        userId,
        nickname,
        avatar,
        ready: bool   // 是否准备
      }
    ]
  },
  timeStamp
}
```

**发送数据**

```json
{
  
}
```

## 所有人均已准备，match创建

**接受数据**
```json
{
  type: 'READY_TO_START',
  matchId,
}
```

## 某人提交

**接收数据**

```json
{
  type: 'SOMEONE_SUBMITS'                  // 6 代表有人提交，此处必须是 6
  match: {
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
    timeStamp
  },
  participant: {
    userId,
    nickname,
    avatar,
  }
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

<h1>12.5修改</h1>

# 老师查看某门课程所有的学生

分页

```json
{
  students: [
    {
      userId,
      email,
      personal_id,
      realname,
      nickname,
      avatar,
      universityId,
      schoolId,
    }
  ],
  pagination: {
    pageNum,    // 当前在第几页
    pageSize,   // 当前页大小
    total,      // 总共有多少学生
  }
}
```

# 老师查看某门课某次比赛的所有对抗成绩

```json
{
  matches: [
    {
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
      timeStamp,        // 比赛的开始时间
      participants: [
        {
          userId,
          personal_id,
          realname,
          email,
          nickname,    // 用户真实昵称
          avatar,      // 用户真实头像
          universityId,
          schoolId,
          rank,
          score
        }
      ]
    }
  ],
  pagination: {
    pageNum,    // 当前在第几页
    pageSize,   // 当前页大小
    total,      // 总共有多少学生
  }
}
```

# 老师查看某门课程下某学生的所有对抗成绩

```json
{
  student: {
    userId,
    email,
    personal_id,
    realname,
    nickname,
    avatar,
    universityId,
    schoolId,
  },
  matches: [
    {
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
      timeStamp,        // 比赛的开始时间
      rank,
      score
    }
  ]
}
```

<h1>12.5修改结束</h1>

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

***以下为新增***

<h1>12.5修改</h1>

# 学生获取正在进行的对抗的websocket链接

```json
{
  websocket // 链接地址
}
```

# 学生获取正在进行的对抗的题目

```json
{
  match: {
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
    participants: [
      {
        userId,
        nickname,           // 随机生成的比赛昵称
        avatar,             // 随机生成的头像
      }
    ],
    questions: [
      {
        questionId,
        questionType,
        question_chapter,
        question_content,
        question_choice_a_content,
        question_choice_b_content,
        question_choice_c_content,
        question_choice_d_content,
      }
    ]
  }
}
```

# 老师查看某门课程下已经结束的所有**比赛**

```json
{
  contests: [
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
    }
  ]
}
```

<h1>12.5修改结束</h1>