# automatic-graph-layout-master

Microsoft Automatic Graph Layout (MSAGL) is a C# toolkit for laying out and viewing graphs: Sugiyama layered layout, MDS, incremental layout, rectilinear and spline edge routing, and GDI/WPF viewers with pan, zoom, search, and tooltips. It was developed at Microsoft by Lev Nachmanson, Sergey Pupyrev, Tim Dwyer and Ted Hart, and published as open source. This is Dave Robinson's working copy of the Microsoft `automatic-graph-layout` tree (GraphLayout.sln, Visual Studio 2015); there is no separable VaderConsulting wrapper. The GDI viewer project is missing `tools/GraphViewerGDI/Draw.cs` because OneDrive did not download that file.

**Source last updated:** 2015-09-18 · **Language:** C# · **Target:** .NET Framework 4.0 (core libraries and most samples; some WPF/Graphmaps projects 4.5; Silverlight 5.0 / 3.5) · **Output:** class libraries (`Microsoft.Msagl.dll`, `Microsoft.Msagl.Drawing.dll`, `Microsoft.Msagl.GraphViewerGdi.dll`) plus WinForms/WPF sample and test exes

## Solution structure

Open `GraphLayout/GraphLayout.sln` (Visual Studio 14 / 2015, format 12.00). A second solution `GraphLayout/Lg.sln` exists for large-graph (Graphmaps) work. Core assemblies are signed (`msaglSigningKey.snk`, `GraphViewerGDI.snk`). Assembly version **3.0.1.1**.

### Core libraries

| Project | Language | Type | Purpose |
|---------|----------|------|---------|
| `Msagl` (`GraphLayout/MSAGL/Msagl.csproj`) | C# | Class library (`Microsoft.Msagl`) | Core geometry and layout engine: Sugiyama, MDS, incremental, routing, phylotree. |
| `drawing` (`GraphLayout/Drawing/drawing.csproj`) | C# | Class library (`Microsoft.Msagl.Drawing`) | Drawing model: graph/node/edge attributes, colours, shapes; feeds layout and renderers. |
| `GraphViewerGDI` (`GraphLayout/tools/GraphViewerGDI/GraphViewerGDI.csproj`) | C# | Class library (`Microsoft.Msagl.GraphViewerGdi`) | WinForms `GViewer` control (pan/zoom/edit). **`Draw.cs` is missing** from this dump. |

### Tools

| Project | Language | Type | Purpose |
|---------|----------|------|---------|
| `ArgsParser` | C# | Class library | Command-line argument parsing for console tools. |
| `DebugCurveViewer` | C# | WinForms exe | Debug viewer for MSAGL geometry curves. |
| `DgmlParser` | C# | Class library | DGML graph parse (uses VSSDK.GraphModel 12). |
| `Dot2Graph` | C# | Class library | GraphViz DOT lexer/parser into MSAGL graphs. |
| `Dot2Svg` | C# | Console exe | DOT to SVG conversion. |
| `WpfGraphControl` | C# | Class library | WPF graph viewer control (.NET 4.5). |
| `GraphmapsWpfControl` | C# | Class library | WPF Graphmaps (large-graph) control (.NET 4.5). |
| `msbuildlogger` (`tools/Utilities/msbuildlogger`) | C# | Class library | MSBuild logger helper (not in GraphLayout.sln). |

### Samples (WinForms / WPF / console)

| Project | Language | Type | Purpose |
|---------|----------|------|---------|
| `WindowsApplicationSample` | C# | WinForms exe | Basic GDI viewer sample from the upstream README. |
| `WpfApplicationSample` | C# | WPF exe | WPF viewer host (.NET 4.5). |
| `Editing` | C# | Exe | Interactive graph editing over GDI viewer. |
| `EdgeRoutingSample` | C# | Console exe | Edge-routing demonstration. |
| `DrawingFromGeometryGraphSample` | C# | WinForms exe | Build a drawing graph from a geometry graph. |
| `SettingGraphBoundsSample` | C# | WinForms exe | Aspect-ratio / graph bounds sample. |
| `UsingMDSLayoutSample` | C# | WinForms exe | MDS (multidimensional scaling) layout. |
| `FastIncrementalLayoutWithGdi` | C# | WinForms exe | Fast incremental layout with GDI viewer. |
| `LayoutOfADisconnectedGraphWithSugiyama` | C# | WinForms exe | Sugiyama layout of disconnected components. |
| `NodesWithImages` | C# | WinForms exe | Nodes rendered with images. |
| `PhyloTreeSampleOverGDI` | C# | WinForms exe | Phylogenetic tree layout over GDI. |
| `FindEmptySpotSample` | C# | WinForms exe | Find empty regions in a drawing. |
| `FindOverlapSample` | C# | Exe | Overlap detection. |
| `GeometryRoutinesSample` | C# | Exe | Geometry helper routines. |
| `LocationLabeler` | C# | Exe | Node/edge location labelling. |
| `LoadingDgmlGraph` | C# | Exe | Load a DGML graph into MSAGL. |
| `xCodeMap` | C# | Exe | Code-map style graph sample (.NET 4.5). |

