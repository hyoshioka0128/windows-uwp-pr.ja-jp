---
ms.assetid: 0CBCEEA0-2B0E-44A1-A09A-F7A939632F3A
title: ストーリーボードに設定されたアニメーション
description: ストーリーボードに設定されたアニメーションは、単なる視覚なアニメーションではありません。
ms.date: 07/13/2018
ms.topic: article
keywords: windows 10, uwp
ms.localizationpriority: medium
ms.openlocfilehash: ebc87c685d92fa4dbc1a954e2fc6f0cf549a5554
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66366075"
---
# <a name="storyboarded-animations"></a>ストーリーボードに設定されたアニメーション

ストーリーボードに設定されたアニメーションは、単なる視覚なアニメーションではありません。 ストーリーボードに設定されたアニメーションは、依存関係プロパティの値を時間の関数として変更する手段です。 アニメーション ライブラリからではないストーリーボードに設定されたアニメーションが必要になる主な理由として、コントロール テンプレートまたはページ定義の一部としてコントロールの表示状態を定義できることが挙げられます。

## <a name="differences-with-silverlight-and-wpf"></a>Silverlight や WPF を使ったアニメーションとの違い

Microsoft Silverlight または Windows Presentation Foundation (WPF) に慣れている方は、このセクションをお読みください。それ以外の方は飛ばしてくださって結構です。

一般に、Windows ランタイム アプリのストーリーボードに設定されたアニメーションの作成は、Silverlight や WPF と似ています。 ただし、重要な違いがいくつかあります。

