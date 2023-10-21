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

