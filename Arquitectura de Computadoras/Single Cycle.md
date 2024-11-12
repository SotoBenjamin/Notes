Executes instructions in a single cycle.
We begin constructing the datapath by connecting the state elements.
![[Captura de pantalla 2024-11-10 a la(s) 12.55.37 p. m..png]]
## Single Cycle Datapath
![[Captura de pantalla 2024-11-10 a la(s) 10.20.58 p. m. 1.png]]
## Single Cycle Control
	-PCSrc : selector de PC´ entre PC + 4 y Result
	-MemtoReg : selector de Result entre Read Data y ALU Result
	-MemWrite : Enable de Data Memory WE Mem[AluRegult = A] <- WD
    -ALUControl(1:0) : Controla el comportamiento de las operaciones del ALU
    -ALUSrc : selectro de SrcB entre RD2 y ExtImm
    -ImmSrc : Selecciona cuanto se debe extender dependiendo de la operación
	-RegWrite : Enable of Register File Write. A3 = WD3 (Result)
	-RegSrc0: Selector de RA1 entre Instr19:6 (Rn) y 15 (Branch)
	-RegSrc1 : Selector de RA2 entre RD (Instr15:12) y 
	 

![[Captura de pantalla 2024-11-10 a la(s) 10.24.49 p. m..png]]
## Main Decoder
![[Captura de pantalla 2024-11-10 a la(s) 10.25.37 p. m..png]]
## Alu Decoder and PC Logic
![[Captura de pantalla 2024-11-10 a la(s) 10.26.26 p. m..png]]
## ImmSrc
![[Captura de pantalla 2024-11-11 a la(s) 1.17.02 p. m..png]]