-   ストーリーボードに設定されたアニメーションは、UI を視覚的にアニメーション化する唯一の方法ではなく、アプリ開発者にとってもっと簡単な方法も他にあります。 ストーリーボードに設定されたアニメーションを使わず、テーマ アニメーションと切り替え効果のアニメーションを使う方が設計上効率的であるケースはよくあります。 これらを使うと、複雑なアニメーション プロパティのターゲット設定を扱わずに済み、推奨 UI アニメーションをすばやく作成できます。 詳しくは、「[アニメーションの概要](xaml-animation.md)」をご覧ください。
-   Windows ランタイムの多くの XAML コントロールには、組み込み動作の一部としてテーマ アニメーションと切り替え効果のアニメーションが組み込まれています。 ほとんどの場合、WPF や Silverlight コントロールには既定のアニメーション動作がありませんでした。
-   UI のパフォーマンスが低下するとアニメーション システムによって判断された場合、作成したすべてのカスタム アニメーションが Windows ランタイム アプリでそのまま動くわけではありません。 アプリのパフォーマンスに影響を及ぼす可能性があるとシステムによって判断されたアニメーションを*依存型アニメーション*といいます。 "依存型" と呼ばれるのは、アニメーションのクロッキングは UI スレッドに対して直接作用するためです。この UI スレッドは、アクティブなユーザー入力やその他の更新によって UI に対してランタイムの変更の適用が試行される部分でもあります。 UI スレッドで大量のシステム リソースを消費する依存型アニメーションの場合、特定の状況においてアプリが応答していないかのように見えることがあります。 自分が作成したアニメーションが、レイアウトの変更を含め、UI スレッドのパフォーマンスへの影響を伴う可能性がある場合は、アニメーションを明示的に有効にし、動作することを確かめる必要があります。 これを行うのが、特定のアニメーション クラスに用意されている **EnableDependentAnimation** プロパティです。 詳しくは、「[依存型および独立型アニメーション](./storyboarded-animations.md#dependent-and-independent-animations)」をご覧ください。
-   カスタム イージング関数は現在 Windows ランタイムではサポートされていません。

## <a name="defining-storyboarded-animations"></a>ストーリーボードに設定されたアニメーションの定義

ストーリーボードに設定されたアニメーションは、依存関係プロパティの値を時間の関数として変更する手段です。 アニメーション化するプロパティは、アプリの UI に直接影響するプロパティであるとは限りません。 ただし、XAML はアプリ UI を定義するものであるため、通常は、アニメーション化の対象となる UI 関連のプロパティです。 たとえば、[**RotateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.RotateTransform) の角度やボタンの背景色の値をアニメーション化することができます。

ストーリーボードに設定されたアニメーションを定義する主な場面の 1 つは、コントロールの作成や再テンプレート化を担当しており、表示状態を定義する必要があるときです。 詳しくは、「[表示状態用にストーリーボードに設定されたアニメーション](https://docs.microsoft.com/previous-versions/windows/apps/jj819808(v=win.10))」をご覧ください。

表示状態とアプリのカスタム アニメーションのどちらを定義するときも、このトピックで説明するストーリーボードに設定されたアニメーションの概念と API はほぼ適用できます。

アニメーション化するためには、ストーリーボードに設定されたアニメーションでターゲットに設定するプロパティが*依存関係プロパティ*である必要があります。 依存関係プロパティは、Windows ランタイム XAML 実装の重要な機能です。 通常、一般的な UI 要素の書き込み可能なプロパティは依存関係プロパティとして実装されるため、アニメーション化したり、データ バインディング値を適用したり、[**Style**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) を適用し、[**Setter**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Setter) でプロパティのターゲット設定を行ったりできます。 依存関係プロパティのしくみについて詳しくは、「[依存関係プロパティの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/dependency-properties-overview)」をご覧ください。

ほとんどの場合、ストーリーボードに設定されたアニメーションを定義するには XAML を記述します。 Microsoft Visual Studio などのツールを利用すれば、XAML は自動的に生成されます。 ストーリーボードに設定されたアニメーションをコードを使って定義することもできますが、あまり一般的ではありません。

シンプルな例を見てみましょう。 この XAML の例では、[**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) プロパティを特定の [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) オブジェクトでアニメーション化しています。

```xaml
<Page ...>
  <Page.Resources>
    <!-- Storyboard resource: Animates a rectangle's opacity. -->
    <Storyboard x:Name="myStoryboard">
      <DoubleAnimation
        Storyboard.TargetName="MyAnimatedRectangle"
        Storyboard.TargetProperty="Opacity"
        From="1.0" To="0.0" Duration="0:0:1"/>
    </Storyboard>
  </Page.Resources>

  <!--Page root element, UI definition-->
  <Grid>
    <Rectangle x:Name="MyAnimatedRectangle"
      Width="300" Height="200" Fill="Blue"/>
  </Grid>
</Page>
```

### <a name="identifying-the-object-to-animate"></a>アニメーション化の対象となるオブジェクトの指定

先ほどの例では、ストーリーボードで [**Rectangle**](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle) の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) プロパティがアニメーション化されています。 オブジェクト自体ではアニメーションを宣言しません。 代わりに、ストーリーボードのアニメーション定義内で宣言します。 ストーリーボードは、アニメーション化するオブジェクトの XAML UI 定義のすぐ近くにない XAML で定義されるのが普通です。 代わりに、通常は、XAML リソースとして設定します。

ターゲットにアニメーションを接続するには、識別用のプログラミング名でターゲットを参照します。 必ず XAML UI 定義の [x:Name 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-name-attribute)を適用して、アニメーション化するオブジェクトに名前を付けてください。 その後で、アニメーション定義内の [**Storyboard.TargetName**](https://docs.microsoft.com/dotnet/api/system.windows.media.animation.storyboard.targetname?view=netframework-4.8) を設定することで、アニメーション化するオブジェクトのターゲット設定を行います。 **Storyboard.TargetName** の値には、ターゲット オブジェクトの名前文字列を使います。これは、前に別の場所で x:Name 属性を使って設定した値です。

### <a name="targeting-the-dependency-property-to-animate"></a>アニメーション化する依存関係プロパティの指定

アニメーションの [**Storyboard.TargetProperty**](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ms616983(v%3Dvs.95)) の値を設定します。 これにより、アニメーション化するターゲット オブジェクトのプロパティが決まります。

ターゲット オブジェクトの直接のプロパティではないプロパティをターゲットにする必要があることもありますが、オブジェクトとプロパティの関係の中でより深い入れ子の状態になります。 アニメーション化できるプロパティの型 ([**Double**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN)、[**Point**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Point)、[**Color**](https://docs.microsoft.com/uwp/api/Windows.UI.Color)) を参照できるまで、関係する一連のオブジェクトとプロパティの値をドリルダウンするために、これが必要になることがよくあります。 この概念を *"間接的なターゲット設定"* と呼び、この方法でアニメーションの対象プロパティを設定する構文を *"プロパティ パス"* と呼びます。

次に例を示します。 ストーリーボードに設定されたアニメーションの一般的なシナリオの 1 つに、コントロールが特定の状態にあることを表すためにアプリ UI やコントロールの一部の色を変更するというシナリオがあります。 たとえば、赤から緑に変化するように [**TextBlock**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.TextBlock) の [**Foreground**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.textblock.foreground) をアニメーション化するとします。 [  **ColorAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.ColorAnimation) の呼び出しが必要と思われるでしょう。それは正しいものの、 オブジェクトの色に影響する UI 要素のプロパティは、実際には [**Color**](https://docs.microsoft.com/uwp/api/Windows.UI.Color) 型ではなく、 [  **Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) 型です。 そのため、アニメーションのターゲット設定に実際に必要なのは、[**SolidColorBrush**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) クラスの [**Color**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush.Color) プロパティです。これは、これらの色関連の UI プロパティに一般的に使われる **Brush** 派生型です。 アニメーションのプロパティのターゲット設定に使うプロパティ パスの作成という点に注目すると、次のようになります。

```xaml
<Storyboard x:Name="myStoryboard">
  <ColorAnimation
    Storyboard.TargetName="tb1"
    Storyboard.TargetProperty="(TextBlock.Foreground).(SolidColorBrush.Color)"
    From="Red" To="Green"/>
</Storyboard>
```

この構文について、各部分に注目して説明します。

- プロパティ名は、かっこ () の各セットで囲みます。
- プロパティ名の中にドットがありますが、そのドットは型名とプロパティ名を区切って対象のプロパティを明確にするためのものです。
- かっこ内にない中央のドットはステップを表します。 これは、最初のプロパティ (オブジェクト) の値を受け取り、オブジェクト モデルをステップ実行してから、最初のプロパティの値の特定のサブプロパティをターゲットとするという意味に解釈されます。

次に、アニメーションのターゲット設定のシナリオを示します。おそらくこうしたシナリオでは、間接的なプロパティのターゲット設定と、使う構文に似たプロパティ パス文字列を使うことになります。

- [  **RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform) に適用される、[**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) の [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.translatetransform.x) 値のアニメーション化: `(UIElement.RenderTransform).(TranslateTransform.X)`
- [  **Fill**](/uwp/api/Windows.UI.Xaml.Shapes.Shape.Fill) に適用される、[**LinearGradientBrush**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.LinearGradientBrush) の [**GradientStop**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.GradientStop) 内の [**Color**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush.Color) のアニメーション化: `(Shape.Fill).(GradientBrush.GradientStops)[0].(GradientStop.Color)`
- [  **RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform) に適用される、[**TransformGroup**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TransformGroup) における 4 つの変換の 1 つである [**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) の [**X**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.translatetransform.x) 値のアニメーション化: `(UIElement.RenderTransform).(TransformGroup.Children)[3].(TranslateTransform.X)`

これらの例の一部では、数を囲む角かっこが使われていることがわかります。 これはインデクサーです。 前のプロパティ名に値としてコレクションが含まれており、そのコレクション内からの項目 (0 から始まるインデックスで識別される) が必要であることを示しています。

XAML 添付プロパティをアニメーション化することもできます。 `(Canvas.Left)` のように、必ず完全な添付プロパティの名前をかっこで囲んでください。 詳しくは、「[XAML 添付プロパティのアニメーション化](./storyboarded-animations.md#animating-xaml-attached-properties)」をご覧ください。

アニメーション化するプロパティの間接的なターゲット設定をプロパティ パスで行う方法について詳しくは、「[プロパティ パス構文](https://docs.microsoft.com/windows/uwp/xaml-platform/property-path-syntax)」または「[**Storyboard.TargetProperty 添付プロパティ**](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ms616983(v%3Dvs.95))」をご覧ください。

### <a name="animation-types"></a>アニメーション型

Windows ランタイムのアニメーション システムには、ストーリーボードに設定されたアニメーションを適用できる 3 つの型があります。

-   [**二重**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN)、いずれかでアニメーション化できる[ **DoubleAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.DoubleAnimation)
-   [**ポイント**](https://docs.microsoft.com/uwp/api/Windows.Foundation.Point)、いずれかでアニメーション化できる[ **PointAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.PointAnimation)
-   [**色**](https://docs.microsoft.com/uwp/api/Windows.UI.Color)、いずれかでアニメーション化できる[ **ColorAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.ColorAnimation)

また、後ほど説明するオブジェクトの参照値に使える汎用 [**Object**](https://docs.microsoft.com/dotnet/api/system.object?redirectedfrom=MSDN) アニメーション型もあります。

### <a name="specifying-the-animated-values"></a>アニメーション化された値の指定

オブジェクトとプロパティをアニメーション化のターゲットとして設定する方法については以上ですが、アニメーションを実行するとプロパティ値にどのような影響があるかについてはまだ説明していません。

ここまでで説明したアニメーションの種類は、**From**/**To**/**By** アニメーションとも呼ばれます。 これは、アニメーションが、アニメーション定義からのこれらの入力の 1 つ以上を使って、時間の経過と共にプロパティの値を変更することを意味します。

-   開始値は **From** です。 **From** 値を指定しない場合、開始値は、アニメーション化されたプロパティにアニメーションの実行前に設定されていた値になります。 これは、既定値、スタイルまたはテンプレートからの値、XAML UI 定義またはアプリ コードによって個別に適用された値のいずれかである可能性があります。
-   アニメーションの終了時の値は **To** 値です。
-   開始値を基準とする相対的な終了値を指定するには、**By** プロパティを設定します。 **To** のプロパティの代わりに、これを設定します。
-   **To** 値または **By** 値を指定しない場合、終了値は、アニメーション化されたプロパティにアニメーションの実行前に設定されていた値になります。 この場合は、**From** 値をお勧めします。そうしないと、アニメーションによって値がまったく変更されず、開始値と終了値が同じになるためです。
-   アニメーションには **From**、**By**、または **To** のうち少なくとも 1 つが指定されるのが一般的ですが、3 つすべてが指定されることはありません。

前の XAML の例に戻り、**From** 値と **To** 値、それに **Duration** をもう一度見てみましょう。 この例では [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) プロパティをアニメーション化します。**Opacity** のプロパティ型は [**Double**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN) です。 そのため、ここで使うアニメーションは [**DoubleAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.DoubleAnimation) です。

`From="1.0" To="0.0"` は、アニメーション開始時の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) プロパティの初期値が 1 で、これが 0 になるまでアニメーション化することを示します。 つまり、これらの [**Double**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN) 値が **Opacity** プロパティに与える効果は、当初不透明な状態のオブジェクトを徐々に透明にするというものです。

```xaml
...
<Storyboard x:Name="myStoryboard">
  <DoubleAnimation
    Storyboard.TargetName="MyAnimatedRectangle"
    Storyboard.TargetProperty="Opacity"
    From="1.0" To="0.0" Duration="0:0:1"/>
</Storyboard>
...
```

`Duration="0:0:1"` は、アニメーションの継続期間、つまり四角形が消える速さを指定します。 [  **Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) プロパティは、*時間*:*分*:*秒*という形式で指定します。 この例のアニメーションの継続時間は 1 秒ということになります。

[  **Duration**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Duration) 値と XAML 構文について詳しくは、「[**Duration**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Duration)」をご覧ください。

> [!NOTE]
> 紹介した例の場合、アニメーション化するオブジェクトの開始状態の [**Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) が既定値か明示的な設定かを問わず常に 1 である場合は、**From** 値を省略できます。そのときアニメーションでは暗黙的な開始値が使われ、同じ結果になります。

### <a name="fromtoby-are-nullable"></a>From/To/By では null が許容される

**From**、**To**、または **By** は省略でき、省略した値の代わりにアニメーション化されない現在の値を使うことができると説明しました。 アニメーションの **From**、**To**、**By** の各プロパティは、想定した型ではない場合があります。 たとえば、[**DoubleAnimation.To**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.doubleanimation.easingfunction) プロパティの型は [**Double**](https://docs.microsoft.com/dotnet/api/system.double?redirectedfrom=MSDN) ではなく、 **Double** に対しては [**Nullable**](https://docs.microsoft.com/dotnet/api/system.nullable-1?redirectedfrom=MSDN) です。 既定値は 0 ではなく **null** です。 **null** 値により、アニメーション システムは、**From**、**To**、または **By** プロパティの値が明示的に設定されていないことを識別します。 Visual C コンポーネント拡張 (C +/cli CX) がない、 **Nullable**型であるため、使用して[ **IReference** ](https://docs.microsoft.com/uwp/api/Windows.Foundation.IReference_T_)代わりにします。

### <a name="other-properties-of-an-animation"></a>アニメーションのその他のプロパティ

次のセクションで説明するプロパティはいずれも省略可能であり、ほとんどのアニメーションに適した既定値を持ちます。

### <a name="autoreverse"></a>**AutoReverse**

アニメーションで [**AutoReverse**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.autoreverse) または [**RepeatBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.repeatbehavior) を指定しなかった場合、そのアニメーションは 1 回実行され、さらに [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) で指定された期間実行されます。

[  **AutoReverse**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.autoreverse) プロパティは、[**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) の最後に達した後で逆にタイムラインを再生するかどうかを指定します。 これを **true** に設定すると、アニメーションは宣言済みの [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) の最後に達した後で逆に再生され、値がその終了値 (**To**) から開始値 (**From**) に変更されます。 これは、アニメーションが実質的に [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) の倍の時間実行されることを表します。

### <a name="repeatbehavior"></a>**RepeatBehavior**

[  **RepeatBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.repeatbehavior) プロパティは、タイムラインの再生回数か、タイムラインを繰り返すより長い期間を指定します。 既定では、タイムラインの反復回数は "1x" であり、その [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) の間に 1 回再生され、繰り返されません。

アニメーションが複数回反復して実行されるようにすることができます。 たとえば、値 "3x" により、アニメーションは 3 回実行されます。 また、[**RepeatBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.repeatbehavior) に別の [**Duration**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Duration) を指定することもできます。 その **Duration** は、アニメーション自体の **Duration** よりも長くしてください。 たとえば、[**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) が "0:0:2" のアニメーションに対して **RepeatBehavior** を "0:0:10" に指定した場合、アニメーションは 5 回繰り返されます。 この値が割り切れない場合、**RepeatBehavior** の時間に達した時点でアニメーションは途切れてしまいます。 最後に、特別な "Forever" という値を指定することもできます。この値を指定すると、アニメーションは意図的に停止されるまで無限に実行されます。

[  **RepeatBehavior**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.RepeatBehavior) 値と XAML 構文について詳しくは、「[**RepeatBehavior**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.RepeatBehavior)」をご覧ください。

### <a name="fillbehaviorstop"></a>**FillBehavior ="Stop"**

既定では、アニメーションが終了すると、その継続期間を超過した後も、プロパティ値は最終的な **To** か、**By** で変更された値で維持されます。 ただし、[**FillBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.fillbehavior) プロパティの値を [**FillBehavior.Stop**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.FillBehavior) に設定した場合、アニメーション化された値はアニメーションが適用される前の値か、より正確には、依存関係プロパティ システムによって特定された現在の有効な値に戻ります (この違いについて詳しくは、「[依存関係プロパティの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/dependency-properties-overview)」をご覧ください)。

### <a name="begintime"></a>**BeginTime**

既定では、アニメーションの [**BeginTime**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.begintime) は "0:0:0" であるため、上位の [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) の実行と同時に開始されます。 この動作は、**Storyboard** に複数のアニメーションが含まれており、アニメーションどうしの開始のタイミングをずらしたり、開始のタイミングを意図的に少し遅らせたりする場合には、変更できます。

### <a name="speedratio"></a>**SpeedRatio**

[  **Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) に複数のアニメーションがある場合は、**Storyboard** を基準に 1 つ以上のアニメーションのタイム レートを変更できます。 これは、アニメーションの実行中に経過する [**Duration**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Duration) 時間を最終的に制御する親 **Storyboard** です。 このプロパティはあまり利用されません。 詳しくは、「[**SpeedRatio**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.speedratio)」をご覧ください。

## <a name="defining-more-than-one-animation-in-a-storyboard"></a>**Storyboard** での複数のアニメーションの定義

[  **Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) のコンテンツとして、複数のアニメーション定義を設定できます。 同じターゲット オブジェクトの 2 種類のプロパティに関連のアニメーションを適用している場合は、複数のアニメーションが存在する可能性があります。 たとえば、UI 要素の [**RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform) として使われる [**TranslateTransform**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.TranslateTransform) の [**TranslateX**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.compositetransform.translatex) プロパティと  [**TranslateY**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.compositetransform.translatey) プロパティを両方とも変更する必要がある場合は、要素は対角線状に変換されます。 そのためには 2 つのアニメーションが必要ですが、それらを常に一緒に実行するために、同じ **Storyboard** に設定したい場合もあります。

これらのアニメーションは同じ型でなくてもよく、同じオブジェクトをターゲットにする必要もありません。 継続時間が違っていてもかまわず、プロパティ値を共有する必要はありません。

親 [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) が実行されると、その中の各アニメーションも実行されます。

[  **Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) クラスには、実際にはアニメーション型と同様に多数の同じアニメーション プロパティがあります。どちらも [**Timeline**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Timeline) 基底クラスを共有しているためです。 そのため、**Storyboard** には [**RepeatBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.repeatbehavior) か [**BeginTime**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.begintime) を設定できます。 通常は、含まれるすべてのアニメーションにその動作を持たせる場合を除いて、これらを **Storyboard** に設定することはありません。 一般に、**Storyboard** に設定されている **Timeline** プロパティはそのすべての子アニメーションに適用されます。 非設定の場合、**Storyboard** には、含まれるアニメーションの最も長い [**Duration**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Duration) 値から計算された暗黙的な継続時間が使われます。 子アニメーションのいずれかよりも短い [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) を **Storyboard** に明示的に設定すると、そのアニメーションは途中で途切れてしまいます。これは、通常は望ましくありません。

ストーリーボードには、同じオブジェクトの同じプロパティをターゲットにしてアニメーション化する 2 つのアニメーションを含めることはできません。 これを試みると、ストーリーボードの実行を試みたときにランタイム エラーが発生します。 この制限は、[**BeginTime**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.begintime) 値と継続時間が意図的に異なる設定になっているためにアニメーションが時間的に重ならない場合でも適用されます。 実際に 1 つのストーリーボードで同じプロパティにより複雑なアニメーション タイムラインを適用する場合は、キー フレーム アニメーションを使います。 「[キーフレームとイージング関数のアニメーション](key-frame-and-easing-function-animations.md)」をご覧ください。

アニメーション システムは、複数のアニメーションをプロパティの値に適用できます (それらが複数のストーリーボードからの入力である場合)。 意図的にこの動作を使って同時にストーリーボードを実行するのは一般的ではありません。 ただし、コントロールのプロパティに適用する、アプリで定義されたアニメーションによって、コントロールの表示状態モデルの一部として以前に実行されたアニメーションの **HoldEnd** 値が変更される可能性があります。

## <a name="defining-a-storyboard-as-a-resource"></a>リソースとしてのストーリーボードの定義

[  **Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) は、アニメーション オブジェクトを入れるコンテナーです。 **Storyboard** は、ページ レベルの [**Resources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.resources) または [**Application.Resources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application.resources) で、アニメーション化の対象となるオブジェクトから利用できるリソースとして定義するのが一般的です。

次の例は、前の例の [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) がページ レベルの [**Resources**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.resources) の定義にどのように含まれているかを示しており、**Storyboard** は、ルート [**Page**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Controls.Page) のキーを持つリソースです。 [x:Name 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-name-attribute)に注目してください。 この属性は、コードだけでなく XAML の他の要素でも後から **Storyboard** を参照できるように、**Storyboard** に対して変数名を定義する方法を示しています。

```xaml
<Page ...>
  <Page.Resources>
    <!-- Storyboard resource: Animates a rectangle's opacity. -->
    <Storyboard x:Name="myStoryboard">
      <DoubleAnimation
        Storyboard.TargetName="MyAnimatedRectangle"
        Storyboard.TargetProperty="Opacity"
        From="1.0" To="0.0" Duration="0:0:1"/>
    </Storyboard>
  </Page.Resources>
  <!--Page root element, UI definition-->
  <Grid>
    <Rectangle x:Name="MyAnimatedRectangle"
      Width="300" Height="200" Fill="Blue"/>
  </Grid>
</Page>
```

リソースを XAML ファイル (page.xaml や app.xaml など) の XAML ルートで定義する方法は、キーを持つリソースを XAML で編成する場合の一般的な方法です。 リソースを別個のファイルに分け、アプリやパッケージにマージすることもできます。 詳しくは、「[ResourceDictionary と XAML リソースの参照](https://docs.microsoft.com/windows/uwp/controls-and-patterns/resourcedictionary-and-xaml-resource-references)」をご覧ください。

> [!NOTE]
> Windows ランタイムの XAML は [x:Key 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-key-attribute)か [x: Name 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-name-attribute)を使ったリソースの識別をサポートします。 [  **Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) では x: Name 属性を使う方が一般的です。これを変数名を使って参照することになるためで、その [**Begin**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.begin) メソッドを後で呼び出してアニメーションを実行できるようにする目的があります。 [x:Key 属性](https://docs.microsoft.com/windows/uwp/xaml-platform/x-key-attribute)を使う場合は、[**Item**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.resourcedictionary.item) インデクサーなどの [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) メソッドを使ってキーを持つリソースとしてそれを取得し、取得したオブジェクトを **Storyboard** にキャストして、**Storyboard** メソッドを使う必要があります。

### <a name="storyboards-for-visual-states"></a>表示状態用のストーリーボード

また、コントロールの見た目に対して表示状態のアニメーションを宣言する場合は、アニメーションを [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) ユニットに含めます。 その場合、定義する **Storyboard** 要素は、[**Style**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Style) (キーを持つリソースである **Style**) 内でより深く入れ子にされる [**VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) コンテナーに含めます。 この場合、**Storyboard** に対してキーや名前は必要ありません。それは、これが、[**VisualStateManager**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.visualstatemanager) が呼び出すことができるターゲットの名前を持つ  **VisualState** であるためです。 ページまたはアプリの **Resources** コレクションに配置する代わりに、コントロールのスタイルを別個の XAML [**ResourceDictionary**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.ResourceDictionary) ファイルに格納する方法は一般的な方法です。 詳しくは、「[表示状態用にストーリーボードに設定されたアニメーション](https://docs.microsoft.com/previous-versions/windows/apps/jj819808(v=win.10))」をご覧ください。

## <a name="dependent-and-independent-animations"></a>依存型および独立型アニメーション

ここで、アニメーション システムの動作についていくつか重要な点を紹介しておきます。 特に、アニメーションには、Windows ランタイム アプリが画面にレンダリングされるしくみや、そのレンダリングでの処理スレッドの使い方と深い関係があります。 Windows ランタイム アプリには常にメイン UI スレッドがあり、このスレッドで現在の情報を基に画面を更新します。 また、Windows ランタイム アプリには合成スレッドがあります。このスレッドは、レイアウトを表示の直前に事前計算するために使われます。 UI をアニメーション化すると、UI スレッドに対し多数の処理が発生する可能性があります。 システムは、各更新間の非常に短い時間を使って画面の大きな領域を再描画しなければなりません。 これはアニメーション化されたプロパティの最新のプロパティ値を取得するために必要です。 注意しないと、アニメーションによって UI の応答性が低下したり、同じ UI スレッドにある他のアプリ機能のパフォーマンスに影響したりするおそれがあります。

UI スレッドの処理を遅くする可能性があると判断された各種アニメーションは、*依存型アニメーション*と呼ばれます。 この心配のないアニメーションは*独立型アニメーション*と呼ばれます。 依存型アニメーションと独立型アニメーションの違いは、先ほど説明したアニメーションの型 ([**DoubleAnimation**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.DoubleAnimation) など) だけでは決まりません。 アニメーション化するプロパティや、コントロールの継承や複合などの要因によって決まります。 アニメーションで UI を変更しても、UI スレッドへの影響がごく小さく、アニメーションを合成スレッドによって独立型アニメーションとして処理できることもあります。

アニメーションに次のいずれかの特性がある場合は独立型と見なされます。

-   アニメーションの [**Duration**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.duration) が 0 秒である (「警告」をご覧ください)
-   アニメーションのターゲットが [**UIElement.Opacity**](/uwp/api/Windows.UI.Xaml.UIElement.Opacity) である
-   これらのサブプロパティ値、アニメーションのターゲット[ **UIElement** ](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.UIElement)プロパティ。[**Transform3D**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.transform3d)、 [ **RenderTransform**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.rendertransform)、 [**プロジェクション**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.projection)、 [ **クリップ**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.clip)
-   アニメーションのターゲットが [**Canvas.Left**](https://docs.microsoft.com/dotnet/api/system.windows.controls.canvas.left?view=netframework-4.8) または [**Canvas.Top**](https://docs.microsoft.com/dotnet/api/system.windows.controls.canvas.top?view=netframework-4.8)
-   アニメーションのターゲットが [**Brush**](/uwp/api/Windows.UI.Xaml.Media.Brush) 値であり、[**SolidColorBrush**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush) を使い、その [**Color**](/uwp/api/Windows.UI.Xaml.Media.SolidColorBrush.Color) をアニメーション化する
-   アニメーションが [**ObjectAnimationUsingKeyFrames**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.ObjectAnimationUsingKeyFrames) である

> [!WARNING]
> アニメーションが独立型であると見なされるためには、明示的に `Duration="0"` を設定する必要があります。 たとえば、この XAML から `Duration="0"` を削除した場合、フレームの [**KeyTime**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.doublekeyframe.keytime) が "0:0:0" であった場合でも、アニメーションは独立型であると見なされます。

```xaml
<Storyboard>
  <DoubleAnimationUsingKeyFrames
    Duration="0"
    Storyboard.TargetName="Button2"
    Storyboard.TargetProperty="Width">
    <DiscreteDoubleKeyFrame KeyTime="0:0:0" Value="200"/>
  </DoubleAnimationUsingKeyFrames>
</Storyboard>
```

アニメーションがこれらの条件を満たしていない場合は、おそらく依存型アニメーションです。 既定では、アニメーション システムは依存型アニメーションを実行しません。 そのため、開発とテストのプロセス中に、アニメーションの実行を確認できない可能性もあります。 このアニメーションを使うことはできるものの、こうした各依存型アニメーションを明示的に有効にする必要があります。 アニメーションを有効にするには、アニメーション オブジェクトの **EnableDependentAnimation** プロパティを **true** に設定します  (アニメーションを表す [**Timeline**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Timeline) サブクラスごとにプロパティの実装は異なりますが、いずれも名前は `EnableDependentAnimation` です)。

アプリ開発者に課される依存型アニメーションを有効にするという要件は、開発経験を活かしたアニメーション システムにおける重要な設計の一側面です。 開発者は、アニメーションには UI の応答性の低下というパフォーマンス コストが存在することに注意しなければなりません。 パフォーマンスの低いアニメーションは、フルスケールのアプリでの分離とデバッグが困難です。 そのため、アプリの UI エクスペリエンスに実際に必要な依存型アニメーションだけを有効にする方が適切です。 多くのサイクルを使う装飾的なアニメーションによりアプリのパフォーマンスが低下しないように注意する必要があります。 アニメーションのパフォーマンスに関するヒントについて詳しくは、「[アニメーションとメディアの最適化](https://docs.microsoft.com/windows/uwp/debug-test-perf/optimize-animations-and-media)」をご覧ください。

アプリ開発者は、**EnableDependentAnimation** が **true** でも、依存型アニメーションを常に無効にするアプリ全体の設定を適用することもできます。 「[**Timeline.AllowDependentAnimations**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.allowdependentanimations)」をご覧ください。

> [!TIP]
> Blend for Visual Studio 2017 では、アニメーション ウィンドウを使用しているは、visual state プロパティに依存するアニメーションを適用しようとしたときに場合、は、デザイナーで警告が表示されます。 ビルド出力またはエラーの一覧で、警告は表示されません。 XAML を手動で、編集する場合、デザイナーでは、警告が表示されません。 出力ウィンドウのデバッグ出力時のデバッグ時に、警告が表示されます、アニメーションは独立していないはスキップされます。


## <a name="starting-and-controlling-an-animation"></a>アニメーションの開始と制御

ここまでで説明した内容だけでは、実際にはアニメーションは動作せず、適用もされません。 アニメーションが開始および実行されるまでは、アニメーションが XAML で宣言している値の変更は行われません。 アプリの有効期間またはユーザー エクスペリエンスに関連する何らかの方法で、アニメーションを明示的に開始する必要があります。 最も単純なレベルでは、アニメーションの親である [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) で [**Begin**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.begin) メソッドを呼び出してアニメーションを開始します。 XAML からメソッドを直接呼び出すことはできないため、アニメーションを有効にする場合は、必ずコードから行うことになります。 アプリのページまたはコンポーネントのコード ビハインドか、コントロールのロジック (カスタム コントロール クラスを定義する場合) を使うことになります。

通常は、[**Begin**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.begin) を呼び出し、継続時間が過ぎるまで単純にアニメーションを実行します。 ただし、[**Pause**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.pause)、[**Resume**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.resume)、[**Stop**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.stop) メソッドを使って実行時に [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) を制御することも、高度なアニメーション コントロールのシナリオに使われるその他の API を使うこともできます。

無限に繰り返すアニメーション (`RepeatBehavior="Forever"`) を含むストーリーボードで [**Begin**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.begin) を呼び出すと、アニメーションは、それを含むページがアンロードされるか、[**Pause**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.pause) または [**Stop**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.stop) を明示的に呼び出すまで実行されます。

### <a name="starting-an-animation-from-app-code"></a>アプリ コードからのアニメーションの開始

アニメーションは、自動的に開始することも、ユーザー操作に応答して開始することもできます。 自動的に開始する場合は、通常、アニメーション トリガーとして機能する [**Loaded**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.loaded) などのオブジェクト有効期間イベントを使います。 このとき便利なのが **Loaded** イベントです。その時点で UI は対話式操作に対応しているうえ、アニメーションが先頭で切れることもありません。UI の別の部分がまだ読み込んでいるためです。

この例では、[**PointerPressed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.uielement.pointerpressed) イベントを四角形に関連付けて、ユーザーが四角形をクリックしたときにアニメーションが開始されるようにしています。

```xaml
<Rectangle PointerPressed="Rectangle_Tapped"
  x:Name="MyAnimatedRectangle"
  Width="300" Height="200" Fill="Blue"/>
```

イベント ハンドラーは、[**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) の [**Begin**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.storyboard.begin) メソッドを使って **Storyboard** (アニメーション) を開始します。

```csharp
myStoryboard.Begin();
```

```cppwinrt
myStoryboard().Begin();
```

```cpp
myStoryboard->Begin();
```

```vb
myStoryBoard.Begin()
```

アニメーションが値を適用した後、他のロジックを実行する必要がある場合は、[**Completed**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.completed) イベントを処理できます。 また、プロパティ システム/アニメーション操作のトラブルシューティングには、[**GetAnimationBaseValue**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.dependencyobject.getanimationbasevalue) メソッドが役立つ場合があります。

> [!TIP]
> アプリ コードからアニメーションを開始するアプリのシナリオを実現するためにコードを記述している際に、アニメーションや切り替えが、独自の UI シナリオのためのアニメーション ライブラリに既に存在するかどうかをもう一度確かめたい場合があります。 ライブラリ アニメーションは使いやすいうえ、すべての Windows ランタイム アプリで UI エクスペリエンスの一貫性を高めるのに役立ちます。

 

### <a name="animations-for-visual-states"></a>表示状態用のアニメーション

コントロールの表示状態を定義するために使われる [**Storyboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard) の実行動作は、アプリがストーリーボードを直接実行する方法とは異なります。 XAML で表示状態の定義に適用されるとおり、**Storyboard** は上位の [**VisualState**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.VisualState) の要素であり、状態全体は [**VisualStateManager**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.visualstatemanager) API を使って制御されます。 含まれるアニメーションは、上位の [**VisualState** がコントロールによって使われるときにアニメーション値と **Timeline**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Timeline) プロパティに従って実行されます。 詳しくは、「[表示状態用にストーリーボードに設定されたアニメーション](https://docs.microsoft.com/previous-versions/windows/apps/jj819808(v=win.10))」をご覧ください。 表示状態については、明確な [**FillBehavior**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.media.animation.timeline.fillbehavior) は異なります。 表示状態が別の状態に変化すると、新しい表示状態でプロパティに新しいアニメーションを明示的に適用しない場合でも、前の表示状態とそのアニメーションによって適用されるすべてのプロパティの変更が取り消されます。

### <a name="storyboard-and-eventtrigger"></a>**Storyboard** と **EventTrigger**

XAML で完全に宣言できるアニメーションをある方法で開始できます。 しかし、この手法は幅広く使われていません。 これは、[**VisualStateManager**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.visualstatemanager) がサポートされる前の WPF と旧バージョンの Silverlight で使われていた構文です。 この [**EventTrigger**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.EventTrigger) 構文はインポートまたは互換性の理由から Windows ランタイム XAML でも機能するものの、[**FrameworkElement.Loaded**](https://docs.microsoft.com/uwp/api/windows.ui.xaml.frameworkelement.loaded) イベントに基づくトリガー動作でのみ機能します。他のイベントのトリガーを試みると、例外がスローされるか、コンパイルに失敗します。 詳しくは、「[**EventTrigger**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.EventTrigger)」または「[**BeginStoryboard**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.BeginStoryboard)」をご覧ください。

## <a name="animating-xaml-attached-properties"></a>XAML 添付プロパティのアニメーション化

一般的なシナリオではありませんが、アニメーション化された値を XAML 添付プロパティに適用できます。 添付プロパティの概要とその動作について詳しくは、「[添付プロパティの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/attached-properties-overview)」をご覧ください。 添付プロパティをターゲットとして設定するには、プロパティ名をかっこで囲む[プロパティ パス構文](https://docs.microsoft.com/windows/uwp/xaml-platform/property-path-syntax)が必要です。 個別の整数値を適用する [**ObjectAnimationUsingKeyFrames**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.ObjectAnimationUsingKeyFrames) を使って、[**Canvas.ZIndex**](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc190397(v%3Dvs.95)) などの組み込み添付プロパティをアニメーション化することができます。 ただし、Windows ランタイム XAML 実装の制限があるため、カスタム添付プロパティをアニメーション化することはできません。

## <a name="more-animation-types-and-next-steps-for-learning-about-animating-your-ui"></a>その他のアニメーションの種類、UI のアニメーション化に関する次の学習ステップ

ここまで、2 つの値の間をアニメーション化し、アニメーションの実行中に必要に応じて値を線形補間するカスタム アニメーションについて見てきました。 これらは、**From**/**To**/**By** アニメーションと呼ばれています。 これ以外に、開始から終了までの間の中間値を宣言できるタイプのアニメーションもあります。 これらは*キー フレーム アニメーション*と呼ばれます。 **From**/**To**/**By** アニメーションまたはキー フレーム アニメーションの補間ロジックを変更する方法もあります。 それには、イージング関数を適用する必要があります。 これらの概念について詳しくは、「[キーフレームとイージング関数のアニメーション](key-frame-and-easing-function-animations.md)」をご覧ください。

## <a name="related-topics"></a>関連トピック

* [プロパティ パスの構文](https://docs.microsoft.com/windows/uwp/xaml-platform/property-path-syntax)
* [依存関係プロパティの概要](https://docs.microsoft.com/windows/uwp/xaml-platform/dependency-properties-overview)
* [キー フレームと関数のアニメーションにイージング](key-frame-and-easing-function-animations.md)
* [表示状態のアニメーションを再検討](https://docs.microsoft.com/previous-versions/windows/apps/jj819808(v=win.10))
* [コントロール テンプレート](https://docs.microsoft.com/windows/uwp/controls-and-patterns/control-templates)
* [**ストーリー ボード**](https://docs.microsoft.com/uwp/api/Windows.UI.Xaml.Media.Animation.Storyboard)
* [**Storyboard.TargetProperty**](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/ms616983(v%3Dvs.95))
 

 




