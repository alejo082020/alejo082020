-from machine import Pin, ADC, PWM
from utime import sleep_ms
import machine
import time
import esp32


buzzer = PWM(Pin(15))
notas = [391,440,391,554,493,391,440,391,622,554]

led = Pin(4, Pin.OUT)
led2 = Pin (15, Pin.OUT)
valor_sensor = esp32.hall_sensor()

touch1 = machine.TouchPad(machine.Pin(15))
touch1.config(600)
touch2 = machine.TouchPad(machine.Pin(4))
touch2.config(600)

def mapeo(valor_sensor, minimo_entrada, maximo_entrada, minimo_salida, maximo_salida):
  valor_mapeado = (valor_sensor - minimo_entrada) * (maximo_salida - minimo_salida) / (maximo_entrada - minimo_entrada) + minimo_salida
  return valor_mapeado
#--------------------------- [OBJETOS]---------------------------------------
bombillor  = PWM(Pin (13),1000)
bombillog  = PWM(Pin (10),1000)
bombillob  = PWM(Pin (10),1000)
potr = ADC(Pin(35))
potg = ADC(Pin(32))
potb = ADC(Pin(33))

  


while True:
  print(f"rojo:{potr.read()}\t verde:{potg.read()} \t azul:{potb.read()}")
  bombillor.duty( int (potr.read()/4))
  bombillog.duty( int (potg.read()/4))
  bombillob.duty( int (potb.read()/4))
  # bombillo.duty( int (pot.read/4))
  # bombillo.duty_ns( pot.read()*16)
  sleep_ms(3000)
  
    #iman
    #print("efecto hall:")
    #print(esp32.hall_sensor())
  mape=mapeo(esp32.hall_sensor(),-200,200,0,1023)
  mape1=mape<50
  mape2=mape>1023
  led.value(mape1)
  led2.value(mape2)
    #print("map:",mape)
    #time.sleep(0.2)
    
    #touch
  print(touch1.read())
  print(touch2.read())
  led.value(touch1.read())
  led2.value(touch2.read())
  time.sleep(0.2)
   
  for i in notas:
    buzzer.freq(i)
    sleep_ms(650)
