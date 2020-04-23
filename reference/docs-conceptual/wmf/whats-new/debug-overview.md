---
ms.date: 06/12/2017
keywords: wmf,powershell,安装程序
title: PowerShell 脚本调试中的改进
ms.openlocfilehash: f1771a451ba671da2371fcfc95374e6131573ddc
ms.sourcegitcommit: 6545c60578f7745be015111052fd7769f8289296
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "71147807"
---
# <a name="improvements-in-powershell-script-debugging"></a><span data-ttu-id="6b021-103">PowerShell 脚本调试中的改进</span><span class="sxs-lookup"><span data-stu-id="6b021-103">Improvements in PowerShell Script Debugging</span></span>

<span data-ttu-id="6b021-104">PowerShell 5.0 包括用于增强调试体验的多项改进。</span><span class="sxs-lookup"><span data-stu-id="6b021-104">PowerShell 5.0 includes several improvements that enhance the debugging experience.</span></span>

## <a name="break-all"></a><span data-ttu-id="6b021-105">全部中断</span><span class="sxs-lookup"><span data-stu-id="6b021-105">Break All</span></span>

<span data-ttu-id="6b021-106">PowerShell 控制台和 PowerShell ISE 现在可以中断调试器，而运行脚本。</span><span class="sxs-lookup"><span data-stu-id="6b021-106">The PowerShell console and PowerShell ISE now allow you to break into the debugger for running scripts.</span></span> <span data-ttu-id="6b021-107">这在本地和远程会话中很有效。</span><span class="sxs-lookup"><span data-stu-id="6b021-107">This works in both local and remote sessions.</span></span>

<span data-ttu-id="6b021-108">在控制台中，按 <kbd>Ctrl</kbd>+<kbd>Break</kbd>。</span><span class="sxs-lookup"><span data-stu-id="6b021-108">In the console, press <kbd>Ctrl</kbd>+<kbd>Break</kbd>.</span></span>

<span data-ttu-id="6b021-109">在 ISE 中，按 <kbd>Ctrl</kbd>+<kbd>B</kbd>，或使用“调试”->“全部中断”  菜单命令。</span><span class="sxs-lookup"><span data-stu-id="6b021-109">In ISE, press <kbd>Ctrl</kbd>+<kbd>B</kbd>, or use the **Debug -> Break All** menu command.</span></span>

## <a name="remote-debugging-and-remote-file-editing-in-powershell-ise"></a><span data-ttu-id="6b021-110">PowerShell ISE 中的远程调试和远程文件编辑</span><span class="sxs-lookup"><span data-stu-id="6b021-110">Remote debugging and remote file editing in PowerShell ISE</span></span>

<span data-ttu-id="6b021-111">PowerShell ISE 现在可以通过运行 PSEdit 命令，在远程会话中打开并编辑文件。</span><span class="sxs-lookup"><span data-stu-id="6b021-111">PowerShell ISE now lets you open and edit files in a remote session by running the PSEdit command.</span></span>
<span data-ttu-id="6b021-112">例如，你可以在远程会话中打开文件并从命令行进行编辑，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b021-112">For example, you can open a file for editing from the command line in a remote session as follows:</span></span>

```powershell
[RemoteComputer1]: PS C:\> PSEdit C:\DebugDemoScripts\Test-GetMutex.ps1
```

<span data-ttu-id="6b021-113">此外，你现在还可以在远程文件中编辑并保存更改，远程文件是你命中断点时在 PowerShell ISE 中自动打开的文件。</span><span class="sxs-lookup"><span data-stu-id="6b021-113">In addition, you can now edit and save changes in a remote file that is automatically opened in PowerShell ISE when you hit a breakpoint.</span></span> <span data-ttu-id="6b021-114">现在，你可以调试在远程计算机上运行的脚本文件，编辑该文件以修复错误，然后重新运行修改后的脚本。</span><span class="sxs-lookup"><span data-stu-id="6b021-114">Now, you can debug a script file that is running on a remote computer, edit the file to fix an error, and then rerun the modified script.</span></span>

## <a name="advanced-script-debugging"></a><span data-ttu-id="6b021-115">高级脚本调试</span><span class="sxs-lookup"><span data-stu-id="6b021-115">Advanced Script Debugging</span></span>

<span data-ttu-id="6b021-116">新的高级调试功能使你能够附加到已加载 PowerShell 的任何本地计算机进程，并在该进程中调试任意运行空间。</span><span class="sxs-lookup"><span data-stu-id="6b021-116">There are new, advanced debugging features that let you attach to any local computer process that has loaded PowerShell, and debug arbitrary runspaces in that process.</span></span>

### <a name="runspace-debugging"></a><span data-ttu-id="6b021-117">运行空间调试</span><span class="sxs-lookup"><span data-stu-id="6b021-117">Runspace Debugging</span></span>

<span data-ttu-id="6b021-118">已添加的新 cmdlet 使你能够列出某个进程中的当前运行空间，并将 PowerShell 控制台或 PowerShell ISE 调试器附加到该运行空间进行脚本调试：</span><span class="sxs-lookup"><span data-stu-id="6b021-118">New cmdlets have been added that let you list current runspaces in a process, and attach the PowerShell console or PowerShell ISE debugger to that runspace for script debugging:</span></span>

- <span data-ttu-id="6b021-119">Get-Runspace</span><span class="sxs-lookup"><span data-stu-id="6b021-119">Get-Runspace</span></span>
- <span data-ttu-id="6b021-120">Debug-Runspace</span><span class="sxs-lookup"><span data-stu-id="6b021-120">Debug-Runspace</span></span>
- <span data-ttu-id="6b021-121">Enable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="6b021-121">Enable-RunspaceDebug</span></span>
- <span data-ttu-id="6b021-122">Disable-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="6b021-122">Disable-RunspaceDebug</span></span>
- <span data-ttu-id="6b021-123">Get-RunspaceDebug</span><span class="sxs-lookup"><span data-stu-id="6b021-123">Get-RunspaceDebug</span></span>

### <a name="attach-to-process-hosting-powershell"></a><span data-ttu-id="6b021-124">附加到承载 PowerShell 的进程</span><span class="sxs-lookup"><span data-stu-id="6b021-124">Attach to Process hosting PowerShell</span></span>

<span data-ttu-id="6b021-125">你现在可以附加到已加载 PowerShell 的任何计算机进程。</span><span class="sxs-lookup"><span data-stu-id="6b021-125">You can now attach to any computer process that has PowerShell loaded.</span></span> <span data-ttu-id="6b021-126">可通过输入与主机进程交互的会话执行此操作。</span><span class="sxs-lookup"><span data-stu-id="6b021-126">You do this by entering into an interactive session with the host process.</span></span> <span data-ttu-id="6b021-127">有关详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="6b021-127">For more information, see:</span></span>

- [<span data-ttu-id="6b021-128">Enter-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="6b021-128">Enter-PSHostProcess</span></span>](/powershell/module/Microsoft.PowerShell.Core/Enter-PSHostProcess)
- [<span data-ttu-id="6b021-129">Exit-PSHostProcess</span><span class="sxs-lookup"><span data-stu-id="6b021-129">Exit-PSHostProcess</span></span>](/powershell/module/Microsoft.PowerShell.Core/Exit-PSHostProcess)
