好的，结合之前的对话和你提供的参考文章，我为你整理了一份**精简实用的 GitHub + WSL SSH 配置教程**。

---

# GitHub + WSL SSH 配置与使用教程

## 一、生成 SSH 密钥

在 WSL 终端中执行：

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com"
```

- 一路按回车，使用默认路径和空密码即可
- 密钥生成位置：`~/.ssh/id_ed25519`（私钥）和 `~/.ssh/id_ed25519.pub`（公钥）

查看并复制公钥：

```bash
cat ~/.ssh/id_ed25519.pub
```

---

## 二、添加公钥到 GitHub

1. 登录 GitHub → 右上角头像 → **Settings**
2. 左侧菜单 → **SSH and GPG keys**
3. 点击 **New SSH key**
4. 粘贴公钥内容 → 填写标题（如 "WSL"）→ **Add SSH key**

---

## 三、测试 SSH 连接

```bash
ssh -T git@github.com
```

- **首次连接**会提示确认指纹，输入 `yes`
- 成功显示：`Hi 用户名! You've successfully authenticated...`

---

## 四、配置 Git 用户信息

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub邮箱"
```

---

## 五、将当前文件夹上传到 GitHub 仓库

### 5.1 在 GitHub 上创建空仓库

- 点击 **+** → **New repository**
- **不要勾选**：README、.gitignore、License（保持完全空白）
- 复制 SSH 地址：`git@github.com:用户名/仓库名.git`

### 5.2 本地操作

```bash
# 进入项目文件夹
cd /path/to/your/folder

# 初始化 Git 仓库
git init

# 添加所有文件
git add .

# 提交
git commit -m "首次提交"

# 添加远程仓库（SSH 地址）
git remote add origin git@github.com:用户名/仓库名.git

# 重命名分支为 main（可选，与 GitHub 保持一致）
git branch -M main

# 推送
git push -u origin main
```

---

## 六、常见问题与解决

| 问题 | 原因 | 解决方法 |
|------|------|----------|
| `Permission denied (publickey)` | SSH 密钥未添加到 GitHub | 重新添加公钥 |
| `Host key verification failed` | 首次连接 GitHub | 输入 `yes` 确认 |
| `Authentication failed` | 用了 HTTPS 而非 SSH | `git remote set-url origin git@github.com:用户名/仓库名.git` |
| `non-fast-forward` 错误 | 远程仓库有内容（如 README） | `git pull origin main --allow-unrelated-histories` 再推送 |
| `no upstream branch` | 本地分支未关联远程 | `git push -u origin main` |

---

## 七、日常使用命令

```bash
# 查看状态
git status

# 添加所有修改
git add .

# 提交
git commit -m "修改说明"

# 推送
git push

# 拉取远程更新
git pull
```

---

## 八、关键提醒

1. **创建 GitHub 仓库时保持空白**，否则会触发 `non-fast-forward` 错误
2. **始终使用 SSH 地址**（`git@github.com:...`），不要用 HTTPS
3. **首次推送**用 `git push -u origin main` 建立关联，之后直接用 `git push`

---

按照以上步骤操作，即可在 WSL 中顺畅使用 GitHub SSH 连接。