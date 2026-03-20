# Widora MangoPi M28C - ImmortalWrt 23.05 固件自动编译

基于 **ImmortalWrt 23.05** 稳定分支，专为 **Widora MangoPi M28C (Rockchip RK3568)** 打造的定制固件。集成了 5G 模组驱动、iStore 商店、风扇控制以及完美的科学网络插件支持。

## 🔥 固件特色 (Highlights)

* **稳定基座**: 基于 ImmortalWrt 23.05 源码，保留官方稳定性。
* **5G 全网通**: 内置 QMI/MBIM 驱动，集成 `Modemband` (锁频段) 和 `SMS Tool` (短信收发)，插卡即用。
* **iStore 生态**: 预装 `iStore` 商店和 `QuickStart` 首页，软件安装更简单。
* **完美温控**: 内核开启 `kmod-hwmon-pwmfan`，配合 `luci-app-fan`，风扇自动启停/调速。
* **网络增强**: 集成 `OpenClash`、`AdGuardHome`、`MosDNS`。
* *特别修复*: 解决了 MosDNS/AGH 在 ARM 架构下的文件冲突和架构不兼容问题。
* *Golang 修复*: 升级 Go 环境至 1.22+，完美支持 `v2dat` 等新插件。


* **美化主题**: 默认使用 `luci-theme-design`，现代简洁。

## ⚙️ 默认配置 (Default Settings)

| 项目 | 默认值 | 说明 |
| --- | --- | --- |
| **管理 IP** | `192.168.61.1` | 防止与光猫 (1.1) 冲突 |
| **用户名** | `root` |  |
| **密码** | `password` | 或空密码 |
| **Wi-Fi 状态** | **默认开启** | 刷机后无需插网线即可连接 |
| **Wi-Fi 名称** | `MangoPi M28c` | 5G 频段 |
| **Wi-Fi 密码** | `password` | WPA2-PSK 加密 |

> **注意**: 可以在 `diy-part2.sh` 文件末尾修改上述默认 IP 和 Wi-Fi 密码。

## 🚀 如何使用 (How to Build)

1. **Fork 本仓库** 到你的 GitHub 账号。
2. **开启权限** (至关重要):
* 进入 `Settings` -> `Actions` -> `General` -> `Workflow permissions`。
* 勾选 **Read and write permissions** 并保存。


3. **个性化修改**:
* 编辑 `diy-part2.sh`，修改最后几行的 Wi-Fi 名称和密码。


4. **开始编译**:
* 进入 `Actions` 页面，选择 `Build OpenWrt`，点击 `Run workflow`。


5. **下载固件**:
* 编译完成后，在 Actions 运行记录的 `Artifacts` 中下载固件，或在 `Releases` 页面下载。



## 🛠️ 本地编译指南 (Local Build)

如果你拥有 Ubuntu 20.04/22.04 环境，推荐本地编译以节省时间。

### 1. 安装依赖

```bash
sudo apt update -y
sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
bzip2 ccache cmake cpio curl device-tree-compiler fastjar flex gawk gettext gcc-multilib g++-multilib \
git gperf haveged help2man intltool libc6-dev-i386 libelf-dev libfuse-dev libglib2.0-dev libgmp3-dev \
libltdl-dev libmpc-dev libmpfr-dev libncurses-dev libpython3-dev libreadline-dev \
libssl-dev libtool lrzsz genisoimage msmtp ninja-build p7zip p7zip-full patch pkg-config python3 \
python3-pyelftools python3-setuptools qemu-utils rsync scons squashfs-tools subversion swig texinfo \
uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev

```

### 2. 拉取源码

```bash
git clone -b openwrt-23.05 https://github.com/immortalwrt/immortalwrt
cd immortalwrt

```

### 3. 加载自定义配置

复制本仓库 `feeds.conf.default` 和 `diy-part2.sh` 的内容，并在本地执行：

```bash
# 更新 feeds 并执行 diy-part2.sh 中的修复脚本
./scripts/feeds update -a
chmod +x diy-part2.sh
./diy-part2.sh

```

### 4. 编译

```bash
make menuconfig # 选择 Rockchip -> RK3568 -> Widora MangoPi M28C
make download -j8
make -j$(nproc) V=s

```

## 📜 鸣谢 (Credits)

* [ImmortalWrt](https://github.com/immortalwrt/immortalwrt)
* [iStoreOS](https://github.com/linkease/istore)
* [Kenzok8](https://github.com/kenzok8/openwrt-packages)
* [P3TERX Actions](https://github.com/P3TERX/Actions-OpenWrt)
