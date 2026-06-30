# 班级管理助手

一个功能完善的班级管理系统，支持课程表管理、学生管理、成绩管理、成绩分析和我的班级展示。

## 📋 目录

- [技术栈](#技术栈)
- [项目结构](#项目结构)
- [快速开始](#快速开始)
- [功能特性](#功能特性)
- [数据库表结构](#数据库表结构)
- [API 接口](#api-接口)
- [成绩类型](#成绩类型)
- [开发指南](#开发指南)

## 🛠 技术栈

### 后端
- **FastAPI** - 高性能 Python Web 框架
- **PostgreSQL** - 关系型数据库
- **Redis** - 缓存数据库
- **SQLAlchemy** - ORM 框架
- **Pydantic** - 数据验证
- **Uvicorn** - ASGI 服务器

### 前端
- **React 19** - 前端框架
- **Vite** - 构建工具
- **Ant Design** - UI 组件库
- **ECharts** - 数据可视化
- **React Router** - 路由管理

## 📁 项目结构

```
class_assistant/
├── README.md                          # 项目说明文档
├── backend/                           # 后端代码
│   ├── main.py                        # FastAPI 应用入口
│   ├── requirements.txt               # Python 依赖
│   ├── init_db.sql                    # 数据库初始化脚本
│   ├── backend.zip                    # 后端代码压缩包
│   ├── api/                           # API 路由模块
│   │   ├── __init__.py                # 路由注册
│   │   ├── auth.py                    # 认证接口
│   │   ├── classes.py                 # 班级管理接口
│   │   ├── dashboard.py               # 仪表盘接口
│   │   ├── grade_analysis.py          # 成绩分析接口
│   │   ├── grades.py                  # 年级管理接口
│   │   ├── pdf2docx.py                # PDF转Word接口
│   │   ├── schedules.py               # 课程表管理接口
│   │   ├── scores.py                  # 成绩管理接口
│   │   ├── students.py                # 学生管理接口
│   │   ├── subjects.py                # 学科管理接口
│   │   ├── tags.py                    # 标签管理接口
│   │   └── users.py                   # 用户管理接口
│   ├── entity/                        # 数据模型
│   │   ├── models.py                  # SQLAlchemy 模型定义
│   │   └── schemas.py                 # Pydantic 数据验证模式
│   ├── utils/                         # 工具函数
│   │   ├── auth_utils.py              # 认证工具函数
│   │   └── database.py                # 数据库连接配置
│   └── cache/                         # 缓存目录
│       ├── converted/                 # 转换后的文件
│       └── uploads/                   # 上传的文件
└── frontend/                          # 前端代码
    ├── package.json                   # Node.js 依赖配置
    ├── vite.config.js                 # Vite 构建配置
    ├── eslint.config.js               # ESLint 配置
    ├── index.html                     # HTML 入口
    ├── README.md                      # 前端说明
    ├── frontend.zip                   # 前端代码压缩包
    ├── doc/                           # 示例文档
    │   ├── 26春期末5级部.xlsx         # 成绩导入示例
    │   └── 试卷分析.xlsx              # 试卷分析示例
    ├── public/                        # 静态资源
    │   ├── favicon.svg                # 网站图标
    │   └── icons.svg                  # 图标集
    └── src/                           # 源代码
        ├── main.jsx                   # React 应用入口
        ├── App.jsx                    # 主应用组件
        ├── App.css                    # 主应用样式
        ├── index.css                  # 全局样式
        ├── assets/                    # 静态资源
        │   ├── hero.png               # 登录页背景图
        │   ├── react.svg              # React Logo
        │   └── vite.svg               # Vite Logo
        ├── components/                # 公共组件
        │   ├── Layout.jsx             # 布局组件
        │   ├── Layout.css             # 布局样式
        │   └── CRUDManagement.jsx     # 通用 CRUD 组件
        ├── context/                   # 全局状态
        │   └── AuthContext.jsx        # 认证上下文
        ├── pages/                     # 页面组件
        │   ├── Login.jsx              # 登录页
        │   ├── Login.css              # 登录页样式
        │   ├── Dashboard.jsx          # 仪表盘（课程表）
        │   ├── Dashboard.css          # 仪表盘样式
        │   ├── Management.jsx         # 管理页
        │   ├── Management.css         # 管理页样式
        │   ├── Visualization.jsx      # 我的班级
        │   ├── Visualization.css      # 我的班级样式
        │   ├── GradeAnalysis.jsx      # 成绩分析
        │   ├── GradeAnalysis.css      # 成绩分析样式
        │   ├── Tools.jsx              # 工具箱
        │   ├── Tools.css              # 工具箱样式
        │   └── management/            # 管理子页面
        │       ├── GradeManagement.jsx      # 年级管理
        │       ├── ClassManagement.jsx      # 班级管理
        │       ├── StudentManagement.jsx    # 学生管理
        │       ├── ScoreManagement.jsx      # 成绩管理
        │       ├── TagManagement.jsx        # 标签管理
        │       └── UserManagement.jsx       # 用户管理
        ├── pages/tools/               # 工具子页面
        │   └── PdfToWord.jsx          # PDF转Word工具
        └── services/                  # API 服务
            └── api.js                 # API 请求封装
```

## 🚀 快速开始

### 环境要求

- Python 3.8+
- Node.js 18+
- PostgreSQL 12+
- Redis 6+

### 手动启动

#### 1. 数据库初始化

```bash
# 创建数据库
psql -U postgres -c "CREATE DATABASE class_assistant;"

# 初始化表结构（可选，后端会自动创建）
psql -U postgres -d class_assistant -f backend/init_db.sql
```

#### 2. 启动后端

```bash
cd backend
pip install -r requirements.txt
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

#### 3. 启动前端

```bash
cd frontend
npm install
npm run dev
```

### 访问地址

- **前端**: http://localhost:5173
- **后端**: http://localhost:8000
- **API 文档**: http://localhost:8000/docs

### 默认账号

- **用户名**: teacher1
- **密码**: 123456

## ✨ 功能特性

### 1. 登录页
- 用户名密码登录
- 小学大楼背景图
- 记住登录状态

### 2. 首页 - 课程表
- 显示当前登录老师的课程表
- 即将上课的班级显示黄色背景
- 正在上课的班级显示红色背景
- 1分钟自动刷新
- 支持手动刷新

### 3. 管理页
- **年级管理**: 年级的增删改查
- **班级管理**: 班级的增删改查
- **学生管理**: 学生的增删改查 + Excel 导入
- **用户管理**: 用户的增删改查
- **成绩管理**: 成绩的增删改查 + Excel 导入
- **标签管理**: 学生标签的增删改查

### 4. 我的班级
- 选择班级查看
- 展示课堂画面（学生卡通形象）
- 根据班级人数自动计算座位布局
- 点击学生查看信息卡片
- 点击成绩查看近 6 个月成绩变化曲线
- 点击老师查看班级信息
- 点击平均分查看近 6 个月平均成绩变化曲线

### 5. 成绩分析
- 多维度成绩分析
- 成绩趋势图表
- 班级对比分析
- 个人成绩追踪

### 6. 工具箱
- **PDF 转 Word**: 支持 PDF 文件转换为 Word 文档
- 转换进度显示
- 文件下载

## 📊 数据库表结构

| 表名 | 说明 | 主要字段 |
|------|------|----------|
| grades | 年级表 | id, name, created_at, updated_at |
| classes | 班级表 | id, name, grade_id, teacher_id, created_at, updated_at |
| users | 用户表 | id, username, password_hash, role, real_name, created_at, updated_at |
| subjects | 学科表 | id, name, created_at, updated_at |
| students | 学生表 | id, name, class_id, student_no, gender, created_at, updated_at |
| scores | 成绩表 | id, student_id, subject_id, score, exam_type, exam_date, created_at, updated_at |
| tags | 标签表 | id, name, color, created_at, updated_at |
| student_tags | 学生标签关联表 | id, student_id, tag_id, created_at |
| schedules | 课程表 | id, class_id, subject_id, teacher_id, day_of_week, start_time, end_time, created_at, updated_at |

## 🔌 API 接口

### 认证模块
- `POST /api/auth/login` - 用户登录
- `POST /api/auth/logout` - 用户登出
- `GET /api/auth/me` - 获取当前用户信息

### 年级管理
- `GET /api/grades` - 获取年级列表
- `POST /api/grades` - 创建年级
- `PUT /api/grades/{id}` - 更新年级
- `DELETE /api/grades/{id}` - 删除年级

### 班级管理
- `GET /api/classes` - 获取班级列表
- `POST /api/classes` - 创建班级
- `PUT /api/classes/{id}` - 更新班级
- `DELETE /api/classes/{id}` - 删除班级

### 学生管理
- `GET /api/students` - 获取学生列表
- `POST /api/students` - 创建学生
- `PUT /api/students/{id}` - 更新学生
- `DELETE /api/students/{id}` - 删除学生
- `POST /api/students/import` - 批量导入学生

### 成绩管理
- `GET /api/scores` - 获取成绩列表
- `POST /api/scores` - 创建成绩
- `PUT /api/scores/{id}` - 更新成绩
- `DELETE /api/scores/{id}` - 删除成绩
- `POST /api/scores/import` - 批量导入成绩

### 课程表管理
- `GET /api/schedules` - 获取课程表
- `POST /api/schedules` - 创建课程
- `PUT /api/schedules/{id}` - 更新课程
- `DELETE /api/schedules/{id}` - 删除课程

### 标签管理
- `GET /api/tags` - 获取标签列表
- `POST /api/tags` - 创建标签
- `PUT /api/tags/{id}` - 更新标签
- `DELETE /api/tags/{id}` - 删除标签

### 用户管理
- `GET /api/users` - 获取用户列表
- `POST /api/users` - 创建用户
- `PUT /api/users/{id}` - 更新用户
- `DELETE /api/users/{id}` - 删除用户

### 仪表盘
- `GET /api/dashboard/schedule` - 获取今日课程表
- `GET /api/dashboard/stats` - 获取统计数据

### 成绩分析
- `GET /api/grade-analysis/class` - 班级成绩分析
- `GET /api/grade-analysis/student` - 学生成绩分析
- `GET /api/grade-analysis/trend` - 成绩趋势分析

### 工具
- `POST /api/tools/pdf2docx` - PDF 转 Word
- `GET /api/tools/download/{filename}` - 下载转换后的文件

## 📝 成绩类型

- **月考** - 每月定期考试
- **期中考试** - 学期中期考试
- **期末考试** - 学期末考试
- **随堂测验** - 日常课堂测验

## 💻 开发指南

### 后端开发

```bash
# 安装依赖
cd backend
pip install -r requirements.txt

# 启动开发服务器
python -m uvicorn main:app --reload --port 8000

# 访问 API 文档
# http://localhost:8000/docs
```

### 前端开发

```bash
# 安装依赖
cd frontend
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build

# 预览生产构建
npm run preview
```

### 代码规范

- 后端遵循 PEP 8 规范
- 前端使用 ESLint 进行代码检查
- 提交前请运行 `npm run lint` 检查前端代码

## 📄 License

MIT License

## 👥 贡献

欢迎提交 Issue 和 Pull Request！

## 📞 联系方式

如有问题或建议，请联系开发团队。
