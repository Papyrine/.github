# Papyrine

.NET libraries and tools for **creating, converting, and rendering documents** — Word, Excel, Markdown, and diagrams. Most are built directly on [DocumentFormat.OpenXml](https://github.com/dotnet/Open-XML-SDK), and several compose with each other to form a small document-tooling ecosystem.

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

### Low-level OpenXML

| Project | NuGet | Description |
| --- | --- | --- |
| [OpenXmlStreaming](https://github.com/Papyrine/OpenXmlStreaming) | [![NuGet](https://img.shields.io/nuget/v/OpenXmlStreaming.svg)](https://www.nuget.org/packages/OpenXmlStreaming/) | Forward-only writer for `.docx`/`.xlsx`/`.pptx` that streams directly to non-seekable targets (HTTP responses, cloud uploads) without buffering the whole package in memory. |

### Tools

| Project | NuGet | Description |
| --- | --- | --- |
| [WordMD](https://github.com/Papyrine/WordMD) | [![NuGet](https://img.shields.io/nuget/v/WordMD.svg)](https://www.nuget.org/packages/WordMD/) | A .NET global tool for editing Markdown content embedded inside Word `.docx` files using your favourite Markdown editor, with Windows Explorer context-menu integration. |

## How they fit together

- **Excelsior** uses **OpenXmlHtml** to render HTML cell content.
- **Parchment** uses **OpenXmlHtml** for HTML chunks and **Excelsior** for embedded Word tables.
- **Morph** uses **OpenXmlHtml** when rasterizing HTML content.

The result is a layered stack: low-level OpenXML plumbing at the bottom (OpenXmlHtml, OpenXmlStreaming), document generators in the middle (Excelsior, Parchment), and conversion/rendering on top (Morph, Naiad).
