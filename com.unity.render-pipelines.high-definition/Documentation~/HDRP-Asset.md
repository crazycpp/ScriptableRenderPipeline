# The High Definition Render Pipeline Asset

The High Definition Render Pipeline (HDRP) Asset controls the global rendering settings of your Project and creates an instance of the rendering pipeline. A rendering pipeline instance contains intermediate resources and an implementation of the render pipeline. 

Unity does not allocate memory or build Shader variants for disabled features in your HDRP Asset. This means that you can disable settings that you are not using to save memory, but you can not enable disabled features at run time. You can toggle enabled features at run time on a per-Camera basis using [Frame-Settings](Frame-Settings.html).

## Creating an HDRP Asset

A new Project using the HDRP template includes an HDRP Asset file named HDRenderPipelineAsset in the Assets/Settings folder.

If you [upgrade a Project to HDRP](Upgrading-To-HDRP.html) and therefore do not use the HDRP template, you need to add an HDRP Asset to your Project. To create and customize an HDRP Asset:

1. In the Unity Editor, go to the Project window and navigate to the folder you want to create your HDRP Asset in. This folder must be inside the **Assets** folder; you can not create Assets in the **Packages** folder.
2. In the main menu, go to **Assets > Create > Rendering** and click **High Definition Render Pipeline Asset**.
3. Enter a name for the **HDRP Asset** and press the Return key to confirm it.

When you have created an HDRP Asset, you must assign it it to the pipeline:

1. Navigate to **Edit > Project Settings > Graphics** and locate the **Scriptable Render Pipeline Settings** property at the top.
2. Either drag and drop the HDRP Asset into the property field, or use the object picker (located on the right of the field) to select it from a list of all HDRP Assets in your Project.

Unity now uses the High Definition Render Pipeline (HDRP) in your Unity Project. HDRP does not support gamma space, so your Project must use linear color space, To do this:

1. Navigate to **Edit > Project Settings > Player > Other Settings** and locate the **Color Space** property.
2. Select **Linear** from the **Color Space** drop-down.

You can create multiple HDRP Assets containing different settings. This is useful for Project that support multiple platforms, such as PC, Xbox One and PlayStation 4. In each HDRP Asset, you can change settings to suite the hardware of each platform and then assign the relevant one when building your Project for each platform.

To change the HDRP Asset your render pipeline uses, either manually select an HDRP Asset in the Graphics Settings window (as shown above), or  use the GraphicsSettings.renderPipelineAsset property via script.

When you create an HDRP Asset, open it in the Inspector to edit its properties. 

## Rendering

