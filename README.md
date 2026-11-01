# SA-AKI 28 天院内死亡风险预测工具

脓毒症相关急性肾损伤（SA-AKI）患者入住 ICU 后 28 天院内死亡风险预测。
包含两个模块：ExtraTrees 机器学习模型（17 项特征）与简化整数评分卡（9 项变量）。

## 使用说明

纯前端实现，所有计算在浏览器本地完成，**不上传、不保存任何患者数据**。
浏览器要求：Chrome / Edge 80 及以上。

## 目录结构

| 文件 | 说明 |
|---|---|
| `index.html` | 应用入口（单页，无后端） |
| `forest.bin.gz` | 模型森林（gzip，浏览器端解压） |
| `meta.json` | 变量顺序、标准化参数、判定阈值 |
| `verify_set.csv` | 200 例校验样本，用于页面加载时的自检 |
| `.nojekyll` | 关闭 Jekyll 处理，避免构建失败 |

## 部署（GitHub Pages）

1. 新建一个 **Public** 仓库，把本目录全部文件上传到仓库根目录。
2. 仓库 **Settings → Pages → Build and deployment**：
   Source 选 `Deploy from a branch`，Branch 选 `main`，目录选 `/ (root)`，保存。
3. 等待 1–2 分钟，访问 `https://<用户名>.github.io/<仓库名>/`。
4. 如需自定义域名：在仓库根目录新建名为 `CNAME` 的文件，内容写域名（不带 http://），
   再到域名服务商处添加 CNAME 记录指向 `<用户名>.github.io`。

## 更新模型

在本地重新训练后，依次运行 `export_forest.R` → `make_deploy.py`，再把新的
`forest.bin.gz`、`meta.json`、`index.html` 上传覆盖即可。

## 免责声明

本工具仅用于科研与教学演示，不构成诊疗建议。最终临床决策须由医师结合完整病情判断。
