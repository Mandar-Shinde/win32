---
Description: 'To compose to the screen or perform floating-point operations, you need to work in the correct color space.'
ms.assetid: '1DD8E2D3-430F-4EE4-9C41-78736C904920'
title: Converting data for the color space
---

# Converting data for the color space

To compose to the screen or perform floating-point operations, you need to work in the correct color space. We recommend that you perform floating point operations in a linear color space. Then, to present your images to the screen, convert the data to standard RGB data (sRGB, gamma 2.2-corrected) color space. Presenting to the screen in sRGB color space is important for color accuracy. If images are not gamma 2.2-corrected, they allocate too many bits or too much bandwidth to highlights that people can't differentiate, and too few bits or bandwidth to shadow values that people are sensitive to, and so would require more bits or bandwidth to maintain the same visual quality. Therefore, to ensure the best color accuracy, present images to the screen that are gamma 2.2-corrected.

-   [Color accuracy](#color-accuracy)
-   [Related topics](#related-topics)

## Color accuracy

For presentation, integer-valued display formats (such as [**DXGI\_FORMAT\_B8G8R8A8\_UNORM\_SRGB**](https://msdn.microsoft.com/library/windows/desktop/bb173059#dxgi-format-b8g8r8a8-unorm-srgb), [**DXGI\_FORMAT\_R10G10B10\_XR\_BIAS\_A2\_UNORM**](https://msdn.microsoft.com/library/windows/desktop/bb173059#dxgi-format-r10g10b10-xr-bias-a2-unorm), and so on) always contain sRGB gamma-corrected data. Float-valued display formats (currently only [**DXGI\_FORMAT\_R16G16B16A16\_FLOAT**](https://msdn.microsoft.com/library/windows/desktop/bb173059#dxgi-format-r16g16b16a16-float)) contain linear-valued data.

The \_SRGB [format modifier](https://msdn.microsoft.com/library/windows/desktop/bb173059#format-modifiers) indicates to the operating system to help the app place sRGB data on the screen. The app must always place sRGB data into back buffers with integer-valued formats to present the sRGB data to the screen, even if the data doesn't have this format modifier in its format name. For a complete list of display scan-out formats:

-   [DXGI Format Support for Direct3D Feature Level 12.1 Hardware](hardware-support-for-direct3d-12-1-formats.md)
-   [DXGI Format Support for Direct3D Feature Level 12.0 Hardware](hardware-support-for-direct3d-12-0-formats.md)
-   [DXGI Format Support for Direct3D Feature Level 11.1 Hardware](format-support-for-direct3d-11-1-feature-level-hardware.md)
-   [DXGI Format Support for Direct3D Feature Level 11.0 Hardware](format-support-for-direct3d-11-0-feature-level-hardware.md)
-   [Hardware Support for Direct3D 10Level9 Formats](https://msdn.microsoft.com/library/windows/desktop/ff471324)
-   [Hardware Support for Direct3D 10.1 Formats](https://msdn.microsoft.com/library/windows/desktop/cc627091)
-   [Hardware Support for Direct3D 10 Formats](https://msdn.microsoft.com/library/windows/desktop/cc627090)

When you write floating-point output values from the pixel shader into render-target views (**RenderTargetView**s) with the \_SRGB [format modifier](https://msdn.microsoft.com/library/windows/desktop/bb173059#format-modifiers) that are bound to the [pipeline](https://msdn.microsoft.com/library/windows/desktop/ff476882), you convert them to gamma 2.2-corrected color space. Similarly, when shader-resource views (**ShaderResourceView**s) with the \_SRGB format modifier are bound to the pipeline, you convert the values from gamma 2.2-corrected color space to linear color space when you read them from the **ShaderResourceView**s. The shader can then perform operations on them.

For example, use code similar to this to write floating-point output values from a shader into a **RenderTargetView** format:


```
struct PSOut
{
    float4 color : SV_Target;
};

PSOut S( PSIn input )
{
    PSOut output;
    output.color = float4( 1.0, 0.0, 0.0, 1.0 );
    return output;
}
```



When the 'S' routine returns, the floating point (1, 0, 0, 1) values are converted to the **RenderTargetView** format. Then, if you assign the \_SRGB [format modifier](https://msdn.microsoft.com/library/windows/desktop/bb173059#format-modifiers) to the **RenderTargetView**, the gamma conversion occurs.

These are steps to follow to ensure that the content that is displayed on the screen has the best color accuracy.

**To ensure color accuracy in the pipeline**

1.  If a texture has sRGB content, ensure the **ShaderResourceView** has the \_SRGB [format modifier](https://msdn.microsoft.com/library/windows/desktop/bb173059#format-modifiers) so when you read from the **ShaderResourceView** into the shader, you convert the texture content from gamma 2.2-corrected color space to linear color space.
2.  Ensure the **RenderTargetView** also has the \_SRGB [format modifier](https://msdn.microsoft.com/library/windows/desktop/bb173059#format-modifiers) so the shader output values are gamma converted.

If you follow the preceding steps, when you call the [**IDXGISwapChain1::Present1**](idxgiswapchain1-present1.md) method, the content that is displayed on the screen has the best color accuracy.

You can use the [**ID3D11Device::CreateRenderTargetView**](https://msdn.microsoft.com/library/windows/desktop/ff476517) method to create **DXGI\_FORMAT\_\*\_SRGB** views on back buffers from a swap chain that you create only with a **DXGI\_FORMAT\_\*\_UNORM** format. This is a special exception to the rule for creating render-target views, which states that you can use a different format with **ID3D11Device::CreateRenderTargetView** only if you created the resource that you want to view with **DXGI\_FORMAT\_\*\_TYPELESS**.

For more info about rules for converting data, see [Data Conversion Rules](https://msdn.microsoft.com/library/windows/desktop/dd607323).

For info about how to simultaneously both read from and write to a texture, see [Unpacking and Packing DXGI\_FORMAT for In-Place Image Editing](https://msdn.microsoft.com/library/windows/desktop/ff728749).

## Related topics

<dl> <dt>

[Enhancing presentation with the flip model, dirty rectangles, and scrolled areas](dxgi-1-2-presentation-improvements.md)
</dt> </dl>

 

 


