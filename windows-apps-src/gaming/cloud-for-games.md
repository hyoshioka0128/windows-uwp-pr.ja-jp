---
title: UWP ゲーム用のクラウド サービスの使用
description: UWP ゲーム用のバックエンドとしてクラウドを実装することについて説明します。
ms.assetid: 1a7088e0-0d7b-11e6-8e05-0002a5d5c51b
ms.date: 03/27/2018
ms.topic: article
keywords: Windows 10、UWP、ゲーム、クラウド サービス
ms.localizationpriority: medium
ms.openlocfilehash: 15a7e3bed746a31ce2d8f458045cdd1126b71b8c
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368993"
---
#  <a name="using-cloud-services-for-uwp-games"></a>UWP ゲーム用のクラウド サービスの使用

Windows 10 のユニバーサル Windows プラットフォーム (UWP) では、Microsoft デバイス間でのゲームの開発のために使用できる一連の API が用意されています。 複数のプラットフォームやデバイスを対象としてゲームを開発する場合、クラウド バックエンドを使って、需要に応じてゲームをスケーリングすることができます。

ゲームの完全なクラウド バックエンド ソリューションを探している場合は、「[ゲームのバックエンド向けのサービスとしてのソフトウェア](#software-as-a-service-for-game-backend)」を参照してください。

##  <a name="what-is-cloud-computing"></a>クラウド コンピューティングとは

クラウド コンピューティングでは、需要に応じてインターネット経由で IT リソースやアプリケーションを利用することにより、デバイスのデータを保存および処理します。 _クラウド_という用語は、不特定の場所からアクセスできる外部の膨大なリソース (ローカル リソースではない) の可用性を表すメタファーです。
クラウド コンピューティングの原則により、リソースやソフトウェアを利用するための新しい方法が提供されます。 ユーザーは、完全な製品やリソースの料金を事前に支払う必要がなくなり、代わりに、プラットフォーム、ソフトウェア、リソースをサービスとして利用できます。 クラウド プロバイダーは通常、使用量やサービス プランに基づいて顧客に料金を請求します。

##  <a name="why-use-cloud-services"></a>クラウド サービスを使う理由

ゲームでクラウド サービスを使う利点の 1 つは、物理サーバー ハードウェアに事前に投資する必要がなく、後で使用量やサービス プランに従って支払うだけで済むことです。 これは、新しいゲーム タイトルの開発に伴うリスクを管理するための 1 つの方法です。 

もう 1 つの利点として、膨大なクラウド リソースを活用してゲームのスケーラビリティ (同時接続プレイヤー数の急激な増加、負荷の高いリアルタイム ゲームの計算やデータの要件) を実現できることが挙げられます。 これにより、ゲームのパフォーマンスが常に安定します。 さらに、クラウド リソースには、世界中のどこからでも、任意のプラットフォームで実行されている任意のデバイスからアクセスできます。つまり、全世界のすべてのユーザーにゲームを提供できることを意味します。

魅力的なゲームプレイ エクスペリエンスをプレイヤーに提供することが重要です。 クラウドで実行されているゲーム サーバーはクライアント側の更新プログラムに依存しないため、ゲーム全体の制御された安全な環境を実現できます。   また、クライアントを信頼したり、サーバー側のゲーム ロジックを使用したりしないため、クラウドを通じてゲームプレイの整合性を実現できます。 サービス間の接続を構成して、さらに統合されたゲーム エクスペリエンスを実現することもできます。たとえば、ゲーム内購入をさまざまな支払い方法にリンクする、異なるゲーム ネットワークを接続する、ゲーム内の更新を Facebook や Twitter などの人気のソーシャル メディア ポータルで共有することが可能になります。 

専用のクラウド サーバーを使用することによって、大規模で永続的なゲーム ワールドの作成、ゲーマー コミュニティの構築、時間の経過に伴うゲーマー データ収集と分析によるゲームプレイの向上、ゲームの収益化設計モデルの最適化を行うこともできます。

さらに、非同期のマルチプレイヤーのしくみを使うソーシャル ゲームなど、負荷の高いゲーム データ管理機能を必要とするゲームを、クラウド サービスを使って実装できます。

##  <a name="how-game-companies-use-the-cloud-technology"></a>ゲーム開発企業によるクラウド テクノロジの使用方法

さまざまな開発者がどのようにゲームにクラウド ソリューションを実装しているかについて説明します。

<table>
    <colgroup>
    <col width="10%" />
    <col width="30%" />
    <col width="30%" />
    <col width="30%" />
    </colgroup>
    <tr class="header" align="left">
        <th>Developer</th>
        <th>説明</th>
        <th>主なゲーム シナリオ</th>
        <th>詳細</th>
    </tr>
    <tr>
        <td><a href="https://www.tencent.com">Tencent Games</a></td>
        <td><b>Tencent Games</b> は、Azure Service Fabric を使用して従来の PC ゲームをサービスとして配信するための革新的なソリューションを開発しました。 同社のクラウド ゲーム ソリューションでは、"シン クライアント + リッチ クラウド" モデルを使用して、ワークロードをバックエンドのマイクロサービスとして実行します。</td>
        <td>
            <ul>
                <li>従来の PC ゲームがクラウド ゲームとして世界中のユーザーに配信されます。 <li>ゲーム配信プロセスの最適化 <li>ゲーム機能をマイクロサービスとして分離することで複雑さを緩和し、依存関係によるワークロードの繰り返しを軽減します。また、新しい機能を個別に独立してアップグレードできます。 <li>小さなインストール パッケージをダウンロードして、最新のゲーム コンテンツでプレイできます (パッケージ サイズを GB から MB に縮小)。 <li>メンテナンス コストの削減。 </ul>
        </td>
        <td>
            <ul>
                <li><a href="https://customers.microsoft.com/story/tencent-telecommunications-azure-service-fabric-windows-server-en">Tencent Games は、Microsoft クラウド ゲーム ソリューションを構築しました</a>
                <li><a href="https://channel9.msdn.com/Shows/Cloud+Cover/Episode-228-Building-Games-with-Service-Fabric#time=38m33s">Service Fabric を使用したゲームの構築:Tencent の実装 (ビデオ) の詳細について</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td><a href="https://www.halowaypoint.com/">343 industries</a></td>
        <td><b>Halo 5:Guardians</b>実装<a href="https://www.halowaypoint.com/spartan-companies">Halo:Spartan 企業</a>に対してその速度と自動インデックス作成機能のための柔軟性が選択されました (DocumentDB API) を使用して Azure Cosmos DB を使用して、ソーシャル ゲームをプラットフォームとして。</td>
        <td>
            <ul>
                <li>マルチ プレイヤー ゲームプレイでグループの作成/管理を処理するスケーラブルなデータ層 <li>ゲームとソーシャル メディアの統合 <li>複数の属性を使った、リアルタイムのデータ クエリ <li>ゲームプレイの達成度や統計情報の同期 </ul>
        </td>
        <td>
            <ul>
                <li><a href="https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/">実装 (DocumentDB API) を使用して Azure Cosmos DB を使用してソーシャル ゲーム</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td><a href="https://web.ageofascent.com/">Illyriad Games</a></td>
        <td>Illyriad Games は <b>Age of Ascent</b> を開発した企業です。このゲームは、壮大な 3D 空間を舞台にした大規模マルチプレイヤー オンライン (MMO) ゲームであり、最新のブラウザーを備えたデバイスでプレイできます。 したがって、このゲームは、プラグインなしで、PC、ノート PC、スマートフォン、その他のモバイル デバイスでプレイできます。ゲームでは、ASP.NET Core、HTML5、WebGL、および Azure を使用します。</td>
        <td>
            <ul>
                <li>クロスプラットフォーム、ブラウザー ベースのゲーム <li>1 つの大規模かつ永続的でオープンな世界 <li>負荷の高いリアルタイムのゲームプレイの計算を処理 <li>プレイヤー数に応じたスケーリング </ul>
        </td>
        <td>
            <ul>
                <li><a href="https://channel9.msdn.com/Shows/Cloud+Cover/Episode-228-Building-Games-with-Service-Fabric#time=06m52s">Service Fabric を使用したゲームの構築:アセント MMO ゲーム (ビデオ) の有効期間</a>
                <li><a href="https://channel9.msdn.com/Events/Build/2016/KEY02#time=57m20s">Azure Service Fabric (ビデオ) を使用してマイクロ サービスとしてのゲーム コンポーネントを管理します。</a> 
                <li><a href="/Blogs/Azure/Age-of-Ascent-from-Illyriad-Powered-by-Azure-Service-Fabric-and-ASPNET">Age of Ascent 開発者 (ビデオ) へのインタビューします。</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td><a href="https://www.nextgames.com/">Next Games</a></td>
        <td>Next games 社の作成者は、 <b>The Walking Dead:No の Land</b>ビデオ ゲーム AMC の元の系列に基づいています。 Walking Dead ゲームでは、バックエンドとして Azure を使用しています。 1,000,000 ダウンロード開始週末と最初の週が、ゲームが 1 の iPhone と iPad Free、米国でのアプリApp Store では、1、12 か国で無料のアプリと 1 13 か国の無料のゲームです。
        </td>
        <td>
            <ul>
                <li>クロスプラットフォーム <li>ターン制のマルチプレイヤー <li>弾力性のあるパフォーマンスのスケーリング <li>ゲーマーの不正行為に対する保護 <li>動的コンテンツ配布 </ul>
        </td>
        <td>
            <ul>
                <li><a href="https://azure.microsoft.com/blog/how-we-built-it-next-games-global-online-gaming-platform-on-azure/">どのようにして作成しました。次のゲーム グローバル オンライン ゲーム プラットフォーム on Azure (ビデオのブログ)</a>
                <li><a href="https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/">開発サイクルの高速化しより魅力的なゲーム プレイの (DocumentDB API) を使用して Azure Cosmos DB を使用する配信不能のウォーク</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td><a href="https://www.crimecoast.com/">ピクセル大学の強豪</a></td>
        <td>Pixel Squad では、Unity ゲーム エンジンと Azure を使って <b>Crime Coast</b> を開発しました。 <b>Crime Coast</b> は、Android、iOS、Windows プラットフォームでプレイできるソーシャル戦略ゲームです。 このゲームでは、Azure BLOB ストレージ、Managed Azure Redis Cache、負荷分散された IIS VM アレイ、Microsoft 通知ハブが使用されています。 同社のスケーリングの管理方法や、同時接続プレイヤー数が 5,000 人にもなるプレイヤーの急増の処理方法を参考にしてください。
        </td>
        <td>
            <ul>
                <li>クロスプラットフォーム <li>マルチプレイヤー オンライン ゲーム <li>プレイヤー数に応じたスケーリング </ul>
        </td>
        <td>
            <ul>
                <li><a href="https://channel9.msdn.com/Blogs/The-Game-Blog/BizSpark-Interview-with-Pixel-Squad-How-the-used-Azure-Cloud-Services-to-make-an-MMO-with-a-3-man-te">犯罪 Coast MMO ゲームが Azure Cloud Services を使用する方法</a>
            </ul>
        </td>
    </tr> 
</table>

    
### <a name="other-links"></a>その他のリンク

* [Hitman と Azure:クラウドを使用しているターゲットを見つけにくいようなゲーム機能を作成します。](https://channel9.msdn.com/Series/Hitman)
* [Hitcents、ゲーム Troopers および InnoSpark 秘密のソースとして azure に](https://news.microsoft.com/features/game-developers-use-microsoft-azure-as-secret-sauce-for-scale-and-growth-2/)
* [Azure を使用して、Bizspark プログラムにゲームのスタートアップ](https://blogs.technet.microsoft.com/bizspark_featured_startups/2015/09/25/azure-open-for-gaming-startups/)


## <a name="how-to-design-your-cloud-backend"></a>クラウド バックエンドを設計する方法

プロデューサーやゲーム設計者は、ゲームの特徴やゲームに必要な機能について話し合いますが、ゲームのインフラストラクチャをどのように設計するかについての検討から始めることをお勧めします。 さまざまなデバイスや複数の主要プラットフォームを対象にゲームを開発する場合、Azure をゲームのバックエンドとして使用できます。

### <a name="understanding-iaas-paas-or-saas"></a>IaaS、PaaS、SaaS について

まず、ゲームに最適なサービスのレベルについて検討する必要があります。 次の 3 つのサービスの相違点を把握することにより、バックエンドを構築に必要なアプローチを決定できます。

* [Infrastructure as a Service (IaaS)](https://azure.microsoft.com/overview/what-is-iaas/)

    サービスとしてのインフラストラクチャ (IaaS) は、インターネット経由でプロビジョニングおよび管理される、インスタント コンピューティング インフラストラクチャです。 需要に応じてすばやくスケールアップおよびスケールダウンできるように、多くのコンピューターが用意されている可能性を想像してみてください。 IaaS によって、自社で物理サーバーやその他のデータ センターのインフラストラクチャを購入および管理するためのコストや面倒を避けることができます。

* [Platform as a Service (PaaS)](https://azure.microsoft.com/overview/what-is-paas/)

    サービスとしてプラットフォーム (PaaS) は IaaS と同様ですが、サーバー、ストレージ、ネットワークなどのインフラストラクチャの管理も含まれています。 物理サーバーやデータ センターのインフラストラクチャを購入しなくてもよいことに加えて、ソフトウェア ライセンス、基盤となるアプリケーション インフラストラクチャ、ミドルウェア、開発ツール、その他のリソースを購入して管理する必要もありません。

* [Software as a Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/)

    サービスとしてのソフトウェア (SaaS) では、ユーザーがインターネット経由でクラウド ベースのアプリに接続し、そのアプリを使用できます。 これによって、クラウド サービス プロバイダーから従量課金制で購入する完全なソフトウェア ソリューションが完成します。  一般的な例としては、メール、予定表作成、オフィス ツール (Microsoft Office 365) などがあります。 組織用アプリをレンタルで使用し、ユーザーはインターネット経由 (通常は Web ブラウザーを使用) で接続します。 基盤となるインフラストラクチャ、ミドルウェア、アプリ ソフトウェア、アプリ データはすべて、サービス プロバイダーのデータ センターにあります。 サービス プロバイダーはハードウェアとソフトウェアを管理し、適切なサービス契約で、ゲームとデータの可用性およびセキュリティの確保も行います。 SaaS を使用すると、初期費用を最小限に抑え、アプリの利用を迅速に開始できます。


### <a name="design-your-game-infrastructure-using-azure"></a>Azure を使用してゲーム インフラストラクチャを設計する

Azure のクラウド サービスをゲームに使用するためのいくつかの方法を以下に示します。 Azure は、Windows や Linux、および Ruby、Python、Java、PHP などのオープン ソース テクノロジと連携して動作します。 詳しくは、「[ゲームのための Azure](https://azure.microsoft.com/solutions/gaming/)」をご覧ください。

| 必要条件                 | アクティビティのシナリオ                            | 提供されるサービス                      | サービスの機能                                    |
|-----------------------------------|-----------------------------------------------|---------------------------------------|----------------------------------------------------|
| クラウドでのドメインのホスティング     | 効率的に DNS クエリに応答する            | [Azure DNS](https://azure.microsoft.com/services/dns/) | 高パフォーマンスと高可用性を備えたドメインのホスティング  |
| サインイン、本人確認      | ゲーマーがサインインし、ゲーマーの ID が認証される  | [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) | 多要素認証を備えた、あらゆるクラウドとオンプレミス Web アプリへのシングル サインオン            | 
| サービスとしてのインフラストラクチャ モデル (IaaS) を使用したゲーム      | ゲームがクラウド内の仮想マシンでホストされる       | [Azure Vm](https://azure.microsoft.com/services/virtual-machines/) | 組み込みの仮想ネットワークと負荷分散の機能や、オンプレミス システムとのハイブリッド整合性機能を備えたゲーム サーバーとして、1 から数千台の仮想マシンのインスタンスにスケーリング           |
| サービスとしてのプラットフォーム モデル (PaaS) を使用した Web ゲームやモバイル ゲーム            | ゲームが管理対象のプラットフォームでホストされる                | [Azure App Service](https://azure.microsoft.com/services/app-service/) | Web サイトやモバイル ゲーム用の PaaS (つまり Azure VMs とミドルウェア/開発ツール/BI/DB 管理)   |
| OS をさらに制御でき、可用性が高くスケーラブルな n 層クラウド ゲーム (PaaS)        | ゲームが管理対象のプラットフォームでホストされる                | [Azure クラウド サービス](https://azure.microsoft.com/services/app-service/) | PaaS の設計は、拡張性、信頼性、運用コスト効率に優れたアプリケーションのサポートに対応   |
| リージョン間での負荷分散によるパフォーマンスと可用性の向上 | 着信したゲーム要求をルーティング。 最初のレベルの負荷分散として使用できる。       | [Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) | 複数の自動フェールオーバー オプションと、均等または加重値に基づくトラフィック分散機能を提供。 オンプレミスとクラウド システムのシームレスな組み合わせが可能。 |
| ゲーム データ用のクラウド ストレージ       | 最新のゲーム データがクラウドに格納され、クライアント デバイスに送信される | [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)| 格納できるファイルの種類に制限はない。画像、オーディオ、ビデオなどの大量の構造化されていないデータのオブジェクト ストレージ  |
| 一時的なデータ ストレージ テーブル| ゲームのトランザクション (ゲームの状態の変化) が一時的にテーブルに格納される | [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/)| ゲーム データは、ゲームでの必要性に応じて柔軟なスキーマで格納できる |
| ゲームのトランザクションと要求のキュー| ゲームのトランザクションがキューの形式で処理される | [Azure Queue Storage](https://azure.microsoft.com/services/storage/queues/)| キューが予期しないトラフィックのバーストを吸収し、ゲーム中に要求が急激に増加してもサーバーがパンク状態になることを防止できる   |
| スケーラブルなリレーショナル ゲーム データベース| データベースへのゲーム内のトランザクションなど、リレーショナル データの構造化されたストレージ | [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)| サービスとしての SQL データベース ([VM 上の SQL との比較](https://azure.microsoft.com/documentation/articles/data-management-azure-sql-database-and-sql-server-iaas/))  |
| スケーラブルで分散型の待機時間が短いゲーム データベース| 柔軟なスキーマによる、ゲーム データやプレイヤー データの高速の読み取り、書き込み、照会 | [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)| 待機時間の短い、サービスとしての NoSQL ドキュメント データベース   |
| 独自のデータ センターと Azure サービスを使用する | ゲームは独自のデータ センターから取得され、クライアント デバイスに送信される | [Azure Stack](https://azure.microsoft.com/overview/azure-stack/) | 組織で独自のデータ センターからの Azure サービスを提供することで、より多くのことを実現できる  |
| 大量のデータ チャンクの転送| Azure CDN により、ゲームの画像、オーディオ、ビデオなどの大きなファイルを、ユーザーに最も近いコンテンツ配信ネットワーク (CDN) の POP の場所から送信できる    | [Azure Content Delivery Network](https://azure.microsoft.com/services/cdn/) | Azure CDN は、集中管理された大規模なノードの最新ネットワーク トポロジをベースに構築されており、突然のトラフィック スパイクや大きな負荷を処理することにより処理速度と可用性が大幅に向上し、ユーザー エクスペリエンスの向上につながる  |
| 短い待機時間               | より細かい制御とデータの分離の保証により、高速でスケーラブルなゲームを構築するためのキャッシュを実行する。ゲームのマッチメイキング機能の向上にも利用できる | [Azure Redis Cache](https://azure.microsoft.com/services/cache/) | 高速でスケーラブルな Azure アプリケーションを実現するための高スループットで、一貫性のある低待機時間のデータ アクセス  |
| 高スケーラビリティ、低待機時間 | 待機時間の短い読み取りと書き込みによりゲーム ユーザー数の変動を処理する | [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) | 複雑で待機時間が短く、データを多用するシナリオを実現し、一度により多くのユーザーを処理できるように拡張できる。 Service Fabric により、ステートレス アプリケーションで必要な、独立したストアやキャッシュを作成することなくゲームを構築できる |
| デバイスから 1 秒あたり数百万件のイベントを収集する機能                         | デバイスから 1 秒あたり数百万件のイベントをログに記録する | [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) | ゲーム、Web サイト、アプリ、デバイスからのクラウド規模の利用統計情報の取り込み  |
| リアルタイムのゲーム データの処理  | ゲームプレイを向上させるためにゲーム データのリアルタイム分析を実行する| [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) | クラウドでのリアルタイムのストリーム処理  |
| 予測的なゲームプレイの開発         | ゲーマーのデータに基づいてカスタマイズされた動的なゲームプレイを作成する  | [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) | 完全に管理されているクラウド サービスにより、簡単に予測分析ソリューションを構築、展開、共有できる  |
| ゲーム データの収集と分析| リレーショナル データベースと非リレーショナル データベースからのデータの大規模な並列処理 | [Azure Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/)| エンタープライズ クラスの機能を備えたサービスとしての柔軟なデータ ウェアハウス   |
| ユーザー エンゲージメントにより使用と顧客維持を促進| あらゆるバック エンドからあらゆるプラットフォームにターゲット プッシュ通知を送信し、関心を引き出して特定のゲーム操作を促進する | [Azure Notification Hubs](https://azure.microsoft.com/services/notification-hubs/)| 高速にすべての主要なプラットフォーム上のモバイル デバイスの数百万のプッシュをブロードキャスト&mdash;iOS、Android、Windows、Kindle、Baidu します。 ゲームは、任意のバックエンドでホストできる&mdash;クラウドまたはオンプレミスにします。|
| コンテンツを保護しながら、ローカルおよび世界中の対象ユーザーにメディア コンテンツをストリーミング| すべてのデバイスから視聴可能な高品質のゲーム トレーラーや動画クリップをブロードキャスト| [Azure Media Services](https://azure.microsoft.com/services/media-services/)| 組み込まれている Content Delivery Network 機能によるオンデマンドおよびライブのビデオ ストリーミング。 単一のプレーヤーで、コンテンツの保護と暗号化を含めたすべての再生ニーズに対応。| 
| モバイル アプリの開発、配布、ベータ テスト | モバイル アプリをテストして配布する。 アプリ パフォーマンスとユーザー エクスペリエンスを管理する。 | [HockeyApp](https://azure.microsoft.com/services/hockeyapp/)| クラッシュ レポートとユーザー メトリックをアプリの配布とユーザー フィードバック プラットフォームに統合。 Android、Cordova、iOS、OS X、Unity、Windows、Xamarin のアプリをサポート。 また、検討[Visual Studio Mobile Center](https://www.visualstudio.com/vs/mobile-center/) &mdash;ミッション コントロールの豊富な分析を結合するアプリのクラッシュ レポート、プッシュ通知、アプリの配布。 |
| 使用と顧客維持を促進するマーケティング キャンペーンの作成  | データ分析に基づいて対象となるプレイヤーにプッシュ通知を送信し、特定のゲーム操作に対する関心を引き出して利用を促進する | [Mobile Engagement](https://azure.microsoft.com/services/mobile-engagement/) (現在は既存のお客様のみに提供中であり、2018 年 3 月に廃止) |  すべての主要なプラットフォーム (iOS、Android、Windows、Windows Phone) でのゲームプレイ時間とユーザー維持率を向上させる |


##  <a name="startup-and-developer-resources"></a>新興企業と開発者向けのリソース

* [Microsoft for Startups](https://startups.microsoft.com)

    Microsoft for Startups は、新興企業の成長を支援するための製品、技術、および市場参入の利点を提供します。 特典の 1 つとして、Azure 無料アカウントの取得が含まれます。 30 日間サービスを利用できる 200 ドルのクレジット、12 か月間の人気の無料サービス、常に無料の 25 以上のサービスが提供されます。 詳細については、「[Azure の無料アカウントで新規事業のアイデアに命を吹き込む](https://azure.microsoft.com/free/startups/)」を参照してください。
    
* [開発者プログラム](e2e.md#developer-programs)

    Microsoft では、[ID@Xbox](https://www.xbox.com/Developers/id) や [Xbox Live クリエーターズ プログラム](https://developer.microsoft.com/games/xbox/xboxlive/creator)など、Windows ゲームの開発と公開に役立つ開発者向けプログラムを提供しています。

## <a name="learning-resources"></a>学習リソース

* //build 2016:[CodeLabs &mdash; Unity でゲームのスコアを保存するバックエンドを使用して Microsoft Azure App Service と Microsoft SQL Azure](https://github.com/Microsoft-Build-2016/CodeLabs-GameDev-6-Azure)
* //build 2017:[提供する世界クラスのゲームでは、Microsoft Azure を使用した操作性します。Halo、Hitman、Walking Dead (ビデオ) などのタイトルから学んだ教訓](https://channel9.msdn.com/Events/Build/2017/P4062)
* 構成要素、プロジェクト、サービス、および GitHub の Azure を使用して一般的なゲームのワークロードをサポートするためのベスト プラクティスの再利用可能なセット。[Azure でのゲームのための構成要素](https://github.com/MicrosoftDX/nether)
* [ゲーム サービス on Azure (ビデオ)](https://channel9.msdn.com/Series/Gaming-Services-on-Azure)

## <a name="tools-and-other-useful-links"></a>ツールとその他の役立つリンク

* [MSDN フォーラム&mdash;Azure プラットフォーム](https://social.msdn.microsoft.com/Forums/azure/home?category=windowsazureplatform)
* [クラウド ベースのロード テスト ツール](https://www.visualstudio.com/team-services/cloud-load-testing/)
* [Sdk とコマンド ライン ツール](https://azure.microsoft.com/downloads/)
    
## <a name="software-as-a-service-for-game-backend"></a>ゲームのバックエンド向けのサービスとしてのソフトウェア

[Playfab](https://playfab.com/) では、現在、1,200 以上のライブ ゲームを提供しており、毎月 8,000 万人のアクティブ プレイヤーがゲームをプレイしています。 これは、フル スタックの LiveOps とリアルタイム コントロールを含む、優れたバックエンド プラットフォームです。 

SDK を使用して、このソリューションを、モバイル、PC、または本体のゲームに統合できます。 Android、iOS、Unreal、Unity、Windows など、すべての一般的なゲーム エンジンとプラットフォーム用に SDK が用意されています。 開始するには、[ドキュメント](https://api.playfab.com/)をご覧ください。

ゲームのユーザー数の拡大を支援するために、認証、プレイヤー データの管理、マルチプレイヤー、リアルタイム分析などのゲーム サービスを提供します。 リアルタイム データ パイプラインと LiveOps の機能を活用し、カスタマイズしたゲーム内アイテム、イベント、プロモーションを提供することでユーザーのエンゲージメントを向上させます。 A/B テストの実施、レポートの生成、プッシュ通知の送信などの機能も利用できます。 

マイクロソフトでは、常に新しい機能を導入、追加しています。 詳細については、[機能に関するページ](https://playfab.com/features/)を参照してください。価格については、[ユーザーの規模に応じた単純な価格に関するページ](https://playfab.com/pricing/)を参照してください。

## <a name="related-links"></a>関連リンク

* [Windows 10 ゲーム開発ガイド](https://docs.microsoft.com/windows/uwp/gaming/e2e)
* [ゲーム用の azure](https://azure.microsoft.com/solutions/gaming/)
* [Playfab](https://playfab.com/)
* [Microsoft for Startups](https://startups.microsoft.com)
* [ID@Xbox](https://www.xbox.com/Developers/id)


 

 
