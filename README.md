# gpui-pre-wgpu 0.3.14, patched

Based on the published [`gpui-pre-wgpu`](https://crates.io/crates/gpui-pre-wgpu)
0.3.14 snapshot (`zed@f126950`). This branch carries two changes:

- Try Vulkan before initializing EGL on Linux and the BSDs. Hardware GL
  remains a fallback and is preferred to software Vulkan. Device recovery
  still requires a hardware adapter and retries if neither backend works.
- Use the requested `wght` variation when shaping, measuring and rasterizing a
  variable font on Linux. Static faces keep their existing selection and
  rasterization.

The tiled path renderer in 0.3.13 and later has no window-sized path textures
to allocate lazily.

Licensed under Apache-2.0, as the upstream crate is.
