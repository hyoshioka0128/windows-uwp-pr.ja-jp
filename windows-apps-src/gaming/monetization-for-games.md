---
title: ゲームの収益化
description: Windows 10 のユニバーサル Windows プラットフォーム (UWP) ゲームに、バナー広告、ビデオ スポット広告、アプリ内購入を実装します。
ms.assetid: 79f4e177-d8e7-45d3-8a78-31d4c2fe298a
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10, UWP, ゲーム, 収益化
ms.localizationpriority: medium
ms.openlocfilehash: 9ef957700f6554ccece9d0c3bf51ccf4244a4b74
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368414"
---
#  <a name="monetization-for-games"></a>ゲームの収益化

ゲーム開発者にとって収益化のオプションを把握することは、ビジネスを維持し、優れたゲームの開発という素晴らしい仕事を続けるために不可欠です。 この記事では、ユニバーサル Windows プラットフォーム (UWP) ゲームの収益化とその実装方法の概要を示します。

以前は、ゲームから収益を得るには、価格を設定し、それがストアで購入されるのを待つ以外に方法はありませんでした。 しかし今は、さまざまなオプションがあります。 実店舗での販売や、オンラインでの販売 (物理メディアまたはソフト コピー) のほか、ゲームを無料で公開する代わりに広告を表示したり、無料のゲーム内で有料のアイテムを販売したりする方法もあります。 ゲーム自体も、もはや単体の製品ではありません。 メインのゲームに関連して追加のコンテンツを販売する方法が主流となっています。

