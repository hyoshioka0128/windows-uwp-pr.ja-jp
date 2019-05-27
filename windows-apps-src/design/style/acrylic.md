---
description: 半透明テクスチャを作成するブラシの種類。
title: アクリル素材
template: detail.hbs
ms.date: 08/09/2017
ms.topic: article
keywords: windows 10, uwp
pm-contact: yulikl
design-contact: rybick
dev-contact: jevansa
doc-status: Published
ms.localizationpriority: medium
ms.openlocfilehash: 4731ab089189a8a03656281d1a9a6da6e4d24e89
ms.sourcegitcommit: f0f933d5cf0be734373a7b03e338e65000cc3d80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65984260"
---
# <a name="acrylic-material"></a><span data-ttu-id="377ac-104">アクリル素材</span><span class="sxs-lookup"><span data-stu-id="377ac-104">Acrylic material</span></span>

![ヒーロー イメージ](images/header-acrylic.svg)

<span data-ttu-id="377ac-106">アクリルは一種の[ブラシ](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Media.Brush)半透明テクスチャを作成します。</span><span class="sxs-lookup"><span data-stu-id="377ac-106">Acrylic is a type of [Brush](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Xaml.Media.Brush) that creates a translucent texture.</span></span> <span data-ttu-id="377ac-107">アクリルをアプリ サーフェスに適用すると、奥行きを加えたり、視覚的な階層を確立したりすることができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-107">You can apply acrylic to app surfaces to add depth and help establish a visual hierarchy.</span></span>  <!-- By allowing user-selected wallpaper or colors to shine through, acrylic keeps users in touch with the OS personalization they've chosen. -->

