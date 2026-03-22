# Fortune Telling Skills 仓库规则

本仓库是运势测算 Skill 集合，包含多个玄学领域的独立 Skill。

## 架构原则

- 每个 Skill 是一个独立子目录，包含自己的 `SKILL.md` 和 `references/`
- `fortune-hub/` 是统一入口路由 Skill，引导用户选择领域
- 每个 Skill 必须能**独立使用**，不依赖 fortune-hub

## 记忆系统（双源记忆）

每个 Skill 的 `MEMORY.md`（gitignored）存储用户信息，读取顺序：

1. 本 Skill 的 `MEMORY.md` — 最优先
2. `fortune-hub/MEMORY.md` — 补充缺失的共享字段
3. 同仓库其他 Skill 的 `MEMORY.md` — 可选补充
4. 都没有 → 询问用户 → 写入本 Skill 的 `MEMORY.md`

## 表达伦理（所有 Skill 必须遵守）

- 赋权而非预测：让用户感到掌控力增强
- 可能性而非确定性：使用"趋势指向""可能会"
- 引导而非恐吓：负面信息必须附带建设性方向
- 禁止：死亡预测、绝对化断言、恐吓性语言、依赖性引导
