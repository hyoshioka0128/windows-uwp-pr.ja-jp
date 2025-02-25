---
title: Windows ランタイム コンポーネントでのエラー状態の診断
description: この記事では、マネージ コードで記述された Windows ランタイム コンポーネントでの制限に関する追加情報について説明します。
ms.assetid: CD0D0E11-E68A-411D-B92E-E9DECFDC9599
ms.date: 02/08/2017
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: 72a7a7d4bbe6987781c538a7276bf3942f10cf5b
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372203"
---
# <a name="diagnosing-windows-runtime-component-error-conditions"></a>Windows ランタイム コンポーネントでのエラー状態の診断




この記事では、マネージ コードで記述された Windows ランタイム コンポーネントでの制限に関する追加情報について説明します。 ここでは、[Winmdexp.exe (Windows ランタイム メタデータ エクスポート ツール)](https://docs.microsoft.com/dotnet/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool) からのエラー メッセージに示されている情報についても説明します。また、「[C# および Visual Basic での Windows ランタイム コンポーネントの作成](creating-windows-runtime-components-in-csharp-and-visual-basic.md)」に記載されている制限事項の情報について補足説明します。

この記事では、すべてのエラーが説明されているわけではありません。 ここで説明するエラーは一般的なカテゴリにまとめられており、各カテゴリには、関連するエラー メッセージの表が示されています。 この表を利用するには、メッセージ テキストで検索するか (プレース ホルダーの特定の値は省略してください)、メッセージ番号で検索してください。 必要な情報が見つからない場合は、この記事の最後にあるフィードバック ボタンをご利用ください。ドキュメントの内容を充実させるためにご協力をお願いします。 フィードバックを送る際には、エラー メッセージを含めてください。 また、Microsoft Connect の Web サイトで問題点をご連絡していただくこともできます。

## <a name="error-message-for-implementing-async-interface-provides-incorrect-type"></a>非同期インターフェイスの実装に関するエラー メッセージで示される型が正しくない


マネージ型の Windows ランタイム コンポーネントは、非同期処理や非同期操作を表すユニバーサル Windows プラットフォーム (UWP) インターフェイス ([IAsyncAction](https://docs.microsoft.com/windows/desktop/api/windows.foundation/nn-windows-foundation-iasyncaction)、[IAsyncActionWithProgress&lt;TProgress&gt;](https://docs.microsoft.com/previous-versions//br205784(v=vs.85))、[IAsyncOperation&lt;TResult&gt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperation_TResult_)、[IAsyncOperationWithProgress&lt;TResult, TProgress&gt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.IAsyncOperationWithProgress_TResult_TProgress_)) を実装することはできません。 代わりに、.NET Framework には、Windows ランタイム コンポーネントの非同期操作を生成するための [AsyncInfo](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime?redirectedfrom=MSDN) クラスが用意されています。 非同期インターフェイスを実装しようとしたときに Winmdexp.exe により表示されるエラー メッセージでは、このクラスが誤って以前の名前の AsyncInfoFactory として示されます。 .NET Framework では、AsyncInfoFactory クラスが使われなくなりました。

| エラー番号 | メッセージ テキスト|       
|--------------|-------------|
| WME1084      | 型 '{0}'Windows ランタイムの非同期インターフェイスを実装する'{1}'。 Windows ランタイム型は、非同期インターフェイスを実装できません。 System.Runtime.InteropServices.WindowsRuntime.AsyncInfoFactory クラスを使用して、Windows ランタイムへのエクスポート用に非同期操作を生成してください。 |

> **注** Windows ランタイムを参照するエラー メッセージが以前の用語を使用します。 現在では、Windows ランタイムはユニバーサル Windows プラットフォーム (UWP) と呼ばれます。 たとえば、Windows ランタイム型は UWP 型と呼ばれています。

 

## <a name="missing-references-to-mscorlibdll-or-systemruntimedll"></a>mscorlib.dll または System.Runtime.dll への参照が指定されていない


この問題は、コマンド ラインから Winmdexp.exe を使う場合にのみ発生します。 ある .NET Framework コア参照アセンブリから mscorlib.dll および System.Runtime.dll の両方への参照を含めるには、/reference オプションを使用することをお勧めします"%programfiles (x86) %\\参照アセンブリ\\。Microsoft\\Framework\\します。NETCore\\v4.5"("%programfiles%\\..."32 ビット コンピューター)。

| エラー番号 | メッセージ テキスト                                                                                                                                     |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1009      | mscorlib.dll は参照されませんでした。 正しくエクスポートするには、このメタデータ ファイルへの参照が必要です。                               |
| WME1090      | コア参照アセンブリを確認できませんでした。 /reference スイッチを使用して mscorlib.dll および System.Runtime.dll が参照されていることを確認してください。 |

 

## <a name="operator-overloading-is-not-allowed"></a>演算子のオーバーロードが許可されていない


マネージ コードで記述された Windows ランタイム コンポーネントでは、パブリック型のオーバーロードされた演算子を公開することはできません。

> **注** op など、メタデータ名によって、エラー メッセージに、演算子が識別される\_加算、op\_op Multiply、\_ExclusiveOr、op\_暗黙的な (暗黙の変換)などなど。

 

| エラー番号 | メッセージ テキスト                                                                                          |
|--------------|-------------------------------------------------------------------------------------------------------|
| WME1087      | '{0}' は演算子のオーバー ロードします。 マネージ型は、Windows ランタイムで演算子オーバーロードを公開できません。 |

 

## <a name="constructors-on-a-class-have-the-same-number-of-parameters"></a>クラスのコンストラクターに同じ数のパラメーターがある


UWP のクラスは、指定された数のパラメーターを持つコンストラクターを 1 つしか保持できません。たとえば、**String** 型の 1 つのパラメーターを持つコンストラクターと **int** 型 (Visual Basic の **Integer**) の 1 つのパラメーターを持つコンストラクターを両方保持することはできません。 唯一の回避策は、各コンストラクターで異なる数のパラメーターを使うことです。

| エラー番号 | メッセージ テキスト                                                                                                                                            |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1099      | 型 '{0}'に複数のコンス トラクターを持つ'{1}' 個の引数。 Windows ランタイム型には、同じ数の引数を持つ複数のコンストラクターがありません。 |

 

## <a name="must-specify-a-default-for-overloads-that-have-the-same-number-of-parameters"></a>同じ数のパラメーターを持つオーバーロードには既定値を指定する必要がある


UWP では、オーバーロードされたメソッドの 1 つが既定のオーバーロードとして指定されている場合にのみ、同じ数のパラメーターを持つことができます。 「[C# および Visual Basic での Windows ランタイム コンポーネントの作成](creating-windows-runtime-components-in-csharp-and-visual-basic.md)」の「オーバーロードされたメソッド」をご覧ください。

| エラー番号 | メッセージ テキスト                                                                                                                                                                      |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1059      | 複数{0}-のパラメーター オーバー ロード '{1}.{2}' Windows.Foundation.Metadata.DefaultOverloadAttribute で装飾されます。                                                            |
| WME1085      | {0}-のパラメーター オーバー ロード{1}.{2} Windows.Foundation.Metadata.DefaultOverloadAttribute で修飾して既定のオーバー ロードとして指定された 1 つのメソッドが必要です。 |

 

## <a name="namespace-errors-and-invalid-names-for-the-output-file"></a>出力ファイルの名前空間のエラーと無効な名前


ユニバーサル Windows プラットフォームでは、Windows メタデータ (.winmd) ファイルに含まれるすべてのパブリック型は、.winmd ファイルの名前を共有する名前空間、またはそのファイル名のサブ名前空間に含まれている必要があります。 たとえば、Visual Studio プロジェクトの名前が A.B (つまり、Windows ランタイム コンポーネントが A.B.winmd) の場合、パブリック クラス A.B.Class1 と A.B.C.Class2 を含めることができますが、A.Class3 (WME0006) または D.Class4 (WME1044) を含めることはできません。

> **注**  これらの制限は、実装で使用されるプライベート型がのみをパブリックの型を適用します。

 

A.Class3 の場合、Class3 を別の名前空間に移動するか、Windows ランタイム コンポーネントの名前を A.winmd に変更することができます。 WME0006 は警告ですが、エラーとして扱う必要があります。 前の例では、A.B.winmd を呼び出すコードは A.Class3 を特定することはできません。

D.Class4 の場合、ファイル名には D.Class4 と A.B 名前空間内のクラスの両方を含めることはできないため、Windows ランタイム コンポーネントの名前を変更することはできません。 D.Class4 を別の名前空間に移動するか、別の Windows ランタイム コンポーネントに配置できます。

ファイル システムは大文字と小文字を区別できないため、同じ名前で大文字と小文字だけが異なる名前空間は許可されません (WME1067)。

コンポーネントには、少なくとも 1 つの **public sealed** 型 (Visual Basic の **Public NotInheritable**) を含める必要があります。 含めない場合、コンポーネントにプライベート型が含まれるかどうかに応じて、WME1042 または WME1043 を受け取ります。

Windows ランタイム コンポーネントの型には、名前空間と同じ名前を付けることはできません (WME1068)。

> **注意**  Winmdexp.exe がコンポーネントのすべての名前空間を含む名前を生成しようとした場合、Winmdexp.exe を直接呼び出すし、Windows ランタイム コンポーネントの名前を指定するのには、/out オプションを使用しないでください。 名前空間の名前を変更すると、コンポーネントの名前も変更される場合があります。

 

| エラー番号 | メッセージ テキスト                                                                                                                                                                                                                                                                                                                                             |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME0006      | '{0}' このアセンブリの有効な winmd ファイル名ではありません。 Windows メタデータ ファイル内のすべての型は、ファイル名で指定される名前空間のサブ名前空間に存在する必要があります。 このようなサブ名前空間に存在しない型は、ランタイムに見つかりません。 このアセンブリでは、ファイル名として使用できる最も小さい共通の名前空間は '{1}' です。 |
| WME1042      | 入力モジュールには、名前空間内にある少なくとも 1 つのパブリック型を含める必要があります。                                                                                                                                                                                                                                                                   |
| WME1043      | 入力モジュールには、名前空間内にある少なくとも 1 つのパブリック型を含める必要があります。 名前空間内で検出された型はプライベートのみです。                                                                                                                                                                                                               |
| WME1044      | パブリック型が名前空間 ('{1}') を共有しません共通のプレフィックスと他の名前空間 ('{0}')。 Windows メタデータ ファイル内のすべての型は、ファイル名で指定される名前空間のサブ名前空間に存在する必要があります。                                                                                                                              |
| WME1067      | Namespace 名は大文字と小文字が異なることはできません: '{0}'、'{1}'。                                                                                                                                                                                                                                                                                                |
| WME1068      | 型 '{0}'名前空間と同じ名前を持つことはできません'{1}'。                                                                                                                                                                                                                                                                                                 |

 

## <a name="exporting-types-that-arent-valid-universal-windows-platform-types"></a>無効なユニバーサル Windows プラットフォーム型である型をエクスポートする


コンポーネントのパブリック インターフェイスは UWP 型のみを公開する必要があります。 ただし、.NET Framework には、.NET Framework や UWP とはわずかに異なる多数の一般的な型に対応したマッピングが用意されています。 これにより、.NET Framework の開発者は、新しい型を習得せずに、使い慣れた型を使うことができます。 マップされた .NET Framework 型は、コンポーネントのパブリック インターフェイスで使うことができます。 [「C# および Visual Basic での Windows ランタイム コンポーネントの作成」](creating-windows-runtime-components-in-csharp-and-visual-basic.md)の「Windows ランタイム コンポーネントの宣言型」と「ユニバーサル Windows プラットフォーム型のマネージ コードへの引き渡し」、および「 [.NET Framework での Windows ランタイム型の対応付け](net-framework-mappings-of-windows-runtime-types.md)」をご覧ください。

これらのマッピングの多くはインターフェイスです。 たとえば、[IList&lt;T&gt;](https://docs.microsoft.com/dotnet/api/system.collections.generic.ilist-1?redirectedfrom=MSDN) は、UWP インターフェイス [IVector&lt;T&gt;](https://docs.microsoft.com/uwp/api/Windows.Foundation.Collections.IVector_T_) にマップされます。 パラメーター型として IList&lt;string&gt; の代わりに List&lt;string&gt; (Visual Basic の `List(Of String)`) を使うと、Winmdexp.exe によって代替のインターフェイスのリストが提供されます。このリストには、List&lt;T&gt; によって実装されたマップ済みのインターフェイスがすべて含まれています。 List&lt;Dictionary&lt;int, string&gt;&gt; (Visual Basic の List(Of Dictionary(Of Integer, String))) など、入れ子になったジェネリック型を使う場合、Winmdexp.exe によって入れ子のレベルごとに選択肢のリストが提供されます。 これらのリストはかなり長くなる場合があります。

一般に、最適なのは型に最も近いインターフェイスです。 たとえば、Dictionary&lt;int, string&gt; の場合、IDictionary&lt;int, string&gt; が最適と考えられます。

> **重要な**  JavaScript はマネージ型を実装するインターフェイスの一覧の先頭に表示されるインターフェイスを使用します。 たとえば、Dictionary&lt;int, string&gt; を JavaScript コードに返した場合、戻り値の型としてどのインターフェイスを指定しても、IDictionary&lt;int, string&gt; として表示されます。 つまり、後のインターフェイスにメンバーが最初のインターフェイスに含まれていない場合、そのメンバーは JavaScript では認識されません。

> **注意**  の非ジェネリックの使用を避け[IList](https://docs.microsoft.com/dotnet/api/system.collections.ilist?redirectedfrom=MSDN)と[IEnumerable](https://docs.microsoft.com/dotnet/api/system.collections.ienumerable?redirectedfrom=MSDN)インターフェイス、コンポーネントが JavaScript で使用される場合。 これらのインターフェイスは、それぞれ [IBindableVector](https://docs.microsoft.com/uwp/api/windows.ui.xaml.interop.ibindablevector) と [IBindableIterator](https://docs.microsoft.com/uwp/api/windows.ui.xaml.interop.ibindableiterator) にマップされます。 これらは、XAML コントロールのバインドをサポートし、JavaScript には参照されません。 JavaScript では、実行時エラー ("関数 'X' に無効なシグネチャがあるため、呼び出せません") が発生します。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">エラー番号</th>
<th align="left">メッセージ テキスト</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">WME1033</td>
<td align="left">メソッド '{0}'パラメーターが'{1}'type' の{2}'。 '{2}' は、有効な Windows ランタイム パラメーター型ではありません。</td>
</tr>
<tr class="even">
<td align="left">WME1038</td>
<td align="left">メソッド '{0}'型のパラメーターが'{1}' そのシグニチャにします。 この型は有効な Windows ランタイム型ではありませんが、有効な Windows ランタイム型であるインターフェイスを実装しています。 メソッド シグネチャを次のいずれかの型を使用するように変更することを検討してください: '{2}'。</td>
</tr>
<tr class="odd">
<td align="left">WME1039</td>
<td align="left"><p>メソッド '{0}'型のパラメーターが'{1}' そのシグニチャにします。 このジェネリック型は有効な Windows ランタイム型ではありませんが、この型またはそのジェネリック パラメーターは、有効な Windows ランタイム型であるインターフェイスを実装します。 {2}</p>
> **注**  の{2}、Winmdexp.exe は代替のリストをなど、追加します"型の変更を検討してください 'System.Collections.Generic.List&lt;T&gt;' には、次の種類のいずれかのメソッド シグネチャでその代わりに：'System.Collections.Generic.IList&lt;T&gt;, System.Collections.Generic.IReadOnlyList&lt;T&gt;, System.Collections.Generic.IEnumerable&lt;T&gt;'."
</td>
</tr>
<tr class="even">
<td align="left">WME1040</td>
<td align="left">メソッド '{0}'型のパラメーターが'{1}' そのシグニチャにします。 管理されているタスク型を使用するのではなく、Windows.Foundation.IAsyncAction、Windows.Foundation.IAsyncOperation、またはその他の Windows ランタイムの非同期インターフェイスのいずれかを使用してください。 標準の .NET await パターンもこれらのインターフェイスに適用されます。 管理されているタスク オブジェクトを Windows ランタイムの非同期インターフェイスに変換する方法の詳細については、System.Runtime.InteropServices.WindowsRuntime.AsyncInfo を参照してください。</td>
</tr>
</tbody>
</table>

 

## <a name="structures-that-contain-fields-of-disallowed-types"></a>使うことができない型のフィールドを含む構造体


UWP では、構造体にはフィールドのみを含めることができ、フィールドは構造体にのみ含めることができます。 これらのフィールドはパブリック型である必要があります。 有効なフィールド型には、列挙体、構造体、およびプリミティブ型があります。

| エラー番号 | メッセージ テキスト                                                                                                                                                                                                                                                            |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| WME1060      | 構造体 '{0}'はフィールド'{1}'type' の{2}'。 '{2}' は有効な Windows ランタイム フィールド型ではありません。 Windows ランタイムの構造体に含まれる各フィールドに指定できるのは、UInt8、Int16、UInt16、Int32、UInt32、Int64、UInt64、Single、Double、Boolean、String、Enum、または構造体自体のみです。 |

 

## <a name="restrictions-on-arrays-in-member-signatures"></a>メンバーのシグネチャ内における配列の制限


UWP では、メンバーのシグネチャ内の配列は 1 次元で、下限を 0 (ゼロ) に指定する必要があります。 `myArray[][]` (Visual Basic の `myArray()()`) など、入れ子になった配列型を使うことはできません。

> **注** 配列の実装で内部的に使用するにはこの制限は適用されません。

 

| エラー番号 | メッセージ テキスト                                                                                                                                                     |
|--------------|--------------------|
| WME1034      | メソッド '{0}'型の配列を持つ'{1}' でそのシグニチャに下限を 0 以外。 Windows ランタイム メソッドのシグネチャ内の配列では、下限を 0 に指定する必要があります。 |
| WME1035      | メソッド '{0}'複数次元の配列の型が'{1}' そのシグニチャにします。 Windows ランタイム メソッドのシグネチャ内の配列は 1 次元配列にする必要があります。                  |
| WME1036      | メソッド '{0}'、入れ子になった配列の型が'{1}' そのシグニチャにします。 Windows ランタイム メソッドのシグネチャ内の配列を入れ子にすることはできません。                                    |

 

## <a name="array-parameters-must-specify-whether-array-contents-are-readable-or-writable"></a>配列パラメーターでは、配列の内容が読み取り可能であるか書き込み可能であるかどうかを指定する必要がある


UWP では、パラメーターは読み取り専用または書き込み専用に指定する必要があります。 パラメーターは、**ref** (Visual Basic では [OutAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.outattribute?redirectedfrom=MSDN) 属性のない **ByRef**) とマークすることはできません。 これは配列の内容に適用されるため、配列パラメーターは配列の内容が読み取り専用または書き込み専用であるかどうかを示す必要があります。 **out** パラメーター (Visual Basic では OutAttribute 属性のある **ByRef** パラメーター) の方向は明確ですが、値によって渡される配列パラメーター (Visual Basic の ByVal) はマークする必要があります。 [「Windows ランタイム コンポーネントに配列を渡す方法」](passing-arrays-to-a-windows-runtime-component.md)をご覧ください。

| エラー番号 | メッセージ テキスト         |
|--------------|----------------------|
| WME1101      | メソッド '{0}'パラメーターが'{1}' は、配列では、両方が含ま{2}と{3}します。 Windows ランタイムでは、配列パラメーターの内容は、読み取り可能または書き込み可能である必要があります。 属性の 1 つを '{1}' から削除してください。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| WME1102      | メソッド '{0}'が出力パラメーター'{1}' は、配列がある{2}します。 Windows ランタイムでは、出力配列の内容は書き込み可能です。 '{1}' から属性を削除してください。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| WME1103      | メソッド '{0}'パラメーターが'{1}' は、配列では、System.Runtime.InteropServices.InAttribute または system.runtime.interopservices.outattribute が指定されているとします。 Windows ランタイムでは、配列パラメーターに {2} または {3} を指定する必要があります。 これらの属性を削除するか、必要に応じて、適切な Windows ランタイム属性と置き換えてください。                                                                                                                                                                                                                                                                                                                                                                                          |
| WME1104      | メソッド '{0}'パラメーターが'{1}' は、配列ではないと、いずれかが、{2}または{3}します。 Windows ランタイムでは、配列でないパラメーターを {2} または {3} でマークすることがサポートされていません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| WME1105      | メソッド '{0}'パラメーターが'{1}' で、System.Runtime.InteropServices.InAttribute または system.runtime.interopservices.outattribute が指定されています。 Windows ランタイムでは、System.Runtime.InteropServices.InAttribute または System.Runtime.InteropServices.OutAttribute でパラメーターをマークすることはサポートされていません。 System.Runtime.InteropServices.InAttribute を削除して、System.Runtime.InteropServices.OutAttribute を 'out' 修飾子と置き換えることを検討してください。 メソッド '{0}'パラメーターが'{1}' で、System.Runtime.InteropServices.InAttribute または system.runtime.interopservices.outattribute が指定されています。 Windows ランタイムでは、System.Runtime.InteropServices.OutAttribute で ByRef パラメーターをマークすることのみサポートされており、これらの属性の他の使用方法はサポートされていません。 |
| WME1106      | メソッド '{0}'パラメーターが'{1}' は配列です。 Windows ランタイムでは、配列パラメーターの内容が読み取り可能または書き込み可能である必要があります。 {2} または {3} を '{1}' に適用してください。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |


## <a name="member-with-a-parameter-named-value"></a>"value" という名前のパラメーターを持つメンバー


UWP では、戻り値は出力パラメーターであると見なされ、パラメーターの名前は一意である必要があります。 既定では、Winmdexp.exe は戻り値に "value" という名前を設定します。 メソッドに "value" という名前のパラメーターがあると、エラー WME1092 が発生します。 これを修正するには 2 つの方法があります。

-   パラメーターに "value" 以外の名前を付けます (プロパティ アクセサーの場合は "returnValue" 以外の名前)。
-   次に示すように、ReturnValueNameAttribute 属性を使って戻り値の名前を変更します。

    > [!div class="tabbedCodeSnippets"]
    > ```cs
    > using System.Runtime.InteropServices;
    > using System.Runtime.InteropServices.WindowsRuntime;
    >
    > [return: ReturnValueName("average")]
    > public int GetAverage(out int lowValue, out int highValue)
    > ```
    > ```vb
    > Imports System.Runtime.InteropServices
    > Imports System.Runtime.InteropServices.WindowsRuntime
    >
    > Public Function GetAverage(<Out> ByRef lowValue As Integer, _
    > <Out> ByRef highValue As Integer) As <ReturnValueName("average")> String
    > ```

> **注**  戻り値の名前を変更すると、新しい名前が別のパラメーターの名前と競合、エラー WME1091 が発生します。

JavaScript コードは、戻り値も含め、メソッドの出力パラメーターに名前でアクセスできます。 例については、[ReturnValueNameAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.interopservices.windowsruntime.returnvaluenameattribute?redirectedfrom=MSDN) 属性に関するトピックをご覧ください。

| エラー番号 | メッセージ テキスト |
|--------------|--------------|
| WME1091 | メソッド '\{0}' という名前の戻り値が'\{1}'、パラメーター名と同じです。 Windows ランタイム メソッドのパラメーターと戻り値には一意の名前を指定する必要があります。 |
| WME1092 | メソッド '\{0}' という名前のパラメーターが'\{1}' は、既定値と同じ戻り値の名前。 このパラメーターに別の名前を使用するか、System.Runtime.InteropServices.WindowsRuntime.ReturnValueNameAttribute を使用して、戻り値の名前を明示的に指定してください。 |

**注**  既定の名前はプロパティ アクセサーの場合は"returnValue"と"value"その他のすべてのメソッドです。


## <a name="related-topics"></a>関連トピック

* [C# および Visual Basic での Windows ランタイム コンポーネントの作成](creating-windows-runtime-components-in-csharp-and-visual-basic.md)
* [Winmdexp.exe (Windows ランタイム メタデータ エクスポート ツール)](https://docs.microsoft.com/dotnet/framework/tools/winmdexp-exe-windows-runtime-metadata-export-tool)
