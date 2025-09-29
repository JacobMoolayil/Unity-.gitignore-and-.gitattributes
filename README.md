# Unity Project Git Setup

This repository includes configuration files to manage a **Unity project with Git**.  
They ensure that only necessary files are tracked, large generated files are ignored, and that scenes/prefabs can be merged cleanly.

---

## 📂 Files

### 1. `.gitignore`
Controls which files Git ignores.  
In this setup:
- **Ignored Unity cache & build folders**  
  ```
  Library/
  Temp/
  Obj/
  Build/
  Builds/
  Logs/
  UserSettings/
  ```
- **Ignored lightmapping & baked data**  
  - `Lightmap-*` (textures)  
  - `ReflectionProbe-*`  
  - `LightingData*.asset`  
  - `OcclusionCullingData.asset`  
  - `*.navmesh`  

  > `.meta` files are always kept so Unity maintains references.

- **Ignored extras**  
  - Logs (`*.log`)  
  - Asset Store Tools  
  - Memory captures, crash reports, profiler data  

This ensures the repo stays **small, clean, and portable**.

---

### 2. `.gitattributes`
Defines how Git handles line endings, diffs, and merges.  

Key rules:
- **Scripts** (`*.cs`)  
  → Use C# diffing + LF line endings.  
- **Shaders & text assets** (`*.cginc`, `*.shader`)  
  → Stored as text.  
- **Scenes & Prefabs** (`*.unity`, `*.prefab`, `*.anim`, `*.mat`, etc.)  
  → Mergeable using UnityYAMLMerge (resolves conflicts more safely).  
- **.meta files**  
  → Also mergeable (important for asset references).  
- **Binary assets** (`*.asset`)  
  → Tracked via Git LFS (Lightweight storage, avoids bloating repo).  

This setup ensures smooth **collaboration** across different OSes and developers.

---

## 🚀 How to Use
1. Place `.gitignore` and `.gitattributes` in the **root of your Unity project**.  
2. Ensure Git LFS is installed (`git lfs install`).  
3. When updating `.gitattributes`, run:
   ```bash
   git add --renormalize .
   ```
   to apply rules to existing files.  

---

## ✅ Benefits
- Prevents unnecessary files from being pushed.  
- Keeps repo lightweight and clean.  
- Scenes and prefabs are **mergeable** instead of causing conflicts.  
- Consistent cross-platform behavior (Windows, macOS, Linux).  

---

👉 With these configs, your Unity repo will stay **collaboration-friendly** and **maintainable**.
