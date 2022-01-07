# Unity-HDRPShaderGraphToTexture
Demo of a patch to fix Graphics.Blit with HDRP Shader Graphs in Unity 2019.4

Graphics.Blit only works with 2021.2+ Built-In Unlit Shader Graphs. If you are
stuck with an older version of Unity in HDRP, Graphics.Blit will not work with
Shader Graphs unless you use a workaround such as the one shown in this demo.
https://i.imgur.com/NWcq2mb.png

## Why using Graphics.Blit

One might ask why not use an additional Camera in front of a quad to render the
Shader Graph surface? The main reason is using Graphics.Blit to render a Shader
Graph directly to a RenderTexture is WAY faster than doing the same thing with
a big quad and a camera in the scene, as most of the rendering pipeline is
skipped. It is also simpler to setup, and prevent precision issues when running
a simulation (think of a double-buffer ripple solver Shader Graph, for
example).

## How to run the demo:

1) Open scene "Assets/ShadergraphBlit/Example/Scene/BlitShadergraphDemo.unity"
2) Press Play : the Shader Graph named "ShaderGraphBlit" will render to a RenderTexture named "ShaderGraphBlitRT".

## The Shader Graph:
A Custom Function node containing a patch (hlsl) is needed in the Shader Graph, to allow the Graphics.Blit() to properly render the shader into the Render Texture.
This additional node must be attached to a vertex output from the Unlit Master.
![gif](https://i.imgur.com/40PMUoU.png)


## The RenderTexture:
The resulting RenderTexture, updated in real-time.
![gif](https://i.imgur.com/vxgVYcB.png)


## The Script Component:
The script component required to perform the Blit.
Only a Shader reference and the target RenderTexture are needed.
![gif](https://i.imgur.com/ZGhajNh.png)


## Related dicussion
See these
https://forum.unity.com/threads/graphics-blit-with-hdrp-shadergraph.724112/
https://issuetracker.unity3d.com/issues/graphics-dot-blit-will-not-apply-the-material-correctly-when-the-material-uses-hdrp-or-shader-graph-shader


