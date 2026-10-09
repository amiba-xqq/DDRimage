# DDRimage for Windows

DDRimage 是面向免疫荧光、DNA Fiber 和单克隆形成实验的本地图像分析软件，适用于 Windows 10 和 Windows 11。如果想要下载Mac系统版本的，可以查看DDRimage-macos[https://github.com/amiba-xqq/DDRimage-macos]

软件包含以下功能：

1. Leica LIF 文件导出 TIFF
2. 细胞核内蛋白 Foci 统计与作图
3. 细胞核内相对荧光强度统计与作图
4. DNA Fiber 统计与作图
5. 单克隆形成实验统计

## 下载

- [下载 DDRimage Windows 程序包](https://github.com/amiba-xqq/DDRimage/raw/refs/heads/main/DDRimage.zip)
- [下载配套测试数据](https://github.com/amiba-xqq/DDRimage/raw/refs/heads/main/DDRimage_test.zip)
- [查看 SHA-256 校验值](./SHA256SUMS.txt)

`DDRimage.zip` 是程序包。`DDRimage_test.zip` 仅包含测试数据，不能单独运行。

## 第一次安装和启动

1. 下载 `DDRimage.zip`。
2. 右键压缩包并选择“全部解压”，将完整的 `DDRimage` 文件夹解压到有写入权限的位置，例如桌面或 D 盘。不要只复制 `DDRimage.exe`。
3. 打开解压后的 `DDRimage` 文件夹，双击 `DDRimage.exe`。
4. 第一次启动需要联网。程序会下载 64 位 Python 3.12.10，并安装所需的 Python 库。
5. Python 和第三方库保存在软件目录下的 `runtime` 文件夹中，不会修改系统 Python。后续启动会直接复用该环境。

首次准备环境可能需要数分钟，实际时间取决于网络速度。若启动失败，请查看 `DDRimage/data/bootstrap.log`。

`启动DDRimage.cmd` 是备用启动入口。若希望提前检查并安装完整运行环境，可双击 `验证环境.cmd`。

## 测试数据

解压 `DDRimage_test.zip` 后可看到以下目录：

| 目录 | 对应功能 | 使用方式 |
| --- | --- | --- |
| `lif_test` | LIF 导出 TIFF | 在“01 LIF 导出 TIFF”中选择该文件夹 |
| `lif_test` 导出后生成的 TIFF 文件夹 | Foci、核内相对荧光强度 | 先完成 LIF 导出，再在“02”或“03”中选择导出结果 |
| `fiber_test` | DNA Fiber | 在“04 DNA Fiber”中选择该母文件夹 |
| `colony_test` | 单克隆形成 | 在“05 单克隆形成”中选择该母文件夹 |

建议先选择“测试一张”确认阈值、分割和 ROI，再执行全部处理。

## 重要注意事项

- Foci、核内相对荧光强度、DNA Fiber 和单克隆形成的图像统计步骤会清理输入子文件夹中的旧 CSV 和对应结果 TIFF。运行前请备份需要保留的结果。
- Foci、核内相对荧光强度和 DNA Fiber 可分别运行“仅运行图像统计”和“仅生成统计图”。生成统计图前必须已有图像统计产生的 CSV。
- 首次安装需要联网；环境准备完成后，常规图像分析可离线运行。
- 请保留程序目录的完整结构，不要单独移动 `DDRimage.exe`、`app`、`assets` 或 `tools` 中的文件。

## 校验下载文件

在 PowerShell 中进入下载目录，然后运行：

```powershell
Get-FileHash .\DDRimage.zip -Algorithm SHA256
Get-FileHash .\DDRimage_test.zip -Algorithm SHA256
```

结果应与 [SHA256SUMS.txt](./SHA256SUMS.txt) 中的值一致。

## 软件目录说明

- `app/analysis`：由原始 Jupyter Notebook 转换得到的分析脚本
- `source_notebooks`：原始 Notebook 备份
- `runtime`：首次启动时创建的便携 Python 和第三方库
- `data`：启动日志、界面设置和最近一次运行配置
- `requirements.txt`：固定版本的 Python 依赖

## 系统要求

- Windows 10 或 Windows 11，64 位
- 首次启动时需要网络连接
- 建议预留至少 2 GB 可用磁盘空间

