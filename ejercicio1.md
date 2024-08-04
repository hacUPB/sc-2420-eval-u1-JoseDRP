## SOLUCIÓN FINAL EJERCICIO #1


\\
@0
D=A

@1
M=D

@15
D=A
@16
M=D

@0
D=M

@1
D=A
@2
M=D

(LOOP)
@0
D=M
@2
D=D-M
@END_LOOP
D;JLE
END_LOOP

@1
D=M
@2
D=D+A
@1
M=D

@2
D=M
@3
D=D+1
@2
M=D

@LOOP
0;JMP

(END_LOOP)


@1
D=M
@15
M=D

@0
0;JMP
\\