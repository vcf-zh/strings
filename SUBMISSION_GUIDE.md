# 字符串包提交指引

## 前提条件
- SSH 访问 vCenter Server Appliance（通常为 root）
- 已克隆 [vcf-zh/tools](https://github.com/vcf-zh/tools) 仓库

## 提取步骤

```bash
# 克隆工具仓库
git clone https://github.com/vcf-zh/tools.git
cd tools

# 安装依赖
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# 运行提取脚本（替换为你的 vCenter IP 和产品名）
./extract/collect.sh <vcenter_ip> root vsphere 9.0
# 输出：vsphere_9.0_YYYYMMDD.json
```

## 提交步骤

1. Fork [vcf-zh/strings](https://github.com/vcf-zh/strings)
2. 将 JSON 文件放入 `submissions/` 目录
3. 提 PR，标题格式：`[提交] vsphere 9.0 字符串包 YYYY-MM-DD`
4. CI 自动验证格式
5. 验证通过后，维护者合并并触发 AI 翻译

## 字符串包格式要求

文件必须包含 `_meta` 字段：

```json
{
  "_meta": {
    "vcf_version": "9.0",
    "product": "vsphere",
    "extracted_at": "2026-06-15T10:00:00Z"
  },
  "key1": "English string 1",
  "key2": "English string 2"
}
```

## 支持的产品
| 产品 | product 值 |
|------|-----------|
| vSphere Client | `vsphere` |
| vSAN | `vsan` |
| NSX Manager | `nsx` |
| VMware Aria Operations | `operations` |

## 常见问题

**Q: 提取脚本找不到字符串文件？**
A: 不同 vCenter 版本资源路径可能不同，请在 Issue 中反馈你的路径，我们更新脚本。

**Q: CI 验证失败说字符串数量太少？**
A: 每个产品需要至少 50 条字符串，请确保提取了完整的 UI 资源文件。
