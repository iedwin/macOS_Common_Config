### 删除EFI分区

#### 在macbook上安装win10一般有两种方法，一种是直接使用系统提供的bootcamp来安装macOS/win10双系统，好处是比较稳定的安装，而且如果不再想用win10了，可以在macOS下用Disk Utility直接干掉win10的分区。坏处是bootcamp必须依赖macOS,如果你就是想用单win10，bootcamp的方式是无法做到的，这种情况下可以使用第二种方法是用refInd来安装win10或Linux单系统(该部分我会放到后面的章节具体说明)。

#### 由于我的macbook pro是13" 2015低配版,SSD只有120G，容量捉襟见肘，所以有时我会在bootcamp使用完win10后用Disk Utility删除win10分区，但其实bootcamp自动为win10创建的EFI分区在Disk Utility中看不到，该分区有200M+，如果不删的话一是白占着空间，二是有可能导致下次bootcamp失败。所以该分区在每次重装系统前是必须检查的，如果存在必须删掉。

#### 步骤：
- 重启，按住⌘ + R 进入恢复界面
- 左上角菜单里面找到终端，打开并输入
```bash
diskutil umountDisk /dev/disk0 # 最好多umount两次防止遇到resource busy的报错
gpt remove -i 1 /dev/disk0 # 该语句就是删除disk0的分区1，一般就是EFI分区
# gpt add -b 40 -i 1 -s 409600 -t efi /dev/disk0 # 也有不小心删掉自己手动创建EFI分区的情况
```