# 🧱 Monorepo 私有仓库使用说明

本项目是一个基于 **Lerna + pnpm + Verdaccio** 构建的 monorepo 架构，支持本地开发与私有 npm 仓库发布，支持通过 Cloudflare 映射到公网。

## 📁 项目结构

```
monorepo/
├── packages/
│   ├── yd-ui/          # UI 组件库
│   └── yd-hooks/       # 通用 hooks 库
├── package.json
├── pnpm-workspace.yaml
```
  
## 🚀 使用流程

### ✅ 1. 安装依赖

```bash
pnpm install
```

### ✅ 2. 启动 Verdaccio 本地私仓

```bash
pnpm add -g verdaccio   # 如未安装
verdaccio               # 默认监听 http://localhost:4873
```

### ✅ 3. 登录本地私仓

```bash
npm adduser --registry http://localhost:4873
```

### ✅ 4. 发布某个包

```bash
cd packages/yd-ui
npm publish --registry http://localhost:4873
```

### ✅ 5. 启动公网访问

```bash
brew install cloudflared     # 如果未安装
cloudflared tunnel --url http://localhost:4873
```

✅ 获取一个公网地址，例如：
```
https://golden-eagle-7b1a.trycloudflare.com
```

### ✅ 6. 给其他人使用

告诉他将 `.npmrc` 设置为：

```ini
registry=https://golden-eagle-7b1a.trycloudflare.com/
```

然后安装即可：

```bash
npm install @yideng/ui
```

## ✅ 总结命令合集

```bash
verdaccio
npm adduser --registry http://localhost:4873
cd packages/yd-ui
npm publish --registry http://localhost:4873
cloudflared tunnel --url http://localhost:4873
```
