# 批量处理进度

更新时间: 2026-05-20
流程: 5 步（下载音频/页面信息 -> Gemini 转录 -> 信号提取 -> 验证 -> 笔记）

## 总览

| 状态 | 集数 | 数量 |
|------|------|------|
| COMPLETE（有 transcript、signals、verified signals、notes） | 82, 172, 184-191, 193-201, 203-248 | 65 |
| 不存在（RSS / fireside 返回 404） | 192, 202 | 2 |

当前本地已完成全部可用集，最新完成到 EP248。

## 保存策略

- GitHub 保留：`README.md`、处理脚本、`output/notes/*.md`、每集 transcript、signals、verified signals；metadata 和 participants 有则保存。
- 本地忽略：音频 `*.mp3`、虚拟环境、chunk / retry / progress 临时产物、运行缓存。
- 音频可从原始播客 URL 重新下载；不作为 GitHub 持久资产。

## 已知数据缺口

- 缺少 metadata：EP193、EP219、EP221、EP242。
- 缺少 participants：EP172、EP246、EP247。
- 部分历史 participants 文件存在旧 schema（`host`）和新 schema（`hosts`）并存；现有 pipeline 能读取规范命名的 `sv101_ep{N}_participants.json`。

## 已完成集

82, 172, 184, 185, 186, 187, 188, 189, 190, 191, 193, 194, 195, 196, 197, 198, 199, 200, 201, 203, 204, 205, 206, 207, 208, 209, 210, 211, 212, 213, 214, 215, 216, 217, 218, 219, 220, 221, 222, 223, 224, 225, 226, 227, 228, 229, 230, 231, 232, 233, 234, 235, 236, 237, 238, 239, 240, 241, 242, 243, 244, 245, 246, 247, 248.

## 跳过集

- EP192: fireside.fm 返回 404，确认不存在。
- EP202: fireside.fm 返回 404，确认不存在。

## 清理记录

- 2026-05-20: `output/_trash/`、`venv/`、`scripts/__pycache__/`、过时的 `batch_progress.json` 已移到 macOS 垃圾桶。
