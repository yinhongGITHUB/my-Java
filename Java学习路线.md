# Java 学习路线（前端转Java版）

> 适合有前端基础、Java 零基础的开发者，循序渐进，逐步进阶。

---

## 阶段一：Java 基础语法

**目标：** 能读懂并写出基础 Java 程序

- [ ] 安装 JDK（推荐 JDK 17 LTS）
- [ ] 配置开发工具（IntelliJ IDEA 社区版 / VS Code + Java 插件）
- [ ] 基本数据类型（int、double、boolean、char）
- [ ] 变量与常量（var、final）
- [ ] 运算符（算术、比较、逻辑）
- [ ] 流程控制：`if / else`、`switch`
- [ ] 循环：`for`、`while`、`do-while`、`break / continue`
- [ ] 方法（函数）定义与调用、参数与返回值
- [ ] 数组（一维、二维）
- [ ] 字符串（`String` 常用方法）

**推荐练习：**

- 编写计算器程序
- 输出九九乘法表
- 字符串反转与回文检测

---

## 阶段二：面向对象编程（OOP）

**目标：** 理解面向对象思想，掌握 Java 核心概念

- [ ] 类与对象（class、new、构造方法）
- [ ] 封装（private、getter/setter）
- [ ] 继承（extends、super、方法重写）
- [ ] 多态（向上转型、方法重载）
- [ ] 抽象类（abstract）
- [ ] 接口（interface、implements）
- [ ] 静态成员（static）
- [ ] 常用类：`String`、`StringBuilder`、`Math`、`Date`、包装类

**推荐练习：**

- 设计一个"动物"类层级（Animal → Dog/Cat）
- 用接口实现可扩展的图形计算（Shape → Circle/Rectangle）

---

## 阶段三：Java 核心进阶

**目标：** 掌握日常开发必用的核心工具包

- [ ] 集合框架
  - `List`（ArrayList、LinkedList）
  - `Set`（HashSet、TreeSet）
  - `Map`（HashMap、LinkedHashMap）
  - 迭代器（Iterator）
- [ ] 泛型（`<T>`）
- [ ] 异常处理（`try-catch-finally`、自定义异常、`throws`）
- [ ] 枚举（`enum`）
- [ ] 注解（`@Override`、自定义注解基础）

**推荐练习：**

- 用 Map 实现单词词频统计
- 自定义异常类并在业务逻辑中抛出

---

## 阶段四：Java 实用技能

**目标：** 具备实际项目开发能力

- [ ] 文件读写（`File`、`FileReader/Writer`、`BufferedReader`）
- [ ] NIO 基础（`Path`、`Files`）
- [ ] Lambda 表达式（`() -> {}`）
- [ ] Stream API（`filter`、`map`、`collect`、`reduce`）
- [ ] Optional（避免 NPE）
- [ ] 多线程基础（`Thread`、`Runnable`、`synchronized`）
- [ ] 线程池（`ExecutorService`）

**推荐练习：**

- 用 Stream API 处理学生成绩列表（排序、过滤、求均值）
- 读取 CSV 文件并写入新文件

---

## 阶段五：后端开发入门

**目标：** 能独立搭建后端接口，与前端联调

- [ ] Maven / Gradle 项目管理（依赖、构建）
- [ ] Spring Boot 快速入门
  - 项目创建（Spring Initializr）
  - `@RestController`、`@GetMapping`、`@PostMapping`
  - 返回 JSON 数据
  - 接收请求参数（`@RequestParam`、`@PathVariable`、`@RequestBody`）
- [ ] 数据库基础（MySQL）
  - 增删改查 SQL
  - 使用 MyBatis / Spring Data JPA 操作数据库
- [ ] 跨域配置（CORS）
- [ ] 接口文档（Swagger / Knife4j）

**推荐练习：**

- 搭建一个 RESTful 用户管理接口（增删改查）
- 前端调用自己写的 Java 接口

---

## 阶段六：项目实战与工程化

**目标：** 具备独立完成后端项目的能力

- [ ] 项目结构规范（Controller → Service → Repository 三层架构）
- [ ] 全局异常处理（`@ExceptionHandler`）
- [ ] 统一返回格式封装
- [ ] 日志（SLF4J + Logback）
- [ ] 单元测试（JUnit 5、Mockito）
- [ ] 配置管理（`application.yml`、多环境配置）
- [ ] 项目打包与部署（`jar` 包、Docker 基础）

**推荐实战项目：**

- 博客系统（文章增删改查 + 用户登录）
- Todo List 全栈应用（前端 + Spring Boot 后端）

---

## 推荐资源

### 视频课程

| 资源                       | 说明                     |
| -------------------------- | ------------------------ |
| B站 - 黑马程序员 Java 入门 | 免费，内容全面，适合入门 |
| B站 - 尚硅谷 Spring Boot 3 | Spring Boot 最新版教程   |

### 书籍

| 书名                  | 阶段         |
| --------------------- | ------------ |
| 《Java 核心技术 卷I》 | 基础进阶必读 |
| 《Spring Boot 实战》  | 后端开发参考 |

### 刷题 & 练习

- [LeetCode](https://leetcode.cn)（使用 Java 解题）
- [牛客网](https://www.nowcoder.com)（Java 基础题库）

---

## 学习时间建议

| 阶段             | 建议时长 |
| ---------------- | -------- |
| 阶段一：基础语法 | 2～3 周  |
| 阶段二：面向对象 | 2～3 周  |
| 阶段三：核心进阶 | 2 周     |
| 阶段四：实用技能 | 2 周     |
| 阶段五：后端入门 | 3～4 周  |
| 阶段六：项目实战 | 持续进行 |

> 每天保持 1～2 小时学习，约 3～4 个月可具备独立开发能力。
