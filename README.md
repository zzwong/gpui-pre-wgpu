# gpui-pre-wgpu 0.3.9, patched

The published [`gpui-pre-wgpu`](https://crates.io/crates/gpui-pre-wgpu) 0.3.9
crate, a snapshot of Zed's `gpui_wgpu` at `zed@93d7456`, with three patches
carried until a published snapshot makes them unnecessary:

- **Try Vulkan before initialising the GL backend on Linux.** An instance
  created with `VULKAN | GL` initialises EGL to list a GL adapter and leaves
  Mesa's GL stack loaded although only Vulkan is used. GL stays the fallback
  when no Vulkan adapter can drive the surface. Not upstream as of 0.3.14; see
  [zed#63327](https://github.com/zed-industries/zed/issues/63327).
- **Allocate path-rasterization textures on demand.** The window-sized
  intermediate and 4x MSAA targets are created on the first frame that draws a
  vector path. Snapshots from 0.3.13 on draw paths as tiles and have no such
  textures, so this patch ends with 0.3.12.
- **Font weight moves the `wght` axis of a variable font on Linux.** The text
  system loaded a variable font at its default instance, so a requested weight
  only chose among static faces. Static faces render as before. Not upstream as
  of 0.3.14; see [zed#62832](https://github.com/zed-industries/zed/pull/62832).

`git diff 8e94e10` is the full carried delta against the published crate.

Licensed under Apache-2.0, as the upstream crate is.
