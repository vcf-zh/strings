# GitHub 上线操作清单

## 项目概况

本项目包含四个代码仓库，总计 **3,761 个文件**：

| 仓库 | 文件数 | 描述 |
|------|--------|------|
| `strings` | 13 | VCF 中文化翻译字符串库 |
| `tools` | 3,735 | VCF 中文化工具链（包含 Python 环境依赖） |
| `extension` | 7 | VCF 中文化浏览器 Chrome 扩展 |
| `deploy` | 6 | VCF 中文化服务器端部署配置 |

## 第一步：创建 GitHub 组织

1. 访问 https://github.com/organizations/new
2. 组织名填写：`vcf-zh`
3. 类型选择：Free
4. 完成组织创建

## 第二步：创建四个仓库

在 `vcf-zh` 组织下创建以下公开仓库。有两种方式：

### 方式 A：使用 GitHub 网页界面

对于每个仓库，在 GitHub 组织首页：
1. 点击 "New" 按钮
2. 填写仓库名
3. 选择 "Public"
4. 点击 "Create repository"

需要创建的仓库列表：
- **vcf-zh/strings** — VCF 中文化翻译字符串
- **vcf-zh/tools** — VCF 中文化工具链
- **vcf-zh/extension** — VCF 中文化浏览器扩展
- **vcf-zh/deploy** — VCF 中文化服务器端部署

### 方式 B：使用 GitHub CLI（可选）

如果已安装 `gh` 工具，运行以下命令：

```bash
gh repo create vcf-zh/strings   --public --description "VCF 中文化翻译字符串"
gh repo create vcf-zh/tools     --public --description "VCF 中文化工具链"
gh repo create vcf-zh/extension --public --description "VCF 中文化浏览器扩展"
gh repo create vcf-zh/deploy    --public --description "VCF 中文化服务器端部署"
```

## 第三步：推送本地代码到 GitHub

四个仓库都已有本地代码和完整的 git 历史。运行以下命令推送到远程：

```bash
BASE=/Users/tyuan/Documents/vcf-zh

# 推送 strings 仓库
cd $BASE/strings
git remote add origin "https://github.com/vcf-zh/strings.git"
git branch -M main
git push -u origin main

# 推送 tools 仓库
cd $BASE/tools
git remote add origin "https://github.com/vcf-zh/tools.git"
git branch -M main
git push -u origin main

# 推送 extension 仓库
cd $BASE/extension
git remote add origin "https://github.com/vcf-zh/extension.git"
git branch -M main
git push -u origin main

# 推送 deploy 仓库
cd $BASE/deploy
git remote add origin "https://github.com/vcf-zh/deploy.git"
git branch -M main
git push -u origin main
```

**注意：** 使用 HTTPS URL 时，GitHub 会提示输入个人访问令牌（PAT）而非密码。如已配置 SSH，可改用 `git@github.com:vcf-zh/...git` 形式。

## 第四步：配置 GitHub Actions Secrets

仅在 `vcf-zh/tools` 仓库需要配置 Secrets，用于自动翻译工作流。

**步骤：**
1. 打开 https://github.com/vcf-zh/tools/settings/secrets/actions
2. 依次点击 "New repository secret"，添加以下三个 Secret：

| Secret 名称 | 说明 | 获取方式 |
|------------|------|----------|
| `ANTHROPIC_API_KEY` | Claude API Key | 访问 https://console.anthropic.com，在 API Keys 页面复制 |
| `DASHSCOPE_API_KEY` | 通义千问 API Key | 访问 https://dashscope.console.aliyun.com，在 API keys 页面获取 |
| `STRINGS_REPO_TOKEN` | GitHub PAT，需要 `vcf-zh/strings` 仓库的写权限 | 访问 https://github.com/settings/tokens/new，选中 `repo` 和 `workflow` 权限，复制 token |

**配置示例：**

- 打开 `ANTHROPIC_API_KEY` Secret 设置
  - Value：粘贴从 Anthropic 控制台获取的 API Key
  - 点击 "Add secret"

- 重复上述步骤添加 `DASHSCOPE_API_KEY` 和 `STRINGS_REPO_TOKEN`

## 第五步：验证 GitHub Actions 工作流

推送代码后，检查自动化流水线是否正常运行。

**手动触发翻译流程（可选）：**
1. 打开 https://github.com/vcf-zh/tools/actions
2. 选择 "Auto Translate" 工作流
3. 点击 "Run workflow" 按钮
4. 输入参数：
   - `version`: `9.0`
   - `product`: `vsphere`
5. 点击 "Run workflow"
6. 监视流水线运行状态（Translating... → Merging → Complete）

**自动触发条件：**
- 当 `strings` 仓库创建新标签时（格式：`v*`），自动触发翻译

## 第六步：邀请共同维护者（可选）

如需添加其他团队成员维护组织和仓库：

1. 打开 https://github.com/orgs/vcf-zh/people
2. 点击 "Add member" 按钮
3. 输入 GitHub 用户名
4. 选择权限级别并确认邀请

## 完成清单

完成以上步骤后，项目将可用于：

- [ ] GitHub 组织 `vcf-zh` 已创建
- [ ] 四个仓库已创建并设为 Public
- [ ] 本地代码已推送到 GitHub
- [ ] `tools` 仓库的三个 Secrets 已配置
- [ ] GitHub Actions 工作流能正常运行
- [ ] 团队成员已邀请（如需要）

---

**最后验证：** 执行以下命令检查四个仓库是否已正确连接到远程：

```bash
BASE=/Users/tyuan/Documents/vcf-zh
for repo in strings tools extension deploy; do
  echo "=== $repo ==="
  cd $BASE/$repo
  git remote -v
done
```

预期输出应包含指向 `https://github.com/vcf-zh/` 的 origin URL。
