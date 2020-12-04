# 学生查看某门课程自己的历史小测

get  /attend_quiz?studentId&courseId

```json
{
  quizzes: [
    {
      quizId,
      courseId,
      publisherId,
      title,
      participantNumber,
      startTime,
      endTime,
      chapter,
      description,
      score
    }
  ]
}
```

# 学生查看某门课程自己某场小测详情

get  /attend_quiz/{quizId}

```json
{
  quiz: {
    quizId,
    courseId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description,
    score,
    participantNumber,   // 参加了这个小测的人数
    questions: [
      {
        questionId,
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

# 学生参加某门课程的小测页面，显示小测基础信息

get quiz?courseId

```json
{
  quiz: {
    quizId,
    courseId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description,
  }
  bIsParticipating
}
```

# 学生参加某门课程小测

创建/检测参加记录和获取题目

get /quiz_question

```json
{
  quiz: {
    quizId,
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

# 学生查看当前有多少人正在进行同一场小测

get /attend_quiz/count?quizId

```json
{
  participantCount,   // 当前正在参加了这个小测的人数
}
```

# 学生提交小测答案

post  quiz_submission

```json
{
  userId,
  quizId,
  courseId,
  answers: [
    {
      questionId,
      answer
    }
  ]
}
```

# 老师查看某门课小测成绩

get attend_quiz?courseId=

```json
{
  courseId,
  quizzes: [
    {
      quizId,
      courseId,
      publisherId,
      title,
      participantNumber,
      startTime,
      endTime,
      chapter,
      description,
      averageScore           // 平均分
    }
  ]
}
```

# 老师查看某门课某次小测所有学生的成绩（分页）

get quiz_submission/

由于参加一次小测的人数可能很多，所以这里选择分页participators按pageSize和pageNum返回

```json
{
  quiz: {
    quizId,
    courseId,
    publisherId,
    title,
    participantNumber,
    startTime,
    endTime,
    chapter,
    description,
  },
  participators: [
    {
      userId,
      email,
      personal_id,
      realname,
      nickname,
      avatar,
      universityId,
      schoolId,
      score，
    }
  ],
  pagination: {
    pageNum,    // 当前在第几页
    pageSize,   // 当前页大小
    total,      // 该小测总共有多少个参赛者记录
  }
}
```

# 老师查看某门课程的学生小测成绩

get 

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
  quizzes: [
    {
      quizId,
      courseId,
      publisherId,
      title,
      participantNumber,
      startTime,
      endTime,
      chapter,
      description,
      score,
    }
  ]
}
```
