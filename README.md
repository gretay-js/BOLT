See original README:
https://github.com/facebookincubator/BOLT/blob/master/README.md

BOLT for ocaml native code 

Ocaml binaries would need to be built with this version of ocaml compiler: 
https://github.com/ocaml/ocaml/pull/2237

If a call site was removed as a result of dead code elimination
or other optimizations, we cannot reference the label of that callsite in the frametable.
Ideally, we would remove this entry from the frametable,
but it would require BOLT to use the precise structure of
frame_desc entries of the frametable. 
Instead, we change the entry in the frametable to point to the beginning of the frametable label itself.
This is safe because the garbage collector only looks the frametable for up labels in the code section. 
