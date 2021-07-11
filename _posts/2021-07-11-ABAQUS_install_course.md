---
layout: article
title:  "安装ABAQUS官方培训课程示例文件"
author: 李宇琨
key: 20210711
lang: zh
tags: ABAQUS Fortran
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://m2qziq.dm.files.1drv.com/y4mzZWEjjAaNARefyxVkKlxgwEqMB9rIn39wANVzd5uOzUAzLqeuSf42u3C7tSgXdUgrJZgR4-vcrINIiY7YVn1tMjgnuI3pF6Z8KzW6Fb318P6UCPtiZd_k0QYcsEUMmDeeJCoTGPhJz3tIsnBGikod3UQNlytoJym4wcdypIwKdDWVnWdaMzOnBusQVoIn1N71leU_ISdOrv3cxIijF73MQ?width=870&height=400&cropmode=none"
---

ABAQUS的官方培训课程中包含了较多的演示及研讨实例（Workshops），所有的实例都提供了示例文件，包括脚本文件（`.py`）、输入文件（`.inp`）、子程序文件（`.for`）等。ABAQUS提供了两种安装方式：图形界面安装和命令行界面安装。

## 通过 Abaqus/CAE 安装

将用于安装的文件`samples.zip`解压缩后，打开Abaqus/CAE并在菜单栏选择：`Plug-ins` -> `Tools` -> `Install Courses`。

![Install Courses Menu](https://dm2305files.storage.live.com/y4maxYLDzszUkH3t9gX2Y9v2Spm92HCdCu1PMZuJhHzE6cN0wM_iU-SyXgGTsN8Jp4GbAXfVeQe4O5_FAXPrREfXoJ_2sy1KFuJvsfl9wLJPkua-XQHxwd6V66jtlFzkyDqPinp-FuTIByo3BpE7AdbUXkM2sInwrdjgMMwM_e4WbC27NCI15EpjPtjRazGYD-R?width=427&height=266&cropmode=none)

在弹出的`Install Courses`对话框中，选择示例文件需要安装的文件目录，选择需要安装的课程名称，并点击`OK``。

![Install Courses Dialog Box](https://dm2305files.storage.live.com/y4mCRN_oeUlY_BMfD2vTQqZZPcF-ktQi6uQ7ti9IDYLOkGLhTPcb8mrH5YBjoLrQ5iLdb3ZZZjxxPVcQ4-sSGUu_axVsDog_RcphJjUjxoY4GEIG2WNC8fcncHoDDuVL5qmo3kWrOG4wNRovwyZrCAFH4WvdtnN9hYTidi03Z9Q480oe4ufyIzamXBaUR9FJHm7?width=401&height=411&cropmode=none)

## 通过命令行界面安装

首选需要获取Abaqus的安装路径，可以在命令行窗口输入以下命令来查询：

```
abqXXX whereami
```

其中`abqXXX`根据所安装的版本会有不同的名称。

接下来，从安装的压缩包源文件中提取示例文件：

```
abqXXX perl abaqus_dir/SMA/samples/course_setup.pl
```

其中的`abaqus_dir`表示Abaqus的安装路径。

该脚本会将文件安装到当前工作目录中。系统会请求你验证并选择需要安装的文件。出现提示时，按`y`来选择相应的课程文件。在完成需要的选择后，按`q`来跳过剩余的课程文件并继续安装。

### 安装源文件

用于安装的压缩包源文件`samples.zip`，其默认的路径为`abaqus_dir/SMA/samples/job_archive/samples.zip`。
