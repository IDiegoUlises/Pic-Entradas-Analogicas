# Pic Entradas Analogicas

<img src="https://github.com/IDiegoUlises/Pic-Entradas-Analogicas/blob/main/Images/16f887-Pic.png"  />

* **Los Pines AN0 hasta AN12 funcionan como entradas analogicas**
* Vdd: Positivo del microcontrolador
* Vss: Negativo del microcontrolador
* Clkin: Osicilador conectado a negativo
* Clkout: Osicilador conectado a negativo

### Codigo De Una Lectura Analogica

```c
#include <16f887.h> //Nombre del microcontrolador
#device ADC = 10 //10 bits de resolucion
#fuses xt,nowdt  //para osciladores de 4 MegaHertz se usa xt para mayores usa hs
#use delay(clock=4M) //Velocidad del oscilador, la "M" signfica mega
 

void main()
{
   setup_adc_ports(all_analog); //Todos los puertos se seleccionan como analogicos
   setup_adc(adc_clock_internal); //Utiliza el reloj interno
   set_adc_channel(0); //Selecciona el canal este equivale a AN0
   
   while(true)
   {
      int valor = read_adc(); //Realiza una lectura analogica
   }
}
```

### Codigo Con Un Potenciometro

```c
#include <16f887.h> //Nombre del microcontrolador
#device ADC = 10 //10 bits de resolucion, se puede reducir para una menor resolucion
#fuses xt,nowdt  //para osciladores de 4 MegaHertz se usa xt para mayores usa hs
#use delay(clock=4M) //Velocidad del oscilador, la "M" signfica mega

//Esto es una configuracion para la señal PWM
int frecuencia = 255; //Frecuencia del PWM
int preescaler = 1; //Solo se puede configurar el valor de 1 


void main()
{
   //Configurar los puertos analogicos
   setup_adc_ports(sAN0); //Selecciona como analogico solo el puerto AN0, se puede usar all_analog para activar todos los puertos analogicos
   setup_adc(adc_clock_internal); //Utiliza el reloj interno
   set_adc_channel(0); //Elige el canal para luego realizar la lectura este equivale a AN0 
   
   //Configurar para la señal PWM
   setup_timer_2(t2_div_by_16, frecuencia, preescaler); //Configuramos el timer2 ya que la señal pwm se genera con ayuda del reloj del timer2
   setup_ccp1(ccp_pwm); //Asignamos el puerto ccp1 como puerto de pwm
   
   while(true)
   {
      int valor = read_adc(); //Realiza la lectura analogica del puerto AN0
      set_pwm1_duty(valor); //Enviamos una señal pwm de de la lectura del puerto analogico
   }
}
```
