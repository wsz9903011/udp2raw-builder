# Phantun OpenWrt Package Builder

本项目用于通过 **GitHub Actions** 自动编译 **Phantun** 的 OpenWrt 安装包。

## 编译环境

- OpenWrt：25.12.4
- Target：rockchip/armv8
- Architecture：aarch64 (ARMv8)
- SDK：OpenWrt 官方 SDK
- 编译平台：GitHub Actions (Ubuntu 24.04)

---

## 目录结构

```text
.
├── .github
│   └── workflows
│       └── build.yml
├── package
│   └── phantun
│       ├── Makefile
│       └── files
└── README.md
```

---

## 编译步骤

### 1. Fork 或 Clone 本仓库

```bash
git clone https://github.com/<yourname>/phantun-builder.git
```

---

### 2. 上传 Package

将 OpenWrt Package 放入：

```text
package/phantun
```

目录应类似：

```text
package
└── phantun
    ├── Makefile
    ├── files
    └── ...
```

---

### 3. 开始编译

进入 GitHub：

```
Actions
    ↓
Build OpenWrt Package
    ↓
Run workflow
```

等待编译完成。

---

### 4. 下载编译结果

编译成功后：

```
Actions
    ↓
Artifacts
    ↓
OpenWrt-Packages
```

下载即可获得：

```
phantun-client.apk
phantun-server.apk
```

---

# 更换 OpenWrt 架构

本项目默认编译：

- OpenWrt 25.12.4
- rockchip/armv8

如果需要编译其它架构，只需要修改 **build.yml** 中 SDK 下载地址即可。

例如：

```yaml
- name: Download SDK
  run: |
    wget https://downloads.openwrt.org/releases/25.12.4/targets/rockchip/armv8/openwrt-sdk-25.12.4-rockchip-armv8_gcc-14.3.0_musl.Linux-x86_64.tar.zst
```

修改为对应目标平台的 SDK，例如：

### x86_64

```text
https://downloads.openwrt.org/releases/25.12.4/targets/x86/64/
```

### mt7981

```text
https://downloads.openwrt.org/releases/25.12.4/targets/mediatek/filogic/
```

### ipq807x

```text
https://downloads.openwrt.org/releases/25.12.4/targets/qualcommax/ipq807x/
```

### rockchip/armv8

```text
https://downloads.openwrt.org/releases/25.12.4/targets/rockchip/armv8/
```

进入对应目录后，将 SDK 下载地址替换为新的 `openwrt-sdk-*.tar.zst` 即可，无需修改其它代码。

---

## 输出文件

编译完成后生成：

```
bin/packages/<architecture>/
```

其中包含：

- phantun-client.apk
- phantun-server.apk

可直接安装到对应版本的 OpenWrt。

---

## 说明

- 使用 OpenWrt 官方 SDK 编译
- GitHub Actions 自动完成整个编译过程
- 不需要本地 Linux 环境
- 更换 OpenWrt 架构仅需修改 SDK 下载地址
- 更换 OpenWrt 版本同样只需修改 SDK 下载地址
