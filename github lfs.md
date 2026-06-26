# GitHub Large File Storage (LFS) 

GitHub LFS (Large File Storage) is an extension to Git that helps manage large files in a repository.

Normally, Git stores the complete history of every file. This works well for source code, but it becomes inefficient when storing large files like videos, datasets, machine learning models, or archives. Every time a large file changes, Git saves another version, causing the repository to grow quickly.
Git LFS solves this problem by storing the actual large files separately, while Git only keeps a small pointer file that references the real file.
This keeps the library (Git repository) much smaller and faster to work with.

---

# How It Works?
You tell Git LFS which file types should use LFS (for example, *.zip or *.onnx).
When you add and commit those files, Git stores a small pointer file in the repository instead of the actual file.
The real file is uploaded to GitHub's LFS storage.
When someone clones the repository, Git automatically downloads the real files from GitHub LFS.


---

# How to Run

- Initialize Git LFS

```bash
git lfs install
```

Expected output:

```text
Git LFS initialized.
```

- Track Large Files
Tell Git LFS which file types should be stored using LFS.

Example:

```bash
git lfs track "*.zip"
git lfs track "*.mp4"
git lfs track "*.csv"
```

This creates or updates:

```text
.gitattributes
```

Example:

```text
*.zip filter=lfs diff=lfs merge=lfs -text
*.pdf filter=lfs diff=lfs merge=lfs -text
```

> **Always commit `.gitattributes`** so everyone cloning the repository uses the same LFS rules.


- Add Files

Add files normally.

```bash
git add "model.pdf"
git add dataset.zip
git add .gitattributes
```

- Commit:

```bash
git commit -m "temp"
```

- Push:

```bash
git push origin main
```

Git LFS uploads the actual file automatically.


- Clone a Repository

Clone normally.

```bash
git clone https://github.com/suriaman123/temp.git
```

Git LFS automatically downloads the large files.


- Check Tracked Files

See which file patterns are tracked:

```bash
git lfs track
```

Example output:

```text
Listing tracked patterns
*.pdf
*.zip
*.csv
```

- List Files Stored in LFS

```bash
git lfs ls-files
```

Example:

```text
abc123 model.pdf
def456 dataset.zip
```

- Stop Tracking a File Type

If you no longer want a file type stored in LFS:

```bash
git lfs untrack "*.zip"
```

Commit the updated `.gitattributes`.

---

# Common Use Cases
Git LFS is useful for files that are large or change infrequently, such as:
Machine learning models (.pt, .onnx, .ckpt)
Datasets (.csv, .parquet, .zip)
Videos (.mp4, .mov)
Images and design assets (.psd, .png)
Game assets (.fbx, .blend)
Large archives (.zip, .7z, .tar.gz)
 

---

# Benefits
Keeps your Git repository small.
Makes cloning and fetching repositories faster.
Prevents Git history from becoming bloated with large files.
Lets you work with large assets using the same Git commands (git add, git commit, and git push).

In short, GitHub LFS lets Git manage large files efficiently by storing the actual files separately while keeping lightweight references in your repository.


---

# Common Commands

Initialize:

```bash
git lfs install
```

Track:

```bash
git lfs track "*.zip"
```

View tracked patterns:

```bash
git lfs track
```

List LFS files:

```bash
git lfs ls-files
```

Pull missing LFS files:

```bash
git lfs pull
```

Fetch all LFS objects:

```bash
git lfs fetch --all
```

Prune old local LFS objects:

```bash
git lfs prune
```

---

# Common Workflow

```bash
# Install LFS (once)
git lfs install

# Track file types
git lfs track "*.pdf"

# Stage files
git add .gitattributes
git add model.pdf

# Commit
git commit -m "Add model"

# Push
git push origin main
```

---

# Summary

Git LFS works just like Git for everyday use:

1. Install Git LFS.
2. Run `git lfs install` once.
3. Track the file types you want.
4. Commit `.gitattributes`.
5. Add, commit, and push files as usual.

Git automatically stores lightweight pointers in the repository while Git LFS manages the actual large file contents.

useful link: https://youtu.be/judfGU0f6QU?si=1WULLlYmyJBcxxr3
