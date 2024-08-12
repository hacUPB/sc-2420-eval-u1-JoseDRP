```assembler
@2
D=M
@3
M=1

(LOOP)
    @2
    D=M
    @END
    D;JEQ

    @3
    D=M
    @2
    M=D*M
    @2
    D=M
    D=D-1
    @2
    M=D

    @LOOP
    0;JMP

(END)
    @END
    0;JMP
```
