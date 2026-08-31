# 朱文涛 GitHub Pages 个人技术简历网站

这是一个可直接部署到 GitHub Pages 的纯静态项目：不依赖框架、npm、打包工具或外部图片 CDN。本地双击 `index.html` 即可预览，上传 GitHub 后也能直接使用。页面采用白色背景与蓝、青、珊瑚、紫、金等低饱和强调色；10 个重点项目均独立成卡，并使用“逐屏故事窗口”展示背景、方法、技术图、结果和产出。

## 1. 完整文件夹结构

```text
zwtResume/
├── .nojekyll
├── index.html
├── README-部署说明.md
└── assets/
    ├── favicon.svg
    ├── 朱文涛_个人简历.pdf
    ├── AutoAttribRec.pdf
    ├── Multi_channel_Uplift.pdf
    ├── mtgr_arch1.png
    ├── mtgr_sample.png
    ├── mtfm_arch.png
    ├── hta_scta.png
    ├── mtfm_scaling_exp.png
    ├── onelive_tokenizer.png
    ├── mtp_arch.png
    ├── semantic_distill.png
    ├── unir2_arch.png
    ├── unir2_table.png
    ├── gr_infer_arch.png
    ├── rgd_concept.svg
    ├── llm_recall_pipeline.png
    ├── llm_recall_ablation.png
    ├── mixtrans_arch.png
    ├── autoattribrec_arch.png
    ├── autoattribrec_compare.png
    ├── joint_uplift_arch.png
    ├── joint_uplift_table.png
    ├── uno_arch.png
    ├── uno_exp_table.png
    └── diffusion_arch.svg
```

`index.html` 已内置全部 CSS 和 JavaScript，因此项目没有 `css/`、`js/`、`node_modules/` 或构建目录。

## 2. 本地预览

### 最简单方式

解压后直接双击项目根目录的 `index.html`。

### 使用本地静态服务（可选）

如果电脑已安装 Python，可在项目根目录运行：

```bash
python3 -m http.server 8000
```

然后访问 `http://localhost:8000`。

## 3. 替换 assets 中的图片

1. 在 PPT 里选中需要的架构图或表格，导出为 PNG。
2. 参照上方文件树，把图片重命名为对应文件名，例如 `mtfm_arch.png`。
3. 把新图片放入 `assets/` 并覆盖同名文件。
4. 保持文件名和扩展名不变，无需修改 HTML。

建议：

- 架构图优先用 16:9 或接近 16:9 的 PNG。
- 单张图建议宽度 1600–2400 px，既清晰又不会过大。
- 不要在文件名里使用空格、`#`、`?` 等特殊字符。
- 如果修改文件名，必须同步修改 `index.html` 中的 `src="./assets/文件名"` 和点击大图用的 `href`。

## 4. GitHub Pages 完整部署步骤

### 方式 A：网页直接上传（最适合第一次部署）

1. 在 GitHub 新建公开仓库，例如 `zwtResume`。
2. 打开解压后的项目文件夹。
3. 在仓库页面选择 **Add file → Upload files**。
4. 上传项目文件夹里的内容：`index.html`、`.nojekyll`、`README-部署说明.md` 和整个 `assets` 目录。
5. 确认仓库的 `main` 分支根目录可直接看到 `index.html`。不要只上传 ZIP，也不要让 `index.html` 多套一层文件夹。
6. 进入 **Settings → Pages**。
7. 在 **Build and deployment** 中选择 **Deploy from a branch**。
8. Branch 选择 **main**，文件夹选择 **/ (root)**，点击 **Save**。
9. 等待 1–3 分钟；仓库上方 **Actions** 中的 Pages 任务变绿后，访问：

```text
https://你的GitHub用户名.github.io/zwtResume/
```

如果仓库名是 `你的GitHub用户名.github.io`，则地址是：

```text
https://你的GitHub用户名.github.io/
```

### 方式 B：使用 Git 上传

```bash
git init
git add .
git commit -m "build: add personal resume website"
git branch -M main
git remote add origin https://github.com/你的用户名/zwtResume.git
git push -u origin main
```

