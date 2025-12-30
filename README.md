# FRP 自动安装脚本

这是一个自动化的 FRP (Fast Reverse Proxy) 安装脚本，支持自动检测操作系统和架构，选择对应的安装包，并自动配置 systemd 服务。

安装完成后终端输入frp可以快速打开管理菜单

## 功能特性

-  **自动检测系统**：支持多种操作系统和架构
-  **自动匹配包**：根据系统自动选择对应的 FRP 安装包
-  **交互式配置**：引导用户完成配置
-  **自动服务**：自动创建和启动 systemd 服务
-  **完整配置**：生成完整的配置文件

## 支持的平台

脚本会自动检测并支持以下平台：

### 🐧 Linux 发行版
- **Ubuntu** (所有版本)
- **Debian** (所有版本)
- **CentOS/RHEL/Fedora**
- **SUSE/openSUSE**
- **Arch Linux/Manjaro**
- **其他 systemd 兼容系统**

###  macOS
- macOS 10.12+ (支持 Intel 和 Apple Silicon)

###  BSD 系统
- FreeBSD
- OpenBSD

###  架构支持
| 架构 | 说明 | 支持的系统 |
|------|------|-----------|
| `amd64/x86_64` | Intel/AMD 64位 | 所有Linux/macOS/BSD |
| `arm64/aarch64` | ARM 64位 | Apple M1/M2, Raspberry Pi 4+, 服务器 |
| `arm/armhf` | ARM 32位硬浮点 | Raspberry Pi 2/3, 嵌入式设备 |
| `mips/mips64` | MIPS架构 | 路由器, 嵌入式设备 |
| `loong64` | 龙芯架构 | 龙芯服务器/工作站 |
| `riscv64` | RISC-V 64位 | RISC-V开发板/服务器 |
| `ppc64le` | PowerPC 64位 | IBM Power服务器 |
| `s390x` | IBM System z | IBM大型机 |
| `386/i386` | 32位 x86 | 老旧系统 |

###  智能检测
脚本会自动：
- 识别具体的Linux发行版 (Ubuntu, Debian, CentOS等)
- 检测系统架构并映射到对应的包
- 检查系统兼容性 (systemd, 磁盘空间, 内存等)
- 提供详细的系统信息和兼容性报告

## FRP 管理工具

`frp` 脚本是一个一体化的管理工具，类似宝塔面板的 `bt` 命令。它会根据 FRP 是否已安装自动显示相应的功能。

### 未安装时的功能

当 FRP 未安装时，`frp` 命令提供安装功能：

```bash
# 显示安装帮助
frp help

# 安装 FRP 服务器
sudo frp install server

# 安装 FRP 客户端
sudo frp install client
```

### 已安装时的功能

安装完成后，`frp` 命令提供完整的管理功能：

#### ⚙️ **服务管理**
```bash
frp start       # 启动 FRP 服务
frp stop        # 停止 FRP 服务
frp restart     # 重启 FRP 服务
frp status      # 查看详细服务状态
frp reload      # 重新加载配置
```

####  **配置管理**
```bash
frp config      # 查看当前配置
frp edit        # 编辑配置文件 (自动备份)
frp test        # 测试配置语法
frp backup      # 备份当前配置
frp restore     # 从备份恢复配置
```

####  **日志和监控**
```bash
frp logs        # 查看实时日志
frp logf        # 查看日志文件
frp monitor     # 实时监控服务状态
frp connections # 显示连接信息 (仅服务端)
```

####  **其他功能**
```bash
frp help        # 显示帮助信息
frp version     # 显示版本信息
frp info        # 显示系统信息
frp uninstall   # 卸载 FRP
```

### 常用命令示例

```bash
# 快速查看服务状态
frp status

# 编辑配置后重新加载
frp edit
frp test
frp reload

# 查看实时日志
frp logs

# 备份重要配置
frp backup

# 卸载 FRP
sudo frp uninstall
```
| Android | arm64 |

## 文件说明

- **`frp`** - FRP 一体化管理脚本（主要脚本，支持安装和管理）
- **`demo.sh`** - 演示脚本，展示菜单界面和配置流程（无需root权限）
- **`test_install.sh`** - 基础测试脚本，验证安装环境和脚本功能
- **`test_detection.sh`** - 系统检测测试脚本，验证操作系统和架构识别
- **`test_frp_manager.sh`** - FRP 管理脚本测试工具
- **`install.sh`** - 传统安装脚本（已由 frp 脚本替代）
- **`README.md`** - 详细使用说明文档

## 使用方法

### 1. 准备工作

确保脚本有执行权限：

```bash
chmod +x frp
```

### 2. 安装 FRP

#### 如果 FRP 未安装：

