---
title: 深度のテストを使ったシーンのレンダリング
description: シャドウ効果を作成するには、頂点 (またはジオメトリ) シェーダーとピクセル シェーダーに深度のテストを追加します。
ms.assetid: bf496dfb-d7f5-af6b-d588-501164608560
ms.date: 02/08/2017
ms.topic: article
keywords: Windows 10、UWP、ゲーム、レンダリング、シーン、深度のテスト、Direct3D、シャドウ
ms.localizationpriority: medium
ms.openlocfilehash: d1c2c4e5d45b28c318085f4ce257b587f23f1426
ms.sourcegitcommit: ac7f3422f8d83618f9b6b5615a37f8e5c115b3c4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66368106"
---
# <a name="render-the-scene-with-depth-testing"></a><span data-ttu-id="14a08-104">深度のテストを使ったシーンのレンダリング</span><span class="sxs-lookup"><span data-stu-id="14a08-104">Render the scene with depth testing</span></span>




<span data-ttu-id="14a08-105">シャドウ効果を作成するには、頂点 (またはジオメトリ) シェーダーとピクセル シェーダーに深度のテストを追加します。</span><span class="sxs-lookup"><span data-stu-id="14a08-105">Create a shadow effect by adding depth testing to your vertex (or geometry) shader and your pixel shader.</span></span> <span data-ttu-id="14a08-106">パート 3 の[チュートリアル。Direct3d11 の深度バッファーを使用してボリュームをシャドウ実装](implementing-depth-buffers-for-shadow-mapping.md)します。</span><span class="sxs-lookup"><span data-stu-id="14a08-106">Part 3 of [Walkthrough: Implement shadow volumes using depth buffers in Direct3D 11](implementing-depth-buffers-for-shadow-mapping.md).</span></span>

## <a name="include-transformation-for-light-frustum"></a><span data-ttu-id="14a08-107">ライトの視錐台の変換の追加</span><span class="sxs-lookup"><span data-stu-id="14a08-107">Include transformation for light frustum</span></span>


<span data-ttu-id="14a08-108">頂点シェーダーで、各頂点の変換後のライト空間位置を計算する必要があります。</span><span class="sxs-lookup"><span data-stu-id="14a08-108">Your vertex shader needs to compute the transformed light space position for each vertex.</span></span> <span data-ttu-id="14a08-109">定数バッファーを使って、ライト空間のモデル、ビュー、プロジェクションの各マトリックスを提供します </span><span class="sxs-lookup"><span data-stu-id="14a08-109">Provide the light space model, view, and projection matrices using a constant buffer.</span></span> <span data-ttu-id="14a08-110">また、この定数バッファーを使って、照明計算用にライトの位置と法線を提供することもできます。</span><span class="sxs-lookup"><span data-stu-id="14a08-110">You can also use this constant buffer to provide the light position and normal for lighting calculations.</span></span> <span data-ttu-id="14a08-111">ライト空間内の変換された位置は深度のテスト時に使います。</span><span class="sxs-lookup"><span data-stu-id="14a08-111">The transformed position in light space will be used during the depth test.</span></span>

```cpp
PixelShaderInput main(VertexShaderInput input)
{
    PixelShaderInput output;
    float4 pos = float4(input.pos, 1.0f);

    // Transform the vertex position into projected space.
    float4 modelPos = mul(pos, model);
    pos = mul(modelPos, view);
    pos = mul(pos, projection);
    output.pos = pos;

    // Transform the vertex position into projected space from the POV of the light.
    float4 lightSpacePos = mul(modelPos, lView);
    lightSpacePos = mul(lightSpacePos, lProjection);
    output.lightSpacePos = lightSpacePos;

    // Light ray
    float3 lRay = lPos.xyz - modelPos.xyz;
    output.lRay = lRay;
    
    // Camera ray
    output.view = eyePos.xyz - modelPos.xyz;

    // Transform the vertex normal into world space.
    float4 norm = float4(input.norm, 1.0f);
    norm = mul(norm, model);
    output.norm = norm.xyz;
    
    // Pass through the color and texture coordinates without modification.
    output.color = input.color;
    output.tex = input.tex;

    return output;
}
```

<span data-ttu-id="14a08-112">次に、ピクセル シェーダーでは、頂点シェーダーから提供された補完済みのライト空間位置を使って、ピクセルがシャドウ内かどうかをテストします。</span><span class="sxs-lookup"><span data-stu-id="14a08-112">Next, the pixel shader will use the interpolated light space position provided by the vertex shader to test whether the pixel is in shadow.</span></span>

## <a name="test-whether-the-position-is-in-the-light-frustum"></a><span data-ttu-id="14a08-113">位置がライトの視錐台内かどうかのテスト</span><span class="sxs-lookup"><span data-stu-id="14a08-113">Test whether the position is in the light frustum</span></span>


<span data-ttu-id="14a08-114">最初に、X 座標と Y 座標を正規化して、ピクセルがライトの視錐台内かどうかをチェックします。</span><span class="sxs-lookup"><span data-stu-id="14a08-114">First, check that the pixel is in the view frustum of the light by normalizing the X and Y coordinates.</span></span> <span data-ttu-id="14a08-115">場合は、範囲内でどちらも\[0, 1\]でシャドウするピクセルの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="14a08-115">If they are both within the range \[0, 1\] then it's possible for the pixel to be in shadow.</span></span> <span data-ttu-id="14a08-116">それ以外の場合は、深度のテストをスキップできます。</span><span class="sxs-lookup"><span data-stu-id="14a08-116">Otherwise you can skip the depth test.</span></span> <span data-ttu-id="14a08-117">シェーダーでは、[Saturate](https://docs.microsoft.com/windows/desktop/direct3dhlsl/saturate) を呼び出し、結果を元の値と比較することで、これをすばやくテストできます。</span><span class="sxs-lookup"><span data-stu-id="14a08-117">A shader can test for this quickly by calling [Saturate](https://docs.microsoft.com/windows/desktop/direct3dhlsl/saturate) and comparing the result against the original value.</span></span>

