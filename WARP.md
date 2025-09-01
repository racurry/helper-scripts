# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Repository Overview

This is a collection of utility scripts for file and media processing tasks, primarily written in Ruby with some bash scripts. The scripts are designed to be standalone command-line tools for common file manipulation tasks.

## Architecture

### Script Organization
- **Location**: All executable scripts are in the `bin/` directory
- **Languages**: Primarily Ruby scripts with bash for system-level operations
- **Pattern**: Most Ruby scripts follow a consistent pattern with shared constants and utility functions
- **Dependencies**: Scripts rely on external tools like ImageMagick, ffmpeg, and tesseract

### Common Patterns
All Ruby scripts share these architectural elements:
- `IGNORED_FILES = %w{.DS_Store .. .}` - Standard files to skip during directory operations
- `require 'fileutils'` and `require 'shellwords'` - Core dependencies for file operations and shell safety
- Input validation with user-friendly error messages
- `Shellwords.escape()` for safe shell command execution
- Support for both single files and directory batch processing

### Script Categories
1. **Media Conversion**: `mkvtomp4`, `avitomp4`, `vidmerge` (require ffmpeg)
2. **Image Processing**: `backgroundify`, `iconify`, `ocrify` (require ImageMagick/tesseract)
3. **File Management**: `folderify`, `unfolderify`, `batch_rename`, `swap_extension`, `filename_fixer`

## Common Commands

### Running Scripts
All scripts are executable and located in the `bin/` directory:
```bash
./bin/script_name [arguments]
```

### Media Processing
```bash
# Convert MKV files to MP4
./bin/mkvtomp4 filename.mkv
./bin/mkvtomp4 folder_of_mkvs/

# Convert AVI files to MP4
./bin/avitomp4 filename.avi
./bin/avitomp4 folder_of_avis/

# Merge multiple videos
./bin/vidmerge vid1.mp4 vid2.mp4 vid3.mp4 output_name
./bin/vidmerge -d vid1.mp4 vid2.mp4 output_name  # Delete originals
```

### Image Processing
```bash
# Add background color to transparent PNGs
./bin/backgroundify source_dir/ target_dir/ '#555555'

# Create macOS icon sets
./bin/iconify source_image.png

# OCR processing (creates searchable PDF)
./bin/ocrify image_file.png
```

### File Management
```bash
# Create folders for each file and move files into them
./bin/folderify directory_name/

# Flatten folder structure (opposite of folderify)
./bin/unfolderify

# Batch rename files with sequential numbering
./bin/batch_rename directory_name/ "File prefix"

# Change file extensions
cd directory_of_files/
../bin/swap_extension old_ext new_ext

# Clean up filenames (remove dots, digits, extra spaces)
./bin/filename_fixer directory_name/ dedot strip_digits
```

## Development Guidelines

### Adding New Scripts
1. Place executable scripts in the `bin/` directory
2. For Ruby scripts, use the standard shebang: `#!/usr/bin/env ruby`
3. Include the common imports: `fileutils`, `shellwords`
4. Define `IGNORED_FILES` constant for directory operations
5. Use `Shellwords.escape()` for all shell command parameters
6. Provide clear error messages and input validation

### Testing Scripts
Test scripts manually with:
- Single files and directories
- Edge cases (empty directories, missing files, special characters in filenames)
- Both valid and invalid inputs to verify error handling

### Dependencies
Ensure required external tools are installed:
- **ImageMagick**: For `backgroundify`, `iconify`, `ocrify`
- **ffmpeg**: For `mkvtomp4`, `avitomp4`, `vidmerge`
- **tesseract**: For `ocrify` (OCR functionality)

Install via Homebrew:
```bash
brew install imagemagick ffmpeg tesseract
```

### Shell Safety
Always use `Shellwords.escape()` when passing user input or file paths to shell commands to prevent injection attacks and handle special characters properly.

### Error Handling
Follow the established pattern of descriptive, casual error messages that clearly indicate what went wrong and what the user should do.
