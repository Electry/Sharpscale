# Sharpscale

[Download binary](https://forum.devchroma.nl/index.php/topic,112.0.html) | [Report bugs](https://github.com/cuevavirus/sharpscale/issues) | [Source code](https://git.shotatoshounenwachigau.moe/vita/sharpscale/)

Sharpscale is a PSTV and PS Vita plugin that changes the way in which the framebuffer is scaled in relation to the display output size to provide a cleaner and sharper image.

## Usage

Sharpscale can be configured to different scaling methods.

#### Scaling modes

- Original: system default
- Integer: scale by multiplying the width and height of the framebuffer by the largest integer less than or equal to four such that the product width and height is less than or equal to the display width and height, respectively
- Real: no scaling
- Fitted: scale the framebuffer up to four times larger or eight times smaller to fit exactly within the display while preserving aspect ratio

In integer and real modes, a few lines may be cropped from the top and bottom to preserve aspect ratio of the framebuffer.

#### PS1 aspect ratio

PS1 aspect ratio can be forced in integer, real, and fitted scaling modes and is applied before scaling.

- Pixel: aspect ratio of the framebuffer
- 4∶3: aspect ratio is forced to 4∶3
- 16∶9: aspect ratio is forced to 16∶9

Scaling and PS1 aspect ratio will not apply when

- in integer and real modes, if the framebuffer is already larger than the display
- in fitted mode, if the framebuffer is too big to be scaled
- aspect ratio is too different to be forced to 4∶3 or 16∶9

#### Scaling algorithm

- Point: nearest neighbour
- Bilinear: bilinear interpolation (system default)

Whenever scaling mode is original, or otherwise not applied, bilinear interpolation is used.

#### Unlock framebuffer size

- On: allow framebuffers of sizes 1280x720, 1440x1080, and 1920x1080 to be submitted to the kernel
- Off: system default

## Installation

Install under `*KERNEL` of your taiHEN config.

```
*KERNEL
ur0:tai/sharpscale.skprx
```

## Configuration

Use the provided configuration app to change settings instantly without needing to close the foreground application or needing to reboot. If the app crashes on startup, then disable user plugins for this app in your taiHEN config.

![preview-config-app](https://git.shotatoshounenwachigau.moe/vita/sharpscale/plain/preview-config-app.png?h=assets)

## Scaling test

The scaling test program shows horizontal and vertical lines 1 pixel wide alternating between black and white. Use the left and right buttons to cycle between framebuffer resolutions.

Available resolutions:

- 480×272
- 640×368
- 720×408
- 960×544
- 1280×720
- 1440×1080
- 1920×1080

**Warning:** Do not use when HDMI is set to interlaced mode.

## Building

Dependencies:

- [DolceSDK](https://forum.devchroma.nl/index.php/topic,129.0.html)
- [libvita2d_sys](https://github.com/GrapheneCt/libvita2d_sys)
- [fnblit and bit2sfn](https://git.shotatoshounenwachigau.moe/vita/fnblit)
- [GNU Unifont](http://unifoundry.com/unifont/index.html)
- [taiHEN](https://git.shotatoshounenwachigau.moe/vita/taihen/)

The following modifications to libvita2d_sys are required to reduce memory usage:

```
DEFAULT_TEMP_POOL_SIZE      128 KiB
PARAMETER_BUFFER_SIZE       256 KiB
VDM_RING_BUFFER_SIZE         32 KiB
VERTEX_RING_BUFFER_SIZE     128 KiB
FRAGMENT_RING_BUFFER_SIZE    64 KiB

Remove the stencil buffer
```

## Contributing

Use [git-format-patch](https://www.git-scm.com/docs/git-format-patch) or [git-request-pull](https://www.git-scm.com/docs/git-request-pull) and email me at <asakurareiko@protonmail.ch>.

## Credits

- Bounty backers: [ScHlAuChii, eleriaqueen, mansjg, TG](https://www.bountysource.com/issues/78540965-native-resolution-output-for-pstv)
- Video comparisons: Zodasaur
- SceLowio and SceDisplay RE: xerpi
- Author: 浅倉麗子

## See more

CBPS ([forum](https://forum.devchroma.nl/index.php), [discord](https://discordapp.com/invite/2ccAkg3))
