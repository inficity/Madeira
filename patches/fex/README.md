# FEX patches

The FEX submodule stays at its upstream commit; changes that only this fork
carries live here. `app/Madeira/arm64ec-windows/xtajit64.dll` is built with
them applied, so the app works without rebuilding FEX.

To rebuild xtajit64.dll with them:

    git -C FEX apply ../patches/fex/0001-ios-16k-smc-and-branch-history.patch
    build/fex-arm64ec/build.sh

Base: FEX f59cab95659e8add0c88f0c76ec1cf483c536dbf.

- `0001-ios-16k-smc-and-branch-history.patch`
  - InvalidationTracker: on iOS, trap, untrap and claim SMC faults per 16 KB
    host page, since Wine gives a host page the union of its four guest
    pages' protections (ml1307).
  - MADEIRA_FEX_BRANCH_HISTORY: "1" records every executable, any other
    value names the one to record; a NoExec block entry logs the last eight
    executed exits.
