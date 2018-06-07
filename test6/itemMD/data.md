## 数据库设计 [返回](../README.md)

- ### USER表（用户表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |USER_ID|NUMBER(8,0)|主键|否| | | 用户ID|
    |NAME|VARCHAR2(50 BYTE)| |否| | | 用户真实姓名|
    |GITHUB_USERNAME|VARCHAR2(50 BYTE)| |是|空| | GitHUB用户名|
    |UPDATE_DATE|DATE| |是|空| | GitHUB用户名修改日期|
    |PASSWORD|VARCHAR2(512 BYTE)| |是|空| | 加密存储密码，为空表示密码就是学号|
    |DISABLE|VARCHAR2(20 BYTE)| |否| | |是否禁用,值为是表示禁用,其他表示正常.|

- ### TEACHERS表（教师表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TEACHER_ID|VARCHAR2(50 BYTE)|主键|否| | | 老师的编号|
    |USER_ID|NUMBER(8,0)|外键|是| | | 老师的用户ID，USERS表的外键|
    |COURSE_ID|NUMBER(8,0)|外键|是| | | 老师的课程ID，COURSE表的外键|
    |TERM_ID|NUMBER(8,0)|外键|是| | | 老师的上课学期ID，TERM表的外键|
    |DEPARTMENT|VARCHAR2(400 BYTE)| |否| | | 老师属于的部门|

- ### STUDENTS表（学生表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |STUDENT_ID|VARCHAR2(50 BYTE)|主键|否| | | 学生的学号|
    |USER_ID|NUMBER(8,0)|外键|是| |空| 学生的用户ID，USERS表的外键，为空表示还没有建立用户|
    |COURSE_ID|NUMBER(8,0)|外键|是| | | 学生的课程ID，COURSE表的外键|
    |TERM_ID|NUMBER(8,0)|外键|是| | | 学生的上课学期ID，TERM表的外键|
    |CLASS|VARCHAR2(20 BYTE)| |否| | | 学生所属的班级|
    |RESULT_SUM|VARCHAR2(400 BYTE)|外键|是|空| | 成绩汇总（来自GRADES表），以逗号分开，第一个成绩是平均成绩,后面是每次实验的成绩。|
    |WEB_SUM|VARCHAR2(400 BYTE)| |是|空| | GitHub网址是否正确，用逗号分开，Y代表正确，N代表不正确。第1位代表总的GitHUB地址是否正确，第2位表示第1次实验的地址，第3位表示第2位实验地址，依此类推。|

- ### TERM表（上课学期表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TERM_ID|VARCHAR2(50 BYTE)|主键|否| | | 选课学期的编号|
    |COURSE_ID|NUMBER(8,0)|外键|是| | | 该学期的课程ID，COURSE表的外键|
    |NAME|VARCHAR2(400 BYTE)| |否| | | 课程的名称|

- ### COURSE表（课程表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |COURSE_ID|VARCHAR2(50 BYTE)|主键|否| | | 每科课程的编号|
    |TERM_ID|NUMBER(8,0)|外键|是| | | 该课程上课的学期的ID，TERM表的外键|
    |NAME|VARCHAR2(400 BYTE)| |否| | | 课程的名称|
    |CONTENT|VARCHAR2(400 BYTE)| |否| | | 课程的主要内容|

- ### TESTS表（实验表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |TEST_ID|VARCHAR2(50 BYTE)|主键|否| | | 实验的编号|
    |SCOREITEM_ID|NUMBER(8,0)|外键|是| | | 该实验评分项的ID，SCOREITEM表的外键|
    |TITLE|VARCHAR2(400 BYTE)| |否| | | 实验名称|

- ### GRADES表（成绩表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |STUDENT_ID|VARCHAR2(50 BYTE)|主键|否| | | 学生的学号|
    |RESULT|VARCHAR2(50 BYTE)||否| | | 实验分数|
    |MOMO|NUMBER(8,0)||是| | | 实验评价|
    |UPDATE_DATE|VARCHAR2(400 BYTE)| |否| | | 修改日期|

- ### SCOREITEM表（评分项表）

    |字段|类型|主键，外键|可以为空|默认值|约束|说明|
    |:-------:|:-------------:|:------:|:----:|:---:|:----:|:----------|
    |SCOREITEM_ID|VARCHAR2(50 BYTE)|主键|否| | | 评分项的编号|
    |NAME|VARCHAR2(50 BYTE)||否| | | 该评分项的名称|
    |SCORE|NUMBER(8,0)||是| | | 该评分项的分值|
    |CONTENT|VARCHAR2(400 BYTE)| |否| | | 该评分项的内容|