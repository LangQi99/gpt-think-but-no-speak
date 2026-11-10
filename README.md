# GPT Think But No Speak

Agent 负责判断，另一个模型帮它把话说顺。

这是一项用于润色 Agent 汇报的 skill。输入一条进度更新或结果草稿，脚本返回改稿，Agent 再决定最后发给用户的文字。

用 Python 3.10 或更新版本。安装到 Codex 的技能目录后，可以用 `$gpt-think-but-no-speak` 调用。

```sh
git clone https://github.com/LangQi99/gpt-think-but-no-speak.git "${CODEX_HOME:-$HOME/.codex}/skills/gpt-think-but-no-speak"
```

模型地址、模型 ID 和密钥由你提供。调用命令、首次配置和本机记录方式见 [SKILL.md](SKILL.md)。