UWP ゲームの販売促進や収益化には、次の方法があります。
* これは、セキュリティで保護された Microsoft Store では、ゲーム、オンライン ストアの内容[世界規模の配布](#worldwide-distribution-channel)します。 世界中のゲーマーが、[販売者の設定する価格](#set-a-price-for-your-game)でゲームをオンラインで購入できます。
* Windows SDK の API を使って[ゲーム内購入](#in-game-purchases)を作成する。 ゲーマーはゲーム内からアイテムを購入したり、特別な機器、スキン、地図、ゲーム レベルなどの追加のコンテンツを購入したりすることができます。
* [Microsoft Advertising SDK](https://aka.ms/ads-sdk-uwp) の API を使って、広告ネットワークから供給される広告を表示する。 [ゲーム内で広告を表示](#display-ads-in-your-game)し、ゲーマーがビデオ広告を見るとゲーム内のリワードがもらえるオプションを提供できます。
* [広告キャンペーンによってゲームの可能性を最大限に広げる](#maximize-your-games-potential-through-ad-campaigns)。 有料広告、コミュニティ広告 (無料)、または自社広告 (無料) キャンペーンを使ってゲームを宣伝し、ユーザー ベースを拡大します。

## <a name="worldwide-distribution-channel"></a>世界規模の販売チャネル

Microsoft Store が利用できるゲーム ダウンロード 200 台を超える国や地域で支払い Visa、Mastercard、PayPal などのさまざまなフォームを使用して課金のサポートにより、世界中。 国とリージョンの一覧については、次を参照してください。[を定義する市場選択](https://docs.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection)します。

## <a name="set-a-price-for-your-game"></a>ゲームの価格設定

ストアに公開する UWP ゲームは、_有料_または_無料_に設定できます。 有料ゲームでは、ゲームを開始する前に、販売側が設定したゲームの価格がユーザーに請求されます。無料ゲームでは、料金を支払うことなくゲームをダウンロードしてプレイできます。

以下に、ストアでのゲームの価格設定に関するいくつかの重要な概念を説明します。

### <a name="base-price"></a>基本価格

ゲームの基本価格は、提供するゲームが_有料_か_無料_かを決定する要素です。 使用することができます[パートナー センター](https://partner.microsoft.com/dashboard)国と地域に基づいて基準価格を構成します。
場合によっては、価格を決定する際に、[他国向けに販売する場合の納税義務](https://docs.microsoft.com/windows/uwp/publish/tax-details-for-paid-apps)と[特定の市場向けに販売する場合のコストに関する考慮事項](https://docs.microsoft.com/windows/uwp/publish/define-pricing-and-market-selection)を考慮する必要があります。 また[特定の市場向けにカスタム価格を設定](../publish/set-and-schedule-app-pricing.md#override-base-price-for-specific-markets)することもできます。

### <a name="sale-price"></a>セール価格

ゲームの販売促進方法の 1 つに、期間を限定して価格を下げる方法があります。 セール価格を__無料__に設定して、無料でゲームのダウンロードを許可することもできます。
あらかじめセールの開始日と終了日の両方を設定することで、セール キャンペーンのスケジュールを事前に設定できます。 詳しくは、「[アプリとアドオンの販売](https://docs.microsoft.com/windows/uwp/publish/put-apps-and-add-ons-on-sale)」をご覧ください。

## <a name="in-game-purchases"></a>ゲーム内購入

ゲーム内購入とは、ゲームの中で購入できる製品です。 これらの製品は、一般に_アプリ内購入_とも呼ばれます。 Microsoft Store で、これらの製品と呼ばれる_アドオン_します。 [アドオンを公開](https://docs.microsoft.com/windows/uwp/publish/add-on-submissions)パートナー センターを通じてします。 また、ゲームのコードでアドオンを有効にする必要があります。

### <a name="types-of-add-ons"></a>アドオンの種類

ストアでは、_永続的_と_コンシューマブル_の 2 種類のアドオンを作成できます。 永続的なアドオンは、指定された時間にわたって使うことができ、有効期限の間に一度だけ購入できる項目です。 コンシューマブルなアドオンとは、繰り返し購入して使うことができる項目です。

コンシューマブルを作成する際は、追跡方法として、それらの項目が_開発者による管理_か_ストアによる管理_か (この機能は Windows 10、バージョン 1607 以降で使用可能) を決定してください。 開発者に管理された使用できるはのゲーマー; の項目の残高を追跡する責任を負いますストアで管理された使用できると Microsoft Store の追跡項目の分散できます。 詳しくは、「[コンシューマブルなアドオン購入の有効化](https://docs.microsoft.com/windows/uwp/monetize/enable-consumable-add-on-purchases)」をご覧ください。

### <a name="create-in-game-purchases"></a>ゲーム内購入の作成

最新のアプリ内購入およびライセンス情報 API は、Windows SDK (Windows 10 バージョン 1607 以降) の [Windows.Services.Store](https://docs.microsoft.com/uwp/api/windows.services.store) 名前空間に含まれています。 1607 以降のリリースをターゲットとする新しいゲームを開発している場合は、最新のアドオンの種類をサポートし、パフォーマンスに優れた __Windows.Services.Store__ 名前空間の使用をお勧めします。
製品とパートナー センターと、ストアでサポートされる機能の今後の型と互換性がある設計もいます。 以前のバージョンの Windows 10 向けに開発を行う場合は、この代わりに [Windows.ApplicationModel.Store](https://docs.microsoft.com/uwp/api/windows.applicationmodel.store) 名前空間を使います。

詳しくは、「[アプリ内購入と試用版](https://docs.microsoft.com/windows/uwp/monetize/in-app-purchases-and-trials)」をご覧ください。

#### <a name="simplified-purchase-example"></a>単純な購入の例

このセクションでは、単純な購入の例を通じて、さまざまなメソッド呼び出しを使って購入フローを実装する方法を説明します。

|ゲーム内の操作/アクティビティ                                                | ゲームのバックグラウンド タスク                  |
|--------------------------------------------------------------------------|----------------------------------------|
|ゲーマーが、ショップにアクセスします。 ショップ メニューがポップアップ表示され、入手可能なアドオンと購入価格が示されます。 |  ゲームがアドオンの[製品情報を取得](https://docs.microsoft.com/windows/uwp/monetize/get-product-info-for-apps-and-add-ons)し、[アドオンが適切なライセンスを持つかどうかを判定](https://docs.microsoft.com/windows/uwp/monetize/get-license-info-for-apps-and-add-ons)して、ゲーマーが購入できるアドオンをショップのメニューに表示します。                           |
|ゲーマーが __[購入]__ をクリックして項目を購入します。             |__[購入]__ アクションが、項目の購入要求を送信し、それを取得するための支払いプロセスを開始します。 実装は、項目の種類によって異なります。 [永続的または 1 回限りの購入項目](https://docs.microsoft.com/windows/uwp/monetize/enable-in-app-purchases-of-apps-and-add-ons)の場合、ユーザーは有効期限が切れるまで、1 つの項目のみを所有できます。 項目が[コンシューマブル](https://docs.microsoft.com/windows/uwp/monetize/enable-consumable-add-on-purchases)の場合、お客様は 1 つ以上の項目を所有できます。 |

### <a name="test-in-game-purchases-during-game-development"></a>ゲーム開発時のゲーム内購入のテスト

アドオンはゲームと関連して作成する必要があるため、ゲームをストアで公開して提供する必要があります。 このセクションでは、まだ開発段階にあるゲームに対してアドオンを作成する手順を示します 
(完成したゲームを既にストアに公開している場合は、最初の 3 つのステップをスキップして、「[ストアでのアドオンの作成](#create-an-add-on-in-the-store)」に進むことができます)。

開発中のゲームに対してアドオンを作成するには、次の手順を実行します。
1. [パッケージを作成します。](#create-a-package)
2. [非表示としてゲームを発行します。](#publish-the-game-as-hidden)
3. [Visual Studio でゲーム ソリューションをストアに関連付ける](#associate-your-game-solution-with-the-store)
4. [ストアのアドオンを作成します。](#create-an-add-on-in-the-store)

#### <a name="create-a-package"></a>パッケージを作成する

公開されるすべてのゲームは、Windows アプリ認定の最小要件を満たす必要があります。 ゲームが Windows ストアで公開するための要件に適合していることを確認するには、Windows 10 SDK に含まれている [Windows アプリ認定キット](https://docs.microsoft.com/windows/uwp/debug-test-perf/windows-app-certification-kit)を使ってゲームをテストすることができます。 Windows アプリ認定キットが含まれている Windows 10 SDK をまだダウンロードしていない場合は、[Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) にアクセスしてください。

ストアにアップロード可能なパッケージを作成するには:

1. Visual Studio でゲーム ソリューションを開きます。
2. Visual Studio 内で、 __[プロジェクト]__  >  __[ストア]__  >  __[アプリ パッケージの作成]__ の順に選びます。
3. __を Microsoft Store にアップロードするパッケージをビルドするでしょうか。__ オプションを選択し__はい__します。
4. サインイン、[パートナー センター](https://partner.microsoft.com/dashboard)開発者アカウント。 アカウントを持っていない場合は、開発者アカウントに[登録](https://developer.microsoft.com/store/register)できます。
5. アップロード パッケージを作成するアプリを選びます。 アプリの申請をまだ作成していない場合は、新しいアプリ名を指定して新しい申請を作成します。 詳しくは、「[名前の予約によるアプリの作成](https://docs.microsoft.com/windows/uwp/publish/create-your-app-by-reserving-a-name)」をご覧ください。
6. パッケージが正常に作成されたら、 __[Windows アプリ認定キットを起動する]__ をクリックしてテスト プロセスを開始します。
7. エラーを修正してゲームパッケージを作成します。

#### <a name="publish-the-game-as-hidden"></a>非表示としてゲームを公開する

1. 移動して[パートナー センター](https://partner.microsoft.com/dashboard)してサインインします。
2. __[ダッシュボード概要]__ ページまたは __[すべてのアプリ]__ ページで、目的のアプリをクリックします。 アプリの申請をまだ作成していない場合は、 __[新しいアプリの作成]__ をクリックして名前を予約します。
3. __[アプリの概要]__ ページで、 __[提出を開始する]__ をクリックします。
4. この新しい申請を構成します。 [申請] ページで、次の手順を実行します。
    * __[価格と使用可能状況]__ をクリックします。 __可視性__セクションで、'__このアプリを非表示にして、取得しないようにしています.__ ' チームが、ゲームへのアクセスを開発のみを確認します。 詳しくは、「[分布と認知度](https://docs.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability)」をご覧ください。
    * [__プロパティ__] を選択します。 __[カテゴリとサブカテゴリ]__ セクションで __[ゲーム]__ を選択し、ゲームに適したサブカテゴリを選びます。
    * __[年齢区分]__ をクリックします。 質問表に正確に入力します。
    * __[パッケージ]__ をクリックします。 前の手順で作成したゲーム パッケージをアップロードします。
5. ダッシュボードに表示されるその他の申請プロンプトに従って、このゲームを一般のユーザーに対して非表示にしたまま、正常に公開します。
6. __[ストアに提出]__ をクリックします。

詳しくは、「[アプリの申請](https://docs.microsoft.com/windows/uwp/publish/app-submissions)」をご覧ください。

ゲームをストアに提出すると、[アプリの認定プロセス](https://docs.microsoft.com/windows/uwp/publish/the-app-certification-process)が開始します。 このプロセスでは、ゲームが表示されるまでに最大 16 時間かかることがあります。

#### <a name="associate-your-game-solution-with-the-store"></a>ゲーム ソリューションをストアに関連付ける

次の手順を実行して、Visual Studio でゲーム ソリューションを開きます。

1. __[プロジェクト]__  >  __[ストア]__  >  __[アプリケーションをストアと関連付ける]__ の順に選びます。
2. パートナー センターの開発者アカウントにサインインしを使用するこのソリューションを関連付けるアプリ名を選択します。
3. __Package.appxmanifest.xml ファイル__をダブルクリックし、 __[パッケージ化]__ タブに移動してゲームが正しく関連付けられていることを確認します。

すでにライブのゲームとしてストアに掲載されている公開済みのゲームにソリューションを関連付けた場合、ソリューションにアクティブなライセンスが設定され、ゲーム用のアドオン作成が一歩前進します。 詳しくは、「[アプリのパッケージ化](https://docs.microsoft.com/windows/uwp/packaging/index)」をご覧ください。

#### <a name="create-an-add-on-in-the-store"></a>ストアでアドオンを作成する

アドオンを作成する際は、提出した適切なゲームを確認してアドオンを関連付けます。 アドオンに関連付けるすべての多様な情報を構成する方法について詳しくは、「[アドオンの申請](https://docs.microsoft.com/windows/uwp/publish/add-on-submissions)」をご覧ください。

1. 移動して[パートナー センター](https://partner.microsoft.com/dashboard)してサインインします。
2. __[ダッシュボード概要]__ ページまたは __[すべてのアプリ]__ ページで、アドオンを作成するアプリをクリックします。
3. __[アプリの概要]__ ページの __[アドオン]__ セクションで、 __[新しいアドオンを作成する]__ をクリックします。
4. アドオンの製品の種類として、 __[開発者により管理されるコンシューマブル]__ 、 __[ストアで管理されるコンシューマブル]__ 、 __[永続的]__ のいずれかを選択します。
5. 一意の製品 ID を入力します。この製品 ID は、このアドオンをゲーム コードに統合する際に文字列変数として使われます。 この ID は、ユーザーには表示されません。 詳しくは、「[アドオンの製品の種類と製品 ID を設定する](https://docs.microsoft.com/windows/uwp/publish/set-your-add-on-product-id)」をご覧ください。

アドオンのその他の構成は次のとおりです。
* [[プロパティ]](https://docs.microsoft.com/windows/uwp/publish/enter-add-on-properties)
* [価格と可用性](https://docs.microsoft.com/windows/uwp/publish/set-add-on-pricing-and-availability)
* [ストアの一覧](https://docs.microsoft.com/windows/uwp/publish/create-add-on-store-listings)

ゲームに多くのアドオンがある場合は、することができます、プログラムで作成を使用して、 __Microsoft Store 送信 API__します。 詳細については、次を参照してください。[作成し、Microsoft Store サービスを使用して送信を管理](https://docs.microsoft.com/windows/uwp/monetize/create-and-manage-submissions-using-windows-store-services)します。

## <a name="display-ads-in-your-game"></a>ゲーム内での広告の表示

Microsoft Advertising SDK に含まれているライブラリやツールを使って、広告ネットワークから広告を受信するサービスをゲーム内に設定できます。 ゲーマーに対してライブ広告が表示され、ゲーマーが表示された広告を見たり操作したりしたときに、広告主から開発者に報酬が支払われます。
詳しくは、「[アプリでの広告の表示](../monetize/display-ads-in-your-app.md)」をご覧ください。

### <a name="ad-formats"></a>広告の形式

Microsoft Advertising SDK を使って表示できる広告には、いくつかの種類があります。

* バナー広告 &mdash; ゲーム画面の一部に表示される広告であり、通常、ゲーム内に表示されます。
* ビデオ スポット広告 &mdash; 全画面表示の広告であり、ゲームのレベル間で使うと非常に効果的です。 正しく実装すれば、バナー広告よりもゲームのプレイを阻害しない可能性があります。
* ネイティブ広告は、コンポーネント ベースの広告形式で、各広告クリエイティブ (タイトル、画像、説明、行動喚起テキストなど) が個々の要素としてアプリに配信され、それをアプリに統合できます。

### <a name="which-ads-are-displayed"></a>表示される広告

既定では、アプリはマイクロソフトの有料広告ネットワークの広告を表示します。 広告の収益を最大化するには、広告ユニットの広告仲介を有効化することで、その他の有料広告ネットワークの広告を表示できます。 現在提供されている広告ネットワークについて詳しくは、[広告仲介](../publish/in-app-ads.md#mediation)のガイダンスをご覧ください。

### <a name="which-markets-allow-ads-to-be-displayed"></a>広告を表示できる市場

広告がサポートされるすべての国と地域の一覧については、「[広告ネットワークでサポートされる市場](../publish/in-app-ads.md#network-markets)」をご覧ください。

### <a name="apis-for-displaying-ads"></a>広告を表示するための API

ゲームで広告を表示するには、Microsoft Advertising SDK の [AdControl](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.adcontrol) クラス、[InterstitialAd](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.interstitialad) クラス、[NativeAd](https://docs.microsoft.com/uwp/api/microsoft.advertising.winrt.ui.nativead) クラスを使用します。

これにはまず、[Microsoft Advertising SDK](https://aka.ms/ads-sdk-uwp) をダウンロードし、Visual Studio 2015 以降のバージョンと共にインストールします。 詳しくは、「[Microsoft Advertising SDK のインストール](../monetize/install-the-microsoft-advertising-libraries.md)」をご覧ください。

#### <a name="implementation-guides"></a>実装ガイド

次のウォークスルーでは、__AdControl__、__InterstitialAd__、__NativeAd__ を使って広告を実装する方法を説明しています。

* [XAML と .NET でバナー広告を作成します。](https://docs.microsoft.com/windows/uwp/monetize/adcontrol-in-xaml-and--net)
* [HTML5 と JavaScript でバナー広告を作成します。](https://docs.microsoft.com/windows/uwp/monetize/adcontrol-in-html-5-and-javascript)
* [スポット広告を作成します。](https://docs.microsoft.com/windows/uwp/monetize/interstitial-ads)
* [ネイティブの広告を作成します。](https://docs.microsoft.com/windows/uwp/monetize/native-ads)

開発時には、[広告ユニットのテスト値](../monetize/test-mode-values.md)を使って広告がどのようにレンダリングされるかを確認できます。 上のウォークスルーでも、これらの広告ユニットのテスト値が使われています。

設計と実装のプロセスに役立つベスト プラクティスを次に示します。

* [バナー広告のためのベスト プラクティス](https://docs.microsoft.com/windows/uwp/monetize/ui-and-user-experience-guidelines)
* [スポット広告のためのベスト プラクティス](https://docs.microsoft.com/windows/uwp/monetize/ui-and-user-experience-guidelines)

広告が表示されない、ブラック ボックスが点滅し、表示されなくなる、広告が更新されないなど、開発上の一般的な問題に対する解決策については、[トラブルシューティング ガイド](https://docs.microsoft.com/windows/uwp/monetize/troubleshooting-guides)」をご覧ください。

### <a name="prepare-for-release-by-replacing-ad-unit-test-values"></a>広告ユニットのテスト値を置き換えてリリースの準備をする

ライブ テストに移行する準備または公開したゲームで広告を受信する準備ができたら、テスト用の広告ユニット値を、ゲーム用に提供された実際の値に更新する必要があります。 ゲーム用の広告ユニットを作成する方法については、「[アプリの広告ユニットをセットアップする](https://docs.microsoft.com/windows/uwp/monetize/set-up-ad-units-in-your-app)」をご覧ください。

### <a name="other-ad-networks"></a>他の広告ネットワーク

UWP アプリおよび UWP ゲームへの広告提供のための SDK を提供するその他の広告ネットワークを次に示します。

#### <a name="vungle"></a>Vungle

Vungle SDK for Windows は、アプリやゲームに表示するビデオ広告を提供します。 この SDK をダウンロードするには [Vungle SDK](https://v.vungle.com/sdk) にアクセスしてください。

#### <a name="smaato"></a>Smaato

Smaato では、UWP アプリと UWP ゲームにバナー広告を組み込むことができます。 [SDK](https://www.smaato.com/resources/sdks/) をダウンロードし、[ドキュメント](https://wiki.smaato.com/display/SPX/Windows+Phone)で詳しい情報をご覧ください。

#### <a name="adduplex"></a>AdDuplex

AdDuplex を使うと、ゲームにバナー広告やスポット広告を実装できます。

Windows 10 XAML プロジェクトに直接 AdDuplex を統合する方法について詳しくは、次の AdDuplex の Web サイトにアクセスしてください。
* バナー広告:[Windows 10 SDK for XAML](https://adduplex.zendesk.com/hc/en-us/articles/204849031-Windows-10-SDK-for-XAML-apps-installation-and-usage)
* スポット広告:[Windows 10 の XAML AdDuplex スポット広告のインストールと使用](https://adduplex.zendesk.com/hc/en-us/articles/204849091-Windows-10-XAML-AdDuplex-Interstitial-Ad-Installation-and-Usage)

Unity を使って作成された Windows 10 UWP ゲームに AdDuplex SDK を統合する方法については、「[Windows 10 SDK for Unity apps installation and usage (Windows 10 SDK for Unity アプリのインストールと使用)](https://adduplex.zendesk.com/hc/en-us/articles/207279435-Windows-10-SDK-for-Unity-apps-installation-and-usage)」をご覧ください。

## <a name="maximize-your-games-potential-through-ad-campaigns"></a>広告キャンペーンによってゲームの可能性を最大限に広げる

広告を利用して、ゲームの販売促進を強化しましょう。 ゲームの[広告キャンペーンを作成](https://docs.microsoft.com/windows/uwp/publish/create-an-ad-campaign-for-your-app)すると、ゲームの販売を促進するための広告が、他の開発者のアプリやゲームに表示されます。

ゲーマー ベースの増加に役立つキャンペーンを複数の種類から選択できます。

|キャンペーンの種類             | ゲームの広告が表示されるアプリ                                                                                                                                                                   |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|有料                      |ゲームのデバイスまたはカテゴリに一致するアプリ。                                                                                                                                                   |
|コミュニティ (無料)            |コミュニティ広告キャンペーンにオプト インしている他の開発者が公開するアプリ。 詳しくは、「[コミュニティ広告について](https://docs.microsoft.com/windows/uwp/publish/about-community-ads)」をご覧ください。|
|自社 (無料)                |自社が公開したアプリのみ。 詳しくは、「[自社広告について](https://docs.microsoft.com/windows/uwp/publish/about-house-ads)」をご覧ください。                                                            |

## <a name="related-links"></a>関連リンク

* [支払いの受け取り](https://docs.microsoft.com/windows/uwp/publish/getting-paid-apps)
* [勘定科目の種類、場所、および料金](https://docs.microsoft.com/windows/uwp/publish/account-types-locations-and-fees)
* [分析](https://docs.microsoft.com/windows/uwp/publish/analytics)
* [グローバリゼーションとローカライズ](https://docs.microsoft.com/windows/uwp/globalizing/globalizing-portal)
* [アプリの試用版を実装します。](https://docs.microsoft.com/windows/uwp/monetize/implement-a-trial-version-of-your-app)
* [A とアプリの実験を実行する B のテスト](https://docs.microsoft.com/windows/uwp/monetize/run-app-experiments-with-a-b-testing)
