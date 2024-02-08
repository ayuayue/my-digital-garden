---
tags: [java]
title: Java 开发环境
date: 2023-05-28T13:40:53+08:00
lastmod: 2023-05-28T13:40:59+08:00
dg-publish: true
dg-pinned: false
dg-hide: false
dg-hide-in-graph: false
---

本文在 ChatGPT 协助下进行完成，如有错误请指正。

## JDK 介绍

JDK（Java Development Kit）是 Java 开发工具包，它是用于开发、编译、调试和运行 Java 应用程序的软件包。JDK 由 Oracle（以前是 Sun Microsystems）提供，并且是 Java 平台的核心组件。

JDK包含以下主要组件：

1. Java编译器（javac）：用于将Java源代码编译成Java字节码，可以在Java虚拟机（JVM）上执行。

2. Java运行时环境（JRE）：JDK包含JRE，用于执行已编译的Java程序。它包含Java虚拟机（JVM）和Java类库（Java API），使得Java程序可以在不同的操作系统上运行。

3. Java类库：JDK提供了广泛的Java类库，包含了大量的预定义类和方法，用于各种用途，例如字符串处理、输入输出、网络通信、图形界面等。

4. 调试工具：JDK提供了强大的调试工具，如Java调试器（jdb）和Java虚拟机监视器（jvisualvm），用于帮助开发人员诊断和解决代码中的问题。

5. 其他实用工具：JDK还包含其他实用工具，如Java文档生成器（javadoc）用于生成文档、Java格式化工具（javafmt）用于格式化代码等。

总之，JDK 是 Java 开发者必备的工具包，它提供了一切必要的组件，让开发者能够轻松地创建、编译、调试和运行 Java 应用程序。

## 下载安装

