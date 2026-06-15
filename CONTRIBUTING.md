# 贡献指南

感谢参与 VCF 中文化项目！最需要的贡献是**提取真实的 VCF UI 字符串**。

## 三种贡献方式

### 1. 提交英文字符串（有 VCF 9.0 环境的同学最需要做这个）

找到对应产品目录，编辑 `en_US.json`：

```
versions/9.0/vsphere/en_US.json   # vSphere Client
versions/9.0/vsan/en_US.json      # vSAN
versions/9.0/nsx/en_US.json       # NSX Manager
versions/9.0/operations/en_US.json # Aria Operations
```

格式：

```json
{
  "现有的key": "现有的文本",
  "新增.key": "New English Text"
}
```

Key 命名规则：小写加点分隔，前缀参考 `action.`（操作）、`label.`（标签）、`msg.`（提示）、`nav.`（导航）、`status.`（状态）。

提交 PR 后，AI 翻译流水线自动生成 `zh_CN.json` 和 `lookup.json`。

**如何从浏览器提取字符串：**
1. 用 Chrome 打开 vSphere Client / NSX Manager / Aria Operations
2. 按 F12 → Network 标签 → 刷新页面（F5）
3. 搜索 `l10n` 或 `i18n` 或 `messages`，找到含大量 `"key": "value"` 的 JSON 响应
4. 将内容转换为我们的格式后提交 PR

### 2. 修正翻译错误

1. Fork 本仓库
2. 编辑 `versions/{version}/{product}/zh_CN.json`
3. 提 PR，描述中注明原文 / 错误译文 / 修正译文 / 修正原因

品牌词（不得翻译）：vMotion、NSX、DRS、HA、VCF、ESXi、vSAN、BGP、VXLAN 等，详见 [terminology/vmware_terms.json](terminology/vmware_terms.json)。

### 3. 扩充专业词库

1. 编辑 `terminology/vmware_terms.json`
2. 提 PR，注明术语来源（官方文档链接或产品界面截图）

## Issue 类型
- `翻译错误反馈`：原文 / 当前译文 / 建议译文
- `字符串缺失`：产品 / 版本 / 功能区域
- `词库争议`：发起术语译法讨论

## 角色说明
| 角色 | 职责 |
|------|------|
| Maintainer | 最终合并 PR、发布 Tag/Release |
| Reviewer | 审校 AI 翻译 PR、维护词库 |
| Contributor | 提交字符串包、修正译文、扩充词库 |
