# 阶段一：Java 基础语法

> 目标：能读懂并写出基础 Java 程序
> 建议时长：2～3 周

---

## 1. 环境搭建

### 1.1 安装 JDK（macOS）

**方式一：Homebrew 安装（推荐，全程一行命令）**

首先检查是否已安装 Homebrew，打开终端输入：

```bash
brew --version
```

- 有输出（如 `Homebrew 4.x.x`）→ 已安装，直接跳到下一步
- 提示 `command not found` → 未安装，先执行以下命令安装：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> `/bin/bash -c "..."` 的意思是：用系统自带的 bash 执行从网上下载的 Homebrew 安装脚本。

安装好 Homebrew 后，继续安装：

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

然后安装 JDK 17：

```bash
brew install --cask temurin@17
```

安装完成后验证：

```bash
java -version
# 输出：openjdk version "17.x.x" ...
```

> Homebrew 会自动配置环境变量，无需手动修改任何配置文件。

---

**方式二：安装包（纯傻瓜式，不用命令行）**

1. 访问 [https://adoptium.net](https://adoptium.net)，选择 **JDK 17**，下载 macOS `.pkg` 文件
2. 双击 `.pkg`，一路点"继续"安装完成
3. 打开终端，验证安装：
   ```bash
   java -version
   ```
4. 手动配置环境变量，在 `~/.zshrc` 末尾添加：
   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home -v 17)
   export PATH=$JAVA_HOME/bin:$PATH
   ```
   然后执行：
   ```bash
   source ~/.zshrc
   ```

### 1.2 用 jenv 管理多个 JDK 版本（可选）

如果你电脑上安装了多个版本的 JDK，可以用 **jenv** 来随时切换（类似 node 的 nvm）。

按顺序执行以下命令完成全部配置：

```bash
# 1. 安装 jenv
brew install jenv

# 2. 配置环境变量
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
source ~/.zshrc

# 3. 安装 JDK 8、21（JDK 17 已安装可跳过）
brew install --cask temurin@8
brew install --cask temurin@21

# 4. 将所有版本注册到 jenv
jenv add $(/usr/libexec/java_home -v 1.8)
jenv add $(/usr/libexec/java_home -v 17)
jenv add $(/usr/libexec/java_home -v 21)

# 5. 验证
jenv versions
```

**常用命令：**

```bash
jenv versions          # 查看所有已注册的 JDK 版本
jenv global 17         # 全局默认使用 JDK 17
jenv local 1.8         # 仅当前目录使用 JDK 8（会生成 .java-version 文件）
java -version          # 验证当前版本
```

> 注意：JDK 8 在 jenv 中版本号显示为 `1.8`，JDK 17 和 21 直接用 `17`、`21`。

### 1.3 安装 Maven（项目管理工具）

Maven 是 Java 最常用的项目管理和构建工具，负责依赖管理、自动编译打包等。

**安装方法（推荐 Homebrew）：**

```bash
brew install maven
```

安装完成后，验证版本：

```bash
mvn -version
# 输出包含 Maven 版本号、Java 版本等信息
```

**常用命令：**

```bash
mvn -v                # 查看 Maven 版本
mvn clean             # 清理项目生成的 target 目录
mvn compile           # 编译项目
mvn test              # 运行测试
mvn package           # 打包（生成 jar/war 文件）
mvn install           # 安装到本地仓库
mvn dependency:tree   # 查看依赖树
```

> Maven 的配置文件为 `pom.xml`，新手常用 IDEA/VS Code 自动生成项目即可。

---

### 1.3 安装开发工具

使用 **VS Code**，安装 **Extension Pack for Java** 即可，它包含了所有常用 Java 插件：

- Language Support for Java(TM) by Red Hat
- Debugger for Java
- Test Runner for Java
- Maven for Java
- Project Manager for Java

安装方式：打开 VS Code，按 `⇧Shift + ⌘Cmd + X` 打开扩展面板，搜索 `Extension Pack for Java` 安装即可。

### 1.3 第一个 Java 程序

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

> 与前端对比：Java 的 `main` 方法相当于程序的入口，类似 JS 脚本的顶层执行代码。

---

## 2. 基本数据类型

Java 是**强类型语言**，变量必须声明类型。

| 类型      | 说明         | 示例                  | 对应 JS 类型       |
| --------- | ------------ | --------------------- | ------------------ |
| `int`     | 整数         | `int age = 18;`       | `number`           |
| `long`    | 长整数       | `long num = 100L;`    | `number`           |
| `double`  | 浮点数       | `double pi = 3.14;`   | `number`           |
| `float`   | 单精度浮点   | `float f = 1.5f;`     | `number`           |
| `boolean` | 布尔值       | `boolean ok = true;`  | `boolean`          |
| `char`    | 单个字符     | `char c = 'A';`       | `string`（单字符） |
| `String`  | 字符串（类） | `String s = "hello";` | `string`           |

```java
int age = 25;
double salary = 8888.88;
boolean isStudent = false;
char grade = 'A';
String name = "张三";

