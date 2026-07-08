# 使用 VSCode + SSH 令牌克隆 GitHub 仓库（完整新手教程）

本指南将从零开始，教你：

- 安装 Git
- 生成 SSH 密钥并添加到 GitHub
- 使用 VSCode 通过 SSH 地址克隆仓库

---

## 一、安装 Git

### Windows
1. 访问 [Git 官网下载页](https://git-scm.com/downloads)，点击“Windows”下载安装包。
2. 运行安装程序，**建议勾选** “Git Bash Here” 和 “Git GUI Here”（方便右键菜单打开终端）。
3. 其余选项保持默认，完成安装。

### macOS
- 若已安装 Homebrew：终端执行 `brew install git`
- 或直接下载 `.dmg` 安装包安装。

### Linux
- Debian/Ubuntu：`sudo apt update && sudo apt install git`
- RHEL/CentOS：`sudo yum install git`
- Arch：`sudo pacman -S git`

### 验证安装
打开终端（Windows 打开 **Git Bash**），输入：
```bash
git --version
```
若显示版本号（如 git version 2.42.0）即安装成功。

## 二、配置 Git 用户信息（首次使用必须执行）
```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```
>注意：邮箱必须与 GitHub 账号邮箱一致。

## 三、生成 SSH 密钥（令牌）

SSH 密钥由 **公钥**（放在 GitHub）和 **私钥**（留在本地）组成。

1. 打开终端（Windows 打开 Git Bash）。
2. 执行以下命令（推荐 ed25519 算法）：
```bash
   ssh-keygen -t ed25519 -C "你的邮箱@example.com"
```
3. 按提示操作：
   - **保存位置**：直接按回车（默认 `~/.ssh/id_ed25519`）。
   - **密码短语**：可设可不设（直接回车表示无密码）。

---

## 四、将公钥添加到 GitHub

1. **复制公钥内容**   
   用记事本打开 `C:\Users\你的用户名\.ssh\id_ed25519.pub` 再复制。

2. **登录 GitHub，进入设置**  
   - 点击右上角头像 → **Settings**。
   - 左侧菜单选择 **SSH and GPG keys**。
   - 点击绿色按钮 **New SSH key**。
   - **Title**：填写一个识别名称（如 “My Laptop”）。
   - **Key type**：选择 **Authentication Key**。
   - **Key**：粘贴刚才复制的公钥。
   - 点击 **Add SSH key** 保存。

---

## 五、在 VSCode 中克隆仓库

1. 打开 VSCode。
2. 按 `Ctrl+Shift+P`（Windows/Linux）或 `Cmd+Shift+P`（Mac）打开命令面板。
3. 输入并选择 **Git: Clone**。
4. 在输入框中粘贴仓库的 **SSH 地址**（不是 HTTPS）。  
   **如何获取 SSH 地址**：  
   在 GitHub 仓库页面点击绿色的 **Code** 按钮 → 切换到 **SSH** 标签 → 复制地址（格式：`git@github.com:用户名/仓库名.git`）。
5. 选择本地存放目录，等待克隆完成。
6. 点击 **Open** 打开项目。

---

## 六、验证 SSH 连接（可选）

在终端执行：
```bash
ssh -T git@github.com`
```
若看到类似 `Hi 你的用户名! You've successfully authenticated...` 的提示，说明配置成功。

---

## 七、常见问题

### 首次连接提示确认主机指纹
出现 `The authenticity of host ...` 时，输入 `yes` 回车即可。

### 已有 HTTPS 仓库想改为 SSH
在项目目录下执行：
`git remote set-url origin git@github.com:用户名/仓库名.git`

### SSH 连接超时或失败
- 检查网络（尤其国内可能需要稳定环境）。
- Windows 用户可尝试手动启动 ssh-agent 并添加私钥：
  `eval $(ssh-agent -s)`
  `ssh-add ~/.ssh/id_ed25519`   （替换为你的私钥路径）

---

## 完成！

现在你可以自由地使用 VSCode 和 SSH 方式克隆、推送、拉取 GitHub 仓库了，无需每次输入密码。