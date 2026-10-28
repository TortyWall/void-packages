rockchip-vaapi — Void Linux Packaging Notes
Overview

This package provides a Rockchip VA-API video decoding driver based on the Rockchip Media Process Platform (MPP).

The package depends on libva and rockchip-mpp.

Required common/shlibs entries

The rockchip-vaapi driver links against the Rockchip MPP shared libraries. Void Linux uses common/shlibs to map required SONAMEs to their providing packages when generating runtime dependencies.

Ensure that the following entries exist in common/shlibs:

text
librockchip_mpp.so.1 rockchip-mpp-1.1.0_1
librockchip_vpu.so.1 rockchip-mpp-1.1.0_1


Without the appropriate mappings, the 04-generate-runtime-deps hook may fail with an UNKNOWN PKG PLEASE FIX error.

Maintenance
Keep the SONAME mappings in common/shlibs in sync with the libraries provided by rockchip-mpp.
When updating Rockchip MPP, verify whether the SONAMEs or ABI have changed.
Update the package version in the mappings when required by Void Linux packaging conventions.
Do not add duplicate SONAME entries.
Verify the build with:
bash
./xbps-src -f pkg rockchip-mpp
./xbps-src -f pkg rockchip-vaapi

Installation

After a successful build, the package installs the VA-API driver to:

text
/usr/lib/dri/rockchip_drv_video.so


Test driver discovery with:

bash
LIBVA_DRIVER_NAME=rockchip \
LIBVA_DRIVERS_PATH=/usr/lib/dri \
vainfo


Actual hardware acceleration depends on the Rockchip SoC, kernel support, and a compatible MPP installation.