| **Property**                            | **Description**                                              |
| --------------------------------------- | ------------------------------------------------------------ |
| **Lit Shader Mode**                     | Use the drop-down to choose which mode HDRP uses for the [Lit Shader](Lit-Shader.html).<br />&#8226; **Forward Only**: forces HDRP to only use forward rendering for Lit Shaders.<br />&#8226; **Deferred Only**: forces HDRP to use deferred rendering for Lit Shaders (HDRP still renders advanced Materials using forward rendering).<br />&#8226; **Both**: allows the Camera to use deferred and forward rendering.<br /><br />Select **Both** to allow you to switch between forward and deferred rendering for Lit Shaders at run time per Camera. Selecting a specific mode reduces build time and Shader memory because HDRP requires less Shader variants, but it is not possible to switch from one mode to the other at run time. |
| **- Multisample Anti-aliasing Quality** | Use the drop-down to set the number of samples HDRP uses for multisample anti-aliasing (MSAA). The larger the sample count, the better the quality. Select **None** to disable MSAA.<br />This property is only visible when **Lit Shader Mode** is set to **Forward Only** or **Both**. |
| **Motion Vectors**                      | Enable the checkbox to make HDRP support motion vectors. HDRP uses motion vectors for effects like screen space reflection (SSR) and motion blur. When disabled, motion blur has no effect and HDRP calculates SSR with lower quality. |
| **Runtime Debug Display**               | Enable the checkbox to make HDRP display Material and Lighting properties at run time to help debugging.Disable this checkbox to reduce build time and Shader memory. This disables the following debug modes: All Material debug modes except GBuffer debug. The Lux meter, diffuse lighting only, and specular lighting only debug modes. The overriding option for overriding albedo. |
| **Dithering Cross-fade**                | Enable the checkbox to make HDRP support dithering cross fade. This allows HDRP to implement smooth transitions between a GameObject’s LOD levels. When disabled, this reduces build time if you are not using LOD fade. |
| **Transparent Backface**                | Enable the checkbox to make HDRP support transparent back-face render passes. If your Unity Project does not need to make a transparent back-face pass, disable this checkbox to reduce build time. |
| **Transparent Depth Prepass**           | Enable the checkbox to make HDRP support transparent depth render prepasses. If your Unity Project does not need to make a transparent depth prepass, disable this checkbox to reduce build time . |
| **Transparent Depth Postpass**          | Enable the checkbox to make HDRP support transparent depth render postpasses. If your Unity Project does not make use of a transparent depth postpass. Uncheck this checkbox to reduce build time . |
| **Custom Pass**                         | Enable the checkbox to make HDRP support custom passes. If your Unity Project does not make use [Custom Passes](Custom-Pass.html), Uncheck this checkbox to save memory . |
| - **Custom Buffer Format**                | Specify the texture format for the custom buffer. If you experience banding issues due to your custom passes, you can change it to either `R11G11B10` if you don't need alpha or `R16G16B16A16`. |
| **Realtime Raytracing (Preview)**       | Enable the checkbox to enable HDRP realtime ray tracing (Experimental). It requires to have ray tracing compatible hardware. For more information, please refer to the [Ray Tracing Getting Started](Ray-Tracing-Getting-Started.html#HardwareRequirements) page. |
| **Raytracing Tier**                     | Select the active tier for ray tracing effects. For more information, please refer to the [Ray Tracing Tier Table](Ray-Tracing-Getting-Started.html#TierTable). |
| - **LOD Bias**                          | Set the value that Cameras use to calculate their LOD bias. The Camera uses this value differently depending on the **LOD Bias Mode** you select. |
| - **Maximum LOD Level**                 | Set the value that Cameras use to calculate their maximum level of detail. The Camera uses this value differently depending on the **Maximum LOD Level Mode** you select. |

<a name="Decals"></a>

### Decals

These settings control the draw distance and resolution of the decals atlas that HDRP uses when it renders decals projected onto transparent surfaces.

| **Property**                                 | **Description**                                              |
| -------------------------------------------- | ------------------------------------------------------------ |
| **Enable**                                   | Enable the checkbox to make HDRP support decals in your Unity Project. |
| **- Draw Distance**                          | The maximum distance from the Camera at which Unity draws Decals. |
| **- Atlas Width**                            | The Decal Atlas width. This atlas stores all decals that project onto transparent surfaces. |
| **- Atlas Height**                           | The Decal Atlas height. This atlas stores all decals that project onto transparent surfaces. |
| **- Metal and Ambient Occlusion properties** | Enable the checkbox to allow decals to affect metallic and ambient occlusion Material properties. Enabling this feature has a performance impact. |
| **- Maximum** **Decals on Screen**           | The maximum number of decals you can have on screen at one time. |

<a name="DynamicResolution"></a>

### Dynamic Resolution

| **Property**                    | **Description**                                              |
| ------------------------------- | ------------------------------------------------------------ |
| **Enable**                      | Enable the checkbox to make HDRP support dynamic resolution in your Unity Project. |
| **- Dynamic Resolution Type**   | Use the drop-down to select the type of dynamic resolution HDRP uses:<br />&#8226; **Software**: This option allocates render targets to accommodate the maximum resolution possible, then rescales the viewport accordingly. This allows the viewport to render at varying resolutions. |
| **- Upscale Filter**            | Use the drop-down to select the filter that HDRP uses for upscaling.<br />&#8226; **Bilinear**: A low quality upsample. The least resource intensive option.<br />&#8226; **Catmull-Rom**: A bicubic upsample with 4 taps.<br />&#8226; **Lanczos**: A sharp upsample. This method can potentially introduce artifacts so you should not use it for extreme upsampling cases for example, when the screen percentage is less than 50%. |
| **- Minimum Screen Percentage** | The minimum screen percentage that dynamic resolution can reach. |
| **- Maximum Screen Percentage** | The maximum screen percentage that dynamic resolution can reach. This value must be higher than the **Min Screen Percentage**. |
| **- Force Screen Percentage**   | Enable the checkbox to force HDRP to use a specific screen percentage for dynamic resolution. This feature is useful for debugging dynamic resolution. |
| **- Forced Screen Percentage**  | The specific screen percentage that HDRP uses for dynamic resolution. This property is only visible when you enable the **Force Screen Percentage**.. |



## Lighting

| **Property**                       | **Description**                                              |
| ---------------------------------- | ------------------------------------------------------------ |
| **Screen Space Ambient Occlusion** | Enable the checkbox to make HDRP support screen space ambient occlusion (SSAO). SSAO is a technique for approximating ambient occlusion efficiently in real time. |
| **Volumetrics**                    | Enable the checkbox to make HDRP support volumetrics. This allows you to use **Volumetric Fog** for the **Fog Type** in the [Visual Environment](Override-Visual-Environment.html). |
| **- high quality**                 | Enable the checkbox to increase the resolution of volumetrics. This increases the quality of fog effects, but increases the resource intensity greatly. |
| **Light Layers**                   | Enable the checkbox to make HDRP support Light Layers. You can assign a Layer to a Light which then only lights up Mesh Renderers with a matching rendering Layer. |

### Light Layers

Light Layers are used to separate lighting into different layers in order to make object only reacting to certain lights.

| **Property**           | **Description**                                              |
| ---------------------- | ------------------------------------------------------------ |
| **Enable**             | Enable the checkbox to make HDRP support Light Layers. You can assign a Layer to a Light which then only lights up Mesh Renderers with a matching rendering Layer. |
| **Light Layer Name i** | The name displayed on light and meshes when using this HDRenderPipelineAsset. |

### Cookies

Use the Cookie settings to configure the maximum resolution of individual cookies and the maximum resolution of cookie texture arrays that define the number of cookies on screen at one time. Larger sizes use more memory, but result in higher quality images.

| **Property**           | **Description**                                              |
| ---------------------- | ------------------------------------------------------------ |
| **Cookie Size**        | Use the drop-down to select the maximum individual cookie size for 2D cookies. HDRP uses 2D cookies for Directional and Spot Lights. |
| **Texture Array Size** | The maximum Texture Array size for the 2D cookies that HDRP uses for Directional and Spot Lights. Increase this to make HDRP support a greater number of 2D cookies concurrently on screen. |
| **Point Cookie Size**  | Use the drop-down to select the maximum[ Point Cookie](https://docs.unity3d.com/Manual/Cookies.html) size for cubemap cookies. HDRP uses cubemap cookies for Point Lights. |
| **Cubemap Array Size** | The maximum cube map Array size for the Cube cookies that HDRP uses for Point Lights. Increase this to make HDRP support a greater number of cube map cookies concurrently on screen. |

### Reflections

Use the Reflection settings to configure the resolution of your reflections and whether Unity should compress the Reflection Probe caches or not.

| **Property**                               | **Description**                                              |
| ------------------------------------------ | ------------------------------------------------------------ |
| **Screen Space Reflection**                | Enable the checkbox to make HDRP support [screen space reflection](https://docs.unity3d.com/Manual/PostProcessing-ScreenSpaceReflection.html). SSR is a technique for calculating reflections by reusing screen space data. |
| **Compress Reflection Probe Cache**        | Enable the checkbox to compress the [Reflection Probe](Reflection-Probe.html) cache in order to save space on disk. |
| **Reflection Cubemap Size**                | Use the drop-down to select the maximum resolution of individual Reflection Probe[ ](https://docs.unity3d.com/Manual/class-Cubemap.html)[cubemaps](https://docs.unity3d.com/Manual/class-Cubemap.html). |
| **Probe Cache Size**                       | The maximum size of the Probe Cache. Defines how many Probe cube maps HDRP can save in cache. |
| **Compress Planar Reflection Probe Cache** | Enable the checkbox to compress the [Planar Reflection Probe](Planar-Reflection-Probe.html) cache in order to save space on disk. |
| **Planar Reflection Texture Size**         | Use the drop-down to select the maximum resolution of individual Planar Reflection textures. |
| **Planar Probe Cache Size**                | The maximum size of the Planer Reflection Probe cache. Defines how many Probe textures HDRP can save in cache. |
| **Maximum Environment Lights on Screen**   | The maximum number of environment Lights HDRP can manage on screen at once. |

<a name="SkyLighting"></a>

### Sky

These settings control skybox reflections and skybox lighting.

| **Property**               | **Description**                                              |
| -------------------------- | ------------------------------------------------------------ |
| **Reflection Size**        | Use the drop-down to select the maximum resolution of the cube map HDRP uses to manage fallback reflection when no local reflection probes are present. This property has no effect on the quality of the sky itself. |
| **Lighting Override Mask** | Use the drop-down to select the [Volume](Volumes.html) layer mask HDRP uses to override sky lighting. Use this to decouple the display sky and lighting. See the [Environment Lighting](Environment-Lighting.html#DecoupleVisualEnvironment) for information on how to decouple environment lighting from the sky background. |

### Shadow

These settings adjust the size of the shadowmask. Smaller values causes Unity to discard more distant shadows, while higher values lead to Unity displaying more shadows at longer distances from the Camera.

| **Property**                     | **Description**                                              |
| -------------------------------- | ------------------------------------------------------------ |
| **Shadowmask**                  | Enable the checkbox to make HDRP support the [Shadowmask lighting mode](Lighting-Mode-Shadowmask.html) in your Unity Project. |
| **Maximum** **Shadow on Screen** | The maximum number of shadows you can have in view. A Spot Light casts a single shadow, a Point Light casts six shadows, and a Directional Light casts shadows equal to the number of cascades defined in the [HD Shadow Settings](Override-Shadows.html) override. |
| **Filtering Quality**            | Use the drop-down to select the filtering quality for shadows. Higher values increase the shadow quality in HDRP as better filtering near the edges of shadows reduce aliasing effects. Shadow quality only works for Cameras that use [forward rendering](Forward-And-Deferred-Rendering.html). **Deferred** mode uses Medium.<br />To edit this property, select **Both** or **Forward Only** from the **Lit Shader Mode** drop-down. For information on each filtering quality preset, see the [Filtering Qualities table](#FilteringQualities). |
| **Screen Space Shadows**         | Enable the checkbox to allow HDRP to compute shadows in a separate pass and store them in a screen-aligned Texture. |
| - **Maximum**                    | Set the maximum number of screen space shadows that HDRP can handle. |

<a name="ShadowMapSettings"></a>

The following sections allow you to customize the shadow atlases and individual shadow resolution tiers for each type of Light in HDRP. Shadow resolution tiers are useful because, instead of defining the shadow resolution for each individual Light as a number, you can assign a numbered resolution to a named shadow resolution tier then use the named tier instead of rewriting the number. For example, instead of setting the resolution of each Light to 512, you could say that **Medium** resolution shadows have a resolution of 512 and then set the shadow quality of each Light to be **Medium**. This way, you can more easily have consistent shadow quality across your HDRP Project.

The three sections here are:

- **Directional Light Shadows**
- **Punctual Light Shadows**
- **Area Light Shadows**

They all share the same properties, except **Directional Light Shadows** which does not include **Resolution** or **Dynamic Rescale**.

| **Property**        | **Description**                                              |
| ------------------- | ------------------------------------------------------------ |
| ***Light Atlas***   |                                                              |
| **Resolution**      | Use the drop-down to select the resolution of the shadow atlas. |
| **Precision**       | Use the drop-down to select the precision of the shadow map. This sets the bit depth of each pixel of the shadow map. **16 bit** is faster and uses less memory at the expense of precision. |
| **Dynamic Rescale** | Enable the checkbox to allow HDRP to rescale the shadow atlas if all the shadows on the screen don’t currently fit onto it. |

| ***Shadow Resolution Tiers*** |                                                              |
| ----------------------------- | ------------------------------------------------------------ |
| **L**                         | Set the resolution of shadows set to this quality. Light's with their **Resolution** set to **Low** use this resolution for their shadows. |
| **M**                         | Set the resolution of shadows set to this quality. Light's with their **Resolution** set to **Medium** use this resolution for their shadows. |
| **H**                         | Set the resolution of shadows set to this quality. Light's with their **Resolution** set to **High** use this resolution for their shadows. |
| **U**                         | Set the resolution of shadows set to this quality. Light's with their **Resolution** set to **Ultra** use this resolution for their shadows. |
| **Maximum Shadow Resolution** | Set the maximum resolution of any shadow map of this Light type. If you set any shadow resolution to a value higher than this, HDRP clamps it to this value. |

<a name="FilteringQualities"></a>

#### Filtering Qualities

| **Filtering Quality** | **Algorithm**                                                |
| --------------------- | ------------------------------------------------------------ |
| **Low**               | &#8226; **Point/Spot Lights**: Percentage Closer Filtering (PCF) 3x3 (4 taps).<br />&#8226; **Directional Lights**: PCF Tent 5x5 (9 taps).<br />&#8226; **Area Lights**: EVSM. |
| **Medium**            | &#8226; **Point/Spot Lights**: PCF 5x5 (9 taps).<br />&#8226; **Directional Lights**: PCF Tent 5x5 (9 taps).<br />&#8226; **Area Lights**: EVSM. |
| **High**              | &#8226;**Point/Spot/Directional Lights**: Percentage Closer Soft Shadow (PCSS). You can change the sample count to decrease the quality of these shadows. This decreases the resource intensity of this algorithm. To change the sample count for shadows cast by that Light, set the **Filter Sample Count** in the Inspector of each Light component.<br /><br />**Note**: The softness of PCSS shadows is defined by the shape radius of Point and Spot Lights, and by the angular diameter of Directional Lights.<br />&#8226; **Area Lights**: EVSM. |

The PCF algorithm applies a fixed size blur. PCSS applies a different blur size depending on the distance between the shadowed pixel and the shadow caster. This results in a more realistic shadow, that is also more resource intensive to compute.

### Light Loop

Use these settings to enable or disable settings relating to lighting in HDRP.

| **Property**                      | **Description**                                              |
| --------------------------------- | ------------------------------------------------------------ |
| **Maximum Directional On Screen** | The maximum number of Directional Lights HDRP can manage on screen at once. |
| **Maximum Punctual On Screen**    | The maximum number of [Point and Spot Lights](Glossary.html#PunctualLight) HDRP can manage on screen at once. |
| **Maximum Area On Screen**        | The maximum number of area Lights HDRP can manage on screen at once. |

## Material

| **Property**                    | **Description**                                              |
| ------------------------------- | ------------------------------------------------------------ |
| **Distortion**                  | Enable the checkbox to make HDRP support distortion. If your Unity Project does not use distortion, disable this checkbox to reduce build time. |
| **Subsurface Scattering**       | Enable the checkbox to make HDRP support subsurface scattering (SSS). SSS describes light penetration of the surface of a translucent object |
| **- High Quality**             | Enable the checkbox to increase the SSS Sample Count and enable high quality subsurface scattering. Increasing the sample count greatly increases the performance cost of the Subsurface Scattering effect. |
| **Fabric BSDF Convolution** | By default, Fabric Materials reuse the Reflection Probes that HDRP calculates for the Lit Shader (GGX BRDF). Enable the checkbox to make HDRP calculate another version of each Reflection Probe for the Fabric Shader, creating more accurate lighting effects. This increases the resource intensity because HDRP must condition two Reflection Probes instead of one. It also reduces the number of visible Reflection Probes in the current view by half because the size of the cache that store Reflection Probe data does not change and now must store both versions of each Reflection Probe. |
| **Diffusion Profile List**      | Assign __Diffusion Profiles__ to this list to store Subsurface Scattering and Transmission profiles for your Project. To create a Diffusion Profile Asset, navigate to **Assets > Create > Rendering** and click **Diffusion Profile**. |

## Post-processing

| **Property**           | **Description**                                              |
| ---------------------- | ------------------------------------------------------------ |
| **Grading LUT Size**   | The size of the internal and external color grading lookup textures (LUTs). This size is fixed for the Project. You can not mix and match LUT sizes, so decide on a size before you start the color grading process. The default value, **32**, provides a good balance of speed and quality. |
| **Grading LUT Format** | Use the drop-down to select the format to encode the color grading LUTs with. Lower precision formats are faster and use less memory at the expense of color precision. These formats directly map to their equivalent in the built-in [GraphicsFormat](https://docs.unity3d.com/ScriptReference/Experimental.Rendering.GraphicsFormat.html) enum value. |

