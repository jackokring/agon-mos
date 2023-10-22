# Modding Agon MOS

So `linux-arm64` ... The status is not good. The code seems to be
partly buildable using `agon-ez80asm`, another project someone is
working on.

Other options are waiting for a `z88dk` target, (or `sdcc`) and
work on enough conversion and have some headers only from the
`Zilog ZDS II` download.

But it's not really such a bad thing. As the MOS should remain stable
and really only be subject to feature request to obivate complex
reimplementation waste. Like a `.dll` common code idea.

I haven't checked the function list, but can a reload to another
64K base happen? Maybe?

The `agon-vdp` extra modes and things is better to build on anyhow.

## Best Informative Finds So Far

 * The MOS extension 32kB loading from `$B0000` of `.bin` files in
 the `mos` directory without needing the `.bin` extension. This is
 an alternate load transient "reserved" area just below the global heap
 and stack area.
 * File format magic number starting at byte `$40` is `MOS`, `<version byte>`,
 `<adl mode bool byte>`. So for a `$40000` load, it starts at `$40040`.
 This does limit the use of `rst $38` and `im 1`. But seen vector table.
 A `jr 5` perhaps for extended magic? 
 * **N.B.** Is there a stack splat in `misc.asm` within `_exec16` by not setting `sp`
 to some value before `call.is`? Not for `$B0000` loading, but for say
 `$A0000` loading, as it might need a temp save, set `sp`, fix splat,
 do stuff, put stack back, `ret.lis`. It would likely be with some recusion
 and an almost at the limit 16 bit binary, assuming a high memory stack.
 Check splat in `mos.c` function `mos_cmdRUN` before `exec16`?
 **FIX** Perhaps a `ld.sis sp, 0` or `ld.sis sp, $8000` before the `CALL.IS (DE): RET`
 based on the `A` segment being `$0B` to prevent global `SPL` clobber?

