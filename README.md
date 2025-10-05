# SignAnnotate: A Suite of Tools for BSL Research

This project is dedicated to building Python-based tools that automate manual processes for researchers working with the British Sign Language (BSL) Corpus.

## Tool #1: The Offset Identifier (Complete & Delivered)

A Python-based tool for identifying BSL video files with poor offset alignment in the British Sign Language Corpus. This tool processes EAF annotation files and corresponding video files to detect synchronisation issues between multiple camera angles.

The tool extracts frames from video files at the midpoint of "GOOD" sign annotations and displays them side-by-side for visual inspection. Users can quickly identify files where video timing does not match annotation timing, indicating offset alignment problems.

## Installation

### Prerequisites

- Python 3.7 or higher
- FFmpeg (for video frame extraction)

### Setup

```bash
git clone https://github.com/nj-09/bsl-offset-identifier.git
cd bsl-offset-identifier
pip install -r requirements.txt
```

### Install FFmpeg

**macOS:**
```bash
brew install ffmpeg
```

**Ubuntu/Debian:**
```bash
sudo apt-get install ffmpeg
```

**Windows:**
Download from https://ffmpeg.org/download.html

## Configuration

### Option 1: Environment Variables
```bash
export BSL_EAF_FOLDER="/path/to/eaf/files"
export BSL_VIDEO_FOLDER="/path/to/video/files"
```

### Option 2: Data Directory Structure
```
bsl-offset-identifier/
├── CAVA_Data/
│   ├── EAFs/          # Place .eaf files here
│   └── Videos/        # Place video files here
└── [other files]
```

## Usage

### Basic Usage
```bash
python run_bot.py
```

### Testing Setup
```bash
python test_cava.py
```

## How It Works

1. **File Discovery**: Scans for EAF files with minimum 20 total annotations and at least 5 "GOOD" signs
2. **Video Processing**: Extracts frames from corresponding video files at annotation midpoints (47.5%)
3. **Offset Handling**: Applies TIME_ORIGIN offsets from EAF media descriptors
4. **Visual Interface**: Displays frames side-by-side in a web browser
5. **Decision Tracking**: Records accept/reject decisions in CSV format
6. **Resume Capability**: Skips previously processed files

## File Structure

```
bsl-offset-identifier/
├── run_bot.py                   # Main execution script
├── test_cava.py                 # Setup validation
├── requirements.txt             # Python dependencies
├── src/                         # Core source code
│   ├── simple_viewer.py         # Core processing logic
│   ├── decision_server.py       # HTTP server for decision handling
│   ├── collect_decisions.py     # Decision file aggregation
│   └── save_decision.py         # Manual decision recording
├── docs/                        # Documentation
├── debug_tools/                 # Debug utilities
├── decisions.csv               # Output decision tracking (generated)
└── README.md                   # This file
```

## Output

The tool generates:
- **HTML interface**: Browser-based assessment interface
- **CSV file**: Decision tracking with filename, decision, timestamp, and notes
- **Console output**: Processing progress and file information

### CSV Format
```csv
filename,decision,timestamp,notes
BF01F28WDC.eaf,accept,2024-10-03T14:23:15,Good alignment
LN23C.eaf,reject,2024-10-03T14:28:42,Poor timing
```

## Data Source Requirements

### BSL Corpus Data Structure
This tool requires EAF files with **ID gloss annotations** (RH-IDgloss, LH-IDgloss tiers containing signs like "GOOD", "HELLO", etc.).

**Important Note**: Public CAVA narrative files contain only English translations, not ID gloss annotations. For full functionality, this tool requires:
- **Conversation files** with detailed ID gloss annotations (UCL internal access)
- **Annotated EAF files** with RH-IDgloss/LH-IDgloss tiers

### Input Files
- **EAF files**: ELAN annotation files with RH-IDgloss or LH-IDgloss tiers
- **Video files**: Corresponding video files (.mov, .mp4, .avi)
- **Minimum requirements**: 20 total annotations, 5 "GOOD" signs

### Performance
- Target processing speed: 50 files per hour
- Frame extraction: <2 seconds per annotation
- Decision recording: <1ms per entry

## Requirements Met

- Cross-platform compatibility (Windows, macOS, Linux)
- Configurable file paths
- Dual video processing (multiple camera angles)
- Accurate offset handling from EAF media descriptors
- Resume functionality for interrupted sessions
- Batch processing capability
- CSV decision tracking

## Troubleshooting

### Common Issues

**No files found:**
- Verify EAF files contain RH-IDgloss or LH-IDgloss tiers (not just English translations)
- Public CAVA narrative files only have translation tiers - conversation files with ID gloss annotations are required
- Check minimum annotation requirements (20 total, 5 "GOOD")
- Ensure video files are in correct location

**FFmpeg errors:**
- Verify FFmpeg installation: `ffmpeg -version`
- Check video file format compatibility
- Ensure sufficient disk space for temporary files

**Permission errors:**
- Check read/write permissions for data directories
- Verify network access if using remote file paths

### File Format Support
- **EAF files**: ELAN annotation files
- **Video files**: .mov, .mp4, .avi formats
- **Output**: HTML, CSV formats

## License

This tool is designed for academic research use with the British Sign Language Corpus.

## Tool #2: Automatic Sign Recognition (🚧 In Progress)

This is the in-progress module for building a machine learning pipeline to automatically suggest sign annotations from raw video. This component is under active development.
