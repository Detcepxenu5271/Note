# Neovim


## 安装和配置
### 安装最新版本
（如果本地已经安装旧版本，可能要先卸载）

运行命令：
```bash
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
```

### 使用他人的配置
来源：[我的现代化Neovim配置 - ayamir](https://github.com/ayamir/nvimdots)
新来源：[现代Neovim配置 - 南风璇](https://zhuanlan.zhihu.com/p/532361193)

基于 lua 的配置

#### 插件
使用 Packer 管理插件
* 首先修改相应配置文件
* 在 nvim 里输入命令`:PackerSync`安装，`:PackerClean`卸载

#### 备注
本地 wsl1 的 lazygit 未安装成功

依赖
* lldb 太大了（三百兆），没装
* nvm 没理解，不能用 apt 直接安装，没装
