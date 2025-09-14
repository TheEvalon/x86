# V86 x86 Emulator Web Interface

A modern, feature-rich web interface for the V86 x86 emulator that provides an easy-to-use platform for running vintage operating systems and software in the browser.

## Features

### 🖥️ **Core Emulation**
- **x86 PC Emulation** - Full x86 processor emulation via V86
- **Memory Configuration** - Configurable RAM (128MB - 1GB) and Video Memory (8MB - 64MB)
- **Boot Order Control** - Flexible boot priority: HDA first, CDROM first, or single device
- **Multiple Storage** - Support for both hard disk (.img) and CD-ROM (.iso) images

### 💾 **File Support**
- **Hard Disk Images** - Upload and mount .img files for persistent storage
- **CD-ROM Images** - Mount .iso files for software installation and live systems
- **Drag & Drop** - Easy file selection with visual feedback
- **File Validation** - Automatic file type validation and error handling

### 🎮 **Input & Control**
- **Mouse Capture** - Pointer lock for seamless mouse control
- **Keyboard Capture** - Full keyboard input forwarding to virtual machine
- **Special Keys Menu** - Comprehensive special key support including:
  - System keys (Ctrl+Alt+Del, Ctrl+Shift+Esc)
  - Function keys (F1-F12)
  - Navigation keys (Alt+Tab, Alt+F4, Windows key)
  - Special characters (Print Screen, Scroll Lock, Pause/Break, Insert)

### 🎨 **Modern UI**
- **Responsive Design** - Clean, professional interface that works on all devices
- **Real-time Status** - Live feedback on emulator state and operations
- **Visual Indicators** - Clear status indicators for mouse/keyboard capture
- **Organized Controls** - Logical grouping of configuration options

## Quick Start

### Prerequisites
- Modern web browser with WebAssembly support
- Web server (for serving files due to CORS restrictions)

### Setup
1. **Clone or download** this repository
2. **Start a web server** in the project directory:
   ```bash
   python3 -m http.server 8080
   ```
3. **Open browser** and navigate to `http://localhost:8080/main.html`

### Usage
1. **Configure Memory** - Select desired RAM and video memory amounts
2. **Upload Images** - Choose .img files for hard disk and/or .iso files for CD-ROM
3. **Set Boot Order** - Select boot priority from the dropdown menu
4. **Start Emulator** - Click "Start Emulator" to begin
5. **Interact** - Click screen to capture mouse, use special keys menu as needed

## File Structure

```
86/
├── main.html              # Main emulator interface
├── basic.html             # Basic V86 example (reference)
├── README.md              # This documentation
└── build/                 # V86 core files
    ├── libv86.js          # V86 JavaScript library
    ├── v86.wasm           # WebAssembly emulator core
    ├── seabios.bin        # SeaBIOS firmware
    ├── vgabios.bin        # VGA BIOS
    └── screen.js          # Screen adapter
```

## Configuration Options

### Memory Settings
| Option | Values | Default | Description |
|--------|--------|---------|-------------|
| RAM | 128MB, 256MB, 512MB, 1024MB | 512MB | System memory |
| Video Memory | 8MB, 16MB, 32MB, 64MB | 32MB | Graphics memory |

### Boot Order Options
| Option | Description |
|--------|-------------|
| Hard Disk First | Boot from HDA, fallback to CDROM |
| CD-ROM First | Boot from CDROM, fallback to HDA |
| Hard Disk Only | Boot only from HDA |
| CD-ROM Only | Boot only from CDROM |

### Special Keys
The interface provides hardware-accurate scancode injection for special keys:

#### System Keys
- **Ctrl+Alt+Delete** - System interrupt/secure attention
- **Ctrl+Alt+End** - Alternative secure attention
- **Ctrl+Shift+Esc** - Task manager shortcut

#### Function Keys
- **F1-F12** - Standard function keys with proper scancodes

#### Navigation
- **Alt+Tab** - Window switching
- **Alt+F4** - Close application
- **Windows Key** - Start menu/system key
- **Menu Key** - Context menu

#### Special Characters
- **Print Screen** - Screen capture
- **Scroll Lock** - Scroll mode toggle
- **Pause/Break** - System pause
- **Insert** - Insert mode toggle

## Technical Details

### Architecture
- **Frontend** - Modern HTML5/CSS3/JavaScript interface
- **Emulator** - V86 WebAssembly-based x86 emulator
- **Storage** - Browser-based file handling with FileReader API
- **Input** - Pointer Lock API for mouse, scancode injection for keyboard

### Browser Compatibility
- **Chrome/Chromium** 57+ (recommended)
- **Firefox** 52+
- **Safari** 11+
- **Edge** 16+

### Performance Notes
- **Memory Usage** - Configured RAM + ~100MB overhead
- **CPU Usage** - Varies by guest OS and applications
- **Storage** - Files loaded entirely into browser memory
- **Network** - Only initial asset loading, no ongoing network required

## Supported Operating Systems

The emulator can run various x86 operating systems:

### Tested & Working
- **MS-DOS** 6.22 and earlier
- **Windows 95/98/ME** - Full support
- **Windows XP** - Works with sufficient RAM
- **Various Linux distributions** - Lightweight distros recommended
- **FreeDOS** - Excellent compatibility

### Performance Tips
- **Lightweight OS** - Choose minimal installations for better performance
- **Sufficient RAM** - Allocate appropriate memory for target OS
- **Browser Resources** - Close unnecessary tabs for optimal performance

## Troubleshooting

### Common Issues

#### Emulator Won't Start
- Ensure all files are served via HTTP/HTTPS (not file://)
- Check browser console for WebAssembly errors
- Verify uploaded files are valid disk images

#### Mouse/Keyboard Not Working
- Click "Capture Mouse" button or click screen area
- Use Ctrl+Alt to release mouse capture
- Ensure keyboard capture is enabled

#### Poor Performance
- Reduce allocated memory if system is constrained
- Close other browser tabs and applications
- Try a lighter guest operating system

#### File Upload Issues
- Verify file extensions (.img for HDA, .iso for CDROM)
- Check file size limits (browser dependent)
- Ensure files are not corrupted

### Debug Information
Enable browser developer tools (F12) to view:
- Console logs for emulator events
- Network tab for asset loading issues
- Memory usage in Performance tab

## Development

### Customization
The interface is built with vanilla HTML/CSS/JavaScript for easy modification:

- **Styling** - Modify CSS variables in `<style>` section
- **Memory Options** - Edit dropdown values in HTML
- **Special Keys** - Add entries to `special-keys-menu` section
- **Boot Options** - Modify boot order configurations

### V86 Integration
Key V86 API methods used:
- `new V86(config)` - Initialize emulator
- `keyboard_send_scancodes()` - Send special keys
- `lock_mouse()` - Capture mouse input
- `keyboard_set_status()` - Enable/disable keyboard

### Contributing
1. Fork the repository
2. Create feature branch
3. Test thoroughly with various OS images
4. Submit pull request with detailed description

## License

This project builds upon the V86 emulator. Please refer to the original V86 project for licensing terms.

## Credits

- **V86 Emulator** - Core emulation engine by copy (Fabian Hemmer)
- **SeaBIOS** - Open source x86 BIOS implementation
- **Interface Design** - Modern web interface implementation

## Links

- [V86 Project](https://github.com/copy/v86) - Original emulator
- [SeaBIOS](https://www.seabios.org/) - BIOS firmware
- [WebAssembly](https://webassembly.org/) - Core technology

---

**Note**: This is an educational and preservation project. Ensure you have proper licenses for any operating systems or software you run in the emulator.
