# Oct Blueprint Editor

A browser-based, node-graph editor for **Oct-style game config files**: the brace-and-bracket text format with `id Oct.…`, `type …`, `inherit …` and `<Reference>` values. Open a file and see every object as a node, wired together by inheritance and references, much like Unreal Engine Blueprints. Edit the code directly on the nodes as an expandable tree, then copy the result back out. A built-in 3D viewer previews the `.fbx` models and `.png` textures your config points to.

It is a single HTML file with no build step and no server. Everything runs locally in your browser, and your files are never uploaded.

<img width="1912" height="947" alt="Screenshot 2026-11-06 164010" src="https://github.com/user-attachments/assets/699ea616-19ef-430a-95ac-d594e13f8d2f" />

---

## Features

### Graph view
- **One node per object.** Every object with an `id` becomes a node, colored by its `type`.
- **Wires show relationships.**
  - White wires are `inherit` links.
  - Colored wires are `<Reference>` values, attached to the row that holds the reference.
  - Dotted wires show nesting (when "nested objects" is on).
- **Pan, zoom and drag.** Drag the background to pan, scroll to zoom, and drag nodes to rearrange them. **Fit view** and **Auto layout** are in the toolbar.
- **No overlap option.** Nodes can be kept from overlapping when you drag them or when they grow.
- **Filters.** Toggle reference wires and nested objects on or off.

### Edit the code on the nodes
- **Expandable tree on every node.** Each node shows its code as a tree: keys, values, nested `{ }` objects, `[ ]` lists and `//` comments. Click ▸ to expand and click any key or value to edit it.
- **Add and remove anything.** Use the `+ field`, `+ object`, `+ list` and `+ value` buttons, or the × on each row.
- **Lists of plain values** (such as name lists) open as a text box with one value per line.
- **Nodes resize to fit their text,** so long values and paths are never cut off.
- **Link by dragging.** Drag from a node's **Inherit** pin onto another node to add an `inherit` line. Drag from a **Self** pin to make the other node inherit from this one.
- **Side panel.** Select a node to edit its full source, rename its id (all `<ref>` and `inherit` lines that point to it are updated), duplicate it or delete it.
- **Create new objects.** Right-click the canvas or use **+ New node…** to start from a template (character type, variant, cosmetic, instance color, material and more).
- **Source / import.** Paste or edit the full text, or load a file with **Open…** or by dragging it onto the page.

### Model viewer
- Reads the `.fbx` and `.png` paths from your config (for the selected node, or the whole document).
- Previews `.fbx` models in 3D with orbit and zoom controls, and shows the triangle count.
- Applies `.png` textures found through the model's `material` references and `inherit` chains. The dropdown lets you choose auto, none or a specific PNG.
- Because your config only contains partial paths such as `/Art/characters/…`, click **Browse…** and choose the folder that contains them. Files are matched by path suffix, and a file with the same name elsewhere is flagged with an amber dot.
- Green dot: found · Amber: matched by file name only · Red: not found.

---

## Getting started

1. Download `index.html` (or clone this repository).
2. Open it in a modern desktop browser (Chrome, Edge, Firefox or Safari).
3. Click **Open…** and pick your config file, or drag the file onto the page. **Sample** loads a small demo.
4. Edit on the nodes or in the side panel.
5. Click **Copy** to copy the result, or **Save** to download it.

> The model viewer loads three.js and its FBX loader from a CDN the first time you open it, so that part needs an internet connection.

### Controls

| Action | How |
| --- | --- |
| Pan | Drag the background |
| Zoom | Scroll wheel |
| Move a node | Drag its header |
| Add a node | Right-click the canvas |
| Inherit link | Drag from a node's Inherit pin onto another node |
| Select a link | Click the wire |
| Delete a node or inherit link | Select it and press `Delete` |
| Expand or collapse a block | Click the ▸ / ▾ arrow |

---

## Supported format

The parser understands:

- Objects `{ … }` with `key = value` pairs and bare `key value` lines such as `id …`, `type …`, `inherit …` and flags like `abstract`
- Nested objects and lists, including selector objects like `?(name == Head) { … }`
- `<Reference>` values and function values such as `vector(…)`, `color(…)`, `rotation(…)`, `hsv(…)` and `tex(…)`
- `//` comments and blank lines

---

## Limitations

- **Formatting is normalized on output.** Indentation is rewritten with four spaces, so the text won't match the original character for character. Structure, comments and blank lines are kept. Review the diff before committing it to your game project.
- **Browsers can't read a typed disk path,** so the model viewer needs you to choose the folder with **Browse…** each time you open the page.
- **`<Reference>` wires are created by typing** the reference into a value, since dragging wires only creates `inherit` links.
- **Textures** come from the PNGs named in your config. Textures embedded in or referenced by the FBX itself are not loaded, and models that rely on vertex colors may look different than they do in-game.
- Desktop browsers are recommended. Folder selection isn't available on most phones.
- This tool is not affiliated with or endorsed by any game developer. It was written against the file format as seen in sample files, so unusual files may not parse. Please open an issue with an example.

---

## Privacy

Everything happens in your browser. Files are read locally and nothing is sent to a server. The only network requests are to download the 3D libraries for the model viewer.

---

## Built with

- Plain HTML, CSS and JavaScript, with no framework or build tooling
- [three.js](https://threejs.org/) r128, including `FBXLoader`, `OrbitControls` and `fflate`, for the model viewer

---

## Contributing

Bug reports and pull requests are welcome. If a config file won't parse or round-trips incorrectly, please attach a small snippet that reproduces it.

## License

Add your license here (for example MIT).<img width="1912" height="947" alt="Screenshot 2026-11-06 164010" src="https://github.com/user-attachments/assets/bb5b07aa-a1de-4846-9674-fc35e62f941d" />
