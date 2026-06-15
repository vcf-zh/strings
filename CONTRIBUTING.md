# 贡献指南

## 三种贡献方式

### 1. 提交字符串包（需要 vCenter 环境）
参见 [SUBMISSION_GUIDE.md](SUBMISSION_GUIDE.md)

### 2. 修正翻译错误
1. Fork 本仓库
2. 编辑 `versions/{version}/{product}/zh_CN.json`
3. 提 PR，描述中注明：
   - 原文（EN）
   - 错误译文
   - 修正译文
   - 修正原因

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