```bash
# 安装 FRP 服务器
sudo ./frp install server

# 安装 FRP 客户端
sudo ./frp install client

# 查看帮助信息
./frp help
```

安装完成后，脚本会自动部署到系统路径，你可以直接使用 `frp` 命令。

#### 如果 FRP 已安装：

```bash
# 查看服务状态
frp status

# 启动服务
sudo frp start

# 查看实时日志
frp logs

# 编辑配置
sudo frp edit
```

**选项说明：**

1. **FRP 服务器 (frps)**：用于搭建 FRP 服务端，供客户端连接
2. **FRP 客户端 (frpc)**：用于连接到 FRP 服务端，映射本地服务
3. **查看系统信息**：显示当前系统信息和可用的安装包列表
4. **退出安装**：取消安装并退出脚本

## 安装后的文件位置

- **安装目录**：`/opt/frp/`
- **配置文件**：`/etc/frp/`
- **日志文件**：`/var/log/frp/`
- **服务文件**：`/etc/systemd/system/frp{s,c}.service`

## 服务管理

### 查看服务状态
```bash
sudo systemctl status frps  # 服务器
sudo systemctl status frpc  # 客户端
```

### 重启服务
```bash
sudo systemctl restart frps  # 服务器
sudo systemctl restart frpc  # 客户端
```

### 停止服务
```bash
sudo systemctl stop frps  # 服务器
sudo systemctl stop frpc  # 客户端
```

### 查看日志
```bash
sudo journalctl -u frps -f  # 服务器日志
sudo journalctl -u frpc -f  # 客户端日志
```

## 配置说明

### FRP 服务器配置

安装 frps 时会询问以下信息：

- **监听端口**：frps 监听的端口（默认 7000）
- **监听地址**：frps 绑定的地址（默认 0.0.0.0）
- **认证令牌**：客户端连接所需的令牌（可随机生成）
- **管理面板端口**：Web 管理界面端口（默认 7500，可留空禁用）
- **管理面板用户名/密码**：Web 管理界面认证信息

### FRP 客户端配置

安装 frpc 时会询问以下信息：

- **服务器地址**：frps 服务器的 IP 地址
- **服务器端口**：frps 服务器的端口
- **认证令牌**：与服务器一致的令牌
- **代理类型**：TCP 或 HTTP 代理
- **本地服务信息**：本地服务的 IP 和端口
- **远程访问信息**：远程访问的端口或域名

## 注意事项

1. **权限要求**：脚本需要 root 权限运行
2. **网络要求**：确保网络连接正常，脚本会从本地包目录安装
3. **防火墙**：根据需要配置防火墙规则
4. **备份配置**：重要配置请备份 `/etc/frp/` 目录

## 操作系统特定说明

### Ubuntu/Debian
```bash
# 更新包管理器
sudo apt update

# 安装必要工具（如需要）
sudo apt install curl wget tar gzip

# 运行安装脚本
sudo ./install.sh
```

### CentOS/RHEL
```bash
# 更新包管理器
sudo yum update  # CentOS 7
sudo dnf update  # CentOS 8+/RHEL 8+

# 安装必要工具（如需要）
sudo yum install curl wget tar gzip  # CentOS 7
sudo dnf install curl wget tar gzip  # CentOS 8+/RHEL 8+

# 运行安装脚本
sudo ./install.sh
```

### Fedora
```bash
# 更新系统
sudo dnf update

# 安装必要工具（如需要）
sudo dnf install curl wget tar gzip

# 运行安装脚本
sudo ./install.sh
```

### SUSE/openSUSE
```bash
# 更新系统
sudo zypper update

# 安装必要工具（如需要）
sudo zypper install curl wget tar gzip

# 运行安装脚本
sudo ./install.sh
```

### Arch Linux/Manjaro
```bash
# 更新系统
sudo pacman -Syu

# 安装必要工具（如需要）
sudo pacman -S curl wget tar gzip

# 运行安装脚本
sudo ./install.sh
```

## 故障排除

### 服务启动失败

1. 检查配置文件语法：
   ```bash
   sudo frps -c /etc/frp/frps.toml --test  # 服务器
   sudo frpc -c /etc/frp/frpc.toml --test  # 客户端
   ```

2. 查看详细日志：
   ```bash
   sudo journalctl -u frps -n 50  # 最后50行服务器日志
   sudo journalctl -u frpc -n 50  # 最后50行客户端日志
   ```

### 连接问题

1. 检查网络连通性
2. 确认端口未被占用
3. 验证认证令牌是否正确
4. 检查防火墙设置

## 版本信息

- FRP 版本：0.65.0
- 脚本版本：1.0

## 许可证

本脚本遵循与 FRP 相同的许可证。
