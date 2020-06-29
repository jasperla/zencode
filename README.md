# zencode

Currently it's a rather unpolished implementation with plenty of room for improvement.
At the moment Z3 is only used when a block cannot be divided cleanly in two or three parts.

## Usage

Currently all bytes in the range `0x80` - `0xff` are considered bad, additional badbytes can be provided
with `-b`.

For example:

```
% zencode -b '\x00\x0a\x14\x15'  -s '\xe7\xff\xe7\x75\xaf\xea\x75\xaf\xfa\x8b\x74\x30\x30\x77\xb8\xef\x74\x5a\x05\x3c\x2e\xcd\x58\x02\x6a\x52\x42\xff\x42\x42\x42\x42'
[*] bad bytes: b'\x00\n\x14\x15\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff'
[*] shellcode: b'\xe7\xff\xe7u\xaf\xeau\xaf\xfa\x8bt00w\xb8\xeftZ\x05<.\xcdX\x02jRB\xffBBBB'

; 0xe7ffe775
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x4d554d27
add eax, 0x4d554d27
add eax, 0x4d554d27
push eax

; 0xafea75af
; (z3 solved)
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x7f706360
add eax, 0x307a124f
push eax

; 0xfa8b7430
; (z3 solved)
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x7f213e2d
add eax, 0x7b6a3603
push eax

; 0x3077b8ef
; (z3 solved)
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x0860407f
add eax, 0x28177870
push eax

; 0x745a053c
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x745a053c
push eax

; 0x2ecd5802
; (z3 solved)
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x0b4e3f01
add eax, 0x237f1901
push eax

; 0x6a5242ff
; (z3 solved)
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x6850407f
add eax, 0x0101017f
add eax, 0x01010101
push eax

; 0x42424242
and eax, 0x42424242
and eax, 0x3d3d3d3d
add eax, 0x42424242
push eax
```

## ToDo

In no particular order:

- alphanumeric encoding
- linting/style
- print resulting bytes (ready for usage) along with size, etc
- tests
- x86\_64 support
