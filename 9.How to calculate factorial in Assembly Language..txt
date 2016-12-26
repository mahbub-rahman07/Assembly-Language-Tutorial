.MODEL SMALL
.STACK 10H
.CODE

MAIN PROC   
	   
	MOV BH,0
	MOV BL,10D
	   
	
	   INPUT:
	   MOV AH,1
	   INT 21H
	   CMP AL,13D
	   JNE NUMBER
	    
	   AND CX,0
	   MOV CL,BH
	   DEC CX
	   AND AX,0
	   
	   MOV AL,BH
	   
	   
	   JMP FACT
	   
	   
	   NUMBER:
	   SUB AL,30H
	   MOV CL,AL
	   MOV AL,BH
	   MUL BL
	   ADD AL,CL
	   MOV BH,AL
	   
	   JMP INPUT
	   
	FACT:
	     MUL CX
	     LOOP FACT
	 

       AND DX,0
	   MOV CX,10D
	              
	   MOV BX,0000H    
	        
	   STORE:
	   DIV CX             ;DX:AX / CX      REM = DX ,,, QUE = AX
	   MOV [0000H+BX],DX
	   ADD BX,2H
	   MOV DX,0
	   CMP AX,0
	   JNE STORE
	   
	   MOV AH,2
	   MOV  DL,0DH
	   INT 21H
	   MOV DL,0AH
	   INT 21H
	   
	   PRINT: 
	   SUB BX,2H
	   MOV DL,[0000H+BX]
	   ADD DL,30H
	   INT 21H
	   CMP BX,0
	   JNE PRINT
	   
	  	  
			   
	MAIN ENDP
END MAIN