System.out.println("姓名：" + name + "，年龄：" + age);
```

### 类型转换

```java
// 自动转换（小转大，安全）
int a = 10;
double b = a;      // int → double，自动

// 强制转换（大转小，可能丢失精度）
double x = 9.99;
int y = (int) x;   // y = 9，小数部分被截断

// 字符串转数字
int num = Integer.parseInt("123");
double d = Double.parseDouble("3.14");

// 数字转字符串
String s = String.valueOf(100);
String s2 = 100 + "";   // 也可以这样
```

---

## 3. 变量与常量

```java
// 变量：可以改变
int count = 0;
count = 10;

// 常量：用 final 修饰，不可修改（类似 JS 的 const）
final double PI = 3.14159;
// PI = 3.0;  // 报错！

// var：Java 10+，类型推断（类似 JS 的 let）
var message = "Hello";   // 推断为 String
var number = 42;          // 推断为 int
```

---

## 4. 运算符

### 4.1 算术运算符

```java
int a = 10, b = 3;

System.out.println(a + b);   // 13
System.out.println(a - b);   // 7
System.out.println(a * b);   // 30
System.out.println(a / b);   // 3（整数除法，舍去小数）
System.out.println(a % b);   // 1（取余）

// 自增 / 自减
int x = 5;
x++;   // x = 6
x--;   // x = 5
```

### 4.2 比较运算符

```java
int a = 10, b = 20;

System.out.println(a > b);    // false
System.out.println(a < b);    // true
System.out.println(a >= 10);  // true
System.out.println(a == b);   // false
System.out.println(a != b);   // true
```

> ⚠️ 注意：Java 中 `==` 比较基本类型的值，但比较对象时比较的是**引用地址**，字符串比较要用 `.equals()`。

```java
String s1 = new String("hello");
String s2 = new String("hello");

System.out.println(s1 == s2);       // false（引用不同）
System.out.println(s1.equals(s2));  // true（内容相同）
```

### 4.3 逻辑运算符

```java
boolean a = true, b = false;

System.out.println(a && b);   // false（与）
System.out.println(a || b);   // true（或）
System.out.println(!a);       // false（非）
```

---

## 5. 流程控制

### 5.1 if / else

```java
int score = 85;

if (score >= 90) {
    System.out.println("优秀");
} else if (score >= 70) {
    System.out.println("良好");
} else if (score >= 60) {
    System.out.println("及格");
} else {
    System.out.println("不及格");
}
```

### 5.2 switch

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("周一");
        break;
    case 2:
        System.out.println("周二");
        break;
    case 3:
        System.out.println("周三");
        break;
    default:
        System.out.println("其他");
}

// Java 14+ 新写法（推荐）
String result = switch (day) {
    case 1 -> "周一";
    case 2 -> "周二";
    case 3 -> "周三";
    default -> "其他";
};
System.out.println(result);
```

---

## 6. 循环

### 6.1 for 循环

```java
// 基本 for 循环
for (int i = 0; i < 5; i++) {
    System.out.println("第 " + i + " 次");
}

// 增强 for 循环（遍历数组/集合，类似 JS 的 for...of）
int[] numbers = {1, 2, 3, 4, 5};
for (int num : numbers) {
    System.out.println(num);
}
```

### 6.2 while 循环

```java
int count = 0;
while (count < 5) {
    System.out.println("count = " + count);
    count++;
}
```

### 6.3 do-while 循环

```java
// 至少执行一次
int n = 0;
do {
    System.out.println("n = " + n);
    n++;
} while (n < 3);
```

### 6.4 break 与 continue

