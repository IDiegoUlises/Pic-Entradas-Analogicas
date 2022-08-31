# Pic Entradas Analogicas

#include <16f887.h> //Nombre del microcontrolador
#device ADC = 10 //10 bits de resolucion
#fuses xt,nowdt  //para osciladores de 4 MegaHertz se usa xt para mayores usa hs
#use delay(clock=4M) //Velocidad del oscilador, la "M" signfica mega
 

void main()
{
   setup_adc_ports(all_analog); //TODOS LOS PUERTOS ANALOGICOS COMO ANALOGICOS YA QUE NO PUDE UTILIZAR AN1 O AN0 PARA DECLRAR
   setup_adc(adc_clock_internal);
   set_adc_channel(0); //NO ESTOY SEGURO DE ESTO PERO SE SUPONE QUE SE ELIGE EL CANAL 0 QUE EQUIVALE AL PUERTO AN0
   
   while(true)
   {
      int valor = read_adc(); //REALIZA LA LECTURA DEL PUERTO AN0 NO ESTOY SEGURO
   }
}
