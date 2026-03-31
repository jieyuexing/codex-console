# codex-console

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Version](https://img.shields.io/badge/version-v1.1.2-2563eb.svg)](https://github.com/dou-jiang/codex-console/releases)

基于 [cnlimiter/codex-manager](https://github.com/cnlimiter/codex-manager) 持续修复、整合并增强的维护版本，重点补齐当前 OpenAI / Codex CLI 注册链路、任务调度、邮箱服务、支付绑定、系统自检与 Web 管理能力。

项目地址：

- GitHub: [https://github.com/dou-jiang/codex-console](https://github.com/dou-jiang/codex-console)
- Blog: [https://blog.cysq8.cn/](https://blog.cysq8.cn/)

## v1.1.2 更新内容

`v1.1.2` 主要整合并落地了多组 PR 与后续修复，当前版本重点包括：

- 统一鉴权与安全基线：新增 `auth.py`、首次改密页、API 与 WebSocket 鉴权统一收口。
- 自动注册链路增强：补齐自动补货、库存监控、批次取消感知、注册重试与 PR60 anyauto V2 回退链路。
- 系统自检与修复中心：新增自检路由、页面、调度器和运行记录。
- 统一任务中心：将注册、支付、自检、Auto Team 等任务状态统一管理。
- 周期任务调度：支持计划任务创建、启停、立即执行与前端管理。
- New-API 上传：支持独立服务配置、测试、单账号和批量上传，以及注册成功后自动上传。
- Auto Team 模块：新增后端接口与前端管理页面。
- 卡池与绑卡能力：增加卡池管理、上游对接与自动绑卡支持。
- 邮箱服务扩展：补齐 CloudMail、LuckMail、YYDS Mail 等邮箱服务，并保留原有邮件链路。
- 数据库迁移体系：引入 Alembic，补齐迁移目录与说明。
- 测试与 CI：补充多组接口、任务、注册与上传相关测试，并加入测试工作流。

## 核心能力

- Web UI 管理注册、支付、账号、自检、日志、卡池、Auto Team 等功能。
- 支持单任务、批量任务、自动补货、定时任务、任务暂停/继续/取消/重试。
- 支持多种邮箱服务：Tempmail、YYDS Mail、Outlook、CloudMail、LuckMail、DuckMail、Freemail、IMAP、Temp-Mail 自部署等。
- 支持支付链接、绑卡任务、卡池管理、账户快照保留、审计日志。
- 支持 CPA、Sub2API、Team Manager、New-API 等上传链路。
- 支持 SQLite 与 PostgreSQL。
- 支持 Windows / Linux / macOS 打包。

## Blog 说明

维护者会在 Blog 持续更新以下内容：

- 部署教程与环境配置说明
- 版本更新日志与 Release 说明
- 常见问题、报错排查和修复记录
- 邮箱服务、上传服务、任务调度等功能的使用说明
- 与上游变化相关的兼容性调整说明

访问地址：

- [https://blog.cysq8.cn/](https://blog.cysq8.cn/)

## 赞助支持

如果这个项目对你有帮助，欢迎赞助支持项目继续维护与更新。

<table>
  <tr>
    <td align="center">
      <strong>微信赞助</strong><br />
      <img src="docs/assets/wechat-pay.png" alt="微信赞助二维码" width="260" />
    </td>
    <td align="center">
      <strong>支付宝赞助</strong><br />
      <img src="docs/assets/alipay-pay.png" alt="支付宝赞助二维码" width="260" />
    </td>
  </tr>
</table>

## 环境要求

- Python 3.10+
- 推荐使用 `uv`

## 安装依赖

```bash
# 推荐
uv sync

# 或使用 pip
pip install -r requirements.txt
```

## 快速开始

```bash
# 默认启动
python webui.py

# 指定监听地址和端口
python webui.py --host 0.0.0.0 --port 8080

# 调试模式
python webui.py --debug

# 设置 Web UI 访问密码
python webui.py --access-password your_password
```

启动后访问：

- [http://127.0.0.1:8000](http://127.0.0.1:8000)

## 常用环境变量

复制 `.env.example` 为 `.env` 后按需修改：

```bash
cp .env.example .env
```

| 变量 | 说明 | 默认值 |
| --- | --- | --- |
| `APP_HOST` | 监听地址 | `0.0.0.0` |
| `APP_PORT` | 监听端口 | `8000` |
| `APP_ACCESS_PASSWORD` | Web UI 访问密码 | `admin123` |
| `APP_DATABASE_URL` | 数据库连接 | `data/database.db` |

## Docker 部署

### docker-compose

```bash
docker-compose up -d
```

如果需要查看可视化浏览器：

- noVNC: `http://127.0.0.1:6080`

### docker run

```bash
docker run -d \
  -p 1455:1455 \
  -p 6080:6080 \
  -e DISPLAY=:99 \
  -e ENABLE_VNC=1 \
  -e VNC_PORT=5900 \
  -e NOVNC_PORT=6080 \
  -e WEBUI_HOST=0.0.0.0 \
  -e WEBUI_PORT=1455 \
  -e WEBUI_ACCESS_PASSWORD=your_secure_password \
  -v $(pwd)/data:/app/data \
  --name codex-console \
  ghcr.io/<yourname>/codex-console:latest
```

## 数据库迁移

```bash
alembic revision --autogenerate -m "your_change"
alembic upgrade head
```

更多说明见：

- [alembic/README.md](alembic/README.md)

## 致谢

感谢上游项目作者 [cnlimiter](https://github.com/cnlimiter) 提供的基础工程与思路。

## 免责声明

本项目仅供学习、研究和技术交流使用，请遵守相关平台和服务条款，不要用于违规、滥用或非法用途。
因使用本项目产生的任何风险与后果，由使用者自行承担。
