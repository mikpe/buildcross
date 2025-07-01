# buildcross
buildcross - a tool for building GCC cross toolchains

Usage:

	buildcross [options] [<TARGET>] [<CROSS_DIR>]

Options:

	--cross-dir=<CROSS_DIR> | -c <CROSS_DIR>
		Place resulting cross-compiler in <CROSS_DIR>.
		Default: <CWD>/cross-<TARGET>

	--downloads-dir=<DOWNLOADS_DIR> | -d <DOWNLOADS_DIR>
		Place downloaded sources in <DOWNLOADS_DIR>.
		Default: <CWD>/downloads

	--host-tools-dir=<HOST_TOOLS_DIR> | -h <HOST_TOOLS_DIR>
		Place built host tools in <HOST_TOOLS_DIR>.
		Default: <CWD>/host-tools

	-j<N>
		Pass -j<N> to make. Default: empty

	--sources-dir=<SOURCES_DIR> | -s <SOURCES_DIR>
		Place unpacked source archives in <SOURCES_DIR>.
		Default: <CWD>/sources

	--target=<TARGET> | -t <TARGET>
		Build the indicated <TARGET>. If this option is
		not present then <TARGET> must be present as the
		first non-option parameter.

Supported targets and resulting toolchains:

| Target	| Toolchain |
| ------	| --------- |
| 6502		| 6502 (binutils from cc65, libtinyc) |
| a29k		| a29k-unknown-coff (no libc) [^3] |
| aarch64	| aarch64-unknown-linux-gnu |
| aarch64-mingw64 | aarch64-w64-mingw32 |
| alpha		| alpha-unknown-linux-gnu |
| arc		| arc-unknown-linux-gnu |
| arc64		| arc64-unknown-linux-gnu |
| armv7l	| armv7l-unknown-linux-gnueabi |
| avr		| avr-unknown-elf (no libc) |
| avr32		| avr32-unknown-linux-uclibc [^1] |
| bfin		| bfin-unknown-linux-uclibc |
| bpf		| bpf-unknown-none (no libc) |
| c4x		| c4x-unknown-coff (no libc) [^3] |
| c6x		| c6x-unknown-uclinux |
| cr16		| cr16-unknown-elf |
| cris		| crisv32-unknown-linux-uclibc |
| crx		| crx-unknown-elf (no libc) [^1] |
| csky		| csky-unknown-linux-gnu (only little-endian) |
| d10v		| d10v-unknown-elf [^3] |
| d30v		| d30v-unknown-elf (no libc) [^2] |
| epiphany	| epiphany-unknown-elf |
| fr30		| fr30-unknown-elf |
| frv		| frv-unknown-linux-uclibc |
| ft32		| ft32-unknown-elf |
| h8300		| h8300-unknown-linux-uclibc |
| hexagon	| hexagon-unknown-linux-gnu [^3] |
| hppa		| hppa-unknown-linux-gnu (no -m64 support) |
| i860		| i860-stardent-sysv4 (no libc) [^3] |
| i960		| i960-unknown-elf with uclinux and uclibc [^3] |
| ia16		| ia16-unknown-elf [^1] |
| ia64		| ia64-unknown-linux-gnu |
| ip2k		| ip2k-unknown-elf (no libc) [^2] |
| iq2000	| iq2000-unknown-elf |
| kvx		| kvx-unknown-uclibc |
| lm32		| lm32-uclinux-uclibc |
| loongarch64	| loongarch64-unknown-linux-gnu |
| m1750		| m1750-coff (custom libc) [^3] |
| m32c		| m32c-unknown-elf [^1] |
| m32r		| m32r-unknown-elf |
| m6809		| m6809-unknown-none with newlib [^1] |
| m68hc11	| m68hc11-unknown-elf [^1] |
| m68k		| m68k-unknown-linux-gnu |
| m68k-elf	| m68k-unknown-elf |
| m68k-uclibc	| m68k-unknown-linux-uclibc |
| m88k		| m88k-unknown-openbsd (elf, no libc) [^1] |
| maxq		| maxq-unknown-coff (no libc) [^1] |
| mcore		| mcore-unknown-elf |
| mep		| mep-unknown-elf (no libc) [^1] |
| metag		| metag-unknown-linux-uclibc [^1] |
| microblaze	| microblaze-unknown-linux-gnu |
| mips64	| mips64-unknown-linux-gnu with -mabi=64, -mabi=n32, and -mabi=32 support |
| mmix		| mmix-knuth-mmixware with newlib |
| mn10300	| mn10300-unknown-elf |
| moxie		| moxie-unknown-elf |
| msp430	| msp430-unknown-elf |
| mt		| mt-unknown-elf [^3] |
| nds32		| nds32le-unknown-linux-gnu |
| nios2		| nios2-unknown-linux-gnu |
| ns32k		| ns32k-unknown-netbsd (no libc) [^2] |
| nvptx		| nvptx-none with newlib |
| or1k		| or1k-unknown-linux-gnu |
| pdp11		| pdp11-unknown-aout (no libc) |
| pj		| pjl-unknown-elf (no libc) [^3] |
| ppc64		| ppc64-unknown-linux-gnu with -m64 and -m32 support |
| ppc64le	| ppc64le-unknown-linux-gnu (no -m32 support) |
| pru		| pru-unknown-elf |
| rl78		| rl78-unknown-elf |
| riscv64	| riscv64-unknown-linux-gnu (no 32-bit support) |
| rx		| rx-unknown-elf |
| s390x		| s390x-unknown-linux-gnu with -m64 and -m31 support |
| score		| score-unknown-elf (no libc) [^1] |
| sh4		| sh4-unknown-linux-gnu |
| sparc64	| sparc64-unknown-linux-gnu with -m64 and -m32 support |
| tilegx	| tilegx-unknown-linux-gnu |
| tms9900	| tms9900-unknown-elf (no libc) [^1] |
| tricore	| tricore-unknown-elf |
| ubicom32	| ubicom32-linux-uclibc [^1] |
| v850		| v850e-uclinux-uclibc |
| vax		| vax-unknown-linux (no libc or kernel headers) |
| visium	| visium-unknown-elf |
| x86_64	| x86_64-unknown-linux-gnu with -m64, -mx32, and -m32 support |
| x86_64-mingw64 | x86_64-w64-mingw32 with -m64 and -m32 support |
| x86_64-musl	| x86_64-unknown-linux-musl (only -m64) |
| x86_64-uclibc	| x86_64-unknown-linux-uclibc (only -m64) |
| xc16x		| xc16x-unknown-elf [^1] |
| xstormy16	| xstormy16-unknown-elf |
| xtensa	| xtensa-unknown-linux-uclibc |
| z8k		| z8k-unknown-coff with newlib [^3] |
| zpu		| zpu-unknown-elf [^1] |

All toolchains include the libc indicated by their target triplets, elf ones with newlib,
unless otherwise noted.

Notes:

[^1]: Requires an old version of the host GCC. See the code for details.
[^2]: In addition to [^1], requires a special build procedure. See the code for details.
[^3]: In addition to [^2], requires a 32-bit build. See the code for details.
