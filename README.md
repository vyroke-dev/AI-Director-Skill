# AI Director Skill (v2 direction · upgrade preview)

一套受公开影视生成工作流启发的、**独立开发**的 AI 导演 Skill。提供自然语言导演式对话、创意发展、镜头规划、角色/场景/道具连续性、分镜文字预演、视频生成提示词、审查与局部迭代。

**不是** Higgsfield 官方产品、其私有 AI Director 的复制品，也不附带付费视频生成权限。没有外部工具时仍可独立完成导演方案、shot list 和 prompt pack。有可用视频工具时，先检索其真实能力并遵循 `SKILL.md` 中的授权和费用检查点。

## 安装

将整个 `ai-director/` 文件夹复制到所用 Agent 支持的 **Skills 目录**，确保根目录下是 `SKILL.md`（不是嵌套两层）。安装位置及是否支持自动加载由 Agent/IDE 版本决定，请查看宿主平台文档。

对于支持 Skills 标准的 Claude 系环境，一般可将此文件夹加入个人或项目 Skills 目录；在其他 Agent 中，也可直接加载 `SKILL.md` 及其引用文件作为工作规范。**这不等于该 Agent 自动拥有 Higgsfield API 权限。**

## 专业 AI 漫剧与自定义模型

这个仓库是 **可下载并安装到 Agent 的 Skill**，不是需要部署的视频 SaaS。新版导演流程通过独立的 `references/series-production.md`、`references/director-panel.md`、`references/model-routing.md` 为 Agent 提供：

- **AI 漫剧**：分集剧情、场景与分镜导演、人物表演、对白与剪辑节奏，跨集 canon 和状态交接。
- **摄影控制**：全局艺术方向与逐镜头景别、机位、运动、光学意图和灯光。
- **用户自带模型（BYOM）**：从 Agent 实际拥有的工具、API、MCP 或本地模型读取真实能力，再为每个镜头选择兼容的生成方案。
- **成本与审查**：付费调用前审批、可追踪请求、镜头级修复、媒体证据检查。

安装方式保持不变。**不要求 Higgsfield 模型、账号或服务。** 如果 Agent 没有生成工具，仍可产出可交接的剧本、分镜、资产和提示词，不会假装完成渲染。

重要边界：现有 `assets/project.schema.json` 和 `scripts/validate_project.py` 仍采用 v1 的**单影片结构**；多集 ledger 暂时作为独立项目文件，需要后续单独版本化 schema 和自动验证，不应误称已支持全面结构化验证。升级分支中为导演流程与参考规范增强，非完整 v2 发布。

### 漫剧示例

> 我正在制作 AI 漫剧。先读取我的剧本、上一集状态和角色参考，再规划 EP03 的场景、分镜、角色表演、对白和剪辑。保留 canon，只使用 Agent 已连接的我的图像/视频/音频模型。先输出制作方案和费用预检，未经批准不要提交付费生成。

## 快速体验

以中文或英文输入：

> 用 AI Director 为我设计一支 20 秒的雨夜科幻悬疑预告片，9:16，一名人物，要求角色外观一致。先给导演方案、分镜和生成 prompts，不要实际花费 credits。

或：

> Act as my AI Director. Turn this product concept into a 15-second commercial with three coherent shots. Please give camera, lens, lighting and continuity instructions.

## 包内文件

- `SKILL.md`：触发条件、行为原则、模式选择、工作流、交付及质量关卡。
- `references/series-production.md`：AI 漫剧分集、canon、场景与镜头状态管理。
- `references/director-panel.md`：全局/逐镜头摄影、动画表演与节奏控制。
- `references/model-routing.md`：自带模型能力发现、提示词转换、授权与失败恢复。
- `references/`：导演知识、连续性、对话协议、provider 集成、研究来源。
- `assets/project.schema.json`：独立于提供商的 JSON Schema（Draft 2020-12）。
- `assets/project-template.json`：可复制起步模板。
- `assets/example-noir-project.json`：可验证的黑色电影三镜头示例。
- `assets/prompt-templates.md`：分镜、静帧、视频和审查提示词模板。
- `scripts/validate_project.py`：Python 标准库离线项目检查器，无第三方依赖。
- `tests/test_validator.py`：自动化测试。
- `tests/acceptance-cases.md`：实际 Agent 行为测试情景和验收判据。

## 验证

```bash
python3 scripts/validate_project.py assets/example-noir-project.json
python3 -m unittest discover -s tests -v
```

验证器检查必要字段、数据类型、时长之和、ID 引用、屏幕方向及项目内重复 ID。它不能代替真实影片视觉检查和真人试映。

## Integration 边界

官方文档在 2026-11-11 显示 Higgsfield API 使用 `https://platform.higgsfield.ai`、`Authorization: Key ID:SECRET`、异步提交/状态轮询。不同视频模型的 payload 不通用；这里**不**提供未经验证的“通用视频生成 endpoint”。调用前需按当时模型目录进行模型专属配置并获得用户授权。网站订阅与 API 收费体系不同。

## Sources

研究与原始官方链接见 `references/research-notes.md`。内容按公开能力重新设计，不包含第三方源代码或专有提示词。
