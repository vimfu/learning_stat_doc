## 数据模型

注：本模型信息主要为描述各数据实体包含的主要信息, 很多JSON字段未列明数据结构, 具体信息请查看项目代码.

###  学生 (Student_Info)

| 字段名        | 类型        | 描述                   | 源服务              |
| ------------- | ------      | ---------------------- | ------------------- |
| student_id    | long        | 学生的唯一标识         | Orgnization Service |
| student_name  | string      | 学生的姓名             | Orgnization Service |
| class_id      | long        | 所在班级的唯一标识     | Orgnization Service |
| school_id     | long        | 所在学校的唯一标识     | Orgnization Service |
| ...           | ...         | 其他字段               | Orgnization Service |


###  教程 (Tutorial_Info)

| 字段名          | 类型   | 描述                       | 源服务         |
| --------------- | ------ | -------------------------- | -------------- |
| tutorial_id     | long   | 教程的唯一标识             | Tutorial Service |
| tutorial_name   | string | 教程的名称                 | Tutorial Service |
| tutorial_desc   | string | 对教程的描述               | Tutorial Service |
| tutorial_tree   | JSON   | JSON 树状结构，表示教程内容 | Tutorial Service |


###  班级信息 (Class_Info)

| 字段名          | 类型   | 描述                       | 源服务              |
| --------------- | ------ | -------------------------- | ------------------- |
| class_id        | long   | 班级的唯一标识             | Orgnization Service |
| class_name      | string | 班级的名称                 | Orgnization Service |
| class_students  | JSON   | 班级中学生的 ID 列表       | Orgnization Service |
| class_courses   | JSON   | 班级中课程的 ID 列表       | Orgnization Service |


###  学生组信息 (Student_Group_Info)

| 字段名             | 类型   | 描述                         | 源服务              |
| ------------------ | ------ | ---------------------------- | ------------------- |
| student_group_id   | long   | 学生组的唯一标识             | Orgnization Service |
| student_group_name | string | 学生组的名称                 | Orgnization Service |
| student_list       | JSON   | 学生列表信息，包含组长信息等 | Orgnization Service |


###  课程信息 (Course_Info)

| 字段名           | 类型   | 描述                                                | 源服务              |
| ---------------- | ------ | --------------------------                          | ------------------- |
| course_id        | long   | 课程的唯一标识                                      | Orgnization Service |
| course_name      | string | 课程的名称                                          | Orgnization Service |
| course_tutorials | JSON   | 课程包含的教程的 ID 列表 (CourseTutorial Relation)s | Orgnization Service |


###  学校信息 (School_Info)

| 字段名          | 类型   | 描述                       | 源服务              |
| --------------- | ------ | -------------------------- | ------------------- |
| school_id       | long   | 学校的唯一标识             | Orgnization Service |
| school_name     | string | 学校的名称                 | Orgnization Service |
| school_classes  | JSON   | 学校中班级的 ID 列表       | Orgnization Service |
| school_courses  | JSON   | 学校中课程的 ID 列表       | Orgnization Service |


###  学生教程学习状态 (Stu_Tutorial_Summary)

| 字段名                   | 类型   | 描述                                                                                    | 源服务 |
| -----------------------  | ------ | ------------------------                                                                | ------ |
| student_id               | long   | 学生的唯一标识                                                                          | -      |
| tutorial_id              | long   | 教程的唯一标识                                                                          | -      |
| learning_time            | long   | 学生的累计学习时长                                                                      | -      |
| learning_progress        | long   | 学生的学习进度                                                                          | -      |
| learning_score           | double | 学生的学习成绩分数                                                                      | -      |
| recent_learning_behavior | JSON   | 最近的学习行为（如操作记录）                                                            | -      |
| student_groups_result    | JSON   | 学生在每次小组中的成绩汇总                                                              | -      |


###  学生课程学习状态 (Stu_CourseTutorials_Summary)

| 字段名                   | 类型                      | 描述                        | 源服务 |
| -----------------------  | ------                    | ------------------------    | ------ |
| student_id               | long                      | 学生的唯一标识              | -      |
| course_id                | long                      | 课程的唯一标识              | -      |
| course_learning_time     | JSON[tutorial_id, long]   | 学生的累计学习时长          | -      |
| course_learning_progress | JSON[tutorial_id, double] | 学生的学习进度              | -      |
| course_learning_score    | JSON[tutorial_id, double] | 学生的学习成绩分数          | -      |
| course_recent_activities | JSON                      | 最近的学习行为（如操作记录）| -      |


###  学生分组的学习状态 (Student_Group_Summary)

| 字段名                  | 类型   | 描述                     | 源服务 |
| ----------------------- | ------ | ------------------------ | ------ |
| student_group_id        | long   | 学生分组的唯一标识       | -      |
| tutorial_id             | long   | 教程的唯一标识           | -      |
| tutorial_node_id        | long   | 教程内节点的唯一标识     | -      |
| group_learning_time     | JSON   | 学生分组的累计学习时长   | -      |
| group_learning_score    | JSON   | 学生分组的学习成绩分数   | -      |


###  班级层面的学习状态 (Class_Summary)

| 字段名                           | 类型   | 描述                           | 源服务 |
| -----------------------          | ------ | ------------------------------ | ------ |
| class_id                         | long   | 班级的唯一标识                 | -      |
| class_students_learning_time     | JSON   | 班级中所有学生的学习时长汇总   | -      |
| class_students_learning_score    | JSON   | 班级中所有学生的学习分数汇总   | -      |
| class_students_learning_progress | JSON   | 班级中所有学生的学习进度汇总   | -      |
| class_recent_active_stus         | JSON   | 班级中学生的近期学习行为汇总   | -      |


###  课程层面的学习状态 (Course_Summary)

| 字段名                           | 类型   | 描述                                     | 源服务 |
| -----------------------          | ------ | ---------------------------------------- | ------ |
| course_id                        | long   | 课程的唯一标识                           | -      |
| course_class_learning_time       | JSON   | 课程下每个班级的学生学习时长汇总         | -      |
| course_class_learning_score      | JSON   | 课程下每个班级的学生学习分数汇总         | -      |
| course_class_learning_progress   | JSON   | 课程下每个班级的学生学习进度汇总         | -      |


###  学校层面的学习状态 (School_Summary)

| 字段名                          | 类型   | 描述                                     | 源服务 |
| -----------------------         | ------ | ---------------------------------------- | ------ |
| school_id                       | long   | 学校的唯一标识                           | -      |
| school_course_time              | JSON   | 学校中所有课程的学习时长汇总             | -      |
| school_course_score             | JSON   | 学校中所有课程的学习分数汇总             | -      |
| school_course_learning_progress | JSON   | 学校中所有课程的学生学习进度汇总         | -      |
| school_class_time               | JSON   | 学校中所有班级的学习时长汇总             | -      |
| school_class_score              | JSON   | 学校中所有班级的学习分数汇总             | -      |
| school_class_behavior           | JSON   | 学校中所有班级的近期学习行为汇总         | -      |
| school_class_learning_progress  | JSON   | 学校中所有班级的学生学习进度汇总         | -      |