```java
for (int i = 0; i < 10; i++) {
    if (i == 3) continue;   // 跳过 i=3
    if (i == 7) break;      // 遇到 i=7 停止
    System.out.println(i);  // 输出：0 1 2 4 5 6
}
```

---

## 7. 方法（函数）

Java 中的方法必须定义在类中。

```java
public class Calculator {

    // 定义方法：返回类型 方法名(参数类型 参数名)
    public static int add(int a, int b) {
        return a + b;
    }

    // 无返回值用 void
    public static void printHello(String name) {
        System.out.println("Hello, " + name + "!");
    }

    // 方法重载：同名不同参数
    public static double add(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        int result = add(3, 5);
        System.out.println(result);     // 8

        printHello("张三");             // Hello, 张三!

        double r2 = add(1.5, 2.5);
        System.out.println(r2);         // 4.0
    }
}
```

---

## 8. 数组

```java
// 声明并初始化
int[] scores = {90, 85, 78, 92, 88};

// 声明后赋值
String[] names = new String[3];
names[0] = "张三";
names[1] = "李四";
names[2] = "王五";

// 获取长度
System.out.println(scores.length);   // 5

// 遍历数组
for (int i = 0; i < scores.length; i++) {
    System.out.println(scores[i]);
}

// 二维数组
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
System.out.println(matrix[1][2]);   // 6
```

### 数组工具类 Arrays

```java
import java.util.Arrays;

int[] arr = {5, 3, 1, 4, 2};

Arrays.sort(arr);                        // 排序
System.out.println(Arrays.toString(arr)); // [1, 2, 3, 4, 5]

int[] copy = Arrays.copyOf(arr, 3);      // 复制前3个元素
```

---

## 9. 字符串（String）

```java
String s = "Hello, Java!";

// 常用方法
System.out.println(s.length());           // 12，字符串长度
System.out.println(s.toUpperCase());      // HELLO, JAVA!
System.out.println(s.toLowerCase());      // hello, java!
System.out.println(s.contains("Java"));   // true
System.out.println(s.startsWith("Hello")); // true
System.out.println(s.endsWith("!"));      // true
System.out.println(s.indexOf("Java"));    // 7
System.out.println(s.substring(7));       // Java!
System.out.println(s.substring(7, 11));   // Java
System.out.println(s.replace("Java", "World")); // Hello, World!
System.out.println(s.trim());             // 去除首尾空白

// 分割
String csv = "a,b,c,d";
String[] parts = csv.split(",");          // ["a", "b", "c", "d"]

// 拼接（大量拼接推荐用 StringBuilder）
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(", ");
sb.append("Java!");
System.out.println(sb.toString());        // Hello, Java!
```

---

## 10. 阶段练习

### 练习一：计算器

编写一个方法，接收两个数字和一个运算符（`+`、`-`、`*`、`/`），返回计算结果。

```java
public static double calculate(double a, double b, char op) {
    // 请实现这个方法
}
```

### 练习二：九九乘法表

用循环输出如下格式：

```
1×1=1
1×2=2  2×2=4
1×3=3  2×3=6  3×3=9
...
```

### 练习三：字符串工具方法

1. 实现字符串反转（不使用 `StringBuilder.reverse()`）
2. 判断一个字符串是否是回文（如 `"madam"`）
3. 统计字符串中某个字符出现的次数

### 练习四：数组操作

1. 找出数组中的最大值和最小值
2. 计算数组所有元素的平均值
3. 将数组元素逆序排列（不使用库函数）

---

## 知识点速查

| 概念       | Java 写法                      | JS 类比                      |
| ---------- | ------------------------------ | ---------------------------- |
| 变量声明   | `int a = 1;`                   | `let a = 1`                  |
| 常量       | `final int A = 1;`             | `const A = 1`                |
| 打印输出   | `System.out.println()`         | `console.log()`              |
| 字符串拼接 | `"hello" + name`               | `` `hello ${name}` ``        |
| 类型判断   | `a instanceof String`          | `typeof a === 'string'`      |
| 数组长度   | `arr.length`                   | `arr.length`                 |
| 字符串长度 | `str.length()`（方法，有括号） | `str.length`（属性，无括号） |

---

## 下一步

完成本阶段后，进入 **[阶段二：面向对象编程（OOP）](./阶段二：面向对象编程.md)**
