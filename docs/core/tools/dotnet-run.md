---
title: "dotnet run 命令 - .NET Core CLI"
description: "dotnet run 命令提供方便的選項，以透過原始程式碼來執行應用程式。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: b37d1d7ff75aebfcdf3e849931a5d2b3924d5d7a
ms.openlocfilehash: c98a69ced3c309da0ff035efb5c76e7034d54e79
ms.contentlocale: zh-tw
ms.lasthandoff: 09/06/2017

---
# <a name="dotnet-run"></a>dotnet run

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet run` - 執行原始程式碼，而不需要有任何明確的編譯或啟動命令。

## <a name="synopsis"></a>概要

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

```
dotnet run [-c|--configuration] [-f|--framework] [--force] [--launch-profile] [--no-build] [--no-dependencies] [--no-launch-profile] [--no-restore] [-p|--project] [--runtime] [[--] [application arguments]]
dotnet run [-h|--help]
```

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

```
dotnet run [-c|--configuration] [-f|--framework] [-p|--project] [[--] [application arguments]]
dotnet run [-h|--help]
```

---

## <a name="description"></a>說明

`dotnet run` 命令提供方便的選項，以使用一個命令透過原始程式碼來執行應用程式。 可用於在命令列中快速進行反覆開發。 此命令仰賴 [`dotnet build`](dotnet-build.md) 命令來建置程式碼。 建置的任何需求 (例如必須先還原專案) 也同樣適用於 `dotnet run`。 

輸出檔會寫入至預設位置，也就是 `bin/<configuration>/<target>`。 例如，如果您有 `netcoreapp1.0` 應用程式並執行 `dotnet run`，輸出將會放置在 `bin/Debug/netcoreapp1.0` 中。 而且會視需要覆寫檔案。 暫存檔案會放置在 `obj` 目錄中。 

如果專案指定多個架構，執行 `dotnet run` 會導致錯誤，除非使用 `-f|--framework <FRAMEWORK>` 選項來指定架構。

`dotnet run` 命令用於專案內容中，而非已建置的組件。 如果您改為嘗試執行與 Framework 相依的應用程式 DLL，您必須不透過命令使用 [dotnet](dotnet.md)。 例如，若要執行 `myapp.dll`，使用︰

```
dotnet myapp.dll
```

如需 `dotnet` 驅動程式的詳細資訊，請參閱 [.NET Core 命令列工具 (CLI)](index.md) 主題。

為了執行應用程式，`dotnet run` 命令會從 NuGet 快取解析共用執行階段之外的應用程式相依性。 因為它會使用快取相依性，不建議您在生產環境中使用 `dotnet run` 執行應用程式。 相反地，使用 [`dotnet publish`](dotnet-publish.md) 命令[建立部署](../deploying/index.md)，並部署已發佈的輸出。

## <a name="options"></a>選項

# <a name="net-core-2xtabnetcore2x"></a>[.NET Core 2.x](#tab/netcore2x)

`--`

分隔 `dotnet run` 的引數與執行中應用程式的引數。 此項目之後的所有引數會傳遞至執行的應用程式。

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定的[架構](../../standard/frameworks.md)建置並執行應用程式。 架構必須在專案檔中指定。

`-h|--help`

印出命令的簡短說明。

`--launch-profile <NAME>`

啟動應用程式時使用的啟動設定檔名稱 (如果有的話)。 啟動設定檔是在 *launchSettings.json* 檔案中定義，通常稱為 `Development`、`Staging` 和 `Production`。 如需詳細資訊，請參閱[使用多個環境](/aspnet/core/fundamentals/environments)。

`--no-build`

不會在執行前建置專案。

`--no-launch-profile`

不會嘗試使用 *launchSettings.json* 設定應用程式。

`--no-restore`

執行命令時，不執行隱含的還原。

`-p|--project <PATH>`

指定要執行的專案檔路徑 (資料夾名稱或完整路徑)。 如果未指定，則會預設為目前目錄。

`--runtime <RUNTIME_IDENTIFIER>`

指定要還原套件的目標執行階段。 如需執行階段識別項 (RID) 清單，請參閱 [RID 目錄](../rid-catalog.md)。

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--`

分隔 `dotnet run` 的引數與執行中應用程式的引數。 此項目之後的所有引數會傳遞至執行的應用程式。

`-c|--configuration {Debug|Release}`

定義組建組態。 預設值是 `Debug`。

`-f|--framework <FRAMEWORK>`

使用指定的[架構](../../standard/frameworks.md)建置並執行應用程式。 架構必須在專案檔中指定。

`-h|--help`

印出命令的簡短說明。

`-p|--project <PATH/PROJECT.csproj>`

指定專案檔的路徑和名稱。 (請參閱附註)。如果未指定，則會預設為目前目錄。

> [!NOTE]
> 透過 `-p|--project` 選項使用專案檔的路徑和名稱。 CLI 中的迴歸會阻擋提供有 .NET Core 1.x SDK 的資料夾路徑。 如需此問題的詳細資訊，請參閱 [dotnet run -p, can not start a project (dotnet/cli #5992)](https://github.com/dotnet/cli/issues/5992) (dotnet run -p，無法啟動專案 (dotnet/cli #5992))。

---

## <a name="examples"></a>範例

執行目前目錄中的專案：

`dotnet run`

執行指定的專案：

`dotnet run --project /projects/proj1/proj1.csproj`

執行目前目錄中的專案 (因為已使用 `--` 引數，所以這個範例中的 `--help` 引數會傳遞給應用程式)：

`dotnet run --configuration Release -- --help`

