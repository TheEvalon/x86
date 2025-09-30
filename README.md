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
 - **ZIP Archives** - Use .zip files containing a single .img (HDD) or .iso (CD-ROM); archives are automatically extracted in the browser

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
- **Mobile Optimizations** - Safe-area padding, compact controls, and single-column layouts on small screens
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

#### Option 1: Pre-configured OS Launcher (new.html)
1. **Browse OS Collection** - View all available operating systems in grid layout
2. **Select System** - Click any OS card to see details and launch options
3. **Launch OS** - Click launch button for immediate boot with optimal settings
4. **Dual Format Systems** - Choose "Boot Installed" or "Install from CD" for Windows XP
5. **ZIP Support** - Many OS assets can be provided as .zip; the launcher will fetch the archive and extract the inner .img/.iso automatically

#### Option 2: Custom Upload Interface (main.html)
1. **Configure Memory** - Select desired RAM and video memory amounts
2. **Upload Images** - Choose .img files for hard disk and/or .iso files for CD-ROM. You can also upload a .zip containing a single .img as HDA; it will be extracted in-browser
3. **Set Boot Order** - Select boot priority from the dropdown menu
4. **Start Emulator** - Click "Start Emulator" to begin
5. **Interact** - Click screen to capture mouse, use special keys menu as needed

## File Structure

```
86/
├── main.html              # Main emulator interface (custom OS upload)
├── new.html               # OS launcher interface (pre-configured systems)
├── basic.html             # Basic V86 example (reference)
├── index.html             # Directory index
├── README.md              # This documentation
├── OSes/                  # Operating system collection
│   ├── windows1/          # Windows 1.01
│   ├── windows2/          # Windows 2.x
│   ├── windows3/          # Windows 3.0
│   ├── windows311/        # Windows 3.11
│   ├── windows98/         # Windows 98
│   ├── windowsnt4/        # Windows NT 4.0
│   ├── windows2000/       # Windows 2000
│   ├── windowsxp/         # Windows XP (dual format)
│   ├── windowsce5/        # Windows CE 5.0
│   ├── reactos/           # ReactOS
│   ├── Haiku/             # Haiku OS
│   ├── DSL/               # Damn Small Linux
│   ├── android/           # Android x86
│   ├── hbcd/              # Hiren's Boot CD
│   └── CECollection/      # CE Collections
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
 - **ZIP Handling** - Client-side archive extraction powered by JSZip for .zip HDD and ISO assets

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

### Pre-configured Collection (new.html)
- **Windows 1.01** - First Windows version (1985)
- **Windows 2.x** - Early overlapping windows
- **Windows 3.0/3.11** - Program Manager era
- **Windows 98** - Popular 9x series
- **Windows NT 4.0** - Professional NT kernel
- **Windows 2000** - Business stability
- **Windows XP** - Luna interface (dual format)
- **Windows CE 5.0** - Embedded/mobile Windows
- **ReactOS** - Open source Windows NT clone
- **Haiku** - BeOS-inspired modern OS
- **Android x86** - Android for PC
- **Damn Small Linux** - Tiny Linux distribution
- **Hiren's Boot CD** - System rescue tools

### Additional Compatible Systems
- **MS-DOS** 6.22 and earlier
- **Windows 95/ME** - Full support
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

## License and Legal

### V86 Emulator License
This project builds upon the **V86 emulator** created by **copy (Fabian Hemmer)**:
- V86 is released under the **BSD 2-Clause License**
- Original project: [github.com/copy/v86](https://github.com/copy/v86)
- All core emulation functionality is provided by V86
- WebAssembly binaries and JavaScript libraries remain under original V86 license

### Interface License
The web interface components (main.html, new.html) and documentation are provided as educational material:
- Interface design and implementation by this project
- Built specifically for V86 integration
- Provided for educational and preservation purposes

### Operating Systems
- Operating system images are **not included** in this repository
- Users must provide their own legally obtained OS images
- Ensure compliance with software licensing terms
- This project is for **educational and preservation purposes only**

### Disclaimer
- This is an educational project demonstrating V86 capabilities
- No warranty provided for any functionality
- Users responsible for compliance with all applicable licenses
- Operating systems and software must be legally obtained

## Credits and Acknowledgments

### Core Technology
- **V86 Emulator** - Core x86 emulation engine by **copy (Fabian Hemmer)**
  - GitHub: [copy/v86](https://github.com/copy/v86)
  - Website: [copy.sh](https://copy.sh/)
  - An incredible achievement in WebAssembly-based x86 emulation
- **SeaBIOS** - Open source x86 BIOS implementation
- **WebAssembly** - Core runtime technology enabling near-native performance

### Interface Development
- **Web Interface** - Modern responsive UI built for this project
- **OS Launcher** - Pre-configured system collection interface
- **Special Keys Implementation** - Hardware-accurate scancode injection
- **File Management** - Drag-and-drop upload and OS organization

### Operating System Collection
- Various operating systems included for educational and preservation purposes
- Each OS configured with optimal memory and compatibility settings
- Historical systems from Windows 1.01 through modern alternatives

## Links

- [V86 Project](https://github.com/copy/v86) - Original emulator by copy
- [copy.sh](https://copy.sh/) - Creator's website and online demos
- [SeaBIOS](https://www.seabios.org/) - BIOS firmware
- [WebAssembly](https://webassembly.org/) - Core technology
 - Side Project: [games.ioblako.com](https://games.ioblako.com)

## Contact

For questions, feedback, or collaboration:

- Email: [info@iOblako.com](mailto:info@iOblako.com)

## Windows 2000 Setup with QEMU

For installing Windows 2000 to use with this emulator, you can use QEMU to create and install the OS, then use the resulting disk image in V86.

### 1. Create Hard Disk Image (Minimum for Windows 2000)

```bash
# Create a 2GB hard disk image (minimum supported size for Windows 2000)
qemu-img create -f raw win2k.img 2G
```

**Alternative sizes:**
- **Minimum**: 2GB (tight fit, basic installation only)
- **Recommended**: 4GB (allows for some software installation)
- **Comfortable**: 8GB (plenty of space for applications)

### 2. Install Windows 2000 with QEMU

```bash
# One-line command for Windows 2000 installation
qemu-system-i386 -m 512 -hda win2k.img -cdrom /path/to/windows2000.iso -boot d -vga cirrus -audiodev pa,id=audio0 -device sb16,audiodev=audio0 -netdev user,id=net0 -device rtl8139,netdev=net0 -rtc base=localtime -no-acpi -cpu pentium3 -enable-kvm
```

**Multi-line version (same command):**
```bash
qemu-system-i386 \
  -m 512 \
  -hda win2k.img \
  -cdrom /path/to/windows2000.iso \
  -boot d \
  -vga cirrus \
  -audiodev pa,id=audio0 \
  -device sb16,audiodev=audio0 \
  -netdev user,id=net0 \
  -device rtl8139,netdev=net0 \
  -rtc base=localtime \
  -no-acpi \
  -cpu pentium3 \
  -enable-kvm