SpringBoot 官方推荐的环境：[Download Java | Java 8, Java 11, Java 17, Java 20 - OpenJDK Builds for Linux, Windows & macOS](https://bell-sw.com/pages/downloads/#/java-17-lts)

配置 JDK 环境需要以下步骤：

1. 下载JDK：首先，从Oracle官方网站或其他可信来源下载适用于您操作系统的JDK安装程序。确保下载与您操作系统版本对应的JDK。

2. 安装JDK：运行下载的JDK安装程序，并按照安装向导的指示完成安装过程。选择合适的安装路径，一般情况下，安装程序会自动配置环境变量，但请确保您选中了“自动配置环境变量”选项。

3. 配置环境变量（Windows系统）：如果安装程序未自动配置环境变量，您需要手动进行配置。打开控制面板 -> 系统和安全 -> 系统 -> 高级系统设置 -> 环境变量。在“系统变量”下，找到名为"PATH"的变量，并添加JDK的安装路径（例如：`C:\Program Files\Java\jdk1.8.0_XXX\bin`）到该变量的值中。

4. 配置环境变量（macOS和Linux系统）：打开终端，并编辑`~/.bashrc`、`~/.bash_profile`或`~/.profile`文件，根据您使用的Shell类型，添加以下内容： 
   ```
   export JAVA_HOME=/path/to/your/jdk
   export PATH=$PATH:$JAVA_HOME/bin
   ```
   请将`/path/to/your/jdk`替换为您实际的JDK安装路径。

5. 验证配置：打开一个新的终端或命令提示符窗口，并输入`java -version`命令。如果正确配置了JDK环境，会显示已安装的JDK版本信息。

完成上述步骤后，您的 JDK 环境就配置好了。现在您可以使用 Java 编译器（javac）和 Java 运行时环境（JRE）来开发和运行 Java 程序了。

## 关于 Maven 

Maven 是一个流行的项目管理工具，用于构建、管理和发布 Java 项目。它提供了一种结构化的项目管理方法，允许开发人员在不同项目中共享依赖库和构建配置，从而简化了项目的构建过程。

以下是 Maven 的主要特点和用途：

1. 项目构建：Maven 使用 XML 配置文件（pom. Xml）来描述项目的依赖关系、目录结构和构建过程。通过定义项目的依赖和插件，Maven 可以自动下载所需的依赖库并执行编译、测试和打包等构建任务。

2. 依赖管理：Maven 通过中央仓库（Maven Central Repository）来管理大量的开源 Java 库和工具。在 pom. Xml 中定义依赖后，Maven 会自动下载所需的 JAR 文件，并将它们添加到项目的类路径中。

3. 项目生命周期管理：Maven 定义了一组标准化的构建阶段（build phases）和目标（goals），例如编译、测试、打包、部署等。开发人员可以通过执行特定的 Maven 命令来触发这些构建阶段和目标。

4. 插件扩展：Maven 支持插件机制，允许开发人员扩展构建过程和添加自定义任务。许多常见的构建任务，如静态代码分析、文档生成等，都可以通过插件来实现。

5. 多模块项目支持：Maven 可以管理多模块项目，允许将大型项目拆分为多个子模块，并在整个项目中共享依赖和配置。

6. 依赖范围管理：Maven 支持定义依赖的范围，例如编译时依赖、测试时依赖等，以便在不同的构建阶段使用不同的依赖库。

总体而言，Maven 简化了 Java 项目的构建过程，提供了一种标准化的项目管理方法，使得项目构建和依赖管理更加高效和可靠。通过使用 Maven，开发人员可以更专注于编写代码，而无需过多关注项目的构建细节。

### 安装 Maven 

如果使用 IDEA 开发，IDEA 自带了 Maven 和 JDK，可以直接安装并使用，但是推荐还是自行安装，虽然简化了开发环境的配置，但是环境最好不要依赖着工具，不然工具换了或出问题了就要重新配置一次。

要安装 Maven，您需要按照以下步骤进行：

1. 下载 Maven：首先，从 Apache Maven 官方网站（ https://maven.apache.org/ ）下载适用于您操作系统的 Maven 发行版。请选择最新稳定版本的二进制压缩包（zip 或 tar.Gz 格式）。

2. 解压 Maven：将下载的压缩包解压到您选择的目录中。您可以选择将 Maven 解压到任意目录，例如 `/opt`（Linux/macOS）或 `C:\Program Files`（Windows）。

3. 配置环境变量（可选）：为了能够在任意位置使用 Maven 命令，您可以配置环境变量。具体步骤如下：

   Windows 系统：
   - 在“开始”菜单中搜索“环境变量”，打开系统的环境变量设置。
   - 在“系统变量”下，找到名为 `Path` 的变量，点击“编辑”。
   - 添加 Maven 的 bin 目录路径（例如：`C:\path\to\maven\bin`）到变量值中，多个路径之间用分号（;）分隔。
   - 点击“确定”保存变更。

   MacOS 和 Linux 系统：
   - 打开终端，并编辑 `~/.bashrc`、`~/.bash_profile` 或 `~/.profile` 文件，根据您使用的 Shell 类型，添加以下内容： 
     ```
     export PATH=/path/to/your/maven/bin:$PATH
     ```
     请将 `/path/to/your/maven` 替换为您实际的 Maven 安装路径。

4. 验证安装：打开一个新的终端或命令提示符窗口，输入 `mvn -v` 命令。如果成功显示 Maven 的版本信息，说明安装成功。

现在，Maven 已经安装在您的系统上，并且可以通过命令行使用。您可以使用 Maven 来构建和管理 Java 项目了。


### Maven 配置文件 

Maven 的配置文件 `settings.xml` 可以有两个位置：

1. 全局配置文件：全局配置文件位于 Maven 的安装目录下的 `conf` 文件夹中。在 Windows 系统中，默认路径是 `C:\path\to\maven\conf\settings.xml`，而在 Linux/macOS 系统中，默认路径是 `/path/to/your/maven/conf/settings.xml`。

2. 用户级配置文件：用户级配置文件位于用户的主目录下的 `.m2` 文件夹中。在 Windows 系统中，默认路径是 `C:\Users\YourUsername\.m2\settings.xml`，而在 Linux/macOS 系统中，默认路径是 `/Users/YourUsername/.m2/settings.xml`。请注意，`.m2` 文件夹通常是隐藏文件夹，您可能需要启用显示隐藏文件夹选项才能找到它。

当 Maven 启动时，它会先查找用户级配置文件，如果找不到则会查找全局配置文件。如果在用户级配置文件中定义了某个配置项，那么该配置项将覆盖全局配置文件中的相同配置项。

您可以根据需要修改全局配置文件或用户级配置文件中的 `settings.xml` 文件来配置 Maven。修改这些配置文件可以设置 Maven 的镜像、代理、身份验证信息等。

### 配置 Maven 镜像源

Maven 官方镜像再国外，国内网络直连可能会很慢，可以配置国内的镜像源。这里以阿里云为例。

要配置阿里云的 Maven 源，您需要修改 Maven 的配置文件 `settings.xml`，按照以下步骤进行：

1. 找到 `settings.xml` 文件：该文件位于 Maven 的安装目录下的 `conf` 文件夹中。在 Windows 系统中，默认路径是 `C:\path\to\maven\conf\settings.xml`，而在 Linux/macOS 系统中，默认路径是 `/path/to/your/maven/conf/settings.xml`。

2. 备份 `settings.xml` 文件：在进行任何修改之前，最好先备份 `settings.xml` 文件，以防止意外情况。

3. 编辑 `settings.xml` 文件：使用文本编辑器（例如 Notepad++、Visual Studio Code、nano 等），打开 `settings.xml` 文件进行编辑。

4. 添加阿里云 Maven 镜像：在 `<mirrors>` 元素下添加以下配置，这将配置阿里云的 Maven 镜像：

```xml
<mirror>
  <id>aliyunmaven</id>
  <mirrorOf>*</mirrorOf>
  <name>阿里云公共仓库</name>
  <url>https://maven.aliyun.com/repository/public</url>
</mirror>
```

这里，`id` 是镜像的唯一标识，`mirrorOf` 指定了要镜像的远程仓库，`name` 是镜像的名称，`url` 是阿里云的 Maven 镜像地址。
5. 保存并关闭文件：在完成配置后，保存 `settings.xml` 文件并关闭文本编辑器。

现在，您已经成功配置了阿里云的Maven镜像。在使用Maven时，它将使用阿里云的镜像来下载依赖，加快项目构建过程。