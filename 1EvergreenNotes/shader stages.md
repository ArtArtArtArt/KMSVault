---
status: 🌱
type: 
 - definition
 - MOC
tags:
 - programming/gamedev/rendering
---

OpenGL
![[Pasted image 20220213101716.png]]


DirectX
![[Pasted image 20220220082506.png]]

### what each stage does?

- [[vertex specification]] - creating a stream of vetrices and telling the renderer how to interpret them,
- [[vertex shader]] - inputs a single vertice and outputs a single vertice. TRansforms to view porjectin space, May be used for per vertice lighting
- [Hull-Shader Stage](https://docs.microsoft.com/en-us/windows/win32/direct3d11/direct3d-11-advanced-stages-tessellation#hull-shader-stage) - A programmable shader stage that produces a geometry patch (and patch constants) that correspond to each input patch (quad, triangle, or line).
-   [Tessellator Stage](https://docs.microsoft.com/en-us/windows/win32/direct3d11/direct3d-11-advanced-stages-tessellation#tessellator-stage) - A fixed function pipeline stage that creates a sampling pattern of the domain that represents the geometry patch and generates a set of smaller objects (triangles, points, or lines) that connect these samples.
-   [Domain-Shader Stage](https://docs.microsoft.com/en-us/windows/win32/direct3d11/direct3d-11-advanced-stages-tessellation#domain-shader-stage) - A programmable shader stage that calculates the vertex position that corresponds to each domain sample.



---
read more here: https://docs.microsoft.com/en-us/windows/win32/direct3d11/direct3d-11-advanced-stages-tessellation