随后仍按方式 A 的第 6–9 步开启 GitHub Pages。

## 5. 常见部署问题

### 页面只显示 README，没有简历首页

检查 GitHub 仓库的 `main` 分支根目录是否直接存在名为 `index.html` 的文件，并确认 Pages 发布目录是 `/ (root)`。

### 页面能打开，但图片不显示

检查：

- `assets` 目录是否与 `index.html` 同级。
- 文件名大小写是否完全一致，GitHub Pages 区分大小写。
- HTML 中是否使用 `./assets/xxx.png`，不要改成电脑本地的绝对路径。
- 是否只上传了 HTML，忘记上传 `assets`。

### 更新代码后网页没变

先等待 Actions 里的 Pages 部署任务完成，然后使用浏览器强制刷新：Windows 使用 `Ctrl + F5`，macOS 使用 `Command + Shift + R`。

## 6. 修改现有项目卡片

项目和论文内容统一存放在 `index.html` 内部 JavaScript 的数据数组中：

- `const projects = [...]`：10 个独立项目。
- `const papers = [...]`：4 篇论文。
- `const honors = [...]`：4 项荣誉。

一个项目对象的核心结构如下：

```javascript
{
  id: 'mtfm',
  company: '美团',
  palette: 'blue',
  title: 'MTFM 多业务统一精排',
  cover: A + 'mtfm_arch.png',
  contribution: '卡片上展示的核心贡献',
  tags: ['HSTU', '异构 Token'],
  cardMetrics: [metric('>1.5pp', 'CTR-GAUC')],
  slides: [
    slide('01 / 背景', '本屏标题', '本屏摘要', A + 'mtfm_arch.png',
          '内容标题', '<p>详细内容</p>',
          [img('mtfm_arch.png', '图片说明', true)])
  ]
}
```

修改首页卡片时，编辑 `title`、`cover`、`contribution`、`tags` 和 `cardMetrics`；修改详情窗口时，编辑对应项目的 `slides`。

## 7. 新增项目卡片

1. 在 `const projects = [...]` 中复制一个完整项目对象。
2. 将 `id` 改成不重复的英文标识，例如 `new-project`。
3. 修改 `company`。如果使用现有四家公司之一，页面会自动归入对应公司；新增公司时还需要在 `companyMeta` 中加入公司名称、部门、时间和颜色。
4. 设置 `cover`，它会成为首页项目卡片的大图。
5. 在 `slides` 中按顺序增加背景、方法、创新、结果和产出。每个项目可以有不同数量的屏幕和图片。
6. 将新图片放到 `assets/`，并使用相对路径：

```html
<img src="./assets/new_project_arch.png" alt="新项目架构图" loading="lazy">
```

## 8. 新增论文或荣誉卡片

方法与新增项目相同：

- 新论文对象加入 `const papers = [...]`，并为 `cover` 指定一张核心方法图。
- 新荣誉对象加入 `const honors = [...]`。
- 每个 `id` 必须唯一；页面会自动生成卡片和对应详情窗口。

## 9. 逐屏详情窗口交互说明

- 点击任意项目、论文或荣誉卡片打开详情。
- “上一屏 / 下一屏”按钮用于按顺序阅读项目故事。
- 键盘左右方向键可以切换屏幕，`Esc` 关闭窗口。
- 手机端支持左右滑动切换；上下滑动仍用于阅读当前屏的长内容。
- 底部圆点可以直接跳到指定屏幕，顶部显示当前进度，例如 `02 / 05`。
- 点击右上角关闭按钮或蒙层空白处也可关闭。
- 每一屏可以配置一张或多张技术图；多图自动换行，点击图片可查看原图。

## 10. 维护建议

- 所有项目收益均保持统一口径：`+x%`、`+xpp`、`x → y`。
- 未公开的业务信息在上传 GitHub 前请再次审核。
- 有新论文版本时，同步更新论文卡片、项目弹窗和外链。
- 上传后建议在电脑和手机上分别检查卡片、弹窗滚动、PDF 下载和图片大图链接。
