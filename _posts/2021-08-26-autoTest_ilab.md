---
layout: article
title:  "【项目】使用Selenium IDE + Chrome进行虚拟实验的自动化测试"
author: 李宇琨
key: 20210723
lang: zh
tags: Project ABAQUS MATLAB
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: "https://qxoofg-dm2305.files.1drv.com/y4mBY0uVEe-PJUNyhIugDvvGE6dv0nK7LWs-FST9h8ZTsDwxjYRPYEOMjWVn9AjrxWqY5fenVeUF1RJdiO5f4lapIkohlhWaPdLDJCgagNLO2dTzqss86bTU9qH70ycta7uz_4BelqJSKcDHJKmLCLn1DeAPiNwEonzopcsvesEBOh6sXQ9uLpGO9zIBP6tv9Wnqny7XFuy2OCvVsdBxmKE2Q?width=5814&height=3784&cropmode=none"
---

## 简介

该项目使用Selenium IDE和Google Chrome对[国家虚拟仿真实验教学课程共享平台](http://www.ilab-x.com/)中的[复合材料结构强度与稳定性积木式验证虚拟仿真实验](http://www.ilab-x.com/details/2020?id=6585&isView=true)课程实现自动化测试。进行其中的虚拟实验操作并提交结果。具体测试内容参见项目中的`力学虚拟实验操作说明 .pdf`文档。

## 项目代码

[lyk6756/autoTest_ilab-x - GitHub](https://github.com/lyk6756/autoTest_ilab-x)

## 环境准备

已通过测试的运行环境：

* Google Chrome 92.0.4515.159
* Selenium IDE for Chrome 3.17.0

使用Google Chrome浏览器打开[https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd](https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd)将Selenium IDE添加至Chrome即可。

或采用项目中的`Selenium-IDE_v3.17.0.crx`文件进行离线安装。具体安装方式详见[这里](https://www.cnplugins.com/tool/three-methods-to-install-crx.html)。

## 前置条件：登陆

在运行自动化脚本前，**务必**先在Google Chrome浏览器中完成登陆：[国家虚拟仿真实验教学课程共享平台](http://www.ilab-x.com/login)。

## 运行脚本

1. 将项目中的自动运行脚本`autoTest.side`下载到本地。

2. 完成登陆后，在浏览器中打开安装好的Selenium IDE，在弹出的对话框中点击`Open an existing projct`，并选择刚才下载的脚本`autoTest.side`。

  ![Open project](https://dm2305files.storage.live.com/y4m4SjFM2Ofz1XXb_SH6Bx9fPZBnCKSZ6Qt39w3gimZPEc-YCq1Qw1mFpk2iA3GKizCIOwPJfyKvi_l1aHLJcNpqUnB8CjldhluNNz2KERoZOyXU3oOUJuCOCaCGVJTA9VNT3fyWor58f9ImxCPWuc75HhNlV88Khz77rlmnJg42bst952X8mvRTNJZZCmBI7ns?width=618&height=756&cropmode=none)

3. 在运行脚本之前，**务必**先将运行速度调整至最慢。在Selenium IDE窗口中，选择工具栏中的`Test execution speed`（显示为:stopwatch: 图形），并将滑块拖动至最慢。

  ![Open project](https://dm2305files.storage.live.com/y4mtFy9M7JkQOkIU6iW-CCQdZiqWKpf7V4Q8ehevXaPU0OJePPGC0jjwuwJna3LXydVYha1s4V3fPhcBwxMN-D5F2Dmex6swQFDj8CHnFXT2KJg8OOHo-W_LmwtD-7km8gCgzSn1FigJfb1mt3oNTYNlsdcUbHyFF5FAKREtsiSCPN9jkrAkj_g4n66-vtdt-v1?width=618&height=756&cropmode=none)

4. 点击工具栏中的`Run current test`（显示为:arrow_forward: 图形）。脚本开始自动运行，约15分钟左右完成实验操作，并自动提交。

**注意**：脚本运行过程中，请勿对浏览器窗口进行任何操作。

  ![Open project](https://dm2305files.storage.live.com/y4m2FNAOBaSe9QotT6YdK3jEXCPmjSkYYsgozNxTr0lmEtqKu8tB1l7rOP3idGYLxHWhkax8YIKY_QFyURWh2qUfN-3aAxYXvlAwFr7BOeFy9R-qz-AqNcNy14BnMaFIxU7lrLstoQrq_SRUfn_ycNuGyU4jipO-Ayvlu0n9Oq64QRTUEw2z8g_R0TZBoJkIBL4?width=618&height=756&cropmode=none)

---

## 延伸阅读

* [Selenium IDE](https://www.selenium.dev/selenium-ide/)

* [Selenium IDE Web 自动化测试（上） - bilibili](https://www.bilibili.com/video/BV1fJ411w7mk)

* [Python语言下使用Selenium实现对浏览器的自动控制 - 李宇琨的博客](https://lyk6756.github.io/2017/08/01/selenium.html)
