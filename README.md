# Net3dBool 🧊

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![.NET Framework](https://img.shields.io/badge/.NET%20Framework-4.6.1-blue.svg)](https://dotnet.microsoft.com/download/dotnet-framework/net461)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)]()
[![Build](https://img.shields.io/badge/Build-MSBuild-brightgreen.svg)]()
[![NuGet](https://img.shields.io/badge/NuGet-Net3dBool-blue.svg)](https://www.nuget.org/packages/Net3dBool/)

> **A C# port of the Java [j3dbool](https://github.com/mvdnes/j3dbool) library** — Robust Constructive Solid Geometry (CSG) operations for 3D meshes.

Net3dBool implements **Boolean operations on 3D solids** (union, subtraction, intersection) with correct handling of all edge cases involving overlapping coplanar polygons.

---

## ✨ Features

| Operation | Description |
|-----------|-------------|
| 🔗 **Union** | Combine two solids into one (`A ∪ B`) |
| ✂️ **Subtract** | Remove solid B from A (`A - B`) |
| 🔍 **Intersect** | Keep only the overlapping volume (`A ∩ B`) |

<details>
<summary><strong>Technical Highlights</strong></summary>

- ✅ Handles all edge cases with coplanar polygons
- ✅ Robust BSP-tree based algorithm
- ✅ Zero external dependencies (core library)
- ✅ Compatible with .NET Framework 4.6.1+ / .NET Standard 2.0+
- ✅ Includes interactive OpenGL demo (OpenTK)

</details>

---

## 📸 Demo Preview

![Net3dBool Demo](media/screenshot2.png)

*Interactive demo showing CSG operations in real-time*

---

## 📁 Project Structure

```text
Net3dBool/
├── 📄 LICENSE                    # MIT License
├── 📄 README.md                  # This file
├── 📄 .gitignore
├── 📁 media/
│   └── 📸 screenshot2.png        # Demo screenshot
└── 📁 src/
    ├── 📄 Net3dBool.sln          # Visual Studio Solution
    ├── 📁 Net3dBool/             # 📦 Core Library (Class Library)
    │   ├── 📄 Net3dBool.csproj
    │   ├── 📁 Properties/
    │   │   └── AssemblyInfo.cs
    │   ├── BooleanModeller.cs    # Main CSG operations entry point
    │   ├── Solid.cs              # Solid representation
    │   ├── Face.cs               # Polygon face
    │   ├── Vertex.cs             # 3D vertex
    │   ├── Line.cs               # Line segment
    │   ├── Segment.cs            # Segment for BSP
    │   ├── Bound.cs              # Bounding box
    │   ├── Object3D.cs           # 3D object container
    │   ├── Misc.cs               # Math utilities
    │   └── 📁 solids/
    │       └── DefaultCoordinates.cs # Primitive generators (cube, sphere, etc.)
    └── 📁 Net3dBoolDemo/         # 🎮 Demo Application (WPF/OpenTK)
        ├── 📄 Net3dBoolDemo.csproj
        ├── 📁 Properties/
        │   └── AssemblyInfo.cs
        ├── Program.cs            # Entry point
        ├── Window.cs             # OpenGL window
        └── Demo.cs               # Demo logic & UI
```

---

## 🚀 Getting Started

### Prerequisites

- [.NET Framework 4.6.1+](https://dotnet.microsoft.com/download/dotnet-framework/net461) or [.NET 6+](https://dotnet.microsoft.com/download)
- Visual Studio 2019+ / VS Code / Rider
- (Optional) OpenTK for the demo: `dotnet add package OpenTK`

### 📦 Installation

**Option 1: NuGet Package (Recommended)**
```bash
dotnet add package Net3dBool
```

**Option 2: Build from Source**
```bash
# Clone the repository
git clone https://github.com/yourusername/Net3dBool.git
cd Net3dBool

# Build the solution
msbuild src/Net3dBool.sln /p:Configuration=Release
```

---

## 💡 Usage

### Basic Example

```csharp
using Net3dBool;
using Net3dBool.Solids;

// Create two cubes
Solid cubeA = DefaultCoordinates.CreateCube(new Vertex(0, 0, 0), 10);
Solid cubeB = DefaultCoordinates.CreateCube(new Vertex(5, 5, 5), 10);

// Perform Boolean operations
var modeller = new BooleanModeller();

// Union: A ∪ B
Solid union = modeller.Union(cubeA, cubeB);

// Subtract: A - B
Solid subtract = modeller.Subtract(cubeA, cubeB);

// Intersect: A ∩ B
Solid intersect = modeller.Intersect(cubeA, cubeB);
```

### Available Primitives

```csharp
// Cubes
DefaultCoordinates.CreateCube(center, size);

// Spheres (approximated with triangles)
DefaultCoordinates.CreateSphere(center, radius, slices, stacks);

// Cylinders
DefaultCoordinates.CreateCylinder(center, radius, height, slices);

// Cones
DefaultCoordinates.CreateCone(center, radius, height, slices);
```

---

## 🎮 Running the Demo

The demo project showcases all three CSG operations with an interactive OpenGL viewer.

```bash
cd src/Net3dBoolDemo
dotnet run
```

**Controls:**
| Key | Action |
|-----|--------|
| `1` | Show Union |
| `2` | Show Subtract (A - B) |
| `3` | Show Intersect |
| `Mouse Drag` | Rotate view |
| `Scroll` | Zoom in/out |
| `R` | Reset camera |

---

## 📚 API Reference

### `BooleanModeller`
Main entry point for CSG operations.

| Method | Signature | Description |
|--------|-----------|-------------|
| `Union` | `Solid Union(Solid a, Solid b)` | Returns `a ∪ b` |
| `Subtract` | `Solid Subtract(Solid a, Solid b)` | Returns `a - b` |
| `Intersect` | `Solid Intersect(Solid a, Solid b)` | Returns `a ∩ b` |

### `Solid`
Represents a closed 3D solid composed of triangular faces.

| Property | Type | Description |
|----------|------|-------------|
| `Faces` | `List<Face>` | Triangular faces of the solid |
| `Bounds` | `Bound` | Axis-aligned bounding box |

### `Vertex`
3D point with X, Y, Z coordinates.

```csharp
var v = new Vertex(x, y, z);
```

---

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2014 Sebastian Loncar
```

---

## 🙏 Acknowledgments

- Original Java library: **[j3dbool](https://github.com/mvdnes/j3dbool)** by Mikko Vehkala
- Ported to C# by **Sebastian Loncar**
- Demo uses **[OpenTK](https://opentk.net/)** for OpenGL rendering

---

## 📞 Support

- 🐛 [Report Issues](https://github.com/yourusername/Net3dBool/issues)
- 💡 [Request Features](https://github.com/yourusername/Net3dBool/issues/new)
- ⭐ Star this repo if you find it useful!

---

<div align="center">
<sub>Built with ❤️ for the .NET graphics community</sub>
</div>
