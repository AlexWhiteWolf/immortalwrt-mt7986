# 🌌 ImmortalWrt — 极致强化 OpenWrt 分支

ImmortalWrt 是基于 [OpenWrt](https://openwrt.org) 的高端强化分支，专为追求性能极限、稳定体验和全面功能的用户而打造。  
它集成了更多软件包、支持更广泛设备，并提供预设优化配置，同时针对中国大陆用户进行了深度本地化修改。  

在开源精神的基础上，我们引入上游无法采纳的优化技巧与增强功能，确保每台设备都能发挥最佳性能、获得更丰富的功能和更可靠的支持。  

🔹 **默认登录信息**：  
- 🌐 地址：`http://10.0.0.1` 或 `http://immortalwrt.lan`  
- 👤 用户名：`root`  
- 🔑 密码：无  

体验 ImmortalWrt，即刻解锁路由器潜能，让每一次网络连接都如光速般流畅，享受极致高速与稳定。


## 💾 下载 ImmortalWrt 固件

想要体验 ImmortalWrt 的极速与稳定？请下载官方开源无线驱动固件：

- 🌐 [ImmortalWrt 固件选择器](https://firmware-selector.immortalwrt.org/)

🔹 如果您的设备在支持列表中，请点击 **信息** 链接查看详细安装指南，或参考下方支持资源获取更多帮助。


## 🛠 开发与编译

要自行编译 ImmortalWrt 固件，您需要 GNU/Linux、BSD 或 macOS 系统（文件系统必须区分大小写）。Cygwin 不支持，因为其文件系统不区分大小写。

### 💡 编译要求

- 推荐系统：Debian 11 / Ubuntu 20 / Ubuntu 22  
- CPU 架构：AMD64  
- 内存：≥ 4 GB  
- 磁盘空间：≥ 25 GB  
- 网络：可正常访问互联网

### 🔧 必备工具（以 Debian/Ubuntu 为例）

**方法一：通过 APT 安装依赖**  <br/>
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

**方法二：一键初始化环境**  
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


### 📦 相关仓库

ImmortalWrt 的主仓库通过多个子仓库管理不同类别的软件包，所有软件包均可通过 OpenWrt 的包管理器 **opkg** 安装。  
如果您想开发 Web 界面或为 ImmortalWrt 移植软件包，请参考以下官方仓库：

- 🌐 [LuCI Web 界面](https://github.com/immortalwrt/luci) —— 现代化模块化浏览器控制界面  
- 📦 [ImmortalWrt 软件包](https://github.com/immortalwrt/packages) —— 社区移植的功能扩展仓库  
- 🔗 [OpenWrt 路由](https://github.com/openwrt/routing) —— 专注网状路由相关的软件包  
- 🎥 [OpenWrt 视频](https://github.com/openrt/video) —— 专注显示服务器及客户端（Xorg 与 Wayland）  


## 🛡 支持信息

想要查看您的设备是否受支持？请访问 [OpenWrt 硬件数据库](https://openwrt.org/supported_devices)。

### 📚 官方文档

- 🚀 [快速入门指南](https://openwrt.org/docs/guide-quick-start/start) —— 新手快速上手  
- 📖 [用户手册](https://openwrt.org/docs/guide-user/start) —— 全面操作指南  
- 💻 [开发者文档](https://openwrt.org/docs/guide-developer/start) —— 固件与软件包开发参考  
- 🛠 [技术参考](https://openwrt.org/docs/techref/start) —— 底层技术细节与系统架构  


## 📝 许可证

**ImmortalWrt** 基于开源协议 [GPL-2.0-only](https://spdx.org/licenses/GPL-2.0-only.html) 发布，遵循自由软件精神，您可以自由使用、修改和分发。

