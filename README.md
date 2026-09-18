# gpui-pre-wgpu (patched for diffz)

This is the published [`gpui-pre-wgpu`](https://crates.io/crates/gpui-pre-wgpu) 0.3.3
crate, a [gpui-kit](https://github.com/longbridge/gpui-kit) snapshot of Zed's
`gpui_wgpu` at `zed@5b055fa789a8b8d38ac951a6e0cde272f66b4495`, with two patches
carried for [diffz](https://github.com/zzwong/diffz) while the same changes go
upstream to [zed-industries/zed](https://github.com/zed-industries/zed):

- **Try Vulkan before initialising the GL backend on Linux.** The renderer asked
  wgpu for `VULKAN | GL`, so Mesa's GL stack (`libEGL`, `libgallium`, `libLLVM`)
  was loaded and left resident even though only Vulkan was used. GL remains a
  fallback when no Vulkan adapter can drive the surface. See
  [zed#63327](https://github.com/zed-industries/zed/issues/63327).
- **Allocate path-rasterization textures on demand.** The full-window
  intermediate and 4x MSAA targets were allocated for every window, including
  windows that never draw a vector path. They are now created on the first frame
  that draws one, and are otherwise identical to before.

Measured with diffz on a 2880x1920 display: resident memory 209 MB to 74 MB, GPU
memory 246 MB to 136 MB, and about 90 ms faster to first content.

`v0.3.3-upstream` tags the pristine published crate, so `git diff
v0.3.3-upstream` is the full carried delta. This repository is temporary and
will be archived once a gpui-pre snapshot ships the upstream changes.

Licensed under Apache-2.0, as the upstream crate is.
