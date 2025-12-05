# 🌌 适用于 MTK 系列设备的 OpenWrt 源码仓库

## 📖 说明

该项目旨在为 Mediatek Filogic 系列设备提供功能完善的 OpenWrt 系统。

本项目 Fork 自 [padavanonly](https://github.com/padavanonly/immortalwrt-mt798x-6.6),在此基础上扩展了对更多设备的支持，并对设备树（DTS）进行了优化，以兼容旧版 U-Boot。

在此，向所有贡献者表示衷心的感谢！

### 🎯 MTK 系列设备支持概览

| 设备型号  | HNAT 硬件加速 | 2.4G WiFi | 5G WiFi |
| :------: | :-----------: | :-------: | :------: |
| MT7981   | ✅            | ✅        | ✅       |
| MT7986   | ✅            | ✅        | ✅       |
| MT7988   | ❌            | ❌        | ❌       |

---

### 📚 官方文档

- 🚀 [快速入门指南](https://openwrt.org/docs/guide-quick-start/start) —— 新手快速上手  
- 📖 [用户手册](https://openwrt.org/docs/guide-user/start) —— 全面操作指南  
- 💻 [开发者文档](https://openwrt.org/docs/guide-developer/start) —— 固件与软件包开发参考  
- 🛠 [技术参考](https://openwrt.org/docs/techref/start) —— 底层技术细节与系统架构

---

## 🛠 开发与编译

### 使用 Github Action 云编译

您可以使用以下项目进行云端编译：

- [**OPPEN321/OpenWrt**](https://github.com/OPPEN321/OpenWrt)


### 本地编译

> #### **⚠️ 注意事项**
> - **请勿使用 `root` 用户进行编译！**
> - **国内用户编译前建议开启网络代理。**
> - **编译环境要求：至少 4GB 内存和 25GB 可用磁盘空间。**
> - **默认配置：**
>   - 登陆 IP: `10.0.0.1`
>   - 密码: `password`

  - 🔧 必备工具（以 Debian/Ubuntu 为例）<br/>
    - 方法一：通过 APT 安装依赖：
      <details>
        <summary>通过 APT 安装依赖</summary>

        ```bash
        sudo apt update -y
        sudo apt full-upgrade -y
        sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
          bzip2 ccache clang cmake cpio curl device-tree-compiler ecj fastjar flex gawk gettext gcc-multilib \
          g++-multilib git gnutls-dev gperf haveged help2man intltool lib32gcc-s1 libc6-dev-i386 libelf-dev \
          libglib2.0-dev libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses-dev libpython3-dev \
          libreadline-dev libssl-dev libtool libyaml-dev libz-dev lld llvm lrzsz mkisofs msmtp nano \
          ninja-build p7zip p7zip-full patch pkgconf python3 python3-pip python3-ply python3-docutils \
          python3-pyelftools qemu-utils re2c rsync scons squashfs-tools subversion swig texinfo uglifyjs \
          upx-ucl unzip vim wget xmlto xxd zlib1g-dev zstd
        ```
      </details>
    - 方法二：一键初始化环境：
      ```bash
      sudo bash -c 'bash &lt;(curl -s https://build-scripts.immortalwrt.org/init_build_environment.sh )'
      ```
      
### ⚠ 编译注意事项

- 全程使用普通用户操作，禁止 root 或 sudo  
- 其他架构 CPU 可编译，但可能需要额外操作  
- 工作目录及文件夹名称不得包含空格或非 ASCII 字符  
- WSL 用户需移除 Windows PATH，详见 [WSL 编译系统设置](https://openwrt.org/docs/guide-developer/build-system/wsl)  
- **不建议**使用 macOS 编译，参考 [macOS 编译系统设置](https://openwrt.org/docs/guide-developer/build-system/buildroot.exigence.macosx)  
- 更多细节请查阅 [编译系统设置](https://openwrt.org/docs/guide-developer/build-system/install-buildsystem)


### ⚡ 快速开始：编译 MT798X 路由器固件

想要快速体验 ImmortalWrt 的极致性能？请按以下步骤操作：

1. **克隆源码**  
```bash
git clone -b openwrt-24.10 --single-branch --filter=blob:none https://github.com/QuickWrt/immortalwrt-mt798x
```

2. **进入源码目录**  
```bash
cd immortalwrt-mt798x
```

3. **更新 feeds**  
```bash
./scripts/feeds update -a
```

4. **安装所有软件包**  
```bash
./scripts/feeds install -a
```

5. **导入设备默认配置**  
```bash
# MT7981
cp -f defconfig/mt7981-ax3000.config .config

# MT7986
cp -f defconfig/mt7986-ax6000.config .config
```

6. **打开配置菜单**  
```bash
make menuconfig
```
选择所需机型和插件。

7. **下载编译所需库**  
```bash
make download -j$(nproc)
```

8. **首次编译（单线程推荐）**  
```bash
make V=s -j1
```
⚠ 首次编译建议使用单线程，以避免报错或硬件性能不足导致失败。

9. **后续快速编译（多线程）**  
```bash
make V=s -j$(nproc)
```
✅ 成功后即可快速多线程编译，提高效率。
