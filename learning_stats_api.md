### **1. API 基础信息**
- **Base URL**: `https://inner-stats.unipus.cn/v1`
- **Content-Type**: `application/json`

---

### **2. API 设计方案**

#### **2.1 查询学生学习状态**
- **接口描述**：查询某个学生的学习状态，包括学习进度、学习时长、成绩等信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/students/{student_id}`
- **请求参数**：
  - `student_id` (Path)：学生的唯一标识。
  - `date_range` (Query，可选)：时间范围，例如 `2024-01-01,2024-01-31`。
- **请求示例**：
  ```http
  GET /learning-state/students/12345?date_range=2024-01-01,2024-01-31 HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "student_id": "12345",
    "name": "小明",
    "learning_state": {
      "total_study_time": 3600, // 总学习时长（秒）
      "average_score": 10.0,    // 平均成绩
      "average_progress": 39.5, // 平均进度
      "tutorials": [{"id": 1001, "progress": 39.5, "total_study_time": 3600, "score": 10.0}],          // 各教程学习状态列表[(学习进度、学习时长、成绩)]
      "recent_nodeIds":[{"tid": 1001, "nodeId": "TASK006"}] 
    }
  }
  ```

---

#### **2.2 查询分组学习状态**
- **接口描述**：查询某个学生分组的学习状态汇总信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/groups/{group_id}`
- **请求参数**：
  - `group_id` (Path)：分组的唯一标识。
  - `date_range` (Query，可选)：时间范围，例如 `2024-01-01,2024-01-31`。
- **请求示例**：
  ```http
  GET /learning-state/groups/67890?date_range=2024-01-01,2024-01-31 HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "group_id": "67890",
    "group_name": "Group 01",
    "learning_state": {
      "students": [],                // 分组内学生列表
      "average_study_time": 3000,    // 平均学习时长（秒）
      "average_score": 80.2,         // 平均成绩
      "average_progress": 39.5,      // 平均进度
    }
  }
  ```

---

#### **2.3 查询班级学习状态**
- **接口描述**：查询某个班级的学习状态汇总信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/classes/{class_id}`
- **请求参数**：
  - `class_id` (Path)：班级的唯一标识。
  - `date_range` (Query，可选)：时间范围，例如 `2024-01-01,2024-01-31`。
  - `detail` (Query，可选)：true or false
- **请求示例**：
  ```http
  GET /learning-state/classes/1234?date_range=2024-01-01,2024-01-31&detail=true HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "class_id": "1234",
    "class_name": "Class 1A",
    "learning_state": {
      "total_students": 30,          // 班级学生总数
      "average_study_time": 7200,    // 平均学习时长（秒）
      "average_score": 78.6,         // 平均成绩
      "average_progress": 39.5,         // 平均进度
      "students_detail": [...]     // 班级内学生学习详情列表
    }
  }
  ```

---

#### **2.4 查询课程学习状态**
- **接口描述**：查询某个课程的学习状态汇总信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/courses/{course_id}`
- **请求参数**：
  - `course_id` (Path)：课程的唯一标识。
  - `date_range` (Query，可选)：时间范围，例如 `2024-01-01,2024-01-31`。
  - `detail` (Query，可选)：true or false
- **请求示例**：
  ```http
  GET /learning-state/courses/5678?date_range=2024-01-01,2024-01-31&detail=true HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "course_id": "5678",
    "course_name": "Mathematics",
    "learning_state": {
      "total_students": 100,         // 课程参与学生总数
      "total_classes": 10,         // 课程参与班级总数
      "average_study_time": 9000,    // 平均学习时长（秒）
      "average_score": 82.1,         // 平均成绩
      "average_progress": 39.5,         // 平均进度
      "classes_detail": []           // 课程下各班级的统计数据
    }
  }
  ```

---

#### **2.5 查询学校学习状态**
- **接口描述**：查询某个学校的学习状态汇总信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/schools/{school_id}`
- **请求参数**：
  - `school_id` (Path)：学校的唯一标识。
  - `date_range` (Query，可选)：时间范围，例如 `2024-01-01,2024-01-31`。
  - `detail` (Query，可选)：true or false
- **请求示例**：
  ```http
  GET /learning-state/schools/9999?date_range=2024-01-01,2024-01-31&detail=true HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "school_id": "9999",
    "school_name": "High School A",
    "learning_state": {
      "total_students": 500,         // 学校学生总数
      "total_classes": 10,         // 学校班级总数
      "total_courses": 10,         // 学校课程总数
      "average_study_time": 10000,   // 平均学习时长（秒）
      "average_score": 79.5,         // 平均成绩
      "average_progress": 39.5,         // 平均进度
      "classes_detail": []           // 各班级的统计数据
      "courses_detail": []           // 各课程的统计数据
    }
  }
  ```

#### **2.6 查询学生在单一教材里的学习状态**
- **接口描述**：查询某个学生在单一教材里的学习状态，包括学习进度、学习时长、成绩等信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/students/{student_id}/tutorials/{tutorial_id}`
- **请求参数**：
  - `student_id` (Path)：学生的唯一标识。
  - `tutorial_id` (Path)：教材的唯一标识。
- **请求示例**：
  ```http
  GET /learning-state/students/12345/tutorials/1001?date_range=2024-01-01,2024-01-31 HTTP/1.1
  ```
