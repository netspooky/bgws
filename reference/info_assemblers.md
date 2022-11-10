# Assemblers

Assemblers can be useful for building files. I use [nasm](https://github.com/netwide-assembler/nasm) to build raw ELF and PE files, but it can also be used to build entire files. 

The macro capabilities of `nasm` are very useful for filling out spaces with sequences of numbers, and working with complex data structures you can label and arrange.

You can install on most Linux distros with `apt install nasm`. 

Note that nasm assembles x86. There are other assemblers you can explore depending on the architecture. They tend to follow similar semantics for declaring labels and defining characteristics about the file.

Here is an example small ELF file you can build with nasm. 

Build with `nasm -f bin test.asm -o test`

```
BITS 64

        org 0x400000  ; Where to load this into memory

;----------------------+------+-------------+----------+------------------------
; ELF Header struct    | OFFS | ELFHDR      | PHDR     | ASSEMBLY OUTPUT
;----------------------+------+-------------+----------+------------------------
        db 0x7F, "ELF" ; 0x00 | e_ident     | A        | 7f 45 4c 46
        db 2           ; 0x04 | ei_class    | B        | 02
        db 1           ; 0x05 | ei_data     | C        | 01
        db 1           ; 0x06 | ei_version  | D        | 01
        db 0           ; 0x07 |             | E        | 00
        dq 0           ; 0x08 | until 0x10  | F        | 00 00 00 00 00 00 00 00
        dw 0x02        ; 0x10 | e_type      | G        | 02 00
        dw 0x3e        ; 0x12 | e_machine   | H        | 3e 00
        dd 1           ; 0x14 | e_version   | I        | 01 00 00 00
        dq 0x400078    ; 0x18 | e_entry     | J        | 78 00 40 00 00 00 00 00
        dq phdr - $$   ; 0x20 | e_phoff     | K        | 40 00 00 00 00 00 00 00
        dq 0           ; 0x28 | e_shoff     | L        | 00 00 00 00 00 00 00 00
        dd 0           ; 0x30 | e_flags     | M        | 00 00 00 00
        dw 0x40        ; 0x34 | e_ehsize    | N        | 40 00
        dw 0x38        ; 0x36 | e_phentsize | O        | 38 00
        dw 1           ; 0x38 | e_phnum     | P        | 01 00
        dw 0           ; 0x3A | e_shentsize | Q        | 00 00
        dw 0           ; 0x3C | e_shnum     | R        | 00 00
        dw 0           ; 0x3E | e_shstrndx  | S        | 00 00
;----------------------+------+-------------+----------+------------------------
; Program Header Begin | OFFS | ELFHDR      | PHDR     | ASSEMBLY OUTPUT
;----------------------+------+-------------+----------+------------------------
phdr:   dd 1           ; 0x40 | PA          | p_type   | 01 00 00 00 loadable
        dd 5           ; 0x44 | PB          | p_flags  | 05 00 00 00 exec
        dq 0           ; 0x48 | PC          | p_offset | 00 00 00 00 00 00 00 00
        dq $$          ; 0x50 | PD          | p_vaddr  | 00 00 40 00 00 00 00 00
        dq $$          ; 0x58 | PE          | p_paddr  | 00 00 40 00 00 00 00 00
        dq 0x100000000 ; 0x60 | PF          | p_filesz | 80 00 00 00 00 00 00 00
        dq 0x100000000 ; 0x68 | PG          | p_memsz  | 80 00 00 00 00 00 00 00
        dq 0x200000    ; 0x70 | PH          | p_align  | 00 00 20 00 00 00 00 00
_start: mov    al,0x3c ; exit syscall                  | b0 3c 
        mov    di, 6   ; return value 6                | 66 bf 06 00
        syscall        ; call the kernel               | 0f 05
```

Run with:

```
chmod +x test
./test
echo $?
```

You should see a "6" as the return value.

