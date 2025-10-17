JeecgBoot 低代码开发平台（单体架构版）
===============

当前版本： 3.8.3（发布日期：2025-10-09）

[![AUR](https://img.shields.io/badge/license-Apache%20License%202.0-blue.svg)](https://github.com/zhangdaiscott/jeecg-boot/blob/master/LICENSE)
[![](https://img.shields.io/badge/Author-北京国炬软件-orange.svg)](http://jeecg.com/aboutusIndex)
[![](https://img.shields.io/badge/version-3.8.3-brightgreen.svg)](https://github.com/zhangdaiscott/jeecg-boot)
[![GitHub stars](https://img.shields.io/github/stars/zhangdaiscott/jeecg-boot.svg?style=social&label=Stars)](https://github.com/zhangdaiscott/jeecg-boot)
[![GitHub forks](https://img.shields.io/github/forks/zhangdaiscott/jeecg-boot.svg?style=social&label=Fork)](https://github.com/zhangdaiscott/jeecg-boot)

## 项目介绍

**企业级AI低代码平台 - 单体架构版本**

JeecgBoot 是一款基于BPM流程和代码生成的AI低代码平台，助力企业快速实现低代码开发和构建AI应用。

本项目采用**单体架构**配置，移除了微服务相关组件，专注于简单高效的部署和开发。

### 当前架构特点

- ✅ **单体架构**：简化部署，一个jar包即可运行
- ✅ **PostgreSQL数据库**：强大的开源关系型数据库，支持向量搜索
- ✅ **Redis缓存**：高性能内存数据库
- ✅ **零代码配置**：Docker快速搭建开发环境

## 技术架构

### 后端技术栈
- **基础框架**：Spring Boot 3.5.5
- **持久层框架**：MybatisPlus 3.5.12
- **安全框架**：Apache Shiro 2.0.4，Jwt 4.5.0
- **数据库连接池**：阿里巴巴Druid 1.2.24
- **报表工具**：JimuReport 2.1.3
- **AI大模型**：支持 ChatGPT、DeepSeek、千问等
- **缓存**：Redis
- **数据库**：PostgreSQL（支持向量搜索）

### 项目结构
```
jeecg-boot/
├── jeecg-boot-base-core/          # 共通模块：工具类、config、权限等
├── jeecg-module-system/           # System系统管理目录
│   ├── jeecg-system-biz/          # 系统管理业务逻辑
│   ├── jeecg-system-start/        # 单体启动项目(8080端口)
│   └── jeecg-system-api/          # 系统管理模块API
│       └── jeecg-system-local-api/ # 单体应用接口
├── jeecg-boot-module/             # 其他功能模块
│   └── jeecg-boot-module-airag/   # AI相关功能模块
├── db/                            # 数据库脚本
│   ├── Dockerfile                 # PostgreSQL容器配置
│   └── 其他数据库脚本/
│       └── jeecgboot-postgresql17.sql  # PostgreSQL数据库脚本
└── docker-compose.yml             # 开发环境容器编排
```

## 快速开始

### 环境要求
- **Java**: JDK 17+ (推荐 JDK 17)
- **数据库**: PostgreSQL 12+
- **缓存**: Redis 5.0+
- **构建工具**: Maven 3.6+

### 1. 启动开发环境（Docker方式）

```bash
# 启动PostgreSQL和Redis
docker-compose up -d jeecg-boot-postgres jeecg-boot-redis
```

### 2. 修改数据库配置

确保应用配置文件中的数据库连接正确：

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/jeecgboot
    username: postgres
    password: postgres
  redis:
    host: localhost
    port: 6379
```

### 3. 构建和运行应用

```bash
# 构建项目
mvn clean compile

# 打包应用
mvn clean package

# 运行应用
java -jar jeecg-module-system/jeecg-system-start/target/jeecg-system-start-3.8.3.jar
```

### 4. 访问系统

- **系统地址**: http://localhost:8080
- **默认账号**: admin / 123456

## 开发指南

### 本地开发环境搭建

1. **启动基础服务**
   ```bash
   # 启动PostgreSQL和Redis
   docker-compose up -d
   ```

2. **IDEA导入项目**
   - File -> Open -> 选择项目根目录
   - 等待Maven依赖下载完成
   - 安装Lombok插件

3. **配置数据库**
   - PostgreSQL连接信息：`localhost:5432/jeecgboot`
   - 用户名/密码：`postgres/postgres`

4. **运行启动类**
   - 找到 `JeecgSystemApplication.java`
   - 右键运行

### 代码生成

系统提供强大的代码生成器，支持：
- 单表CRUD
- 树形结构
- 一对多关系
- 主子表关系

访问路径：系统管理 -> 代码生成器

## Docker部署

### 开发环境
```bash
# 启动数据库和缓存
docker-compose up -d

# 运行应用
java -jar jeecg-system-start-3.8.3.jar
```

### 生产环境部署
```bash
# 1. 构建应用
mvn clean package -DskipTests

# 2. 上传jar包到服务器
# 3. 启动应用
java -jar -Xms512m -Xmx2048m jeecg-system-start-3.8.3.jar
```

## 数据库支持

| 数据库 | 支持状态 | 说明 |
|--------|----------|------|
| PostgreSQL | ✅ | 主要支持，包含向量搜索功能 |
| MySQL | ❌ | 已移除相关配置 |
| Oracle | ❌ | 已移除相关脚本 |
| SQL Server | ❌ | 已移除相关脚本 |

## 功能特性

### 核心功能
- ✅ 用户权限管理（RBAC）
- ✅ 部门组织管理
- ✅ 数据字典管理
- ✅ 在线表单设计
- ✅ 代码生成器
- ✅ 报表设计器
- ✅ 工作流引擎
- ✅ 定时任务

### AI功能
- ✅ AI对话助手
- ✅ AI知识库问答
- ✅ AI应用搭建
- ✅ 大模型管理（支持ChatGPT、DeepSeek等）
- ✅ 流程编排

### 高级功能
- ✅ 多数据源支持
- ✅ 分布式文件存储
- ✅ 消息中心
- ✅ 系统监控
- ✅ 日志管理

## 技术支持

- **官方网站**: [http://www.jeecg.com](http://www.jeecg.com)
- **技术文档**: [https://help.jeecg.com](https://help.jeecg.com)
- **问题反馈**: [GitHub Issues](https://github.com/jeecgboot/JeecgBoot/issues)
- **QQ交流群**: 964611995

## 版本说明

本版本为**单体架构优化版**，主要变更：

### ✅ 保留
- Spring Boot 3.5.5 基础框架
- PostgreSQL数据库支持
- Redis缓存支持
- AI功能模块
- 所有核心业务功能

### ❌ 移除
- 微服务架构（Spring Cloud、Nacos等）
- MySQL数据库配置
- Docker应用容器化
- 其他数据库脚本（Oracle、SQL Server等）
- 复杂的部署配置

### 🎯 优化目标
- 简化部署流程
- 降低运维复杂度
- 提高开发效率
- 专注核心功能

## 许可证

本项目基于 [Apache License 2.0](https://github.com/zhangdaiscott/jeecg-boot/blob/master/LICENSE) 开源协议。

---

**注意**: 本版本针对单体应用进行了优化，如需微服务版本，请参考官方原版项目。