> <span data-ttu-id="377ac-108">**重要な API**:[AcrylicBrush クラス](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.media.acrylicbrush)、[プロパティをバック グラウンド](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.control.Background)</span><span class="sxs-lookup"><span data-stu-id="377ac-108">**Important APIs**: [AcrylicBrush class](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.media.acrylicbrush), [Background property](https://docs.microsoft.com/en-us/uwp/api/windows.ui.xaml.controls.control.Background)</span></span>

:::row:::
    :::column:::
        Acrylic in light theme
        ![Acrylic in light theme](images/Acrylic_LightTheme_Base.png)
    :::column-end:::
    :::column:::
        Acrylic in dark theme
        ![Acrylic in dark theme](images/Acrylic_DarkTheme_Base.png)
    :::column-end:::
:::row-end:::

## <a name="acrylic-and-the-fluent-design-system"></a><span data-ttu-id="377ac-109">アクリルと Fluent Design System</span><span class="sxs-lookup"><span data-stu-id="377ac-109">Acrylic and the Fluent Design System</span></span>

 <span data-ttu-id="377ac-110">Fluent Design System では、ライト、深度、モーション、マテリアル、スケールを取り入れた、モダンで目を引く UI を作成できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-110">The Fluent Design System helps you create modern, bold UI that incorporates light, depth, motion, material, and scale.</span></span> <span data-ttu-id="377ac-111">アクリルは、アプリに物理的なテクスチャ (マテリアル) と深度を追加する Fluent Design System コンポーネントです。</span><span class="sxs-lookup"><span data-stu-id="377ac-111">Acrylic is a Fluent Design System component that adds physical texture (material) and depth to your app.</span></span> <span data-ttu-id="377ac-112">詳しくは、[UWP 用の Fluent Design の概要に関するページ](/windows/apps/fluent-design-system)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="377ac-112">To learn more, see the [Fluent Design for UWP overview](/windows/apps/fluent-design-system).</span></span>

 ## <a name="video-summary"></a><span data-ttu-id="377ac-113">ビデオの概要</span><span class="sxs-lookup"><span data-stu-id="377ac-113">Video summary</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Windows/Windows-Developer-Day-Fall-Creators-Update/WinDev002/player]

## <a name="examples"></a><span data-ttu-id="377ac-114">例</span><span class="sxs-lookup"><span data-stu-id="377ac-114">Examples</span></span>

:::row:::
    :::column span:::
![一部の画像](images/XAML-controls-gallery-app-icon.png)
    :::column-end:::
    :::column span="2":::
<span data-ttu-id="377ac-116">**XAML コントロール ギャラリー**</span><span class="sxs-lookup"><span data-stu-id="377ac-116">**XAML Controls Gallery**</span></span><br>
<span data-ttu-id="377ac-117">XAML コントロール ギャラリー アプリをインストールした場合にクリックします<a href="xamlcontrolsgallery:/item/Acrylic">ここ</a>をアプリを開き、アクションのアクリルを参照してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-117">If you have the XAML Controls Gallery app installed, click <a href="xamlcontrolsgallery:/item/Acrylic">here</a> to open the app and see acrylic in action.</span></span>

<span data-ttu-id="377ac-118"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">XAML コントロール ギャラリー アプリを入手する (Microsoft Store)</a></span><span class="sxs-lookup"><span data-stu-id="377ac-118"><a href="https://www.microsoft.com/store/productId/9MSVH128X2ZT">Get the XAML Controls Gallery app (Microsoft Store)</a></span></span><br>
<span data-ttu-id="377ac-119"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">ソース コード (GitHub) を入手する</a></span><span class="sxs-lookup"><span data-stu-id="377ac-119"><a href="https://github.com/Microsoft/Xaml-Controls-Gallery">Get the source code (GitHub)</a></span></span>
    :::column-end:::
:::row-end:::

## <a name="acrylic-blend-types"></a><span data-ttu-id="377ac-120">アクリル ブレンドの種類</span><span class="sxs-lookup"><span data-stu-id="377ac-120">Acrylic blend types</span></span>
<span data-ttu-id="377ac-121">アクリルの最も注目すべき特徴は、その透明度です。</span><span class="sxs-lookup"><span data-stu-id="377ac-121">Acrylic's most noticeable characteristic is its transparency.</span></span> <span data-ttu-id="377ac-122">アクリル ブレンドの種類は 2 つあり、素材を通して何が表示されるかを変更することができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-122">There are two acrylic blend types that change what’s visible through the material:</span></span>
 - <span data-ttu-id="377ac-123">**背景アクリル**では、デスクトップの壁紙と現在アクティブになっているアプリの背後にある他のウィンドウが表示されます。これにより、アプリケーション ウィンドウの間に奥行きが出て、ユーザーが個人的に優先する画面を明示しておくことができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-123">**Background acrylic** reveals the desktop wallpaper and other windows that are behind the currently active app, adding depth between application windows while celebrating the user’s personalization preferences.</span></span>
 - <span data-ttu-id="377ac-124">**アプリ内アクリル**では、アプリ フレーム内に奥行きの感覚がもたらされ、フォーカスと階層の両方が提供されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-124">**In-app acrylic** adds a sense of depth within the app frame, providing both focus and hierarchy.</span></span>

 ![背景アクリル](images/BackgroundAcrylic_DarkTheme.png)

 ![アプリ内アクリル](images/AppAcrylic_DarkTheme.png)

 <span data-ttu-id="377ac-127">レイヤーの複数のアクリル サーフェスで注意が必要です: バック グラウンド アクリルの複数のレイヤーが注意をそらす光学フィルターを作成できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-127">Layer multiple acrylic surfaces with caution: multiple layers of background acrylic can create distracting optical illusions.</span></span>

## <a name="when-to-use-acrylic"></a><span data-ttu-id="377ac-128">アクリルを使用する状況</span><span class="sxs-lookup"><span data-stu-id="377ac-128">When to use acrylic</span></span>

* <span data-ttu-id="377ac-129">重複するコンテンツがスクロールまたは操作したときに画面上など、UI をサポートするためには、アプリ内のアクリルを使用します。</span><span class="sxs-lookup"><span data-stu-id="377ac-129">Use in-app acrylic for supporting UI, such as on surfaces that may overlap content when scrolled or interacted with.</span></span>
* <span data-ttu-id="377ac-130">コンテキスト メニュー、フライアウト、光 dismissable UI などの一時的な UI 要素の背景のアクリルを使用します。</span><span class="sxs-lookup"><span data-stu-id="377ac-130">Use background acrylic for transient UI elements, such as context menus, flyouts, and light-dismissable UI.</span></span><br /><span data-ttu-id="377ac-131">一時的なシナリオでアクリルを使用すると、一時的な UI をトリガーするコンテンツで視覚的な関係を維持できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-131">Using Acrylic in transient scenarios helps maintain a visual relationship with the content that triggered the transient UI.</span></span>

<span data-ttu-id="377ac-132">ナビゲーション画面をアプリ内のアクリルを使用している場合は、アプリでフローを向上させるためにアクリル ペインの下にコンテンツを拡張することを検討します。</span><span class="sxs-lookup"><span data-stu-id="377ac-132">If you are using in-app acrylic on navigation surfaces, consider extending content beneath the acrylic pane to improve the flow on your app.</span></span> <span data-ttu-id="377ac-133">NavigationView を使用してはこの処理を自動実行します。</span><span class="sxs-lookup"><span data-stu-id="377ac-133">Using NavigationView will do this for you automatically.</span></span> <span data-ttu-id="377ac-134">ただし、ストライピング効果の作成を回避するため、アクリル - エッジでの複数の部分を配置しないでくださいこのことができます、2 つのぼかしサーフェスの間で不要な継ぎ目を作成します。</span><span class="sxs-lookup"><span data-stu-id="377ac-134">However, to avoid creating a striping effect, try not to place multiple pieces of acrylic edge-to-edge - this can create an unwanted seam between the two blurred surfaces.</span></span> <span data-ttu-id="377ac-135">アクリルは、設計を visual 調和を実現するツールですが、適切に使用されることが余計。</span><span class="sxs-lookup"><span data-stu-id="377ac-135">Acrylic is a tool to bring visual harmony to your designs, but when used incorrectly, can result in visual noise.</span></span>

<span data-ttu-id="377ac-136">アプリにアクリルを組み込むことが最善の方法を次の使用パターンを検討してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-136">Consider the following usage patterns to decide how best to incorporate acrylic into your app:</span></span>

### <a name="horizontal-navigation-or-commanding"></a><span data-ttu-id="377ac-137">水平方向のナビゲーション ウィンドウまたはコマンド実行</span><span class="sxs-lookup"><span data-stu-id="377ac-137">Horizontal navigation or commanding</span></span>

<span data-ttu-id="377ac-138">NavigationView を利用できるように、アプリは、アクリルを追加する場合は、比較的半透明のアクリルを使用して、60% 濃淡の不透明度をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-138">If your app is not able to leverage NavigationView and you plan on adding acrylic on your own, we recommend using relatively translucent acrylic with 60% tint opacity.</span></span>
 - <span data-ttu-id="377ac-139">ウィンドウが他のアプリ コンテンツ上でオーバーレイとして開くときは、[60% のアプリ内アクリル](#acrylic-theme-resources)にする必要があります</span><span class="sxs-lookup"><span data-stu-id="377ac-139">When the pane opens as an overlay above other app content, this should be [60% in-app acrylic](#acrylic-theme-resources)</span></span>

![アプリで水平方向のコマンドを使用してマップ アプリ](images/Maps_In_App_Acrylic_1.png)

<span data-ttu-id="377ac-141">さらに、上部にある、コンテンツの拡張またはアクリル、下のスクロールを持つは、アプリ、さらに魅力的なシームレスなエクスペリエンスです。</span><span class="sxs-lookup"><span data-stu-id="377ac-141">In addition, having your content extend or scroll under the acrylic at the top will give your app a more immersive and seamless experience.</span></span>

### <a name="vertical-panes"></a><span data-ttu-id="377ac-142">垂直方向のウィンドウ</span><span class="sxs-lookup"><span data-stu-id="377ac-142">Vertical Panes</span></span>

<span data-ttu-id="377ac-143">垂直方向のウィンドウまたはヘルプ、アプリのコンテンツのセクションで、サーフェスでは、不透明な背景を使用して、アクリルではなくをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-143">For vertical panes or surfaces that help section off content of your app, we recommend you use an opaque background instead of acrylic.</span></span> <span data-ttu-id="377ac-144">NavigationView の内などの場合は、垂直方向のウィンドウ コンテンツの上に開くには、 **Compact**または**最小限**モードをお勧め、ユーザーがあるこのウィンドウを開いているときに、ページのコンテキストを維持するためにアプリ内のアクリルを使用します。</span><span class="sxs-lookup"><span data-stu-id="377ac-144">If your vertical panes open on top of content, like in NavigationView's **Compact** or **Minimal** modes, we suggest you use in-app acrylic to help maintain the page's context when the user has this pane open.</span></span>

### <a name="transient-surfaces"></a><span data-ttu-id="377ac-145">一時的なサーフェイス</span><span class="sxs-lookup"><span data-stu-id="377ac-145">Transient surfaces</span></span>

<span data-ttu-id="377ac-146">アプリのメニュー フライアウト、非モーダル ポップアップでは、ペイン の light 無視またはバック グラウンドのアクリルを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-146">For apps with menu flyouts, non-modal popups, or light-dismiss panes, it is recommended to use background acrylic.</span></span>

![情報のポップアップを使用してメール アプリのパターン](images/Mail_TransientContextMenu.png)

<span data-ttu-id="377ac-148">コントロールの多くは、既定でアクリルを使用します。</span><span class="sxs-lookup"><span data-stu-id="377ac-148">Many of our controls will use acrylic by default.</span></span> <span data-ttu-id="377ac-149">[MenuFlyouts](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/menus)、 [AutoSuggestBox](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/auto-suggest-box)、 [ComboBox](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.combobox)およびのようなコントロールでは、ポップアップをライト-消去したり、すべて使用する一時的なアクリルときに呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-149">[MenuFlyouts](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/menus), [AutoSuggestBox](https://docs.microsoft.com/windows/uwp/design/controls-and-patterns/auto-suggest-box), [ComboBox](https://docs.microsoft.com/uwp/api/windows.ui.xaml.controls.combobox) and similar controls with light-dismiss popups will all use the transient acrylic when they are invoked.</span></span>

> [!Note]
> <span data-ttu-id="377ac-150">GPU の負荷がデバイスの電力消費量を増やすことができますし、バッテリの寿命を短縮するにはアクリル サーフェスをレンダリングします。</span><span class="sxs-lookup"><span data-stu-id="377ac-150">Rendering acrylic surfaces is GPU-intensive, which can increase device power consumption and shorten battery life.</span></span> <span data-ttu-id="377ac-151">Acrylic 効果は、選択した場合デバイスがバッテリー セーバー モードに入るし、ユーザーには、すべてのアプリのアクリル効果が無効にすることができます自動的に無効にします。</span><span class="sxs-lookup"><span data-stu-id="377ac-151">Acrylic effects are automatically disabled when devices enter Battery Saver mode, and users can disable acrylic effects for all apps, if they choose.</span></span>

## <a name="usability-and-adaptability"></a><span data-ttu-id="377ac-152">使いやすさと適応性</span><span class="sxs-lookup"><span data-stu-id="377ac-152">Usability and adaptability</span></span>
<span data-ttu-id="377ac-153">アクリルの外観は、さまざまなデバイスやコンテキストに合うように自動的に対応します。</span><span class="sxs-lookup"><span data-stu-id="377ac-153">Acrylic automatically adapts its appearance for a wide variety of devices and contexts.</span></span>

<span data-ttu-id="377ac-154">ハイ コントラスト モードでは、ユーザーが選んだ見慣れた背景色が、アクリルの代わりに引き続き表示されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-154">In High Contrast mode, users continue to see the familiar background color of their choosing in place of acrylic.</span></span> <span data-ttu-id="377ac-155">さらに、バック グラウンド アクリルとアプリ内のアクリルの両方は、純色として表示されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-155">In addition, both background acrylic and in-app acrylic appear as a solid color:</span></span>
 - <span data-ttu-id="377ac-156">ユーザーが設定での透過性をオフにする場合 > 個人用設定 > 色</span><span class="sxs-lookup"><span data-stu-id="377ac-156">When the user turns off transparency in Settings > Personalization > Color</span></span>
 - <span data-ttu-id="377ac-157">バッテリー セーバー モードがアクティブにするタイミング</span><span class="sxs-lookup"><span data-stu-id="377ac-157">When Battery Saver mode is activated</span></span>
 - <span data-ttu-id="377ac-158">アプリがローエンド ハードウェアで実行されている場合</span><span class="sxs-lookup"><span data-stu-id="377ac-158">When the app runs on low-end hardware</span></span>

<span data-ttu-id="377ac-159">さらに、バック グラウンド アクリルのみは置換の透明度とテクスチャを純色。</span><span class="sxs-lookup"><span data-stu-id="377ac-159">In addition, only background acrylic will replace its translucency and texture with a solid color:</span></span>
 - <span data-ttu-id="377ac-160">アプリ ウィンドウがデスクトップで非アクティブ化されている場合</span><span class="sxs-lookup"><span data-stu-id="377ac-160">When an app window on desktop deactivates</span></span>
 - <span data-ttu-id="377ac-161">UWP アプリが、電話、Xbox、HoloLens、またはタブレット モードで実行されている場合</span><span class="sxs-lookup"><span data-stu-id="377ac-161">When the UWP app is running on phone, Xbox, HoloLens or tablet mode</span></span>

### <a name="legibility-considerations"></a><span data-ttu-id="377ac-162">見やすくするための考慮事項</span><span class="sxs-lookup"><span data-stu-id="377ac-162">Legibility considerations</span></span>
<span data-ttu-id="377ac-163">アプリがユーザーに表示するすべてのテキストでは、[コントラスト比を適切な値にする](../accessibility/accessible-text-requirements.md)ことが重要です。</span><span class="sxs-lookup"><span data-stu-id="377ac-163">It’s important to ensure that any text your app presents to users [meets contrast ratios](../accessibility/accessible-text-requirements.md).</span></span> <span data-ttu-id="377ac-164">ハイカラーの黒や白のテキスト、またはミディアムカラーの灰色のテキストがアクリル上で適切なコントラスト比になるように、アクリルのレシピは最適化されています。</span><span class="sxs-lookup"><span data-stu-id="377ac-164">We’ve optimized the acrylic recipe so that high-color black, white or even medium-color gray text meets contrast ratios on top of acrylic.</span></span> <span data-ttu-id="377ac-165">プラットフォームによって提供されるテーマ リソースは、既定で、濃淡の色のコントラストが 80% の不透明度に設定されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-165">The theme resources provided by the platform default to contrasting tint colors at 80% opacity.</span></span> <span data-ttu-id="377ac-166">ハイカラーの本文テキストをアクリル上に配置する場合、濃淡の不透明度を下げて、見やすさを維持することができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-166">When placing high-color body text on acrylic, you can reduce tint opacity while maintaining legibility.</span></span> <span data-ttu-id="377ac-167">ダーク モードでは濃淡の不透明度を 70% にすることができ、ライト モードのアクリルではコントラスト比を 50% の不透明度に合わせることができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-167">In dark mode, tint opacity can be 70%, while light mode acrylic will meet contrast ratios at 50% opacity.</span></span>

<span data-ttu-id="377ac-168">アクリル サーフェスの上にアクセント カラーのテキストを配置することはお勧めしません。これは、これらの組み合わせが、15 ピクセルのフォント サイズでのコントラスト比の最小要件を満たさない可能性があるためです。</span><span class="sxs-lookup"><span data-stu-id="377ac-168">We don't recommend placing accent-colored text on your acrylic surfaces because these combinations are likely to not pass minimum contrast ratio requirements at 15px font size.</span></span> <span data-ttu-id="377ac-169">[ハイパーリンク](../controls-and-patterns/hyperlinks.md)はアクリル要素上には配置しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="377ac-169">Try to avoid placing [hyperlinks](../controls-and-patterns/hyperlinks.md) over acrylic elements.</span></span> <span data-ttu-id="377ac-170">また、アクリルの濃淡の色や透明度のレベルを、テーマ リソースによって提供されるプラットフォームの既定値以外にカスタマイズする場合は、見やすさへの影響を考慮してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-170">Also, if you choose to customize the acrylic tint color or opacity level outside of the platform defaults provided by the theme resource, keep the impact on legibility in mind.</span></span>

## <a name="acrylic-theme-resources"></a><span data-ttu-id="377ac-171">アクリルのテーマ リソース</span><span class="sxs-lookup"><span data-stu-id="377ac-171">Acrylic theme resources</span></span>
<span data-ttu-id="377ac-172">新しい XAML AcrylicBrush テーマ リソースや定義済みの AcrylicBrush テーマ リソースを使用して、アクリルをアプリのサーフェスに簡単に適用できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-172">You can easily apply acrylic to your app’s surfaces using the new XAML AcrylicBrush or predefined AcrylicBrush theme resources.</span></span> <span data-ttu-id="377ac-173">まず、アプリ内アクリルまたは背景アクリルのどちらを使用するかを決める必要があります。</span><span class="sxs-lookup"><span data-stu-id="377ac-173">First, you’ll need to decide whether to use in-app or background acrylic.</span></span> <span data-ttu-id="377ac-174">この記事で推奨事項として既に説明した一般的なアプリのパターンを確認してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-174">Be sure to review common app patterns described earlier in this article for recommendations.</span></span>

<span data-ttu-id="377ac-175">背景アクリルやアプリ内アクリルの両方を対象としたブラシのテーマ リソースのコレクションが作成されています。これらのリソースでは、アプリのテーマが重視され、必要に応じて、単色にフォール バックします。</span><span class="sxs-lookup"><span data-stu-id="377ac-175">We’ve created a collection of brush theme resources for both background and in-app acrylic types that respect the app’s theme and fall back to solid colors as needed.</span></span> <span data-ttu-id="377ac-176">*AcrylicWindow* という名前のリソースは背景アクリルを表し、*AcrylicElement* はアプリ内アクリルを表します。</span><span class="sxs-lookup"><span data-stu-id="377ac-176">Resources named *AcrylicWindow* represent background acrylic, while *AcrylicElement* refers to in-app acrylic.</span></span>

<table>
    <tr>
        <th align="center"><span data-ttu-id="377ac-177">リソース キー</span><span class="sxs-lookup"><span data-stu-id="377ac-177">Resource key</span></span></th>
        <th align="center"><span data-ttu-id="377ac-178">濃淡の不透明度</span><span class="sxs-lookup"><span data-stu-id="377ac-178">Tint opacity</span></span></th>
        <th align="center"><span data-ttu-id="377ac-179"><a href="color.md">フォールバックの色</a> </span><span class="sxs-lookup"><span data-stu-id="377ac-179"><a href="color.md">Fallback color</a> </span></span></th>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-180">SystemControlAcrylicWindowBrush、SystemControlAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-180">SystemControlAcrylicWindowBrush, SystemControlAcrylicElementBrush</span></span> <br/> <span data-ttu-id="377ac-181">SystemControlChromeLowAcrylicWindowBrush、SystemControlChromeLowAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-181">SystemControlChromeLowAcrylicWindowBrush, SystemControlChromeLowAcrylicElementBrush</span></span> <br/> <span data-ttu-id="377ac-182">SystemControlBaseHighAcrylicWindowBrush、SystemControlBaseHighAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-182">SystemControlBaseHighAcrylicWindowBrush, SystemControlBaseHighAcrylicElementBrush</span></span> <br/> <span data-ttu-id="377ac-183">SystemControlBaseLowAcrylicWindowBrush、SystemControlBaseLowAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-183">SystemControlBaseLowAcrylicWindowBrush, SystemControlBaseLowAcrylicElementBrush</span></span> <br/> <span data-ttu-id="377ac-184">SystemControlAltHighAcrylicWindowBrush、SystemControlAltHighAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-184">SystemControlAltHighAcrylicWindowBrush, SystemControlAltHighAcrylicElementBrush</span></span> <br/> <span data-ttu-id="377ac-185">SystemControlAltLowAcrylicWindowBrush、SystemControlAltLowAcrylicElementBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-185">SystemControlAltLowAcrylicWindowBrush, SystemControlAltLowAcrylicElementBrush</span></span> </td>
        <td align="center"> <span data-ttu-id="377ac-186">80%</span><span class="sxs-lookup"><span data-stu-id="377ac-186">80%</span></span> </td>
        <td> <span data-ttu-id="377ac-187">ChromeMedium</span><span class="sxs-lookup"><span data-stu-id="377ac-187">ChromeMedium</span></span> <br/> <span data-ttu-id="377ac-188">ChromeLow</span><span class="sxs-lookup"><span data-stu-id="377ac-188">ChromeLow</span></span> <br/><br/> <span data-ttu-id="377ac-189">BaseHigh</span><span class="sxs-lookup"><span data-stu-id="377ac-189">BaseHigh</span></span> <br/><br/> <span data-ttu-id="377ac-190">BaseLow</span><span class="sxs-lookup"><span data-stu-id="377ac-190">BaseLow</span></span> <br/><br/> <span data-ttu-id="377ac-191">AltHigh</span><span class="sxs-lookup"><span data-stu-id="377ac-191">AltHigh</span></span> <br/><br/> <span data-ttu-id="377ac-192">AltLow</span><span class="sxs-lookup"><span data-stu-id="377ac-192">AltLow</span></span> </td>
    </tr>
    </tr>
        <td> <span data-ttu-id="377ac-193"><b>推奨される使用法:</b>これらは、さまざまな使用法で問題なく動作する汎用のアクリル リソースです。</span><span class="sxs-lookup"><span data-stu-id="377ac-193"><b>Recommended usage:</b> These are general-purpose acrylic resources that work well in a wide variety of usages.</span></span> <span data-ttu-id="377ac-194">アプリで使用するセカンダリ テキストの色が AltMedium で、そのサイズが 18 ピクセルよりも小さい場合は、<a href="../accessibility/accessible-text-requirements.md">コントラスト比の要件を満たすように</a>、80% のアクリル リソースをテキストの背景に配置してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-194">If your app uses secondary text of AltMedium color with text size smaller than 18px, place an 80% acrylic resource behind the text to <a href="../accessibility/accessible-text-requirements.md">meet contrast ratio requirements</a>.</span></span> </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-195">SystemControlAcrylicWindowMediumHighBrush、SystemControlAcrylicElementMediumHighBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-195">SystemControlAcrylicWindowMediumHighBrush, SystemControlAcrylicElementMediumHighBrush</span></span> <br/> <span data-ttu-id="377ac-196">SystemControlBaseHighAcrylicWindowMediumHighBrush、SystemControlBaseHighAcrylicElementMediumHighBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-196">SystemControlBaseHighAcrylicWindowMediumHighBrush, SystemControlBaseHighAcrylicElementMediumHighBrush</span></span> </td>
        <td align="center"> <span data-ttu-id="377ac-197">70%</span><span class="sxs-lookup"><span data-stu-id="377ac-197">70%</span></span> </td>
        <td> <span data-ttu-id="377ac-198">ChromeMedium</span><span class="sxs-lookup"><span data-stu-id="377ac-198">ChromeMedium</span></span> <br/><br/> <span data-ttu-id="377ac-199">BaseHigh</span><span class="sxs-lookup"><span data-stu-id="377ac-199">BaseHigh</span></span> </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-200"><b>推奨される使用法:</b>アプリでは、18 px 以上のテキスト サイズを AltMedium 色のセカンダリ テキストを使用している場合は、これら複数の半透明 70% のテキストの背後にあるアクリル リソースを配置できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-200"><b>Recommended usage:</b> If your app uses secondary text of AltMedium color with a text size of 18px or larger, you can place these more translucent 70% acrylic resources behind the text.</span></span> <span data-ttu-id="377ac-201">これらのリソースは、アプリの最上部にある水平方向のナビゲーション領域やコマンド実行領域で使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-201">We recommend using these resources in your app's top horizontal navigation and commanding areas.</span></span>  </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-202">SystemControlChromeHighAcrylicWindowMediumBrush、SystemControlChromeHighAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-202">SystemControlChromeHighAcrylicWindowMediumBrush, SystemControlChromeHighAcrylicElementMediumBrush</span></span> <br/> <span data-ttu-id="377ac-203">SystemControlChromeMediumAcrylicWindowMediumBrush、SystemControlChromeMediumAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-203">SystemControlChromeMediumAcrylicWindowMediumBrush, SystemControlChromeMediumAcrylicElementMediumBrush</span></span> <br/> <span data-ttu-id="377ac-204">SystemControlChromeMediumLowAcrylicWindowMediumBrush、SystemControlChromeMediumLowAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-204">SystemControlChromeMediumLowAcrylicWindowMediumBrush, SystemControlChromeMediumLowAcrylicElementMediumBrush</span></span> <br/> <span data-ttu-id="377ac-205">SystemControlBaseHighAcrylicWindowMediumBrush、SystemControlBaseHighAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-205">SystemControlBaseHighAcrylicWindowMediumBrush, SystemControlBaseHighAcrylicElementMediumBrush</span></span> <br/> <span data-ttu-id="377ac-206">SystemControlBaseMediumLowAcrylicWindowMediumBrush、SystemControlBaseMediumLowAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-206">SystemControlBaseMediumLowAcrylicWindowMediumBrush, SystemControlBaseMediumLowAcrylicElementMediumBrush</span></span> <br/> <span data-ttu-id="377ac-207">SystemControlAltMediumLowAcrylicWindowMediumBrush、SystemControlAltMediumLowAcrylicElementMediumBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-207">SystemControlAltMediumLowAcrylicWindowMediumBrush, SystemControlAltMediumLowAcrylicElementMediumBrush</span></span>  </td>
        <td align="center"> <span data-ttu-id="377ac-208">60%</span><span class="sxs-lookup"><span data-stu-id="377ac-208">60%</span></span> </td>
        <td> <span data-ttu-id="377ac-209">ChromeHigh</span><span class="sxs-lookup"><span data-stu-id="377ac-209">ChromeHigh</span></span> <br/><br/> <span data-ttu-id="377ac-210">ChromeMedium</span><span class="sxs-lookup"><span data-stu-id="377ac-210">ChromeMedium</span></span> <br/><br/> <span data-ttu-id="377ac-211">ChromeMediumLow</span><span class="sxs-lookup"><span data-stu-id="377ac-211">ChromeMediumLow</span></span> <br/><br/> <span data-ttu-id="377ac-212">BaseHigh</span><span class="sxs-lookup"><span data-stu-id="377ac-212">BaseHigh</span></span> <br/><br/> <span data-ttu-id="377ac-213">BaseLow</span><span class="sxs-lookup"><span data-stu-id="377ac-213">BaseLow</span></span> <br/><br/> <span data-ttu-id="377ac-214">AltMediumLow</span><span class="sxs-lookup"><span data-stu-id="377ac-214">AltMediumLow</span></span> </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-215"><b>推奨される使用法:</b>AltHigh 色の主要なテキストのみアクリルの上に配置するときに、アプリは、これらの 60% リソースを利用できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-215"><b>Recommended usage:</b> When placing only primary text of AltHigh color over acrylic, your app can utilize these 60% resources.</span></span> <span data-ttu-id="377ac-216">アプリの<a href="../controls-and-patterns/navigationview.md">垂直方向のナビゲーション ウィンドウ</a> (ハンバーガー メニュー) を描画するときは、60% のアクリルを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-216">We recommend painting your app's <a href="../controls-and-patterns/navigationview.md">vertical navigation pane</a>, i.e. hamburger menu, with 60% acrylic.</span></span> </td>
    </tr>
</table>

<span data-ttu-id="377ac-217">中間色のアクリルに加え、ユーザーが指定したアクセント カラーを使用してアクリルに濃淡を付けるリソースも追加しました。</span><span class="sxs-lookup"><span data-stu-id="377ac-217">In addition to color-neutral acrylic, we've also added resources that tint acrylic using the user-specified accent color.</span></span> <span data-ttu-id="377ac-218">色が付いたアクリルは慎重に使用してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-218">We recommend using colored acrylic sparingly.</span></span> <span data-ttu-id="377ac-219">提供されている dark1 と dark2 のバリアントを使用する場合、濃色テーマのテキストの色と調和するように、白または明るい色のテキストをこれらのリソース上に配置してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-219">For the dark1 and dark2 variants provided, place white or light-colored text consistent with dark theme text color over these resources.</span></span>
<table>
    <tr>
        <th align="center"><span data-ttu-id="377ac-220">リソース キー</span><span class="sxs-lookup"><span data-stu-id="377ac-220">Resource key</span></span></th>
        <th align="center"><span data-ttu-id="377ac-221">濃淡の不透明度</span><span class="sxs-lookup"><span data-stu-id="377ac-221">Tint opacity</span></span></th>
        <th align="center"><span data-ttu-id="377ac-222"><a href="color.md">代替の濃淡の色</a> </span><span class="sxs-lookup"><span data-stu-id="377ac-222"><a href="color.md">Tint and Fallback colors</a> </span></span></th>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-223">SystemControlAccentAcrylicWindowAccentMediumHighBrush、SystemControlAccentAcrylicElementAccentMediumHighBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-223">SystemControlAccentAcrylicWindowAccentMediumHighBrush, SystemControlAccentAcrylicElementAccentMediumHighBrush</span></span>  </td>
        <td align="center"> <span data-ttu-id="377ac-224">70%</span><span class="sxs-lookup"><span data-stu-id="377ac-224">70%</span></span> </td>
        <td> <span data-ttu-id="377ac-225">SystemAccentColor</span><span class="sxs-lookup"><span data-stu-id="377ac-225">SystemAccentColor</span></span> </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-226">SystemControlAccentDark1AcrylicWindowAccentDark1Brush、SystemControlAccentDark1AcrylicElementAccentDark1Brush</span><span class="sxs-lookup"><span data-stu-id="377ac-226">SystemControlAccentDark1AcrylicWindowAccentDark1Brush, SystemControlAccentDark1AcrylicElementAccentDark1Brush</span></span>  </td>
        <td align="center"> <span data-ttu-id="377ac-227">80%</span><span class="sxs-lookup"><span data-stu-id="377ac-227">80%</span></span> </td>
        <td> <span data-ttu-id="377ac-228">SystemAccentColorDark1</span><span class="sxs-lookup"><span data-stu-id="377ac-228">SystemAccentColorDark1</span></span> </td>
    </tr>
    <tr>
        <td> <span data-ttu-id="377ac-229">SystemControlAccentDark2AcrylicWindowAccentDark2MediumHighBrush、SystemControlAccentDark2AcrylicElementAccentDark2MediumHighBrush</span><span class="sxs-lookup"><span data-stu-id="377ac-229">SystemControlAccentDark2AcrylicWindowAccentDark2MediumHighBrush, SystemControlAccentDark2AcrylicElementAccentDark2MediumHighBrush</span></span>  </td>
        <td align="center"> <span data-ttu-id="377ac-230">70%</span><span class="sxs-lookup"><span data-stu-id="377ac-230">70%</span></span> </td>
        <td> <span data-ttu-id="377ac-231">SystemAccentColorDark2</span><span class="sxs-lookup"><span data-stu-id="377ac-231">SystemAccentColorDark2</span></span> </td>
    </tr>
</table>


<span data-ttu-id="377ac-232">特定のサーフェスを塗りつぶすには、上記のテーマ リソースのいずれかを、他のブラシ リソースを適用する要素の背景に適用します。</span><span class="sxs-lookup"><span data-stu-id="377ac-232">To paint a specific surface, apply one of the above theme resources to element backgrounds just as you would apply any other brush resource.</span></span>

```xaml
<Grid Background="{ThemeResource SystemControlAcrylicElementBrush}">
```

## <a name="custom-acrylic-brush"></a><span data-ttu-id="377ac-233">カスタム アクリル ブラシ</span><span class="sxs-lookup"><span data-stu-id="377ac-233">Custom acrylic brush</span></span>
<span data-ttu-id="377ac-234">色の濃淡をアプリのアクリルに加えて、ブランドを表示したり、ページ上にある他の要素と視覚的にバランスをとったりすることができます。</span><span class="sxs-lookup"><span data-stu-id="377ac-234">You may choose to add a color tint to your app’s acrylic to show branding or provide visual balance with other elements on the page.</span></span> <span data-ttu-id="377ac-235">グレースケール以外の色を表示するには、次のプロパティを使って、独自のアクリル ブラシを定義する必要があります。</span><span class="sxs-lookup"><span data-stu-id="377ac-235">To show color rather than greyscale, you’ll need to define your own acrylic brushes using the following properties.</span></span>
 - <span data-ttu-id="377ac-236">**TintColor**: 色/濃淡のオーバーレイ レイヤーです。</span><span class="sxs-lookup"><span data-stu-id="377ac-236">**TintColor**: the color/tint overlay layer.</span></span> <span data-ttu-id="377ac-237">RGB の色の値とアルファ チャネルの不透明度の両方を指定することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-237">Consider specifying both the RGB color value and alpha channel opacity.</span></span>
 - <span data-ttu-id="377ac-238">**TintOpacity**: 濃淡レイヤーの不透明度です。</span><span class="sxs-lookup"><span data-stu-id="377ac-238">**TintOpacity**: the opacity of the tint layer.</span></span> <span data-ttu-id="377ac-239">お勧め 80% の不透明度を出発点として他の translucencies で魅力的なさまざまな色に見える場合があります。</span><span class="sxs-lookup"><span data-stu-id="377ac-239">We recommend 80% opacity as a starting point, although different colors may look more compelling at other translucencies.</span></span>
 - <span data-ttu-id="377ac-240">**TintLuminosityOpacity**: がバック グラウンドからアクリル画面によって許可される彩度の量を制御します。</span><span class="sxs-lookup"><span data-stu-id="377ac-240">**TintLuminosityOpacity**: controls the amount of saturation that is allowed through the acrylic surface from the background.</span></span>
 - <span data-ttu-id="377ac-241">**BackgroundSource**: 背景アクリルまたはアプリ内アクリルのどちらを使用するかを指定するフラグです。</span><span class="sxs-lookup"><span data-stu-id="377ac-241">**BackgroundSource**: the flag to specify whether you want background or in-app acrylic.</span></span>
 - <span data-ttu-id="377ac-242">**FallbackColor**: 純色をバッテリー セーバーのアクリルを置換します。</span><span class="sxs-lookup"><span data-stu-id="377ac-242">**FallbackColor**: the solid color that replaces acrylic in Battery Saver.</span></span> <span data-ttu-id="377ac-243">背景アクリルでは、フォールバックの色は、アプリが作業中のデスクトップ ウィンドウにない場合、またはアプリが電話や Xbox 上で実行されている場合にもアクリルと置き換わります。</span><span class="sxs-lookup"><span data-stu-id="377ac-243">For background acrylic, fallback color also replaces acrylic when your app isn’t in the active desktop window or when the app is running on phone and Xbox.</span></span>

![淡色テーマのアクリルの見本](images/CustomAcrylic_Swatches_LightTheme.png)

![濃色テーマのアクリルの見本](images/CustomAcrylic_Swatches_DarkTheme.png)

![濃淡の不透明度と比較して光度 opactity](images/LuminosityVersusTint.png)

<span data-ttu-id="377ac-247">アクリル ブラシを追加するには、濃色テーマ、淡色テーマ、ハイ コントラスト テーマの 3 つのリソースを定義します。</span><span class="sxs-lookup"><span data-stu-id="377ac-247">To add an acrylic brush, define the three resources for dark, light and high contrast themes.</span></span> <span data-ttu-id="377ac-248">ハイ コントラストでは、濃色/淡色の AcrylicBrush と同じ x:Key で SolidColorBrush を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="377ac-248">Note that in high contrast, we recommend using a SolidColorBrush with the same x:Key as the dark/light AcrylicBrush.</span></span>

> [!Note] 
> <span data-ttu-id="377ac-249">TintLuminosityOpacity 値を指定しない場合、システムは TintColor と TintOpacity に基づき、その値を自動的に調整します。</span><span class="sxs-lookup"><span data-stu-id="377ac-249">If you don't specify a TintLuminosityOpacity value, the system will automatically adjust its value based on your TintColor and TintOpacity.</span></span>

```xaml
<ResourceDictionary.ThemeDictionaries>
    <ResourceDictionary x:Key="Default">
        <AcrylicBrush x:Key="MyAcrylicBrush"
            BackgroundSource="HostBackdrop"
            TintColor="#FFFF0000"
            TintOpacity="0.8"
            TintLuminosityOpacity="0.5"
            FallbackColor="#FF7F0000"/>
    </ResourceDictionary>

    <ResourceDictionary x:Key="HighContrast">
        <SolidColorBrush x:Key="MyAcrylicBrush"
            Color="{ThemeResource SystemColorWindowColor}"/>
    </ResourceDictionary>

    <ResourceDictionary x:Key="Light">
        <AcrylicBrush x:Key="MyAcrylicBrush"
            BackgroundSource="HostBackdrop"
            TintColor="#FFFF0000"
            TintOpacity="0.8"
            TintLuminosityOpacity="0.5"
            FallbackColor="#FFFF7F7F"/>
    </ResourceDictionary>
</ResourceDictionary.ThemeDictionaries>
```

<span data-ttu-id="377ac-250">次のサンプルは、コードで AcrylicBrush を宣言する方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="377ac-250">The following sample shows how to declare AcrylicBrush in code.</span></span> <span data-ttu-id="377ac-251">アプリが複数の OS ターゲットをサポートする場合は、この API がユーザーのコンピューターで利用できることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-251">If your app supports multiple OS targets, be sure to check that this API is available on the user’s machine.</span></span>

```csharp
if (Windows.Foundation.Metadata.ApiInformation.IsTypePresent("Windows.UI.Xaml.Media.XamlCompositionBrushBase"))
{
    Windows.UI.Xaml.Media.AcrylicBrush myBrush = new Windows.UI.Xaml.Media.AcrylicBrush();
    myBrush.BackgroundSource = Windows.UI.Xaml.Media.AcrylicBackgroundSource.HostBackdrop;
    myBrush.TintColor = Color.FromArgb(255, 202, 24, 37);
    myBrush.FallbackColor = Color.FromArgb(255, 202, 24, 37);
    myBrush.TintOpacity = 0.6;

    grid.Fill = myBrush;
}
else
{
    SolidColorBrush myBrush = new SolidColorBrush(Color.FromArgb(255, 202, 24, 37));

    grid.Fill = myBrush;
}
```

## <a name="extend-acrylic-into-the-title-bar"></a><span data-ttu-id="377ac-252">アクリルをタイトル バーに拡張する</span><span class="sxs-lookup"><span data-stu-id="377ac-252">Extend acrylic into the title bar</span></span>

<span data-ttu-id="377ac-253">アプリのウィンドウを滑らかな外観にするには、タイトル バー領域にアクリルを使います。</span><span class="sxs-lookup"><span data-stu-id="377ac-253">To give your app's window a seamless look, you can use acrylic in the title bar area.</span></span> <span data-ttu-id="377ac-254">この例では、[ApplicationViewTitleBar](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar) オブジェクトの [ButtonBackgroundColor](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar.ButtonBackgroundColor) および [ButtonInactiveBackgroundColor](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar.ButtonInactiveBackgroundColor) プロパティを [Colors.Transparent](https://docs.microsoft.com/uwp/api/Windows.UI.Colors.Transparent) に設定することで、アクリルをタイトル バーに拡張します。</span><span class="sxs-lookup"><span data-stu-id="377ac-254">This example extends acrylic into the title bar by setting the [ApplicationViewTitleBar](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar) object's [ButtonBackgroundColor](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar.ButtonBackgroundColor) and [ButtonInactiveBackgroundColor](https://docs.microsoft.com/uwp/api/Windows.UI.ViewManagement.ApplicationViewTitleBar.ButtonInactiveBackgroundColor) properties to [Colors.Transparent](https://docs.microsoft.com/uwp/api/Windows.UI.Colors.Transparent).</span></span>

```csharp
private void ExtendAcrylicIntoTitleBar()
{
    CoreApplication.GetCurrentView().TitleBar.ExtendViewIntoTitleBar = true;
    ApplicationViewTitleBar titleBar = ApplicationView.GetForCurrentView().TitleBar;
    titleBar.ButtonBackgroundColor = Colors.Transparent;
    titleBar.ButtonInactiveBackgroundColor = Colors.Transparent;
}
```

<span data-ttu-id="377ac-255">このコードは、ここに示すようにアプリの [OnLaunched](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application#Windows_UI_Xaml_Application_OnLaunched_Windows_ApplicationModel_Activation_LaunchActivatedEventArgs_) メソッド (_App.xaml.cs_) 内の [Window.Activate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.window.Activate) の呼び出しの後か、アプリの最初のページに配置できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-255">This code can be placed in your app's [OnLaunched](https://docs.microsoft.com/uwp/api/windows.ui.xaml.application#Windows_UI_Xaml_Application_OnLaunched_Windows_ApplicationModel_Activation_LaunchActivatedEventArgs_) method (_App.xaml.cs_), after the call to [Window.Activate](https://docs.microsoft.com/uwp/api/windows.ui.xaml.window.Activate), as shown here, or in your app's first page.</span></span>

```csharp
// Call your extend acrylic code in the OnLaunched event, after
// calling Window.Current.Activate.
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;

    // Do not repeat app initialization when the Window already has content,
    // just ensure that the window is active
    if (rootFrame == null)
    {
        // Create a Frame to act as the navigation context and navigate to the first page
        rootFrame = new Frame();

        rootFrame.NavigationFailed += OnNavigationFailed;

        if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
        {
            //TODO: Load state from previously suspended application
        }

        // Place the frame in the current Window
        Window.Current.Content = rootFrame;
    }

    if (e.PrelaunchActivated == false)
    {
        if (rootFrame.Content == null)
        {
            // When the navigation stack isn't restored navigate to the first page,
            // configuring the new page by passing required information as a navigation
            // parameter
            rootFrame.Navigate(typeof(MainPage), e.Arguments);
        }
        // Ensure the current window is active
        Window.Current.Activate();

        // Extend acrylic
        ExtendAcrylicIntoTitleBar();
    }
}
```

<span data-ttu-id="377ac-256">また、通常はタイトル バーに自動的に表示されるアプリのタイトルを、`CaptionTextBlockStyle` を使用した TextBlock で描画する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="377ac-256">In addition, you'll need to draw your app's title, which normally appears automatically in the title bar, with a TextBlock using `CaptionTextBlockStyle`.</span></span> <span data-ttu-id="377ac-257">詳しくは、「[タイトル バーのカスタマイズ](../shell/title-bar.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="377ac-257">For more info, see [Title bar customization](../shell/title-bar.md).</span></span>

## <a name="dos-and-donts"></a><span data-ttu-id="377ac-258">推奨と非推奨</span><span class="sxs-lookup"><span data-stu-id="377ac-258">Do's and don'ts</span></span>
* <span data-ttu-id="377ac-259">アクリルは、ナビゲーション ウィンドウなど、アプリのプライマリ サーフェス以外のサーフェスで背景素材として使用してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-259">Do use acrylic as the background material of non-primary app surfaces like navigation panes.</span></span>
* <span data-ttu-id="377ac-260">シームレスなエクスペリエンスを実現するには、アプリの周囲とわずかにブレンドするようにして、アクリルをアプリの 1 つ以上の端にまで拡張してください。</span><span class="sxs-lookup"><span data-stu-id="377ac-260">Do extend acrylic to at least one edge of your app to provide a seamless experience by subtly blending with the app’s surroundings.</span></span>
* <span data-ttu-id="377ac-261">アプリの大きな背景サーフェイスでデスクトップのアクリルを入れないでください - 一時的なサーフェイスの主に使用されているアクリルのメンタル モデルが破損します。</span><span class="sxs-lookup"><span data-stu-id="377ac-261">Don't put desktop acrylic on large background surfaces of your app - this breaks the mental model of acrylic being used primarily for transient surfaces.</span></span>
* <span data-ttu-id="377ac-262">アプリ内アクリルと背景アクリルは、継ぎ目部分での視覚的なテンションを回避するために、隣接するようには配置しないでください。</span><span class="sxs-lookup"><span data-stu-id="377ac-262">Don’t place in-app and background acrylics directly adjacent to avoid visual tension at the seams.</span></span>
* <span data-ttu-id="377ac-263">複数のアクリル ウィンドウを、同じ濃淡や不透明度で隣接するように配置しないでください。このようにすると、望ましくない継ぎ目が表示されます。</span><span class="sxs-lookup"><span data-stu-id="377ac-263">Don't place multiple acrylic panes with the same tint and opacity next to each other because this results in an undesirable visible seam.</span></span>
* <span data-ttu-id="377ac-264">アクリル サーフェスの上には、アクセント カラーのテキストを配置しないでください。</span><span class="sxs-lookup"><span data-stu-id="377ac-264">Don’t place accent-colored text over acrylic surfaces.</span></span>

## <a name="how-we-designed-acrylic"></a><span data-ttu-id="377ac-265">アクリルをどのように設計したか</span><span class="sxs-lookup"><span data-stu-id="377ac-265">How we designed acrylic</span></span>

<span data-ttu-id="377ac-266">アクリルの主要なコンポーネントを微調整して、ユニークな外観とプロパティを作成しました。</span><span class="sxs-lookup"><span data-stu-id="377ac-266">We fine-tuned acrylic’s key components to arrive at its unique appearance and properties.</span></span> <span data-ttu-id="377ac-267">透明度、ぼかしフラット サーフェスをビジュアルの深さとディメンションを追加するノイズと始めました。</span><span class="sxs-lookup"><span data-stu-id="377ac-267">We started with translucency, blur and noise to add visual depth and dimension to flat surfaces.</span></span> <span data-ttu-id="377ac-268">除外ブレンド モード レイヤーを追加して、アクリルの背景に配置される UI のコントラストと見やすさを確保しました。</span><span class="sxs-lookup"><span data-stu-id="377ac-268">We added an exclusion blend mode layer to ensure contrast and legibility of UI placed on an acrylic background.</span></span> <span data-ttu-id="377ac-269">最後に、ユーザーの個性を反映できるように、色の濃淡を追加しました。</span><span class="sxs-lookup"><span data-stu-id="377ac-269">Finally, we added color tint for personalization opportunities.</span></span> <span data-ttu-id="377ac-270">次のレイヤーを組み合わせることで、新しくて使いやすい素材が生みだされます。</span><span class="sxs-lookup"><span data-stu-id="377ac-270">In concert these layers add up to a fresh, usable material.</span></span>

<span data-ttu-id="377ac-271">![Acrylic レシピ](images/AcrylicRecipe_Diagram.jpg)
</span><span class="sxs-lookup"><span data-stu-id="377ac-271">![Acrylic recipe](images/AcrylicRecipe_Diagram.jpg)
</span></span><br/><span data-ttu-id="377ac-272">アクリルのレシピ: 背景、ぼかし、除外ブレンド、色/濃淡のオーバーレイ、ノイズ</span><span class="sxs-lookup"><span data-stu-id="377ac-272">The acrylic recipe: background, blur, exclusion blend, color/tint overlay, noise</span></span>


## <a name="get-the-sample-code"></a><span data-ttu-id="377ac-273">サンプル コードを入手する</span><span class="sxs-lookup"><span data-stu-id="377ac-273">Get the sample code</span></span>

- <span data-ttu-id="377ac-274">[XAML コントロール ギャラリー サンプル](https://github.com/Microsoft/Xaml-Controls-Gallery) - インタラクティブな形で XAML コントロールのすべてを参照できます。</span><span class="sxs-lookup"><span data-stu-id="377ac-274">[XAML Controls Gallery sample](https://github.com/Microsoft/Xaml-Controls-Gallery) - See all the XAML controls in an interactive format.</span></span>

## <a name="related-articles"></a><span data-ttu-id="377ac-275">関連記事</span><span class="sxs-lookup"><span data-stu-id="377ac-275">Related articles</span></span>

[<span data-ttu-id="377ac-276">**強調表示を表示します。**</span><span class="sxs-lookup"><span data-stu-id="377ac-276">**Reveal highlight**</span></span>](reveal.md)
