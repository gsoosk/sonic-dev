# Presentations

Two talks on the work in this repository: building a hardware-free test oracle for
the SONiC `xcvrd` transceiver daemon, and using it to drive an automated Python→Rust
port.

| file | slides | audience | date |
|---|---|---|---|
| [`python-to-rust-short.pptx`](python-to-rust-short.pptx) | 15 | intern showcase — general engineering audience | September 2026 |
| [`python-to-rust-full.pptx`](python-to-rust-full.pptx) | 31 | full technical talk | August 2026 |

Same story at two depths. Start with the short deck; use the full one when the
mechanics matter.

## Short — *A multi-agent pipeline for automatic code migration*

Written for people who have never heard of SONiC. Motivates the problem (what
`xcvrd` is and why it matters), explains why "just ask an LLM to translate it" fails
at whole-daemon scale, then covers the two ideas that make it work: an oracle that
needs no hardware, and a deterministic pipeline whose two loops make it
self-correcting. Ends on results, the benchmark/optimize extension, and what's next.

## Full — *Testing the SONiC transceiver daemon with an emulator, and porting it with a multi-agent framework*

The same arc with the engineering shown. Roughly:

1. **Background** — SONiC, `xcvrd`, why Rust, and why naive translation is unreliable
   at scale.
2. **The oracle** — the `xcvr-emu` emulator, the virtual optoe implementation, wiring
   it into the SONiC virtual testbed, the emulator bugs found and fixed along the way,
   and the ~100 end-to-end tests that judge a daemon purely by what it writes to
   STATE_DB.
3. **The pipeline** — related work (ReCodeAgent), then a slide per stage:
   `analyze → scope → plan → select_milestone → translate → validate → parity_verify`,
   plus the generalized form.
4. **Results and benchmarking** — E2E and SONiC-MGMT status, honest performance
   numbers, and the benchmark/optimize stages added afterwards.

## Note on the numbers

Both decks report performance as measured at the time they were given. The Rust port
was **not** faster than Python out of the pipeline — it was optimized for correctness
first — and the decks say so rather than picking a flattering framing. The
benchmark/optimize stages are what closed part of that gap; see `benchmark/README.md`
for the current measurements and their provenance.
