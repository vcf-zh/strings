# vcf-zh/strings

VCF 中文化项目的字符串仓库。存放各版本、各产品的英文原文（`en_US.json`）和中文译文（`zh_CN.json`），以及供浏览器扩展使用的合并查找表（`lookup.json`）。

## 目录结构

```
versions/
  9.0/
    vsphere/
      en_US.json      # 英文原文
      zh_CN.json      # 中文译文
    vsan/
    nsx/
    operations/
    lookup.json       # 扩展使用：英文原文 → 中文译文
terminology/
  vmware_terms.json   # 品牌词和专业术语词库
```

## 如何贡献字符串

如果你有 VCF 9.0 环境，可以帮助提取真实的 UI 字符串：

1. Fork 本仓库
2. 在 `versions/9.0/<产品>/en_US.json` 中添加或补充英文字符串
3. 格式为 `"描述性的.key": "English text"`
4. 提交 PR，AI 翻译流水线会自动生成中文译文

详见 [贡献指南](CONTRIBUTING.md)。

## 产品覆盖

| 产品 | 说明 |
|------|------|
| vsphere | vSphere Client（vCenter UI） |
| vsan | vSAN 存储管理 |
| nsx | NSX 网络与安全 |
| operations | VMware Aria Operations |

## 翻译质量

- 主引擎：Google Gemini 2.0 Flash
- 备用引擎：MiniMax Text-01
- 品牌词（DRS、HA、vMotion、NSX 等）强制保留英文
- 每次 PR 自动运行完整性、占位符、术语三项检查
