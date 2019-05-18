# hello-world

#include <MCP3208.h>
#include <SPI.h>
MCP3208 adc(6);
/*----------------funcion motores-------------------*/
#define ENB1 12										//
#define IN1 3										//	
#define IN2 4										//
#define IN3 8										//
#define IN4 9										//
#define ENB2 5										//
/*--------------------------------------------------*/
#define COL 2000 //Este valor seria un promedio entre el blanco y el negro, o sea éste valor es el que divide el blanco del negro
//(le puse " 2000 " como estimativo)

void setup() {
    adc.begin();
	pinMode (ENB1,OUTPUT); 
	pinMode (ENB2,OUTPUT); 
	pinMode (IN1, OUTPUT);
	pinMode (IN2, OUTPUT);
	pinMode (IN3, OUTPUT);
	pinMode (IN4, OUTPUT);
}
void loop() {
    int S1 = adc.analogRead(1);
    int S2 = adc.analogRead(2);
    int S3 = adc.analogRead(3);
    int S4 = adc.analogRead(4);
    int S5 = adc.analogRead(5);
    int S6 = adc.analogRead(6);
    int S7 = adc.analogRead(7);
    
	if((S1 > COL)&&(S2 > COL)&&(S3 > COL)<&&(S4 > COL)&&(S5 > COL)&&(S6 > COL)&&(S7 > COL)){ //B   B B B B B B 
		motorSpeed(150,150);
    }
	else if((S1 < COL)&&(S2 < COL)&&(S3 < COL)&&(S4 < COL)&&(S5 < COL)&&(S6 < COL)&&(S7 < COL)){ //N   N N N N N N 
		motorSpeed(150,150);
    }
    else if((S1 < COL)&&(S2 > COL)&&(S3 > COL)&&(S4 < COL)&&(S5 < COL)&&(S6 > COL)&&(S7 > COL)){ //N   B B N N B B 
		motorSpeed(150,150);
    }
	else if((S1 < COL)&&(S2 > COL)&&(S3 > COL)&&(S4 < COL)&&(S5 > COL)&&(S6 > COL)&&(S7 > COL)){ //N   B B N B B B 
		motorSpeed(100,150);
    }
	else if((S1 < COL)&&(S2 > COL)&&(S3 > COL)&&(S4 > COL)&&(S5 < COL)&&(S6 > COL)&&(S7 > COL)){ //N   B B B N B B 
		motorSpeed(150,100);
    }
	else if((S1 > COL)&&(S2 > COL)&&(S3 < COL)&&(S4 < COL)&&(S5 > COL)&&(S6 > COL)&&(S7 > COL)){ //B   B N N B B B 
		motorSpeed(50,150);
    }
	else if((S1 > COL)&&(S2 > COL)&&(S3 > COL)&&(S4 > COL)&&(S5 < COL)&&(S6 < COL)&&(S7 > COL)){ //B   B B B N N B 
		motorSpeed(150,50);
    }
	else if((S1 > COL)&&(S2 > COL)&&(S3 > COL)&&(S4 > COL)&&(S5 > COL)&&(S6 < COL)&&(S7 < COL)){ //B   B B B B N N
		motorSpeed(150,-50);
    }
	else if((S1 > COL)&&(S2 < COL)&&(S3 < COL)&&(S4 > COL)&&(S5 > COL)&&(S6 > COL)&&(S7 > COL)){ //B   N N B B B B 
		motorSpeed(-50,150);
    }
}
/* A ESTA FUNCION NO LE DES BOLA!!! TAMPOCO TOQUES NADA! 
Es la funcion de motores que hice.
Vos solo enes que usar " motorSpeed(velocidad1,velocidad2); "    
*/
void motorSpeed(int i2,int i1){	
	int a,b,c,d;
	
	if(i1>=0){
		a=1;
		b=0;
	}
	if(i1<0){
		a=0;
		b=1;
		i1 = i1+i1*-2;
	}
	if(i2>=0){
		c=1;
		d=0;
	}
	if(i2<0){
		c=0;
		d=1;
		i2 = i2+i2*-2;
	}
	digitalWrite (IN4, a);
	digitalWrite (IN3, b);
	digitalWrite (IN1, c);
	digitalWrite (IN2, d);
	analogWrite(ENB1,i1);
	analogWrite(ENB2,i2);
}
