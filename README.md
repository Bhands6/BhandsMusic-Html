# BhandsMusic 官网静态页

BhandsMusic 桌面播放器的单页官网（纯静态，无构建步骤）。

- 线上地址：https://bhands6.github.io/BhandsMusic-Html/
- 主项目：https://github.com/Bhands6/BhandsMusicChange
- 国内镜像发布源：https://cnb.cool/BhandsCnb/BhandsMusic

## 结构

```
index.html            整页（HTML + CSS + 原生 JS，无框架、无构建）
assets/shots/         视觉预设与启动页截图（31 张，自托管）
assets/fonts/         woff2 字体（按页面用字子集化，共约 570KB）
.github/workflows/    push 到 main 自动发布到 GitHub Pages
.nojekyll             关闭 Jekyll 处理
```

## 本地预览

```bash
py -3 -m http.server 8080
# 打开 http://127.0.0.1:8080
```

## 几点约定

- **图片必须自托管。** 原稿 hotlink 到 `raw.githubusercontent.com`，该域名在国内不可直连，页面会大面积白图。
- **字体不走 Google Fonts。** `fonts.googleapis.com` / `fonts.gstatic.com` / `fonts.gstatic.cn` 在国内均不可达，字体为 Noto Serif SC 200/400/600/900 + Cormorant Garamond + DM Mono 的本地子集。
  改动文案后如出现新汉字，需重新子集化，否则缺字会回退到系统宋体。
- 页面不依赖任何后端接口，整站为静态资源。

## 更新流程

改 `index.html` → commit → push `main`，Actions 会自动重新发布，约 1 分钟内生效。

字体子集化命令（在字体 TTF 与页面同目录时）：

```bash
py -3 -m fontTools.subset NotoSerifSC_200ExtraLight.ttf \
  --text-file=index.html --flavor=woff2 \
  --output-file=assets/fonts/noto-serif-sc-200.woff2
```
