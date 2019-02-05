Ocaml binaries would need to be built with a this version of ocaml compiler: 
https://github.com/gretay-js/ocaml/tree/try-with

If a call site was removed as a result of dead code elimination
or other optimizations, we cannot reference the label of that callsite.
Ideally, we would remove this entry from the frametable,
but it would require us to use the precise structure of
frame_desc entries of the frametable.
Instead, we can leave the entry as is, but attach a label that points to
an address that is guaranteed not to be a return of a call (in the new code),
and therefore the GC will never need to look it up.
We choose to set the label to the frame table itself.
This might later interfere with other pointers from frametable
to data section which are designated for dwarf debug info.

See original README:
https://github.com/facebookincubator/BOLT/blob/master/README.md
