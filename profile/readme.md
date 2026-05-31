# Papyrine

.NET libraries and tools for **creating, converting, and rendering documents** — Word, Excel, Markdown, and diagrams — alongside supporting libraries for geospatial maps and icons. Several build directly on [DocumentFormat.OpenXml](https://github.com/dotnet/Open-XML-SDK), and many compose with each other to form a small document-tooling ecosystem.


## The name

**Papyrine** — *PAP-ih-rin* (`/ˈpæpɪrɪn/`): "PAP" as in *pap*, a short *i*, and "-rin" rhyming with *bin*.

From Latin *papyrus* (paper / papyrus plant) + the suffix *-ine* (meaning "of, relating to, or resembling"). Fittingly, Papyrine is a family of libraries for creating and transforming documents: the modern descendants of the papyrus scroll.


## Projects


### Document generation

| Project | NuGet | Description |
| --- | --- | --- |
| [Excelsior](https://github.com/Papyrine/Excelsior) | [![NuGet](https://img.shields.io/nuget/v/Excelsior.svg)](https://www.nuget.org/packages/Excelsior/) | Data-driven Excel (`.xlsx`) generation and reading from .NET models, with attribute- and fluent-based column configuration, styling, formulas, HTML cells, and round-trip deserialization. Also ships a Word table generator. |
| [Parchment](https://github.com/Papyrine/Parchment) | [![NuGet](https://img.shields.io/nuget/v/Parchment.svg)](https://www.nuget.org/packages/Parchment/) | Word (`.docx`) generation from a .NET model plus a [Liquid](https://shopify.github.io/liquid/)-driven docx or Markdown template — token substitution, loops, conditionals, and HTML/Markdown/table content blocks. |


### Conversion & rendering

| Project | NuGet | Description |
| --- | --- | --- |
| [Morph](https://github.com/Papyrine/Morph) | [![NuGet](https://img.shields.io/nuget/v/Morph.OpenXml.Skia.svg)](https://www.nuget.org/packages/Morph.OpenXml.Skia/) | Renders Word `.docx` documents or HTML to PNG images. No Microsoft Word dependency; cross-platform, with SkiaSharp and fully-managed ImageSharp backends. |
| [OpenXmlHtml](https://github.com/Papyrine/OpenXmlHtml) | [![NuGet](https://img.shields.io/nuget/v/OpenXmlHtml.svg)](https://www.nuget.org/packages/OpenXmlHtml/) | Converts HTML into native OpenXml elements for embedding in `.xlsx` and `.docx` files — rich text, tables, lists, images, and CSS-to-Word style mapping, with no `altChunk`. |
| [Naiad](https://github.com/Papyrine/Naiad) | [![NuGet](https://img.shields.io/nuget/v/Naiad.svg)](https://www.nuget.org/packages/Naiad/) | Renders [Mermaid](https://mermaid.js.org/) diagrams to SVG. No browser or JavaScript runtime required; supports 25+ diagram types and Iconify/FontAwesome icon packs. |
| [PandocNet](https://github.com/Papyrine/PandocNet) | [![NuGet](https://img.shields.io/nuget/v/Pandoc.svg)](https://www.nuget.org/packages/Pandoc/) | Converts documents between formats via [Pandoc](https://pandoc.org/) — wraps `pandoc.exe` with [CliWrap](https://github.com/Tyrrrz/CliWrap) and exposes strongly-typed options per format, for text, stream, and file conversions. |


### Geospatial

| Project | NuGet | Description |
| --- | --- | --- |
| [GeoConvert](https://github.com/Papyrine/GeoConvert) | [![NuGet](https://img.shields.io/nuget/v/GeoConvert.svg)](https://www.nuget.org/packages/GeoConvert/) | Converts maps between geospatial vector formats — GeoJSON, TopoJSON, Shapefile, FlatGeobuf, KML/KMZ, GPX, WKT/WKB, CSV, and GeoParquet — plus PNG export. No third-party dependencies; ships as a library and a `geoconvert` command-line tool. |
| [MapBundle](https://github.com/Papyrine/MapBundle) | [![NuGet](https://img.shields.io/nuget/v/MapBundle.svg)](https://www.nuget.org/packages/MapBundle/) | Bundled, offline map data for .NET — borders, cities, waterways, and base layers shipped as [FlatGeobuf](https://flatgeobuf.org/) inside per-region NuGet packages. Data from [OpenStreetMap](https://www.openstreetmap.org/) and [Natural Earth](https://www.naturalearthdata.com/); layers are returned as GeoConvert feature collections. |


### Low-level & building blocks

| Project | NuGet | Description |
| --- | --- | --- |
| [OpenXmlStreaming](https://github.com/Papyrine/OpenXmlStreaming) | [![NuGet](https://img.shields.io/nuget/v/OpenXmlStreaming.svg)](https://www.nuget.org/packages/OpenXmlStreaming/) | Forward-only writer for `.docx`/`.xlsx`/`.pptx` that streams directly to non-seekable targets (HTTP responses, cloud uploads) without buffering the whole package in memory. |
| [IconifyBundle](https://github.com/Papyrine/IconifyBundle) | [![NuGet](https://img.shields.io/nuget/v/IconifyBundle.svg)](https://www.nuget.org/packages/IconifyBundle/) | Strongly-typed [Iconify](https://iconify.design/) icons for .NET. A source generator bundles only the icons you reference — baked into the assembly (Resource mode) or written to build output as `.svg` files (Disk mode) — with Blazor helpers included. |


### Tools

| Project | NuGet | Description |
| --- | --- | --- |
| [MsOfficeDiff](https://github.com/Papyrine/MsOfficeDiff) | [![NuGet](https://img.shields.io/nuget/v/MsWordDiff.svg?label=MsWordDiff)](https://www.nuget.org/packages/MsWordDiff/)<br>[![NuGet](https://img.shields.io/nuget/v/MsExcelDiff.svg?label=MsExcelDiff)](https://www.nuget.org/packages/MsExcelDiff/) | A pair of .NET global tools — `diffword` and `diffexcel` — that compare two Word documents or Excel workbooks side by side using Microsoft Office's built-in comparison features. Windows-only; requires the relevant Office app installed. |


## How they fit together

- **Excelsior** uses **OpenXmlHtml** to render HTML cell content.
- **Parchment** uses **OpenXmlHtml** for HTML chunks and **Excelsior** for embedded Word tables.
- **Morph** uses **OpenXmlHtml** when rasterizing HTML content.
- **MapBundle** builds on **GeoConvert**, returning its bundled layers as GeoConvert feature collections.

The result is a layered stack: low-level plumbing and shared assets at the bottom (OpenXmlHtml, OpenXmlStreaming, IconifyBundle), document generators in the middle (Excelsior, Parchment), and conversion/rendering on top (Morph, Naiad, PandocNet). The geospatial pair (GeoConvert → MapBundle) and the diff tooling (MsOfficeDiff) stand alongside as self-contained sub-families.
