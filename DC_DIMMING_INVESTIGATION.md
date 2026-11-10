# RFC: Investigate Native DC Dimming Support on POCO M5s (`rosemary`)

## Summary

Some POCO M5s users running LineageOS have reported display flickering
at low brightness and visual discomfort.

The stock vendor image contains references to MediaTek DC Backlight and
Ultra Dimming functionality. However, it is not yet clear whether these
components can be used by the LineageOS display stack.

## Existing findings

The following elements were identified in the stock vendor image:

-   MediaTek PQ HAL: `vendor.mediatek.hardware.pq@2.15`.
-   Vendor properties:
    -   `ro.vendor.pq.mtk_dc_support=1`
    -   `ro.vendor.pq.mtk_ultra_dimming_support=1`
    -   `ro.vendor.mtk_ultra_dimming_support=1`
-   The panel configuration contains a `<dcBacklight>` section with a
    threshold, coefficients, and DSI command parameters.
-   The PQ implementation contains references to `loadDCTable()` and
    `loadGlobalPQDCIndex()`.
-   `libaal_mtk.so` contains the `CAALFW::PanelUltraDim()` symbol.

## Important limitations

These findings confirm that the vendor image contains related
configuration and implementation references.

They do **not** confirm that:

-   the PQ HAL loads or uses the `<dcBacklight>` panel configuration;
-   the DSI commands are actually applied by the current LineageOS
    stack; or
-   the active Samsung panel on `rosemary` supports the required
    behavior through the current kernel and vendor integration.

No runtime activation or panel-command testing has been performed as
part of this investigation.

## Questions for maintainers

1.  Could the existing MediaTek PQ implementation provide a usable basis
    for native DC Dimming support?
2.  Is the `<dcBacklight>` configuration relevant to the active Samsung
    panel variant on `rosemary`?
3.  Would this functionality require changes to the device tree, kernel
    display driver, vendor integration, or Android framework?
4.  Is this repository an appropriate place for this investigation, or
    should it be discussed in another LineageOS component?

## Request

I would appreciate technical guidance from the maintainers on whether
this feature is feasible and what the appropriate next step would be.

This document is an investigation request, not an implementation. It
does not propose enabling undocumented properties or sending unverified
panel commands. The goal is to establish feasibility before any code
changes are proposed.

Thank you for your time and consideration.
