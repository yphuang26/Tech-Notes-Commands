
### Steps
---
1. Navigate to the **VirtualBox Installation Directory**, eg:
```shell
cd C:\Program Files\Oracle\VirtualBox
```
2. Use the **VBoxManage** Command to Resize the VDI, eg:
```shell
VBoxManage modifyhd "D:\VirtualBox VMs\testVM\testVM.vdi" --resize 40960
```
### Additional
---
修改大小只能輸入 MB，參考此連結將 GB 轉換成 MB: [Convert GB to MB](https://www.unitconverters.net/data-storage/gb-to-mb.htm)
