# Render Pipeline Debug

The **Render Pipeline Debug** window is a specific window for the Scriptable Render Pipeline that contains debugging and visualization tools. You can use these tools to quickly understand and solve any issues you might encounter. It contains mostly graphics-related tools but you can extend it to include tools for any other field, such as animation. The **Render Pipeline Debug** window separates debug items into different sections as follows:

- [Decals](#DecalsPanel)
- [Display Stats](#StatsPanel)
- [Material](#MaterialPanel)
- [Lighting](#LightingPanel)
- [Rendering](#RenderingPanel)
- [Camera](#CameraPanel)

![](Images/RenderPipelineDebug1.png)

The Render Pipeline Debug window.

## Using the Render Pipeline Debug window

To open the Render Pipeline Debug window in the Editor, go to  **Window > Render Pipeline > Render Pipeline Debug**. You can also open this window at run time in Play Mode, or in the standalone Unity Player on any device on **Development build**. Use the keyboard shortcut Ctrl+Backspace (command+Backspace on macOS) or press L3 and R3 (Left Stick and Right Stick) on a controller to open the window.

You can display read-only items such as the FPS counter independently of the **Render Pipeline Debug** window. This means that when you disable the **Render Pipeline Debug** window, they are still visible in the top right corner of the screen. This is particularly useful if you want to track particular values without cluttering the screen.

### Navigation at run time

To change the current active item:

- **Keyboard**: Use the arrow keys.
- **Xbox controller**: Use the Directional pad (D-Pad).
- **PlayStation controller**: Use the Directional buttons.

To change the current tab:

- **Keyboard**: Use the Page up and Page down keys.
- **Xbox controller**: Use the Left Bumper and Right Bumper.
- **PlayStation controller**: Use the L1 button and R1 button.

To display the current active item independently of the debug window:

- **Keyboard**: Press the right Shift key.
- **Xbox controller**: Press the X button.
- **PlayStation controller**: Press the Square button.

<a name="DecalsPanel"></a>

## Decals panel

The **Decals** panel has tools that you can use to debug [decals](Decal-Shader.html) in your project.

| **Debug Option**  | **Description**                                              |
| ----------------- | ------------------------------------------------------------ |
| **Display Atlas** | Enable the checkbox to display the decal atlas for a Camera in the top left of that Camera's view. |
| **Mip Level**     | Use the slider to select the mip level for the decal atlas. The higher the mip level, the blurrier the decal atlas. |

<a name="StatsPanel"></a>

## Display Stats panel

The **display stats** panel is only visible in play mode and can be used to debug performance issues in your project.  
| **Debug Option**  | **Description**                                              |
| ----------------- | ------------------------------------------------------------ |
| **Frame Rate** | Shows the frame rate in frames per second for the current camera view. |
| **Frame Time** | Shows the total frame time for the current camera view. |
| **RT Mode** | If ray tracing is enabled, shows the ray tracing Tier used during rendering.  |
| **Count Rays** | Enable the checkbox to count the number of traced rays per effect (In MRays / frame) |
| **Ambient Occlusion** | The number of rays that were traced for Ambient Occlusion (AO) computations, when RT AO is enabled   |
| **Shadows Directional** | The number of rays that were traced for directional lights, when RT shadows are enabled  |
| **Shadows Area** | The number of rays that were traced towards area lights, when RT shadows are enabled  |
| **Shadows Point/Spot** | The number of rays that were traced towards punctual (point/spot) lights, when RT shadows are enabled  |
| **Reflection Forward** | The number of rays that were traced for reflection computations using forward shading |
| **Reflection Deferred** | The number of rays that were traced for reflection computations using deferred shading |
| **Diffuse GI Forward** | The number of rays that were traced for diffuse Global Illumination (GI) computations using forward shading |
| **Diffuse GI Deferred** | The number of rays that were traced for diffuse Global Illumination (GI) computations using deferred shading |
| **Recursive** | The number of rays that were traced for diffuse Global Illumination (GI) computations when recursive RT is enabled |

<a name="MaterialPanel"></a>

## Material panel

The **Material** panel has tools that you can use to visualize different Material properties.

| **Debug Option**             | **Description**                                              |
| ---------------------------- | ------------------------------------------------------------ |
| **Common Material Property** | Use the drop-down to select a Material property to visualize on every GameObject on screen. All HDRP Materials share the properties available. |
| **Material**                 | Use the drop-down to select a Material property to visualize on every GameObject on screen using a specific Shader. The properties available depend on the HDRP Material type you select in the drop-down. |
| **Engine**                   | Use the drop-down to select a Material property to visualize on every GameObject on a screen that uses a specific Shader. The properties available are the same as **Material** but are in the form that the lighting engine uses them (for example, **Smoothness** is **Perceptual Roughness**). |
| **Attributes**               | Use the drop-down to select a 3D GameObject attribute, like Texture Coordinates or Vertex Color, to visualize on screen. |
| **Properties**               | Use the drop-down to select a property that the debugger uses to highlight GameObjects on screen. The debugger highlights GameObjects that use a Material with the property that you select. |
| **GBuffer**                  | Use the drop-down to select a property to visualize from the GBuffer for deferred Materials. |
| **Material Validator**       | Use the drop-down to select properties to show validation colors for.**Diffuse Color**: Select this option to check if the diffuse colors in your Scene adheres to an acceptable [PBR](Glossary.html#PhysicallyBasedRendering) range. If the Material color is out of this range, the debugger displays it in the **Too High Color** color if it is above the range, or in the **Too Low Color** if it is below the range.**Metal or SpecularColor**: Select this option to check if a pixel contains a metallic or specular color that adheres to an acceptable PBR range. If it does not, the debugger highlights it in the **Not A Pure Metal Color**.For information about the acceptable PBR ranges in Unity, see the [Material Charts documentation](https://docs.unity3d.com/Manual/StandardShaderMaterialCharts.html). |
| **- Too High Color**         | Use the color picker to select the color that the debugger displays when a Material's diffuse color is above the acceptable PBR range. This property only appears when you select **Diffuse Color** or **Metal or SpecularColor** from the **Material Validator** drop-down. |
| **- Too Low Color**          | Use the color picker to select the color that the debugger displays when a Material's diffuse color is below the acceptable PBR range. This property only appears when you select **Diffuse Color** or **Metal or SpecularColor** from the **Material Validator** drop-down. |
| **- Not A Pure Metal Color** | Use the color picker to select the color that the debugger displays if a pixel defined as metallic has a non-zero albedo value. The debugger only highlights these pixels if you enable the **True Metals** checkbox. This property only appears when you select **Diffuse Color** or **Metal or SpecularColor** from the **Material Validator** drop-down. |
| **- Pure Metals**            | Enable the checkbox to make the debugger highlight any pixels which Unity defines as metallic, but which have a non-zero albedo value. The debugger uses the **Not A Pure Metal Color** to highlight these pixels. This property only appears when you select **Diffuse Color** or **Metal or SpecularColor** from the **Material Validator** drop-down. |

<a name="LightingPanel"></a>

## Lighting panel

The **Lighting** panel has tools that you can use to visualize various components of the lighting system in your Scene, like, shadowing and direct/indirect lighting.

| **Debug Option**                     | **Description**                                              |
| ------------------------------------ | ------------------------------------------------------------ |
| **Show Directional Lights**          | Enable the checkbox to see Directional Lights in your Scene. Disable this checkbox to remove Directional Lights from your Scene's lighting. |
| **Show Punctual Lights**             | Enable the checkbox to see [punctual Lights](Glossary.html#PunctualLight) in your Scene. Disable this checkbox to remove punctual Lights from your Scene's lighting. |
| **Show Area Lights**                 | Enable the checkbox to see area Lights in your Scene. Disable this checkbox to remove punctual Lights from your Scene's lighting. |
| **Show Reflection Probes**           | Enable the checkbox to see Reflection Probes in your Scene. Disable this checkbox to remove Reflection Probes from your Scene's lighting. |
| **Shadow Debug Mode**                | Use the drop-down to select which shadow debug information to overlay on the screen.**None**: Select this mode to remove the shadow debug information from the screen.**VisualizePunctualLightAtlas**: Select this mode to overlay the shadow atlas for [punctual Lights](Glossary.html#PunctualLight) in your Scene.**VisualizeDirectionalLightAtlas**: Select this mode to overlay the shadow atlas for Directional Lights in your Scene.**VisualizeAreaLightAtlas**: Select this mode to overlay the shadow atlas for area Lights in your Scene.**VisualizeShadowMap**: Select this mode to overlay a single shadow map for a Light in your Scene.**SingleShadow**: Select this mode to replace the lighting in the Scene with lighting just from the Light you have selected (in black and white). |
| **- Use Selection**                  | Enable the checkbox to show the shadow map for the Light you select in the Scene. This property only appears when you select **VisualizeShadowMap** or **SingleShadow** from the **Shadow Debug Mode** drop-down. |
| **- Shadow Map Index**               | Use the slider to select the index of the shadow map to view. To use this property correctly, you must have at least one [Light](Light-Component.html) in your Scene that uses shadow maps. |
| **Global Shadow Scale Factor**       | Use the slider to set the global scale that HDRP applies to the shadow rendering resolution. |
| **Clear Shadow Atlas**               | Enable the checkbox to clear the shadow atlas every frame.   |
| **Shadow Range Minimum Value**       | Set the minimum shadow value to display in the various shadow debug overlays. |
| **Shadow Range Maximum Value**       | Set the maximum shadow value to display in the various shadow debug overlays. |
| **Lighting Debug Mode**              | Use the drop-down to select a lighting mode to debug. For example, you can visualize diffuse lighting, specular lighting, and Directional Light shadow cascades. |
| **Light Hierarchy Debug Mode**       | Use the drop-down to select a light type to show the direct lighting for or a Reflection Probe type to show the indirect lighting for. |
| **Fullscreen Debug Mode**            | Use the drop-down to select a fullscreen lighting effect to debug. For example, you can visualize [Contact Shadows](Override-Contact-Shadows.html), the depth pyramid, and indirect diffuse lighting. |
| **Override Smoothness**              | Enable the checkbox to override the smoothness for the entire Scene. |
| **- Smoothness**                     | Use the slider to set the smoothness override value that HDRP uses for the entire Scene. |
| **Override Albedo**                  | Enable the checkbox to override the albedo for the entire Scene. |
| **- Albedo**                         | Use the color picker to set the albedo color that HDRP uses for the entire Scene. |
| **Override Normal**                  | Enable the checkbox to override the normals for the entire Scene. |
| **Override Specular Color**          | Enable the checkbox to override the specular color for the entire Scene. |
| **- Specular Color**                 | Use the color picker to set the specular color that HDRP uses for the entire Scene. |
| **Override Emissive Color**          | Enable the checkbox to override the emissive color for the entire Scene. |
| **- Emissive Color**                 | Use the color picker to set the emissive color that HDRP uses for the entire Scene. |
| **Tile/Cluster Debug**               | Use the drop-down to select an internal HDRP lighting structure to visualize on screen.**None**: Select this option to turn off this debug feature.**Tile**: Select this option to show an overlay of each lighting tile, and the number of lights in them.**Cluster**: Select this option to show an overlay of each lighting cluster that intersects opaque geometry, and the number of lights in them.**Material Feature Variants**: Select this option to show the index of the lighting Shader variant that HDRP uses for a tile. You can find variant descriptions in the *lit.hlsl* file. |
| **- Tile/Cluster Debug By Category** | Use the drop-down to select the Light type that you want to show the Tile/Cluster debug information for. The options include [Light Types](Light-Component.html), [Decals](Decal-Projector.html), and [Density Volumes](Density-Volumes.html).This property only appears when you select **Tile** or **Cluster** from the **Tile/Cluster Debug** drop-down. |
| **Display Sky Reflection**           | Enable the checkbox to display an overlay of the cube map that the current sky generates and HDRP uses for lighting. |
| **- Sky Reflection Mipmap**          | Use the slider to set the mipmap level of the sky reflection cubemap. Use this to view the sky reflection cubemap's different mipmap levels.This property only appears when you enable the **Display Sky Reflection** checkbox. |
| **Display Light Volumes**            | Enable the checkbox to show an overlay of all light bounding volumes. |
| **- Light Volume Debug Type**        | Use the drop-down to select the method HDRP uses to display the light volumes.**Gradient**: Select this option to display the light volumes as a gradient.**ColorAndEdge**: Select this option to display the light volumes as a plain color (a different color for each Light Type) with a red border for readability.This property only appears when you enable the **Display Light Volumes** checkbox. |
| **- Max Debug Light Count**          | Use the slider to rescale the gradient. Lower this value to make the screen turn red faster. Use this property to change the maximum acceptable number of lights for your application and still see areas in red. This property only appears when you enable the **Display Light Volumes** checkbox. |
| **Debug Exposure**                   | Set the exposure that HDRP applies when you select a **Lighting Debug Mode**. This is useful because HDRP does not apply normal Scene exposure when it is in debug mode. |

<a name="RenderingPanel"></a>

## Rendering panel

The **Rendering** panel has tools that you can use to visualize various HDRP rendering features.

| **Debug Option**              | **Description**                                              |
| ----------------------------- | ------------------------------------------------------------ |
| **Fullscreen Debug Mode**     | Use the drop-down to select a rendering mode to display as an overlay on the screen.**Motion Vectors**: Select this option to display motion vectors.**NaN Tracker**: Select this option to display an overlay that highlights [NaN](<https://en.wikipedia.org/wiki/NaN>) values. |
| **MipMaps**                   | Use the drop-down to select a mipmap streaming property to debug.**None**: Select this option to disable this debug feature.**MipRatio**: Select this option to display a heat map of pixel to texel ratio. A blue tint represents areas with too little Texture detail (the Texture is too small). A bed tint represents areas with too much Texture detail (the Texture is too large for the screen area). If the debugger shows the original colour for a pixel, this means that the level of detail is just right.**MipCount**: Select this option to display mip count as grayscale from black to white as the number of mips increases (for up to 14 mips, or 16K size). Red inidates Textures with more than 14 mips. Magenta indicates Textures with 0 mips or that the Shader does not support mip count.**MipCountReduction**: Select this option to display the difference between the current mip count and the original mip count as a green scale. A brighter green represents a larger reduction (that mip streaming saves more Texture memory). Magenta means that the debugger does not know the original mip count.**StreamingMipBudget**: Select this option to display the mip status due to streaming budget. Green means that streaming Textures saves some memory. Red means that mip levels are lower than is optimal, due to full Texture memory budget. White means that streaming Textures saves no memory.**StreamingMip**: Select this option to display the same information as **StreamingMipBudget**, but to apply the colors to the original Textures. |
| **- Terrain Texture**         | Use the drop-down to select the terrain Texture to debug the mipmap for. This property only appears when you select an option other than **None** from the **MipMaps** drop-down. |
| **Color Picker - Debug Mode** | Use the drop-down to select the format of the color picker display. |
| **Color Picker - Font Color** | Use the color picker to select a color for the font that the Color Picker uses for its display. |
| **False Color Mode**          | Enable the checkbox to define intensity ranges that the debugger uses to show a color temperature gradient for the current frame. The color temperature gradient goes from blue, to green, to yellow, to red. |
| **- Range Threshold 0**       | Set the first split for the intensity range.This property only appears when you enable the **False Color Mode** checkbox. |
| **- Range Threshold 1**       | Set the second split for the intensity range.This property only appears when you enable the **False Color Mode** checkbox. |
| **- Range Threshold 2**       | Set the third split for the intensity range.This property only appears when you enable the **False Color Mode** checkbox. |
| **- Range Threshold 3**       | Set the final split for the intensity range.This property only appears when you enable the **False Color Mode** checkbox. |
| **MSAA Samples**              | Use the drop-down to select the number of samples the debugger uses for [MSAA](Anti-Aliasing.html#MSAA). |
| **Freeze Camera for Culling** | Use the drop-down to select a Camera to freeze in order to check its culling. To check if the Camera's culling works correctly, freeze the Camera and move occluders around it. |
| **XR Debug Mode**             | Use the drop-down to select which XR debug information to view in the **Game** window.**None**: Select this option to disable **XR Debug Mode**.**Composite**: Select this option to composite four tiles in the **Game** window. HDRP renders these tiles with multi-pass and single-pass instancing so you can debug the rendering path. |
| **- Display Borders**         | Enable the checkbox to render a red line at the border between the tiles. This property only appears when you select **Composite** from the **XR Debug Mode** drop-down. |
| **- Animate Tiles**           | Enable the checkbox to change the split ratio for the tiles so that their size changes every frame. This property only appears when you select **Composite** from the **XR Debug Mode** drop-down. |

The **Color Picker** works with whichever debug mode HDRP displays at the time. This means that you can see the values of various components of the rendering like Albedo or Diffuse Lighting. By default, this displays the value of the main High Dynamic Range (HDR) color buffer.

<a name="CameraPanel"></a>

## Camera panels

In the **Render Pipeline Debug** window , each active Camera in the Scene has its own debug window. Use the Camera's debug window to temporarily change that Camera's [Frame Settings](Frame-Settings.html) without altering the Camera data in the Scene. The Camera window helps you to understand why a specific feature does not work correctly. You can access all of the information that HDRP uses the render the Camera you select.

**Note**: The Camera debug window is only available for Cameras, not Reflection Probes.

The following columns are available for each Frame Setting:

| **Column**     | **Description**                                              |
| -------------- | ------------------------------------------------------------ |
| **Debug**      | Displays Frame Setting values you can modify for the selected Camera. You can use these to temporarily alter the Camera’s Frame Settings for debugging purposes. You cannot enable Frame Setting features that your HDRP Asset does not support. |
| **Sanitized**  | Displays the Frame Setting values that the selected Camera uses after Unity checks to see if your HDRP Asset supports them. |
| **Overridden** | Displays the Frame Setting values that the selected Camera overrides. If you do not check the **Custom Frame Settings** checkbox, check it and do not override any settings, this column is identical to the **Default** column. |
| **Default**    | Displays the default Frame Setting values in your current [HDRP Asset](HDRP-Asset.html). |

Unity processes **Sanitized**, **Overridden**, and **Default** in a specific order. First it checks the **Default** Frame Settings, then checks the selected Camera’s **Overridden** Frame Settings. Finally, it checks whether the HDRP Asset supports the selected Camera’s Frame Settings and displays that result in the **Sanitized** column.

### Interpreting the Camera window

![](Images/RenderPipelineDebug2.png)

- In the image above, the **Light Layers** checkbox is disabled at the **Sanitized** step. This means that, although **Light Layers** is enabled in the Frame Settings this Camera uses, it is not enabled in the HDRP Asset’s **Render Pipeline Supported Features**.
- Also in the image above, the **Decals** checkbox is disabled at the **Overridden** step. This means that **Decals** is enabled in the default Camera Frame Settings and then **Decals** is disabled for that specific Camera’s **Custom Frame Settings**.