### Tests

| Project | Language | Type | Purpose |
|---------|----------|------|---------|
| `MSAGLTests` | C# | Test library | Unit tests (Sugiyama, incremental, bundling, resources/DOT fixtures). |
| `TestForGDI` | C# | Exe | GDI viewer test host. |
| `TestFormForGViewer` | C# | Class library | Shared GViewer test form. |
| `TestForAvalon` | C# | Exe | WPF/Avalon test host. |
| `TestWpfViewer` | C# | Exe | WPF viewer tests (.NET 4.5). |
| `TestGraphmaps` | C# | Exe | Graphmaps large-graph tests (.NET 4.5). |
| `Test01` | C# | Exe | Additional layout/viewer test harness. |
| `TestConstraints` | C# | Exe | Constraint solver tests. |
| `TestSolverShell` | C# | Exe | Projection/solver shell tests. |
| `VoronoiDiagramTest` | C# | Exe | Voronoi diagram tests (.NET 4.5). |

### Silverlight and SharpKit (not in GraphLayout.sln)

| Project | Language | Type | Purpose |
|---------|----------|------|---------|
| `msaglsilverlight` | C# | Silverlight library | Core MSAGL for Silverlight 5. |
| `MsaglDrawingSilverlight` | C# | Silverlight library | Drawing layer for Silverlight. |
| `GraphControlSilverlight` / `GraphControlTest` | C# | Silverlight library | Silverlight graph control and test (also duplicated under `MsaglSilverlight/SilverlightSample`). |
| `MsaglSharpKit` / `MsaglDrawingSharpkit` | C# | Class library | SharpKit C#-to-JavaScript port of layout/drawing. |
| `WebMsagl` | C# | ASP.NET library | Web host for the SharpKit viewer (jQuery 2.1.3, RequireJS). |
| `ConsoleTest` (MsaglSharpkit) | C# | Console exe | SharpKit console test. |

NuGet packages in `GraphLayout/packages/`: MathNet.Numerics 2.6.1, VSSDK.GraphModel 12.0.4, VSSDK.IDE.12. `bin/` and `obj/` build outputs were omitted from this import (about 1 GB of DLLs/PDBs in the OneDrive zip).

## How to open

Open **`GraphLayout/GraphLayout.sln`** in Visual Studio 2015 or later (solution format 12.00 / Visual Studio 14; `.csproj` ToolsVersion 4.0). Build `Msagl`, then `drawing`, then `GraphViewerGDI` (the last will fail until `Draw.cs` is restored from upstream). Sample entry point: `Samples/WindowsApplicationSample`. Optional: `GraphLayout/Lg.sln` for Graphmaps. Silverlight and SharpKit projects are opened from their own `.csproj` files.

## Attribution and provenance

Working copy from Dave Robinson's OneDrive Historical Dev folder `automatic-graph-layout-master`.

- **Authors:** Lev Nachmanson, Sergey Pupyrev, Tim Dwyer, Ted Hart (Microsoft)
- **Assembly company:** MS
- **Assembly copyright:** Copyright © MS 2005 (engine), 2006 (drawing)
- **Assembly version:** 3.0.1.1
- **Upstream:** [Microsoft/automatic-graph-layout](https://github.com/Microsoft/automatic-graph-layout)
- **Original README:** kept as `README.upstream.md`
- **Bundled third-party:** MathNet.Numerics 2.6.1; VSSDK.GraphModel 12; jQuery 2.1.3 and RequireJS (`r.js`) in WebMsagl (keep third-party author emails in those license headers)

OneDrive reported eight files not downloaded; six were under `bin/` (gitignored anyway). Missing source: `GraphLayout/tools/GraphViewerGDI/Draw.cs`. VS `.suo` / `.vs/` were in the zip and are gitignored.

## License

Original **MIT License, Copyright (c) Microsoft Corporation** as in `LICENSE`. This repository does **not** relicense the tree as VaderConsulting MIT. There is no separable Dave Robinson wrapper or sample. See `LICENSE` and `THIRD_PARTY_NOTICES.md`.
