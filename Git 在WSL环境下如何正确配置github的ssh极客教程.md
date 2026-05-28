---
title: "Git 在WSL环境下如何正确配置github的ssh|极客教程"
source: "https://geek-docs.com/git/git-questions/299_git_does_anybody_know_how_to_get_github_ssh_to_work_correctly_on_wsl_windows_subsystem_for_linux.html"
author:
published:
created: 2026-05-28
description: "Git 在WSL环境下如何正确配置github的ssh  在本文中，我们将介绍如何在Windows Subsystem for Linux（简称WSL）环境下正确配置Github的SSH连接。WSL是一种在Windows系统上运行Linux环境的工具，可以方便地进行开发和部署。而SSH是一种安全的网络协议，用于在计算机之间进行加密通信。  阅读更多：Git 教程  什么是SSH  SSH（Secu"
tags:
  - "clippings"
---
## Git 在WSL环境下如何正确配置github的ssh

在本文中，我们将介绍如何在Windows Subsystem for Linux（简称WSL）环境下正确配置Github的SSH连接。WSL是一种在Windows系统上运行Linux环境的工具，可以方便地进行开发和部署。而SSH是一种安全的网络协议，用于在计算机之间进行加密通信。

## 什么是SSH

SSH（Secure Shell）是一种安全的网络协议，用于在不安全的网络上对计算机进行安全的远程访问。通过SSH，我们可以在不泄露密码的情况下，远程登录并执行命令。而Github作为一个代码托管平台，使用SSH认证来保证代码的安全性。

## 生成SSH密钥

首先，在WSL中打开终端。然后，使用以下命令生成SSH密钥：

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

这里的”your\_email@example.com”应该替换为你在Github上注册的邮箱地址。生成密钥时，可以选择使用新的密钥名称，也可以使用默认的密钥名称。一般情况下，我们使用默认的密钥名称即可。

生成密钥后，可以通过以下命令查看密钥内容：

```bash
cat ~/.ssh/id_ed25519.pub
```

复制输出的公钥内容。

## 配置SSH密钥

接下来，将复制的公钥内容添加到Github账户的SSH密钥中。登录Github账户，点击右上角的个人头像，选择”Settings”，然后选择”SSH and GPG keys”。点击”New SSH key”按钮，将之前复制的公钥内容粘贴到”Key”输入框中，并为密钥添加一个描述。点击”Add SSH key”按钮完成添加。

## 测试SSH连接

完成密钥的添加后，我们可以测试SSH连接是否正常工作。在WSL终端中输入以下命令：

```bash
ssh -T git@github.com
```

如果一切正常，你会看到一条欢迎消息，表示SSH连接成功。

## 配置Git

配置好SSH后，我们还需要配置 [Git](https://geek-docs.com/git/git-top-articles/1000100_git_index.html "Git 教程") ，让Git使用SSH来进行代码的克隆和提交。在WSL终端中输入以下命令：

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

将”Your Name”和”your\_email@example.com”分别替换为你的用户名和邮箱地址。

## 示例

假设我们要克隆一个Github仓库到WSL环境中。首先，通过SSH协议获取仓库的克隆链接。在仓库主页上，点击”Code”按钮，选择”SSH”，复制下来SSH链接。

然后，在WSL终端中进入想要保存该仓库的目录，输入以下命令：

```bash
git clone git@github.com:username/repo.git
```

将”username/repo.git”替换为实际的仓库路径。执行该命令后，Git会自动从远程仓库克隆代码到本地。

在本地对代码进行修改后，可以通过以下命令将修改的代码提交到远程仓库：

```bash
git add .
git commit -m "some changes"
git push
```

这样，我们就成功地使用SSH连接和操作Github仓库了。

## 总结

本文介绍了如何在Windows Subsystem for Linux环境下正确配置Github的SSH连接。通过生成SSH密钥、配置Github账户和Git，我们能够使用SSH协议进行代码的克隆和提交。希望本文能对使用WSL的开发者们有所帮助。