- **响应示例**：
  ```json
  {
    "student_id": "12345",
    "student_name": "小明",
    "tutorial_id": "1001",
    "tutorial_name": "Introduction to Programming",
    "total_study_time": 7200, // 总学习时长（秒）
    "average_score": 85.5,    // 平均成绩
    "progress": 0.75,  // 完成进度（百分比，0~1之间）
    "recent_nodeId":["TASK006"],
    "chapters": [
        {
        "chapter_id": "CH001",
        "chapter_name": "Chapter 1: Basics of Programming",
        "total_study_time": 3600,
        "average_score": 90,
        "completion_rate": 1.0,
        "sections": [
            {
            "section_id": "SEC001",
            "section_name": "Section 1.1: Introduction",
            "total_study_time": 1200,
            "average_score": 95,
            "completion_rate": 1.0,
            "parts": [
                {
                "part_id": "PART001",
                "part_name": "Part 1.1.1: What is Logic?",
                "total_study_time": 600,
                "average_score": 100,
                "completion_rate": 1.0,
                "tasks": [
                    {
                    "task_id": "TASK001",
                    "task_name": "Task 1.1.1.1: Read the Introduction",
                    "study_time": 300,
                    "score": 100,
                    "completion_status": true
                    },
                    {
                    "task_id": "TASK002",
                    "task_name": "Task 1.1.1.2: Complete the Quiz",
                    "study_time": 300,
                    "score": 100,
                    "completion_status": true
                    }
                ]
                }
            ]
            },
            {
            "section_id": "SEC002",
            "section_name": "Section 1.2: Basic Concepts",
            "total_study_time": 2400,
            "average_score": 85,
            "completion_rate": 0.5,
            "parts": [
                {
                "part_id": "PART003",
                "part_name": "Part 1.2.1: Variables and Data Types",
                "total_study_time": 1200,
                "average_score": 80,
                "completion_rate": 0.5,
                "tasks": [
                    {
                    "task_id": "TASK005",
                    "task_name": "Task 1.2.1.1: Read the Article",
                    "study_time": 600,
                    "score": 80,
                    "completion_status": true 
                    },
                    {
                    "task_id": "TASK006",
                    "task_name": "Task 1.2.1.2: Solve the Exercises",
                    "study_time": 600,
                    "score": 80,
                    "completion_status": false
                    }
                ]
                },
                {
                "part_id": "PART004",
                "part_name": "Part 1.2.2: Control Structures",
                "total_study_time": 1200,
                "average_score": 90,
                "completion_rate": 0.5,
                "tasks": [
                    {
                    "task_id": "TASK007",
                    "task_name": "Task 1.2.2.1: Watch the Lecture",
                    "study_time": 800,
                    "score": 90,
                    "completion_status": true
                    },
                    {
                    "task_id": "TASK008",
                    "task_name": "Task 1.2.2.2: Complete the Assignment",
                    "study_time": 400,
                    "score": 90,
                    "completion_status": false
                    }
                ]
                }
            ]
            }
        ]
        },
        ...
    ]
    }
  ```

#### **2.7 查询学生的所有在学教材的学习状态**
- **接口描述**：查询某个学生的所有在学教材的学习状态，包括学习进度、学习时长、成绩等信息。
- **请求方法**：`GET`
- **接口路径**：`/learning-state/students/{student_id}/tutorials`
- **请求参数**：
  - `student_id` (Path)：学生的唯一标识。
- **请求示例**：
  ```http
  GET /learning-state/students/12345/tutorials/1001?date_range=2024-01-01,2024-01-31 HTTP/1.1
  ```
- **响应示例**：
  ```json
  [{
    "student_id": "12345",
    "student_name": "小明",
    "tutorial_id": "1001",
    "tutorial_name": "Introduction to Logic",
    "total_study_time": 7200, // 总学习时长（秒）
    "average_score": 85.5,    // 平均成绩
    "progress": 0.75,  // 完成进度（百分比，0~1之间）
    "recent_nodeId":["TASK006"],
    "chapters": [
        {
        "chapter_id": "CH001",
        "chapter_name": "Chapter 1: Basics of Logic",
        "total_study_time": 3600,
        "average_score": 90,
        "completion_rate": 1.0,
        "sections": [...]
        },
        ...
    ]
    }, {
    "student_id": "12345",
    "student_name": "小明",
    "tutorial_id": "1002",
    "tutorial_name": "Introduction to Programming",
    "total_study_time": 7200, // 总学习时长（秒）
    "average_score": 85.5,    // 平均成绩
    "progress": 0.75,  // 完成进度（百分比，0~1之间）
    "recent_nodeId":["TASK001"],
    "chapters": [
        {
        "chapter_id": "CH001",
        "chapter_name": "Chapter 1: Basics of Programming",
        "total_study_time": 3600,
        "average_score": 90,
        "completion_rate": 1.0,
        "sections": [...]
        },
        ...
    ]
    } ]
  ```

---


### **字段说明**
1. **tutorial_id / chapter_id / section_id / part_id / task_id**: 唯一标识符。
2. **total_study_time**: 学生在该节点的总学习时长（秒）。
3. **average_score**: 该节点的平均成绩。
4. **completion_rate**: 完成进度（百分比，0~1之间）。
5. **tasks**: 最小粒度的学习任务，包含学习时长、成绩和完成状态。
6. **completion_status**: 任务完成状态，布尔值（`true` 表示已完成，`false` 表示未完成）。

---

### **数据层级**
- **Tutorial** 包含多个 **Chapter**。
- **Chapter** 包含多个 **Section**。
- **Section** 包含多个 **Part**。
- **Part** 包含多个 **Task**。

此 JSON 数据结构清晰地展示了各层节点的学习统计数据，便于进一步分析和展示。如果需要调整格式或增加字段，请随时告知！
---

### **3. 错误响应格式**
- **错误响应示例**：
  ```json
  {
    "error": {
      "code": 404,
      "message": "Student not found"
    }
  }
  ```

---


如果需要扩展接口功能或调整设计，请随时补充需求！
