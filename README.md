# mermaid-zh · Mermaid 在线编辑器（简体中文本地版）

## 本项目主要解决什么问题

**本地一键跑通 Mermaid 在线编辑器，并提供简体中文界面。**

官方 [mermaid-live-editor](https://github.com/mermaid-js/mermaid-live-editor) 功能完整，但界面默认是英文，且很多人希望：

- 在本机直接编辑，不依赖外网在线服务
- 改完代码后实时预览
- 切换深色 / 浅色主题
- 导出 PNG、SVG

本仓库在官方开源编辑器基础上，做了**简体中文界面本地化**（`zh-cn-local`），方便中文用户本地安装、演示和二次开发。

> 上游项目： [mermaid-js/mermaid-live-editor](https://github.com/mermaid-js/mermaid-live-editor)（MIT License）  
> 本仓库保留上游 `LICENSE`，中文改动仅针对界面文案，不改变 Mermaid 渲染逻辑。

---

## 功能一览

| 能力 | 说明 |
| --- | --- |
| 实时预览 | 左侧编辑，右侧即时出图 |
| 简体中文界面 | 菜单、按钮、导出等主要文案已汉化 |
| 主题切换 | 深色 / 浅色 |
| 导出 | PNG、SVG |
| 本地运行 | `pnpm` 安装依赖后即可开发服务器预览 |

截图见 [`docs/screenshots/`](docs/screenshots/)。

---

## 快速开始

### 环境要求

- Node.js（建议与上游一致的较新 LTS）
- [pnpm](https://pnpm.io/)

### 安装与运行

```bash
git clone https://github.com/qhe85266-cyber/mermaid-zh.git
cd mermaid-zh
pnpm install
pnpm dev
```

浏览器打开终端里提示的本地地址（一般为 `http://localhost:3000` 或 Vite 打印的端口）即可使用。

其他常用命令：

```bash
pnpm build      # 生产构建
pnpm preview    # 预览构建结果
```

---

## 中文改动说明与如何还原英文

- 中文界面改动集中在 `src/lib/components/` 与 `src/routes/(app)/edit/+page.svelte` 等界面组件。
- 仓库根目录提供完整补丁文件 [`zh-cn.patch`](zh-cn.patch)，对应「上游 develop → 简体中文」的差异。

### 还原为英文界面

任选其一：

```bash
# 方式 A：用 git 撤掉汉化提交（若你基于本仓库历史）
git revert HEAD   # 或 reset 到汉化前的上游提交（慎用）

# 方式 B：从当前树反向打补丁（在干净工作区）
git apply -R zh-cn.patch
```

也可直接对照上游重新 clone：

```bash
git clone https://github.com/mermaid-js/mermaid-live-editor.git
```

---

## 与上游的关系

| 项目 | 说明 |
| --- | --- |
| 上游 | https://github.com/mermaid-js/mermaid-live-editor |
| 许可证 | MIT（见 [`LICENSE`](LICENSE)） |
| 本仓库增量 | 简体中文 UI 文案 + 本 README + 验证截图 + `zh-cn.patch` |
| 未包含 | `node_modules`、构建产物、`.svelte-kit` 等本地缓存 |

欢迎把上游的安全修复与功能更新合并回来；合并冲突时优先保留功能正确性，再补中文文案。

---

## 免责声明

本仓库为学习 / 演示用途的本地化衍生，**不是** Mermaid 官方中文版。图表语法与渲染仍由上游 Mermaid 生态提供。顶部推广横幅、部分图表类型英文名等上游内容可能仍为英文。
