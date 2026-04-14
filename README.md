<div align="center">

<img src="./.assets/DogDayAndroid.png" width="200" height="175" alt="banner">

# Chopin Kernel Builder

使用 GitHub Actions 为 Redmi Note 10 Pro (chopin) 构建 4.14 内核

![License](https://img.shields.io/static/v1?label=License&message=BY-NC-SA&logo=creativecommons&color=green)

</div>

---

## 功能特性

- 基于 **Proton Clang** 工具链编译 4.14 内核
- 集成 **ReSukiSU** (Manual Hook) KernelSU 支持
- 支持 **KPM**（内置 / KPatch-Next）后补丁
- **AnyKernel3** 刷入包打包（可选）
- **ccache** 编译加速 + 缓存管理
- 自动发布 **GitHub Release**，附带结构化构建信息
- 所有功能通过 `workflow_dispatch` inputs **运行时动态配置**

## 使用方法

1. Fork 本仓库
2. 前往 **Actions** 页面 → **Chopin 4.14 内核构建** → **Run workflow**
3. 按需调整以下 inputs 后点击运行：

| Input | 类型 | 默认值 | 说明 |
|-------|------|--------|------|
| `ksu_enabled` | boolean | `true` | 是否集成 ReSukiSU (Manual Hook) |
| `kpm_enable` | choice | `builtin` | KPM 模式：`false` / `builtin` / `kpn` |
| `use_anykernel` | boolean | `true` | 是否打包 AnyKernel3 刷入包 |
| `ccache_enabled` | boolean | `true` | 是否启用 ccache 加速 |
| `ccache_update` | boolean | `false` | 是否强制刷新 ccache 缓存 |
| `release` | boolean | `true` | 是否发布到 GitHub Releases |
| `kernel_suffix` | string | _(空)_ | 自定义内核后缀 |

4. 编译完成后，在 **Artifacts** 或 **Releases** 页面下载产物

> [!NOTE]
> 首次运行或遇到 Release 403 错误时，请前往仓库 **Settings → Actions → General → Workflow permissions**，选择 **Read and write permissions**。

## 工作流结构

```
build job          → 编译内核，上传 Image + AnyKernel3.zip
  └── release job  → 下载产物，创建 GitHub Release
```

## 致谢

- [ChopinKernels/kernel-builder-chopin](https://github.com/ChopinKernels/kernel-builder-chopin) — 原仓库
- [DogDayAndroid/Android-Kernel-Builder](https://github.com/DogDayAndroid/Android-Kernel-Builder) — 项目原型
- [cctv18/oppo_oplus_realme_sm8850](https://github.com/cctv18/oppo_oplus_realme_sm8850) — 脚本灵感
- [ReSukiSU](https://github.com/ReSukiSU/ReSukiSU) — KernelSU Manual Hook
- [SukiSU-Ultra/SukiSU_KernelPatch_patch](https://github.com/SukiSU-Ultra/SukiSU_KernelPatch_patch) — KPM 补丁工具
- [KernelSU-Next/KPatch-Next](https://github.com/KernelSU-Next/KPatch-Next) — KPN 补丁工具
- [osm0sis/AnyKernel3](https://github.com/osm0sis/AnyKernel3) — 内核刷入包框架
- [kdrag0n/proton-clang](https://github.com/kdrag0n/proton-clang) — Proton Clang 编译工具链

## License

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
