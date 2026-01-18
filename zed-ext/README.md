# Go Template LSP for Zed

A Zed extension providing Language Server Protocol support for Go templates (`text/template` and `html/template`).

## Features

- **Diagnostics**: Real-time error detection for template syntax
- **Hover**: Type information and documentation on hover
- **Go to Definition**: Navigate to template definitions
- **Folding Ranges**: Collapse template blocks and comments
- **Syntax Highlighting**: Full highlighting for Go template syntax

## Supported File Extensions

- `.gotmpl`, `.go.tmpl`, `.gtpl`, `.tpl` - Go text templates
- `.gohtml`, `.go.html`, `.html.tmpl` - Go HTML templates

## Installation

### From Zed Extensions

1. Open Zed
2. Go to Extensions (Cmd+Shift+X)
3. Search for "Go Template LSP"
4. Click Install

### As Dev Extension

1. Clone this repository
2. In Zed, go to Extensions > "Install Dev Extension"
3. Select the `zed-ext` directory

## How It Works

The extension downloads a prebuilt LSP binary from GitHub releases on first use. The binary is built using [goreleaser](https://goreleaser.com/) and published for:

- macOS (arm64, amd64)
- Linux (arm64, amd64)
- Windows (amd64)

## Credits

This extension is built on the work of several open source projects:

- **LSP Implementation**: Based on [yayolande/go-template-lsp](https://github.com/yayolande/go-template-lsp) (MIT License)
  - Provides the core language server functionality
- **Tree-sitter Grammar**: [ngalaiko/tree-sitter-go-template](https://github.com/ngalaiko/tree-sitter-go-template) (MIT License)
  - Provides parsing for Go template syntax
- **Syntax Highlighting Queries**: Adapted from [hjr265/zed-gotmpl](https://github.com/hjr265/zed-gotmpl) (MIT License)
  - Provides the tree-sitter query patterns

## License

MIT License - see [LICENSE](LICENSE) for details.

## Development

### Building the LSP Binary

```bash
go build -o go-template-lsp ./cmd/go-template-lsp
```

### Testing Manually

```bash
echo '{"jsonrpc":"2.0","id":1,"method":"initialize","params":{}}' | ./go-template-lsp
```

### Building the Zed Extension

```bash
cd zed-ext
cargo build --target wasm32-wasip1
```
