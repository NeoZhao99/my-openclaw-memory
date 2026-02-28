# QMD 安装配置指南

## 简介
QMD (Quick Memory Database) 是 OpenClaw 的高效记忆后端，可以显著降低 token 消耗，提升性能。

## 系统要求
- Windows 10/11 或 macOS/Linux
- Node.js 18+ (推荐 20+)
- Bun 1.0+

## 安装步骤

### 1. 安装 Bun
如果您还没有安装 Bun，请先安装：

```bash
# 使用 npm 安装 Bun
npm install -g bun

# 验证安装
bun --version
```

### 2. 安装 QMD

```bash
# 全局安装 QMD
bun install -g https://github.com/tobi/qmd

# 验证安装
bun list -g | grep qmd
```

### 3. 配置 OpenClaw

编辑 OpenClaw 配置文件 `~/.openclaw/openclaw.json`，添加或修改 memory 配置：

```json
{
  "memory": {
    "backend": "qmd",
    "qmd": {
      "update": {
        "interval": "5m"
      }
    }
  }
}
```

### 4. 重启 OpenClaw

```bash
# 重启 OpenClaw gateway
openclaw gateway restart
```

## 配置说明

### 更新间隔设置
- `interval`: 记忆更新间隔，支持以下格式：
  - `"5m"`: 5 分钟
  - `"1h"`: 1 小时
  - `"24h"`: 24 小时

### 推荐配置
```json
{
  "memory": {
    "backend": "qmd",
    "qmd": {
      "update": {
        "interval": "5m"
      }
    }
  }
}
```

## 验证安装

### 检查 QMD 是否安装成功
```bash
# 检查 Bun 版本
bun --version

# 检查 QMD 安装
bun list -g | grep qmd
```

### 检查 OpenClaw 配置
```bash
# 获取当前配置
openclaw gateway config get
```

## 常见问题

### QMD 命令无法运行
如果在 Windows 上遇到 `bash.exe` 错误，这是正常现象，因为 QMD 主要通过 OpenClaw 内部调用，不需要直接运行。

### 配置未生效
1. 确保配置文件格式正确
2. 重启 OpenClaw gateway
3. 检查 OpenClaw 日志确认配置加载

## 性能优化

- **降低更新间隔**: 设置为 `"1m"` 可获得更及时的记忆更新
- **增加更新间隔**: 设置为 `"15m"` 可进一步降低资源消耗
- **监控效果**: 观察 token 消耗变化，调整到最佳平衡点

## 卸载

```bash
# 卸载 QMD
bun uninstall -g @tobilu/qmd

# 恢复 OpenClaw 默认配置
# 编辑配置文件，将 memory.backend 改为 "default"
```

## 参考链接

- [QMD GitHub 仓库](https://github.com/tobi/qmd)
- [OpenClaw 文档](https://docs.openclaw.ai)
- [Bun 官方文档](https://bun.sh)

---

**文档创建时间**: 2026-02-28
**适用版本**: OpenClaw 2026.2.13+
**QMD 版本**: @tobilu/qmd#40610c3