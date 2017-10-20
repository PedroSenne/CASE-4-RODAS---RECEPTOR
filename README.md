#include <VirtualWire.h> //Inclui a biblioteca VirtualWire.h

#define IN1 11 //MOTOR A
#define IN2 10 //MORO A'
#define IN3 9 //MOTOR B
#define IN4 5 //MOTOR B'

char letra = 'S'; //Cria variável para armazenar as letras que serão recebida

void setup()
{

pinMode(IN1, OUTPUT); // DECLARANDO OS MOTORES COMO SAÍDAS
pinMode(IN2, OUTPUT); //
pinMode(IN3, OUTPUT); //
pinMode(IN4, OUTPUT); //


pinMode(13, OUTPUT); //LED 1
pinMode(12, OUTPUT); //LED 2
 Serial.begin(9600);

  //++++++++++++++Inicializa o módulo receptor+++++++++++++++++++
  vw_set_ptt_inverted(true);
  vw_setup(2000);
  vw_set_rx_pin(3); //Configura o pino D3 para a leitura dos dados
  vw_rx_start(); //Inicia a leitura de dados do módulo receptor
  //==============================================================
}


void loop()
{

//MONITORAMENTO
Serial.print("Recebendo: ");
Serial.println(letra);

  uint8_t buf[VW_MAX_MESSAGE_LEN]; //Variável para o armazenamento do buffer dos dados
  uint8_t buflen = VW_MAX_MESSAGE_LEN; //Variável para o armazenamento do tamanho do buffer

  if (vw_get_message(buf, &buflen)) //Se no buffer tiver algum dado (letra)
  {

    letra = buf[0]; //Armazena o que foi recebido na variável letra

    if (letra == 'B') //Se a letra recebida for igual a F(Forward), vai para frente
    {
      
digitalWrite(IN1, LOW);
digitalWrite(IN2, HIGH);
      
digitalWrite(IN3, HIGH);
digitalWrite(IN4, LOW);

digitalWrite(13, HIGH);
digitalWrite(12, HIGH);
 
     }

    else if (letra == 'F') //Se a letra recebida for igual a B(Back), movimenta o carrinho para trás
    {

digitalWrite(IN1, HIGH);
digitalWrite(IN2, LOW);

digitalWrite(IN3, LOW);
digitalWrite(IN4, HIGH);

digitalWrite(13, HIGH);
digitalWrite(12, HIGH);

    }

    else if (letra == 'R') //Se a letra recebida for igual a R(RIGHT+FORWARD), movimenta o carrinho para direita/frente
    {
digitalWrite(IN1, HIGH);
digitalWrite(IN2, LOW);

digitalWrite(IN3, HIGH);
digitalWrite(IN4, LOW);

digitalWrite(13, HIGH);
digitalWrite(12, HIGH);
      
      }

else if (letra == 'L') //Se a letra recebida for igual a L(LEFT+FORWARD), movimenta o carrinho para esquerda/frente
    { 
digitalWrite(IN1, LOW);
digitalWrite(IN2, HIGH);
 
digitalWrite(IN3, LOW);
digitalWrite(IN4, HIGH);

digitalWrite(13, HIGH);
digitalWrite(12, HIGH);
     
    } 
      
else if (letra == 'S') //Se a letra recebida for igual a S(Stop), para o carrinho
    {

digitalWrite(IN1, HIGH);
digitalWrite(IN2, HIGH);
digitalWrite(IN3, HIGH);
digitalWrite(IN4, HIGH);

digitalWrite(13, LOW);
digitalWrite(12, LOW);

}    
}
}
