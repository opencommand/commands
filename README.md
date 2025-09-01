# Commands

A declarative command definition framework that enables type-safe, cross-platform command-line tools with clean syntax.

## 🚀 Features

- **Declarative Syntax**: Define command structures with clean, readable syntax
- **Type Safety**: Built-in type system with compile-time parameter validation
- **Cross-Platform**: Generate commands for Windows (batch/cmd) and Unix (bash/sh)
- **Modular Design**: Import and implement commands across modules for code reuse
- **Smart Compilation**: Automatically generate platform-specific implementations

## 📖 Examples

### Basic Command Definition

```hulo
// Define cat command
cmd cat {
    showAll: bool           // -A, --show-all
    numberNonBlank: bool    // -b, --number-nonblank
    number: num             // -n, --number
    squeezeBlank: bool      // -s, --squeeze-blank
    showTabs: bool          // -T, --show-tabs
    showNonPrinting: bool   // -v, --show-nonprinting
    help: bool              // --help
    version: bool           // --version
    
    @Option("FILE")
    files: str[]
}
```

### Subcommand Definition

```hulo
cmd add {
    cmd volume {
        @Option("volumename")
        volumename: str
        
        @Option("provider")
        provider: symbol
    }
    
    cmd alias {
        @Option("aliasname")
        aliasname: str
        
        @Option("aliasvalue")
        aliasvalue: str
    }
}
```

### Cross-Platform Implementation

```hulo
// Implement Windows batch version of echo
impl bat.echo for bash.echo {
    cmd off {
        off() => $this null // do nothing
    }
    
    cmd on {
        on() => $this null // do nothing
    }
    
    echo($super.help) => $this $this.to_str()
}
```

## 🛠️ Build Targets

- `@hulo:build batch` - Generate Windows batch/cmd scripts
- `@hulo:build bash` - Generate Unix bash/sh scripts

## 📁 Project Structure

```
commands/
├── a/          # Commands starting with A
│   ├── add.hl
│   ├── arp.hl
│   └── ...
├── c/          # Commands starting with C
│   ├── cat.hl
│   ├── cls.hl
│   └── ...
├── e/          # Commands starting with E
│   ├── echo.impl.hl
│   ├── del.hl
│   └── ...
└── ...
```

## 🎯 Use Cases

- **System Administration**: Define cross-platform system management commands
- **Development Tools**: Create type-safe command-line utilities
- **Automation Scripts**: Generate portable script files
- **Educational**: Learn declarative command definition approaches

## 🤝 Contributing

Issues and Pull Requests are welcome!

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

