# 菠萝蓝牙耳机 · 售后 AI 客服系统(课程项目)

> 「数据库与 AI 协同开发实战」小组作业仓库,**仅供学习使用**。
> 一个面向菠萝蓝牙耳机用户的 AI 售后客服系统:Android 客户端 + FastAPI 后端 + DeepSeek 大模型 + 知识库检索,附带商城(商品/购物车/订单)、人工客服转接(WebSocket)和管理后台。

## 功能总览

| 模块 | 说明 |
|---|---|
| 🤖 AI 对话 | DeepSeek 大模型 + 专业知识库(7 大类 35+ 条),多轮对话、上下文记忆、非相关问题自动引导 |
| 🧑‍💼 人工客服 | 对话中「转人工」→ WebSocket 实时接入,客服下班后自动恢复 AI 应答 |
| 🛒 商城 | 商品列表/详情(真实 AirPods 全系数据)、购物车、下单、订单列表与详情 |
| 📋 对话历史 | 保存、单条删除、一键清空 |
| 🔐 用户体系 | 注册/登录、Token 鉴权、限流中间件 |
| 🖥️ 管理后台 | H5 网页后台(商品增删改、图片上传、知识库管理) |
| 📱 多端 | 原生 Android App、微信小程序(历史版本)、H5 下载页(扫码装 APK) |

## 目录结构

```
.
├── c/                  ★ 当前主项目(最新最完整的一版)
│   ├── android/            Android 客户端(Java,com.airpods.assistant)
│   ├── backend/            FastAPI 后端(auth / chat / knowledge)
│   ├── deploy/             部署配置(nginx、systemd、部署脚本)
│   ├── docs/               全部课程文档(需求、原型、测试、竞品分析等)
│   └── README.md           主项目详细说明(架构、接口、启动步骤)
├── 大数据/              「大数据」方向组员的材料
│   ├── 后端/                后端进阶版:多了 admin/agent/cart/orders/products/websocket 路由、
│   │                        管理后台 admin/index.html、APK 下载页 download/
│   ├── 技术选型/            课程课件(MySQL、Python 操作数据库等 PDF,第三方资料)
│   ├── DESIGN.md            UI 设计规范(设计令牌)
│   └── create_word*.py      自动生成 Word 报告的脚本
├── legacy/             历史协作快照(早期分组提交,仅作存档)
│   ├── 前端/                 前端快照 + 打包好的 app-debug.apk
│   ├── 前端开发  UI设计  测试工程师 (1)/   前端/UI/测试同学的完整包(含小程序)
│   └── 后端/                 早期后端杂项
├── docs/               零散运营文档与图片(商品模板、截图等)
└── scripts/tests/      API 联调测试脚本(test_*.py)
```

**哪一版是最新的?** —— `c/` 目录(以及 `大数据/后端/` 里的进阶路由实现)。`legacy/` 下的三个目录是组员早期的整包提交,内容已大部分并入 `c/`,保留仅作学习记录。

## 技术栈

- **后端**:Python · FastAPI · Uvicorn · MySQL / SQLite · jieba · WebSocket · requests
- **AI**:DeepSeek API + 提示词工程 + 知识库检索
- **客户端**:Android(Java,Material Design,Retrofit + OkHttp)、微信小程序
- **部署**:Nginx · systemd · Python 部署脚本

## 快速开始

### 后端

```bash
cd 大数据/后端          # 功能最全的一版(或 c/backend,精简版)
pip install -r requirements.txt
# 配置 .env(数据库连接、DeepSeek API Key 等)
uvicorn main:app --host 0.0.0.0 --port 8000
```

接口文档:`http://127.0.0.1:8000/docs`;管理后台:`/admin`;APK 下载页:`/download`。

### Android

```bash
cd c/android
./gradlew assembleDebug
```

用 Android Studio 打开 `c/android` 直接运行也可以;`ApiClient.java` 里配置后端地址。

### 部署

参考 `c/README.md` 与 `c/deploy/`(nginx.conf、systemd service、setup.sh)。
⚠️ 含服务器密码的部署脚本已在 `.gitignore` 中排除,仓库内保留的是早期版本,请不要再提交明文密码。

## 文档索引(c/docs)

| 文档 | 内容 |
|---|---|
| 知识库文档.md | 35+ 条售后知识条目 |
| UI原型描述.md / 管理员后台原型描述.md | 界面原型 |
| 测试用例表.md / AI回答测试报告_v1.md / Bug列表.md | 测试记录 |
| 用户画像文档.md / 用户体验反馈与优化记录.md | 用研 |
| 竞品体验报告.md / 竞品对比分析表.md | 竞品分析 |

## 说明

- 本仓库为课程学习项目,商品数据(AirPods 系列)仅用于演示。
- 仓库名已从占位符「-」更名为 `pineapple-after-sales-robot`(旧链接自动重定向)。
