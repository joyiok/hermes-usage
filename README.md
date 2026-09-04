# hermes-usage

查看 Hermes Agent `state.db` 里记录的 LLM token 用量 —— 按模型、按会话，只读（不会锁住正在运行的 gateway 数据库）。

## 安装

```bash
cp hermes-usage ~/.hermes/bin/   # 或放到 PATH 上的任意位置
chmod +x ~/.hermes/bin/hermes-usage
```

## 用法

```bash
hermes-usage                 # 当前会话（最近活跃的），按模型拆分 + TOTAL
hermes-usage --session 会话ID # 指定一个会话
hermes-usage --all           # 所有会话逐条明细 + GRAND TOTAL（含 approval/background 等后台任务）
hermes-usage --list          # 会话列表 + 总计行
```

通过 `$HERMES_HOME` 定位数据库（没有则回退到 `~/.hermes`），多 profile 通用。

## 说明

- 数字在每次 API 调用完成后更新；正在进行中的这一轮还没计入。
- `cost_status` 通常是 `unknown`、费用为 0 —— 多数 provider 不上报计价，token 数才是可靠信号。
- 长会话里 `cache_read_tokens` 占大头（缓存命中远大于输入 = prompt caching 正常工作）。

## SKILL.md

附带 Hermes skill 定义 —— 把本仓库（或只要 `SKILL.md`）放到 skills 目录，agent 需要时就会用 `hermes-usage` 查用量。

## License

MIT
