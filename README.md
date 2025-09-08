# hdgrace Repository – Download Links & AI-Folder Archive

GitHub’s REST API supports downloading the **entire** repository as a ZIP or TAR archive. Unfortunately it does *not* support creating ZIPs of individual sub-directories directly via a single API call. Below you’ll find:

1. Links to grab the **entire** `hdgrace` repo as ZIP or TAR  
2. How to list and download the `ai/` folder contents via the Contents API  
3. A sample shell script to automate fetching and zipping only the `ai/` folder

---

## 1. Full-Repo Archives

- ZIP (default branch, e.g. `main` or `master`):
  ```
  https://api.github.com/repos/kangheedon1/hdgrace/zipball
  ```
- TAR (default branch):
  ```
  https://api.github.com/repos/kangheedon1/hdgrace/tarball
  ```
- ZIP (explicit `main` branch via GitHub UI):
  ```
  https://github.com/kangheedon1/hdgrace/archive/refs/heads/main.zip
  ```

These URLs download the **entire** repository, not a sub-directory.

---

## 2. Listing `ai/` Folder via API

To see all files under the `ai/` folder:

```bash
curl -H "Accept: application/vnd.github.v3+json" \
     https://api.github.com/repos/kangheedon1/hdgrace/contents/ai?ref=main
```

Each entry in the JSON response includes a `"download_url"` field—for example:

```json
{
  "name": "model.py",
  "path": "ai/model.py",
  "download_url": "https://raw.githubusercontent.com/kangheedon1/hdgrace/main/ai/model.py",
  ...
}
```

---

## 3. Sample Script: Download & Zip `ai/` Folder

```bash name=download_ai_folder.sh
#!/usr/bin/env bash
# Download all files in hdgrace/ai and create ai_folder.zip

OWNER="kangheedon1"
REPO="hdgrace"
BRANCH="main"
API_URL="https://api.github.com/repos/$OWNER/$REPO/contents/ai?ref=$BRANCH"
TMPDIR=$(mktemp -d)
ZIPFILE="ai_folder.zip"

echo "Listing ai/ folder..."
files=$(curl -s -H "Accept: application/vnd.github.v3+json" "$API_URL" \
         | jq -r '.[] | select(.type=="file") | .download_url')

echo "Downloading ${#files[@]} files…"
for url in $files; do
  filename=$(basename "$url")
  curl -sL "$url" -o "$TMPDIR/$filename"
done

echo "Creating ZIP archive $ZIPFILE…"
(cd "$TMPDIR" && zip -j "../$ZIPFILE" ./*)

echo "Done. Archive located at ./$ZIPFILE"
```

1. **Prerequisites:**  
   - `curl`  
   - `jq` (to parse JSON)  
   - `zip`  

2. **Usage:**  
   ```bash
   chmod +x download_ai_folder.sh
   ./download_ai_folder.sh
   ```
