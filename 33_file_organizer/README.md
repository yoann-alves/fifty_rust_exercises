# Exercise 33: File Organizer

## 🎯 Objectives

Create a file organization utility:

- Sort files by extension into folders
- Create folders for each file type
- Support batch renaming operations
- Preview changes before applying

## 📚 Concepts

- Filesystem operations
- Path manipulation
- Extension extraction
- Batch operations
- Safe file operations

## 📖 Background

**File organization** helps maintain clean directories. Instead of dozens of mixed files in one folder, group them logically by type.

**Before organization:**

```
downloads/
├── photo1.jpg
├── document.pdf
├── photo2.jpg
├── song.mp3
└── notes.txt
```

**After organization:**

```
downloads/
├── images/
│   ├── photo1.jpg
│   └── photo2.jpg
├── documents/
│   ├── document.pdf
│   └── notes.txt
└── music/
    └── song.mp3
```

**Common categorizations:**

```
Images:     .jpg, .png, .gif, .bmp
Documents:  .pdf, .doc, .txt, .docx
Music:      .mp3, .wav, .flac
Videos:     .mp4, .avi, .mkv
Archives:   .zip, .tar, .gz
```

**Batch renaming** is useful for:

- Sequential numbering: photo_001.jpg, photo_002.jpg
- Adding prefixes: vacation_sunset.jpg
- Adding dates: 2025-01-15_document.pdf
- Case normalization: PHOTO.JPG → photo.jpg

## ⚙️ Requirements

**First Pass:**

- ✅ Scans directory for files
- ✅ Groups files by extension
- ✅ Creates folders for each type
- ✅ Moves files to appropriate folders
- ✅ No compiler warnings

**Second Pass:**

- ✅ **Zero warnings**: `cargo clippy` must pass clean
- ✅ **Formatted**: Run `cargo fmt`
- ✅ **Documented**: Explain organization strategy
- ✅ **Preview mode**:
  - Show what would happen (dry run)
  - Require confirmation before changes
  - Display file count per category
- ✅ **Folder mapping**:
  - Customizable extension → folder rules
  - Default categories (images, documents, music, etc.)
  - Unknown extensions → "others" folder
- ✅ **Batch renaming**:
  - Pattern-based renaming
  - Sequential numbering
  - Prefix/suffix addition
  - Date-based naming
- ✅ **Safety features**:
  - Detect name conflicts
  - Handle duplicates (rename with suffix)
  - Don't lose data
- ✅ **Error handling**:
  - Permission denied
  - Invalid filenames
  - Files already exist
  - Disk full
- ✅ **Edge cases**:
  - Files without extension
  - Hidden files (start with .)
  - Very large directories
  - Symbolic links

## 🚫 Constraints

- Standard library only
- Safe operations (no data loss)
- Proper error handling

## 💡 Approaches

**Extension detection:**

- Extract from filename
- Handle case variations (.JPG vs .jpg)
- Files without extension → decide what to do

**Folder mapping strategies:**

- Hard-coded categories
- Configuration file
- User-defined rules
- Default category for unknowns

**Operation flow:**

- Scan and analyze first
- Show preview
- Get confirmation
- Execute operations
- Report results

**Batch rename patterns:**

- Replace parts of filename
- Add counters
- Include metadata (date, size)
- Preserve extensions

**Conflict resolution:**

- Append number (file_1.txt, file_2.txt)
- Ask user
- Skip
- Overwrite with warning

**Safety mechanisms:**

- Preview before executing
- Confirmation prompts
- Log operations
- Ability to undo (optional)

## ✅ Validation

**Test directory:**

```
messy/
├── photo1.JPG
├── photo2.jpg
├── report.pdf
├── song.mp3
├── video.mp4
├── notes.txt
└── readme
```

**After organizing:**

```
messy/
├── images/
│   ├── photo1.JPG
│   └── photo2.jpg
├── documents/
│   ├── report.pdf
│   └── notes.txt
├── music/
│   └── song.mp3
├── videos/
│   └── video.mp4
└── others/
    └── readme
```

**Preview output:**

```
Preview of changes:
  → Creating folder: images/
  → Creating folder: documents/
  → Creating folder: music/
  → Creating folder: videos/
  → Creating folder: others/

  Moving files:
    photo1.JPG → images/
    photo2.jpg → images/
    report.pdf → documents/
    notes.txt → documents/
    song.mp3 → music/
    video.mp4 → videos/
    readme → others/

Total: 7 files will be moved into 5 folders
Proceed? (y/n):
```

**Batch rename example:**

```
Before rename:
  images/photo1.jpg
  images/photo2.jpg

After rename (pattern: "vacation_{num}"):
  images/vacation_001.jpg
  images/vacation_002.jpg
```

**Conflict handling:**

```
Error: File "document.pdf" already exists in documents/
Options:
  1. Rename to "document_1.pdf"
  2. Skip this file
  3. Overwrite
Your choice:
```

## 🔍 Challenge

Add intelligent categorization by inspecting file content (not just extension), or create an undo system that can reverse multiple organization operations.

---

**Previous:** [32_directory_tree](../32_directory_tree/README.md) | **Next:** [34_duplicate_finder](../34_duplicate_finder/README.md)
