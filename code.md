```
section .text
        global _start                   ;must be declared for linker (ld)
                                        ;global is used to export the _start label
                                        ;this will be the entry point to the program

_foobar:                                ;tells foobar entry point
        push ebp                        ;this will save the ebp register into stack
        mov ebp, esp                    ;moves ebp register to esp register
        sub esp, 4                      ;subtracts esp register to 4 to make empty stacks

        mov eax, DWORD[ebp+8]           ;this should have 20
        mov ebx, DWORD[ebp+12]          ;this should have 10
        add eax, ebx                    ;adds eax (20) to ebx (10), so that will equal to 30.

        mov ecx, DWORD[ebp+16]          ;this should have 30
        add eax, ecx                    ;adds eax (30 (20 plus 10)) to ecx (30), so that will equal to 60.

        mov [result], eax               ;returns the overall result
        leave                           ;leave foobar
        ret                             ;return

_start:                                 ;tells linker entry point
        push DWORD[x]                   ;alternative for mov eax, [x]
        push DWORD[y]                   ;alternative for mov ebx, [y]
        push DWORD[z]                   ;alternative for mov ecx, [z]
        call _foobar                    ;call the function foobar

        mov eax, 1                      ;set eax register to 1
        int 0x80                        ;call kernel

section .data
        x dd 20                         ;initialized variable x (20)
        y dd 10                         ;initialized variable y (10)
        z dd 30                         ;initialized variable z (30)
        mov DWORD[ebp-4], eax           ;locally saves the sum into the function

segment .bss
        result resb 1                   ;uninitialized variable result (reserve a byte)
```