```cpp
// Compute texture coordinates for the current point's location on the shadow map.
float2 shadowTexCoords;
shadowTexCoords.x = 0.5f + (input.lightSpacePos.x / input.lightSpacePos.w * 0.5f);
shadowTexCoords.y = 0.5f - (input.lightSpacePos.y / input.lightSpacePos.w * 0.5f);
float pixelDepth = input.lightSpacePos.z / input.lightSpacePos.w;

float lighting = 1;

// Check if the pixel texture coordinate is in the view frustum of the 
// light before doing any shadow work.
if ((saturate(shadowTexCoords.x) == shadowTexCoords.x) &&
    (saturate(shadowTexCoords.y) == shadowTexCoords.y) &&
    (pixelDepth > 0))
{
```

## <a name="depth-test-against-the-shadow-map"></a><span data-ttu-id="14a08-118">シャドウ マップに対する深度のテスト</span><span class="sxs-lookup"><span data-stu-id="14a08-118">Depth test against the shadow map</span></span>


<span data-ttu-id="14a08-119">サンプル比較関数 ([SampleCmp](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplecmp) または [SampleCmpLevelZero](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplecmplevelzero)) を使って、深度マップに対するライト空間内のピクセルの深度をテストします。</span><span class="sxs-lookup"><span data-stu-id="14a08-119">Use a sample comparison function (either [SampleCmp](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplecmp) or [SampleCmpLevelZero](https://docs.microsoft.com/windows/desktop/direct3dhlsl/dx-graphics-hlsl-to-samplecmplevelzero)) to test the pixel's depth in light space against the depth map.</span></span> <span data-ttu-id="14a08-120">正規化されたライト空間の深度値 (`z / w`) を計算し、その値を比較関数に渡します。</span><span class="sxs-lookup"><span data-stu-id="14a08-120">Compute the normalized light space depth value, which is `z / w`, and pass the value to the comparison function.</span></span> <span data-ttu-id="14a08-121">サンプラーでは LessOrEqual 比較テストを使うため、比較テストに合格すると組み込みメソッドの関数は 0 を返します。これは、そのピクセルがシャドウの内側にあることを示しています。</span><span class="sxs-lookup"><span data-stu-id="14a08-121">Since we use a LessOrEqual comparison test for the sampler, the intrinsic function returns zero when the comparison test passes; this indicates that the pixel is in shadow.</span></span>

```cpp
// Use an offset value to mitigate shadow artifacts due to imprecise 
// floating-point values (shadow acne).
//
// This is an approximation of epsilon * tan(acos(saturate(NdotL))):
float margin = acos(saturate(NdotL));
#ifdef LINEAR
// The offset can be slightly smaller with smoother shadow edges.
float epsilon = 0.0005 / margin;
#else
float epsilon = 0.001 / margin;
#endif
// Clamp epsilon to a fixed range so it doesn't go overboard.
epsilon = clamp(epsilon, 0, 0.1);

// Use the SampleCmpLevelZero Texture2D method (or SampleCmp) to sample from 
// the shadow map, just as you would with Direct3D feature level 10_0 and
// higher.  Feature level 9_1 only supports LessOrEqual, which returns 0 if
// the pixel is in the shadow.
lighting = float(shadowMap.SampleCmpLevelZero(
    shadowSampler,
    shadowTexCoords,
    pixelDepth + epsilon
    )
    );
```

## <a name="compute-lighting-in-or-out-of-shadow"></a><span data-ttu-id="14a08-122">シャドウの内側または外側の照明の計算</span><span class="sxs-lookup"><span data-stu-id="14a08-122">Compute lighting in or out of shadow</span></span>


<span data-ttu-id="14a08-123">ピクセルがシャドウの内側にない場合は、ピクセル シェーダーは直接照明を計算し、それをピクセル値に追加します。</span><span class="sxs-lookup"><span data-stu-id="14a08-123">If the pixel is not in shadow, the pixel shader should compute direct lighting and add it to the pixel value.</span></span>

```cpp
return float4(input.color * (ambient + DplusS(N, L, NdotL, input.view)), 1.f);
```

```cpp
float3 DplusS(float3 N, float3 L, float NdotL, float3 view)
{
    const float3 Kdiffuse = float3(.5f, .5f, .4f);
    const float3 Kspecular = float3(.2f, .2f, .3f);
    const float exponent = 3.f;

    // Compute the diffuse coefficient.
    float diffuseConst = saturate(NdotL);

    // Compute the diffuse lighting value.
    float3 diffuse = Kdiffuse * diffuseConst;

    // Compute the specular highlight.
    float3 R = reflect(-L, N);
    float3 V = normalize(view);
    float3 RdotV = dot(R, V);
    float3 specular = Kspecular * pow(saturate(RdotV), exponent);

    return (diffuse + specular);
}
```

<span data-ttu-id="14a08-124">それ以外の場合は、アンビエント照明を使ってピクセル値を計算します。</span><span class="sxs-lookup"><span data-stu-id="14a08-124">Otherwise, the pixel shader should compute the pixel value using ambient lighting.</span></span>

```cpp
return float4(input.color * ambient, 1.f);
```

<span data-ttu-id="14a08-125">このチュートリアルの次のパートでは、[ハードウェアの範囲でシャドウ マップをサポートする](target-a-range-of-hardware.md)方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="14a08-125">In the next part of this walkthrough, learn how to [Support shadow maps on a range of hardware](target-a-range-of-hardware.md).</span></span>

 

 




