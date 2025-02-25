---
title: ARM での x86 および ARM32 エミュレーションのしくみ
description: ARM での x86 アプリのエミュレーションの概要。
ms.date: 02/15/2018
ms.topic: article
keywords: windows 10 s, 常時接続, ARM での x86 エミュレーション
ms.localizationpriority: medium
ms.openlocfilehash: 31f6a41d678cde146884a45aec24cae2d47597a4
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66372852"
---
# <a name="how-x86-emulation-works-on-arm"></a>ARM での x86 エミュレーションのしくみ
x86 アプリのエミュレーションにより、Win32 アプリのリッチなエコシステムが ARM で利用できるようになります。 これにより、アプリに変更を加えなくても、ユーザーが既存の x86 win32 アプリを問題なく実行できるようになります。 アプリは、固有の API ([IsWoW64Process2](https://docs.microsoft.com/windows/desktop/api/wow64apiset/nf-wow64apiset-iswow64process2)) を呼び出すことを除いて、ARM PC の Windows で実行されていることを認識することもありません。

Windows 10 の [WOW64](https://msdn.microsoft.com/en-us/library/windows/desktop/aa384249(v=vs.85).aspx) レイヤーを使うと、ARM64 バージョンの Windows 10 で x86 コードを実行できます。 x86 エミュレーションは、パフォーマンスを高める最適化によって x86 命令のブロックを ARM64 命令にコンパイルすることで機能します。 サービスは、変換されたこれらのコード ブロックをキャッシュして命令変換のオーバーヘッドを減らし、コードをもう一度実行するときの最適化を実現します。 キャッシュはモジュールごとに生成されるため、他のアプリが初回起動時にそれらを使うことができます。 

これらのテクノロジについて詳しくは、[ARM 版 Windows 10](https://channel9.msdn.com/Events/Build/2017/P4171) Channel9 ビデオをご覧ください。 