```

**Command breakdown:**
- `-m 512` - 512MB RAM (optimal for Windows 2000)
- `-hda win2k.img` - Use created disk image as primary hard drive
- `-cdrom windows2000.iso` - Mount Windows 2000 installation ISO
- `-boot d` - Boot from CD-ROM first for installation
- `-vga cirrus` - Compatible VGA adapter for Windows 2000
- `-audiodev pa,id=audio0 -device sb16,audiodev=audio0` - Sound Blaster 16 audio (modern QEMU syntax)
- `-netdev user,id=net0 -device rtl8139,netdev=net0` - Network adapter
- `-rtc base=localtime` - Use local time (important for Windows)
- `-no-acpi` - Disable ACPI (better compatibility with older Windows)
- `-cpu pentium3` - Pentium 3 CPU (period-appropriate)
- `-enable-kvm` - Enable hardware acceleration (if available)

### 3. After Installation - Boot from Hard Disk

```bash
# One-line command to boot installed Windows 2000
qemu-system-i386 -m 512 -hda win2k.img -vga cirrus -audiodev pa,id=audio0 -device sb16,audiodev=audio0 -netdev user,id=net0 -device rtl8139,netdev=net0 -rtc base=localtime -no-acpi -cpu pentium3 -enable-kvm
```

### 4. Using the Image in V86 Emulator

Once Windows 2000 is installed:

1. **Copy the image file** to your web server directory
2. **Upload via interface** - Use the "Choose HDA File" button in main.html
3. **Configure memory** - Set RAM to 512MB, Video Memory to 32MB
4. **Set boot order** - Select "Hard Disk First" or "Hard Disk Only"
5. **Start emulator** - Windows 2000 should boot from the disk image

### Installation Tips

#### During Windows 2000 Installation:
- **Partition**: Create a single primary partition using all available space
- **File System**: Choose NTFS for better performance and features
- **Components**: Minimal installation to save space and improve performance
- **Drivers**: Windows 2000 should detect most emulated hardware automatically

#### For V86 Compatibility:
- **Keep installation minimal** - Avoid unnecessary software
- **Disable visual effects** - Use classic appearance for better performance
- **Install essential drivers** - Basic VGA and sound drivers should work
- **Network**: Basic networking should function in both QEMU and V86

### Performance Notes

- **QEMU Installation**: Faster, hardware acceleration available
- **V86 Runtime**: Slower but runs in browser, good for demonstration
- **File Size**: Keep disk images as small as possible for web use
- **Memory**: 512MB is optimal balance of functionality and performance

### Troubleshooting

#### If QEMU installation fails:
- Try without `-enable-kvm` on systems without KVM support
- Use `-cpu qemu32` instead of `pentium3` for broader compatibility
- Increase memory to `-m 1024` if installation is very slow

#### If V86 won't boot the image:
- Ensure Windows 2000 is fully shut down (not hibernated)
- Try with different memory configurations in V86
- Check browser console for any error messages

---

**Note**: This is an educational and preservation project. Ensure you have proper licenses for any operating systems or software you run in the emulator.
