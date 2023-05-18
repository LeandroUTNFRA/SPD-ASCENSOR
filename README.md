# SPD-ASCENSOR
PARCIAL


# ASCENSOR
![237538890-8f919336-8052-4280-936c-923b4aac6ce3](https://github.com/LeandroUTNFRA/SPD-ASCENSOR/assets/122940722/32940376-443a-4ee9-a15e-feeee6c329a8)

# CIRCUITO
un display de 7 segmentos que informa el piso actual, dos led que informan el estado del ascensor 
y tres botones para las operaciones que desea el usuario (subir,bajar,parar)
![SPD PARCIAL](https://github.com/LeandroUTNFRA/SPD-ASCENSOR/assets/122940722/b659ac48-e87d-452a-b0dc-4175ff41022d)

# CODIGO
* se definen los pines, contadores, flags y funciones
* los leds y dysplay 7 segmentos se declaran en el setup como salida
* con respecto a los botone se los declaran como entrada
~~~cpp
bool MensajeMostrado = false;
bool Flag = true;
//Botones
# define BotonSubir 6
# define BotonParar 5
# define BotonBajar 3
// LEDS
# define LedVerde 2
# define LedRojo 4    
//Display 7 segmentos
# define A 13
# define B 12
# define C 11
# define D 10
# define E 9
# define F 8
# define G 7
int contador = 0;
// Funciones
void EncenderDisplay(int numero);
void SubirBajar();
void PararAscensor();
void setup()
{
  pinMode(BotonSubir, INPUT);
  pinMode(BotonParar, INPUT);
  pinMode(BotonBajar, INPUT);
  pinMode(LedVerde, OUTPUT);
  pinMode(LedRojo, OUTPUT);
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
  pinMode(E, OUTPUT);
  pinMode(F, OUTPUT);
  pinMode(G, OUTPUT);
  Serial.begin(9600);
  
}
~~~

# FUNCIONES
## PARAR ASCENSOR
en esta funcion si se apreta el boton para parar el ascensor lo que va hacer es mostrar 
una P en el display 7 segmentos y un mensaje que el "MONTACARGA EN PAUSA", si se vuelve a presionar mostrara
otro mensaje "MONTACARGA EN MARCHA" con lo cual ya se podra subir o bajar 
~~~cpp
void PararAscensor(){
  int Boton3 = digitalRead(BotonParar);
	if (Boton3 == LOW){
      EncenderDisplay(11);
    while (Boton3 == LOW) {
      digitalWrite(LedVerde, LOW);
      digitalWrite(LedRojo, HIGH);
      if (!MensajeMostrado) 
      {
         Serial.println("MONTACARGA EN PAUSA");
         MensajeMostrado = true;
  	   }
      Flag=false;
      
      delay(500);
      
      if (digitalRead(BotonParar) == LOW) {
       	Flag=true;
        Serial.println("MONTACARGA EN MARCHA");
         delay(1000);
        digitalWrite(LedRojo, LOW);
        break;
      }
    }
  }
}
~~~

##  SUBIRBAJAR
en esta funcion dependiendo el boton presionado va subir o bajar 
y se valida si llega a un piso mayor a 9 o menor a 0 tira error y pide que suba o que baje
~~~cpp
void  SubirBajar()
{
  int Boton1=digitalRead(BotonSubir);
  int Boton2=digitalRead(BotonBajar);
  
  if (Boton1 == LOW){
  	contador++;
    digitalWrite(LedVerde, HIGH);
  	EncenderDisplay(contador);
    while (contador < 0 || contador > 9) {
        Serial.println("ERROR BAJE");
        delay(1000);
        contador--;
      }
    
  }
  else if(Boton2 == LOW){
  contador--;
  digitalWrite(LedVerde, HIGH);
  EncenderDisplay(contador);
  while (contador < 0 || contador > 9) {
        Serial.println("ERROR SUBA");
        delay(1000);
        contador++;
      }
  }

}
~~~

# ENCENDERDIPLAY
Esta funcion dependiendo el numero que se
le pase por parametro va enscender un numero 
del display
~~~cpp
void EncenderDisplay(int numero)
{
  switch(numero)
  {
  	case 1:
    	digitalWrite(B, HIGH);
    	digitalWrite(C, HIGH);
  	delay(3000);
    	digitalWrite(B, LOW);
    	digitalWrite(C , LOW);
    	break;
    case 2:
        digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);
        digitalWrite(D, HIGH);
    	digitalWrite(E, HIGH);
        digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(B, LOW);
    	digitalWrite(D, LOW);
        digitalWrite(E, LOW);
    	digitalWrite(G, LOW);
    	break;
        
    case 3:
    	digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);  		
        digitalWrite(C, HIGH);
    	digitalWrite(D, HIGH);
        digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);  		
    	digitalWrite(B, LOW);  		
    	digitalWrite(C, LOW);  		
        digitalWrite(D, LOW);  		
    	digitalWrite(G, LOW);
    	break;
    case 4:
    	digitalWrite(B, HIGH);
    	digitalWrite(C, HIGH);
        digitalWrite(F, HIGH);
        digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(B, LOW);
    	digitalWrite(C, LOW);
        digitalWrite(F, LOW);
    	digitalWrite(G, LOW);
    	break;
    case 5:
    	digitalWrite(A, HIGH);
    	digitalWrite(C, HIGH);
        digitalWrite(D, HIGH);
    	digitalWrite(F, HIGH);
        digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(C, LOW);
    	digitalWrite(D, LOW);
        digitalWrite(F, LOW);
    	digitalWrite(G, LOW);
    	break;
    case 6:
    	digitalWrite(A, HIGH);
    	digitalWrite(C, HIGH);
        digitalWrite(D, HIGH);
    	digitalWrite(E, HIGH);
        digitalWrite(F, HIGH);
    	digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(C, LOW);
    	digitalWrite(D, LOW);
        digitalWrite(E, LOW);
    	digitalWrite(F, LOW);
    	digitalWrite(G, LOW);
    	break;
    case 7:
    	digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);
        digitalWrite(C, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(B, LOW);
    	digitalWrite(C, LOW);
    	break;
    case 8:
    	digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);
        digitalWrite(C, HIGH);
        digitalWrite(D, HIGH);
    	digitalWrite(E, HIGH);
        digitalWrite(F, HIGH);
        digitalWrite(G, HIGH);
    	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(B, LOW);
        digitalWrite(C, LOW);
    	digitalWrite(D, LOW);
        digitalWrite(E, LOW);
    	digitalWrite(F, LOW);
    	digitalWrite(G, LOW);
    	break;
    case 9:
    	digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);
        digitalWrite(C, HIGH);
    	digitalWrite(D, HIGH);
        digitalWrite(F, HIGH);
        digitalWrite(G, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(B, LOW);
    	digitalWrite(C, LOW);
        digitalWrite(D, LOW);
    	digitalWrite(F, LOW);
        digitalWrite(G, LOW);
    	break;
    case 0:
    	digitalWrite(A, HIGH);
    	digitalWrite(B, HIGH);
        digitalWrite(C, HIGH);
    	digitalWrite(D, HIGH);
        digitalWrite(E, HIGH);
    	digitalWrite(F, HIGH);
  	delay(3000);
    	digitalWrite(A, LOW);
    	digitalWrite(B, LOW);
    	digitalWrite(C, LOW);
        digitalWrite(D, LOW);
    	digitalWrite(E, LOW);
    	digitalWrite(F, LOW);
    	break;
    case 11:
      digitalWrite(A, HIGH);
      digitalWrite(B, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(F, HIGH);
      digitalWrite(G, HIGH);
      delay(3000);
      digitalWrite(A, LOW);
      digitalWrite(B, LOW);
      digitalWrite(E, LOW);
      digitalWrite(F, LOW);
      digitalWrite(G, LOW);
      break;
  }}
  ~~~
# LINK DEL PROYECTO
https://www.tinkercad.com/things/9C3bCQkykqN



