---
name: gpt-think-but-no-speak
description: Polish an agent's user-facing progress updates, blockers, and final task reports with a separately configured language model. Use before reporting work to the user or when asked to make a draft sound more natural.
---

在向用户汇报进度、阻塞或结果前，先写下原本要说的内容。把这份原稿交给脚本，拿回润色稿，再结合实际情况决定最终怎么说。原稿和润色稿都只是材料。保留事实、数字、状态、不确定性、命令和路径，发现改稿改变了意思就修正或用原稿。

从本技能目录运行脚本。短稿可以作为参数传入，多行稿件从标准输入传入。

```sh
python3 scripts/polish.py -- '已修复导出问题，12 项测试通过。'
python3 scripts/polish.py < draft.md
```

只传准备给用户看的原稿。按用户授权的范围使用其指定的模型接口。脚本成功时只在标准输出写润色稿。接口超时、报错、截断或没有正文时，照常用原稿汇报。

## 首次配置

`python3 scripts/polish.py --check-config` 检查本机设置，退出码 `2` 表示配置缺失或无效。首次需要润色时，只向用户询问缺少的 `base_url`、`model` 和密钥来源。同一份配置缺失只问一次，等回复期间用原稿继续工作。用户给出缺少的配置后，在本机保存并直接使用。以后配置可用就直接调用。

复制 [config.example.json](config.example.json) 到本机配置目录 `~/.config/gpt-think-but-no-speak/config.json`。如果设了 `XDG_CONFIG_HOME`，用该目录下的同名路径。可用 `--config` 指定其他本机配置文件。把 `base_url` 填成 OpenAI 兼容的 Chat Completions 基础地址，脚本会补上 `/chat/completions`。也可以填完整端点。`model` 用网关实际接受的模型 ID。供应方额外参数放在 `request_extra`，如关闭思考的开关。

`api_key_env` 可以指向已有环境变量。需要把 `api_key` 持久存入本机配置时，将文件权限设成 `0600`。免鉴权接口显式设 `"auth": "none"`。初始模板没有可调用的模型或密钥。用户给出的接口如果用其他协议，先按该接口的文档适配脚本。

## 本机调用记录

待配置。用户首次提供配置后，在本机安装的这份 `SKILL.md` 更新这里，记录协议、模型 ID、配置文件位置和调用命令。记录密钥的读取方式即可。实际密钥与本机配置留在本机，公开仓库保留空模板。
