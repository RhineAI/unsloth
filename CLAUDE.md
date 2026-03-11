# Project Notes

## `rc` 命令

定义在 `~/.bashrc` 中的自定义函数，用于将本地项目同步到远程服务器并执行命令。

### 功能

- 自动检测当前目录名，将项目 rsync 同步到远程服务器 `10.176.56.244` 的 `/data/disk1/guohaoran/<目录名>/`
- 不带参数：同步后 SSH 登录到远程对应目录
- 带参数：同步后在远程对应目录下执行指定命令

### 实现方式

1. 用 `$(pwd)` 获取当前本地路径，`basename` 提取目录名
2. 拼接远程路径 `/data/disk1/guohaoran/<目录名>`
3. `rsync -az` 同步，排除 `.git/`、`__pycache__/`、`.venv/`、`node_modules/` 等
4. 根据是否有参数决定 SSH 登录还是远程执行命令

### 示例

```bash
# 在 /c/Projects/unsloth 目录下运行将自动对应远程目录 /data/disk1/guohaoran/unsloth/

# 同步目录并直接进入远程服务器终端
rc

# 同步项目并查看远程服务器上的目录信息
rc "ls"

# 同步项目并查看远程 GPU 状态
rc "nvidia-smi"
```

## Language

1. 输出语句与日志使用英文
2. 交流对话与注释使用中文
