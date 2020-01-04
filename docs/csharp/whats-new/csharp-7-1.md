# C# 7.1 中的新增功能

在 C# 7.1 ，提供以下功能：

* [非同步Main方法 ( Async Main method )](#非同步Main方法)
  - 程式進入點可使用`async`修飾詞。
* [預設常值運算式 ( Default literal expressions )](#預設常值運算式)
  - 在目標型別可推斷時，您可以在預設值運算式中使用預設常值運算式。
* [Tuple型別推導 ( Inferred tuple element names )](#Tuple型別推導)
  - 多數情形下，Tuple元素的名稱可從Tuple初始化中推導出來。

## 深入瞭解新版本
C# 7.1 自 Visual Studio 2017 15.3 版本起與 .NET Core SDK 2.0 版本起開始支援，預設值 C# 7.1 功能為關閉，
若要啟用 C# 7.1 功能，您必需確認您的專案編輯語言版本設定值。


在 Visual Studio ，設定 C# 7.1 功能啟用的方法為專案總管中欲於設定功能啟用的專案上右鍵選單選擇「專案屬性」
(**Properties**) ，選擇「建置」頁籤 (**Build**) 後，按下「進階」按紐 (**Advanced**) ，將看見下面對話視窗：


在此對話視窗中選擇「語言版本」 (**Build**) 選項下拉選單值為「 C# 最新主要版本」 (**C# latest minor version (latest)**) 
或為 「 C# 7.1 」(**C# 7.1**)，按下確定按紐後， Visual Studio 將會為您選取的專案 csproj 設定檔中寫入以下啟用設定：


```xml
<PropertyGroup>
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```


選單值「 C# 最新主要版本」與「 C# 7.1 」差異在於選擇 C# 最新主要版本設定時將會使用您當前機器上的最新版本，而選擇
 「C# 7.1」 則為明確指定使用 C# 7.1 而非使用當前機器現有更新版本。

> [!NOTE]
> 如果使用 Visual Studio IDE 介面更新 csproj 設定檔， IDE 介面將會為您所選取專案進行個別設定更新，並產
> 生單一的設定值。然而若有為個別開發環境設定環境變數，或者在當前定選擇所有設定更新時，您將會看到以下設定方式

```xml
<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|AnyCPU'">
  <LangVersion>latest</LangVersion>
</PropertyGroup>

<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|AnyCPU'">
  <LangVersion>latest</LangVersion>
</PropertyGroup>
```

LangVersion 提供了以下有效數值設定選項：

* `ISO-1`
* `ISO-2`
* `3`
* `4`
* `5`
* `6`
* `7`
* `7.1`
* `default`
* `latest`

文字字串 `default` 與 `latest` 分別提供使用當前機器所使用的最新版本與次要最新版本。
您可以使用最新版本 SDK 與其相關工具進行細部個別設定。


## 非同步Main方法

現在 *async main* 方法可以讓您在您的`Main`方法中使用`await`。
在過去您必須這樣寫:

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

現在您可以這樣寫:

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

如果您的程式並不需要傳回執行完成狀態 (**An exit code**) ，你可以定義 Main 方法使其傳回
<xref:System.Threading.Tasks.Task>:

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

你可以在程式編輯指南中的 [Main方法](../programming-guide/main-and-command-args/index.md)  (**Main() and command-line arguments**) 
章節閱讀細節。

## 預設常值運算式

本方法提供[預設值運算式](../programming-guide/statements-expressions-operators/default-value-expressions.md) (**Default value expressions**)的加強。此表達式將會對一個變數初始化一個預設值。在過去您必須這樣寫：

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

現在您可以省略右邊的初始化類型：

```csharp
Func<string, bool> whereClause = default;
```

您可以在程式設計指南中的[預設值運算式](../programming-guide/statements-expressions-operators/default-value-expressions.md)章節閱讀細節。

本次加強也變更了 [Default 關鍵字](../language-reference/keywords/default.md) (**Default keyword**) 的解析規則。

## Tuple型別推導

本方法為 C# 7.0 版本 Tuple 方法的改進，在進行 Tuple 方法初始化變數時，需要在初始化變數左方定義一個分類變數名稱
，然而許多情況下分類變數名稱常與初始化變數名稱相同：

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count: count, label: label);
```

改進後的方法在進行變數初始化時分類變數名稱可以由變數名稱推導：

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

您可以在 [Tuples類型](../tuples.md) (**Tuple types**) 章節中學習更多關於此功能的細節。

## 組件版本資源

C# 7.1 起提供了兩個新的組件編譯時參考組件編譯參數： [/refout](../language-reference/compiler-options/refout-compiler-option.md)
 與 [/refonly](../language-reference/compiler-options/refonly-compiler-option.md)，您可以在連結的章節更詳細的解釋這些選項以及細節。
