# StudyFlow - 学习任务管理系统

## 项目简介

StudyFlow 是一个面向学生的学习任务管理系统，支持个人任务管理与学习进度跟踪。系统采用分层架构设计，提供清晰的任务管理和进度可视化功能，帮助学生高效规划学习计划。

## 系统角色

| 角色 | 类型 | 描述 |
|------|------|------|
| **个人用户（User）** | 学生 | 系统的唯一用户角色，可以创建和管理个人学习任务、跟踪学习进度、查看统计报告 |

系统面向学生个人使用，每位用户拥有独立的个人任务管理空间。

## 功能特性

- 用户注册与登录
- 学习任务的创建、编辑、删除
- 任务状态管理（未开始/进行中/已完成）
- 任务分类与标签
- 截止日期与优先级设置
- 学习进度统计与可视化
- 任务提醒通知

## 目录结构

```
studyflow/
├── src/
│   ├── domain/              # 领域层：核心业务实体与规则
│   ├── application/         # 应用层：用例与业务流程编排
│   ├── infrastructure/      # 基础设施层：数据持久化与外部服务
│   └── interfaces/          # 接口层：API 控制器与前端接口
├── test/                    # 测试文件
├── docs/                    # 项目文档
├── package.json             # 项目配置与依赖
├── tsconfig.json            # TypeScript 配置
└── README.md                # 项目说明文档
```

## 模块简介

### domain（领域层）

负责定义核心业务实体、值对象、领域服务及业务规则。

- **Entity**: Task（任务）、User（用户）等核心实体
- **ValueObject**: TaskStatus（任务状态）、Priority（优先级）等
- **DomainService**: 业务规则校验逻辑
- **Repository Interface**: 仓储接口定义

核心业务规则：
1. 任务截止时间不能早于创建时间
2. 已完成任务不能修改为未开始状态
3. 高优先级任务必须具有截止日期

### application（应用层）

协调领域对象完成业务用例，负责业务流程编排。

- **UseCase**: CreateTaskUseCase、UpdateTaskUseCase、TrackProgressUseCase 等
- **DTO**: 数据传输对象定义
- **ApplicationService**: 应用服务，协调多个用例

### infrastructure（基础设施层）

提供技术实现，支持数据持久化、外部服务集成等。

- **Persistence**: 数据库实现（SQLite/PostgreSQL）
- **Repository**: 仓储接口的具体实现
- **ExternalService**: 邮件通知、日志等外部服务
- **Config**: 配置管理与环境变量

### interfaces（接口层）

暴露系统接口，处理外部请求与响应。

- **Controller**: REST API 控制器
- **Routes**: 路由定义
- **Middleware**: 认证、日志、错误处理中间件
- **ViewModel**: 视图模型与响应格式化

## 运行方式

### 环境要求

- Node.js >= 18.0.0
- npm >= 9.0.0

### 安装依赖

```bash
npm install
```

### 开发模式运行

```bash
npm run dev
```

### 编译项目

```bash
npm run build
```

### 生产模式运行

```bash
npm start
```

### 运行测试

```bash
npm test
```

### 代码格式化

```bash
npm run format
```

### 代码检查

```bash
npm run lint
```

## 持续集成

项目已预配 GitHub Actions 与 Gitee Go 两套 CI 配置。

| CI 平台 | 配置文件 | 触发条件 |
|---------|----------|----------|
| GitHub Actions | `.github/workflows/ci.yml` | push / PR 到 master |
| Gitee Go | `.gitee/workflows/ci.yml` | push / PR 到 master |

每次自动执行：
```
checkout → setup-node (Node 20) → npm ci → npm run lint → npm test → 保存报告
```

### CI 状态

[![CI](https://github.com/your-org/studyflow/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/studyflow/actions/workflows/ci.yml)

> ⚠️ 更换仓库地址后请替换上方 badge 链接地址。

### 在本地模拟 CI 流程

```bash
npm ci            # 1. 纯净安装
npm run lint      # 2. 代码检查
npm test          # 3. 运行测试
```

---

## 技术栈

- **语言**: TypeScript
- **运行时**: Node.js
- **测试框架**: Jest
- **代码规范**: ESLint + Prettier
- **架构模式**: 领域驱动设计（DDD）分层架构

## API 概览

| 方法 | 路径 | 描述 |
|------|------|------|
| POST | /api/auth/register | 用户注册 |
| POST | /api/auth/login | 用户登录 |
| GET | /api/tasks | 获取任务列表 |
| POST | /api/tasks | 创建任务 |
| PUT | /api/tasks/:id | 更新任务 |
| DELETE | /api/tasks/:id | 删除任务 |
| GET | /api/progress | 获取进度统计 |
| GET | /api/health | 健康检查 |

## 项目状态

- **测试**: 73 个测试用例，全部通过
- **代码检查**: ESLint 0 error
- **架构**: DDD 四层架构（domain / application / infrastructure / interfaces）
- **服务器**: Express 已集成，`npm run dev` 启动监听 3000 端口

## 许可证

MIT License