See original README:
https://github.com/facebookincubator/BOLT/blob/master/README.md

BOLT for ocaml native code 

Ocaml binaries would need to be built with a this version of ocaml compiler: 
https://github.com/gretay-js/ocaml/tree/try-with

Currently, when running llvm-bolt, include the following arguments: 
-eliminate-unreachable=0 -simplify-conditional-tail-calls=0

If a call site was removed as a result of dead code elimination
or other optimizations, we cannot reference the label of that callsite in the frametable.
Ideally, we would remove this entry from the frametable,
but it would require us to use the precise structure of
frame_desc entries of the frametable. 

