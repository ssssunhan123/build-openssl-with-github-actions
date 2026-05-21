# Build OpenSSL with GitHub Actions

使用 GitHub Actions 自动构建 OpenSSL 静态库和动态库，支持 Linux 和 Windows 平台。

[![Build OpenSSL](https://github.com/ssssunhan123/build-openssl-with-github-actions/actions/workflows/build.yaml/badge.svg)](https://github.com/ssssunhan123/build-openssl-with-github-actions/actions/workflows/build.yaml)

## 构建环境

| 平台 | 编译器 | 架构 |
|------|--------|------|
| Linux (ubuntu-latest) | GCC | x86_64 |
| Windows (windows-latest) | MSVC | x86_64 (VC-WIN64A-HYBRIDCRT, UCRT) |

## 构建产物

每次构建会生成对应平台的 OpenSSL 安装目录，包含：

- `bin/` — 可执行文件（openssl）
- `lib/` — 静态库（.a / .lib）和动态库（.so / .dll）
- `include/` — 头文件

## 触发方式

| 事件 | 行为 |
|------|------|
| Push 到 `master` 分支 | 构建并上传 artifacts |
| Pull Request | 构建并上传 artifacts |
| 推送 `v*.*.*` 标签 | 构建并自动发布 GitHub Release |

也可以手动在 Actions 页面通过 `workflow_dispatch` 触发。

## 修改 OpenSSL 版本

编辑 [.github/workflows/build.yaml](.github/workflows/build.yaml) 中的环境变量：

```yaml
env:
  OPENSSL_VERSION: 3.5.6   # 修改为你需要的版本
```

## 下载构建产物

- **Artifacts**：在 Actions 运行页面下载（保留 90 天）
- **Release**：推送版本标签后，在 [Releases](https://github.com/ssssunhan123/build-openssl/releases) 页面下载

## 发布新版本

```bash
git tag v3.5.6
git push origin v3.5.6
```

推送标签后，CI 会自动构建 Linux 和 Windows 产物并发布到 GitHub Release。
