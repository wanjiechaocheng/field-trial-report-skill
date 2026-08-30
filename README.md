# field-trial-report —— 田间试验报告自动生成 Skill

一个用于 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)（及其他支持本地 Skill 的 Agent）的 **Skill**：根据作物品种区域试验/生产试验的原始数据，自动生成结构完整、含数据表和品种评述的试验总结报告。

支持作物：**水稻、玉米、小麦、棉花**，并可按模板扩展其他作物。

## 目录结构

```
field-trial-report-skill/
├── README.md                      本说明
├── LICENSE                        MIT 许可证
├── field-trial-report/            ← 技能本体（复制这一整个文件夹即可安装）
│   ├── SKILL.md                   主技能：通用结构、作物调度、文风与表格规范
│   ├── crops/                     各作物专属规范
│   │   ├── cotton.md              棉花（纤维品质/抗病虫/审定标准）
│   │   ├── rice.md                水稻（农艺/米质/抗性）
│   │   ├── corn.md                玉米（农艺/籽粒品质/抗性）
│   │   └── wheat.md               小麦（农艺/籽粒品质/抗性）
│   └── templates/
│       └── report-outline.md      通用报告骨架模板
└── examples/                      （可选）放你自己的往年范本，供 AI 对齐格式
```

## 安装

把 `field-trial-report/` 文件夹整体复制到任一被扫描的技能根目录即可（**无需重启**，监听器会自动发现）：

- **项目级**（仅该项目生效，推荐）：
  - `<项目根>/.dsh/skills/field-trial-report/`
  - 或 `<项目根>/.agents/skills/field-trial-report/`
- **用户级**（所有会话全局生效）：
  - `~/.dsh/skills/field-trial-report/`
  - Windows 上通常为 `C:\Users\<用户名>\.dsh\skills\field-trial-report\`

## 使用

1. 把试验数据（Excel、文本或直接描述）发给 Agent，例如：
   > 根据这份 2024 年水稻区试数据，生成区域试验总结报告。
2. Agent 会自动识别作物并加载对应规范、按报告结构撰写。
3. 也可以手动强制调用：输入 `/field-trial-report`。

## 扩展新作物

1. 在 `crops/` 下新建 `<作物>.md`，仿照既有文件填写：农艺性状与单位、产量指标、品质指标、抗性指标与分级、审定/筛选标准、常见表格。
2. 在 `SKILL.md` 的「支持作物与作物规范文件」表格中登记一行。

## 参考范本

把往年的真实总结报告（PDF 或 `.txt`）放进 `examples/`，AI 写作时会自动读取并对齐其章节结构、措辞与表格样式，输出更贴合你的既有格式。范本涉及内部数据时，请勿上传到公开仓库。
