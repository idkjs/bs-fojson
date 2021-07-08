"fojson" = "faux (yo)json"

There are [bs-yojson](https://github.com/roddyyaga/bs-yojson) provides direct BuckleScript bindings for
[yojson](https://github.com/ocaml-community/yojson). However, they produce a large amount of JavaScript (because yojson
implements JSON parsing/printing itself). This package rewrites parts of Yojson to reduce the size of the JavaScript
produced by using JavaScript JSON parsing/printing. It should also be faster because of this. There are some changes to
the API as specified in `yojson.mli` (for instance a lot of undocumented functions are removed) but it should stay the
same for the purposes of `ppx_yojson_conv` and `ppx_deriving_yojson`.

Changes that have been made:
- Removed undocumented functions
- Changed yojson-to-string implementations to go via `Js.Json`
- Changed string-to-yojson implementations to go via `Js.Json` and a hack to account for the JSON representation of ints
  and floats being the same
- Changed default mode to standard JSON rather than OCaml extensions


## Error on Updating `bs-platform`

```sh
File "/Users/mando/Github/bs-fojson/node_modules/@roddynpm/bs-biniou/src/bi_outbuf.ml", line 56, characters 4-24:
Error: The implementation /Users/mando/Github/bs-fojson/node_modules/@roddynpm/bs-biniou/src/bi_outbuf.ml
       does not match the interface src/bi_outbuf.cmi:
       Values do not match:
         val create_output_writer :
           ?len:int ->
           ?shrlen:int -> < output : string -> int -> int -> unit; .. > -> t
       is not included in
         val create_output_writer :
           ?len:int ->
           ?shrlen:int -> < output : string -> int -> int -> int; .. > -> t
       File "/Users/mando/Github/bs-fojson/node_modules/@roddynpm/bs-biniou/src/bi_outbuf.mli", line 70, characters 0-105:
         Expected declaration
       File "/Users/mando/Github/bs-fojson/node_modules/@roddynpm/bs-biniou/src/bi_outbuf.ml", line 56, characters 4-24:
         Actual declaration
bsb: [36/38] src/bi_inbuf.cmj
```
