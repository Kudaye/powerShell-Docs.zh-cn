---
title: 在 Windows 上安装 PowerShell
description: 介绍如何在 Windows 上安装 PowerShell
ms.date: 08/06/2018
ms.openlocfilehash: bb0971b6c4ac99bde70b226da2becf2f4ed82083
ms.sourcegitcommit: d36db3a1bc44aee6bc97422b557041c3aece4c67
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082777"
---
# <a name="installing-powershell-on-windows"></a>在 Windows 上安装 PowerShell

有多种方法可以在 Windows 中安装 PowerShell。

## <a name="prerequisites"></a>先决条件

若要通过 WSMan 启用 PowerShell 远程处理，需要满足以下先决条件：

- 在 Windows 10 之前的 Windows 版本上安装[通用 C 运行时](https://www.microsoft.com/download/details.aspx?id=50410)。 可通过直接下载或 Windows 更新进行安装。 经完全修补（含可选包）且受支持的系统中已安装有通用 C 运行时。
- 在 Windows 7 和 Windows Server 2008 R2 上安装 Windows Management Framework (WMF) 4.0 或更高版本。 有关 WMF 的详细信息，请参阅 [WMF 概述](/powershell/scripting/wmf/overview)。

## <a name="installing-the-msi-package"></a><a id="msi" />安装 MSI 包

若要在 Windows 客户端或 Windows Server（适用于 Windows 7 SP1、Server 2008 R2 以及更高版本）上安装 PowerShell，请从 GitHub [版本][releases]页面下载 MSI 包。 向下滚动到要安装的版本的“资产”部分。 “资产”部分可能处于折叠状态，因此可能需要单击使其展开。

MSI 文件类似于 `PowerShell-<version>-win-<os-arch>.msi`

下载后，双击安装程序并按照提示进行操作。

安装程序在 Windows“开始”菜单中创建一个快捷方式。

- 默认情况下，包安装位置为 `$env:ProgramFiles\PowerShell\<version>`
- 可以通过“开始”菜单或 `$env:ProgramFiles\PowerShell\<version>\pwsh.exe` 启动 PowerShell

> [!NOTE]
> PowerShell 7 安装到新目录，并与 Windows PowerShell 5.1 并行运行。 对于 PowerShell Core 6.x，PowerShell 7 是删除 PowerShell Core 6.x 的就地升级。
>
> - PowerShell 7 安装到 `%programfiles%\PowerShell\7`
> - `%programfiles%\PowerShell\7` 文件夹已添加到 `$env:PATH`
> - `%programfiles%\PowerShell\6` 文件夹已删除
>
> 如果需要与 PowerShell 7 并行运行 PowerShell 6，请使用 [ZIP 安装](#zip)方法重新安装 PowerShell 6。

### <a name="administrative-install-from-the-command-line"></a>通过命令行进行管理安装

可以通过命令行安装 MSI 包。 这样，管理员可以部署包而无需用户交互。 适用于 PowerShell 的 MSI 包包含下列属性以控制安装选项：

- **ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL** - 此属性控制向 Windows 资源管理器中的上下文菜单添加“打开 PowerShell”项的选项。
- **ENABLE_PSREMOTING** - 此属性控制用于在安装过程中启用 PowerShell 远程处理的选项。
- **REGISTER_MANIFEST** - 此属性控制用于注册 Windows 事件日志记录清单的选项。

下面的示例演示如何在启用所有安装选项的情况下以无提示方式安装 PowerShell。

```powershell
msiexec.exe /package PowerShell-<version>-win-<os-arch>.msi /quiet ADD_EXPLORER_CONTEXT_MENU_OPENPOWERSHELL=1 ENABLE_PSREMOTING=1 REGISTER_MANIFEST=1
```

有关 Msiexec.exe 命令行选项的完整列表，请参阅[命令行选项](/windows/desktop/Msi/command-line-options)。

## <a name="installing-the-msix-package"></a><a id="msix" />安装 MSIX 包

要在 Windows 10 客户端上手动安装 MSIX 包，请从 GitHub [版本][releases]页面下载 MSIX 包。 向下滚动到要安装的版本的“资产”部分。 “资产”部分可能处于折叠状态，因此可能需要单击使其展开。

MSIX 文件类似于 - `PowerShell-<version>-win-<os-arch>.msix`

下载后，请勿简单地双击安装程序，因为此程序包需要使用非虚拟资源。  要安装，必须使用 `Add-AppxPackage` cmdlet：

```powershell
Add-AppxPackage PowerShell-<version>-win-<os-arch>.msix
```

## <a name="installing-the-zip-package"></a><a id="zip" />安装 ZIP 包

提供有 PowerShell 二进制 ZIP 存档，从而支持高级部署方案。 请注意，使用 ZIP 存档时，不同于使用 MSI，你无法获取 MSI 先决条件检查。 要使 WSMan 远程处理正常工作，请确保您已满足[先决条件](#prerequisites)。

## <a name="deploying-on-windows-iot"></a>在 Windows IoT 上部署

Windows IoT 已经附带了 Windows PowerShell，我们可以使用它来部署 PowerShell 7。

1. 在目标设备中创建 `PSSession`

   ```powershell
   Set-Item -Path WSMan:\localhost\Client\TrustedHosts <deviceip>
   $S = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. 将 ZIP 包复制到设备

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-<version>-win-<os-arch>.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. 连接到设备并展开存档

   ```powershell
   Enter-PSSession $s
   Set-Location u:\users\administrator\downloads
   Expand-Archive .\PowerShell-<version>-win-<os-arch>.zip
   ```

4. 在 PowerShell 7 中设置远程处理

   ```powershell
   Set-Location .\PowerShell-<version>-win-<os-arch>
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. 连接到设备上的 PowerShell 7 终结点

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.<version>
   ```

## <a name="deploying-on-nano-server"></a>在 Nano Server 上进行部署

这些说明假定某个 PowerShell 版本已在 Nano Server 映像上运行，并且其已经由 [Nano Server 映像生成器](/windows-server/get-started/deploy-nano-server)生成。
Nano Server 是“无外设”OS。 可以使用两种不同的方法部署 PowerShell 二进制文件。

1. 脱机 - 安装 Nano Server VHD，并将 zip 文件的内容解压到安装映像中的所选位置。
2. 联机 - 通过 PowerShell 会话传输 zip 文件，并在所需位置中将其解压。

这两种情况下皆需要 Windows 10 x64 ZIP 发布包，且需要在“管理员”PowerShell 实例中运行命令。

### <a name="offline-deployment-of-powershell"></a>PowerShell 脱机部署

1. 使用常用 zip 实用工具将包解压到已安装的 Nano Server 映像中的目录。
2. 卸载映像并启动。
3. 连接到 Windows PowerShell 的收件箱实例。
4. 按照说明使用[“另一种实例技术”](../learn/remoting/wsman-remoting-in-powershell-core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register)创建远程处理终结点。

### <a name="online-deployment-of-powershell"></a>PowerShell 联机部署

以下步骤将指导你向 Nano Server 运行实例部署 PowerShell，并配置其远程终结点。

- 连接到 Windows PowerShell 的收件箱实例

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- 将文件复制到 Nano Server 实例

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- 输入会话

  ```powershell
  Enter-PSSession $session
  ```

- 提取 ZIP 文件

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShell_<version>"
  ```

- 如果需要基于 WSMan 的远程处理，请按照说明使用[“另一种实例技术”](../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register)创建远程处理终结点。

## <a name="install-as-a-net-global-tool"></a>作为 .NET 全局工具安装

如果你已安装 [.NET Core SDK](/dotnet/core/sdk)，则可以轻松地安装 PowerShell 作为 [.NET 全局工具](/dotnet/core/tools/global-tools)。

```
dotnet tool install --global PowerShell
```

dotnet 工具安装程序将 `$env:USERPROFILE\dotnet\tools` 添加到 `$env:PATH` 环境变量中。 但是，当前运行的 shell 没有更新的 `$env:PATH`。 应该可以通过键入 `pwsh` 从新 shell 启动 PowerShell。

## <a name="how-to-create-a-remoting-endpoint"></a>如何创建远程处理终结点

PowerShell 同时支持采用 WSMan 和 SSH 的 PowerShell 远程处理协议 (PSRP)。 有关详细信息，请参阅：

- [在 PowerShell Core 中进行 SSH 远程处理][ssh-remoting]
- [在 PowerShell Core 中进行 WSMan 远程处理][wsman-remoting]

<!-- [download-center]: TODO -->

[releases]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../learn/remoting/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../learn/remoting/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
