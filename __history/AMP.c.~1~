#include <12f629.h>

#FUSES INTRC_IO, NOWDT, PUT, NOPROTECT, NOMCLR, BROWNOUT 
#use delay(clock=4000000)
#use standard_io (A)

 // Pin defines
#define Device_SDA PIN_A0
#define Device_SCL  PIN_A1
#use i2c(master, sda=Device_SDA, scl=Device_SCL,FORCE_SW)  // Configure Device as Master
#define CLIP_DET PIN_A4
/////////////////////////////////
/////////////////////////////////

#define WRT  0xFE;
#define RD   0x01;
////////////////////////
#define TIMEOFF    50 // base 10ms 

int8 AMP_ADD = 0xD8;


/////////Function declaration//////

int8 StartUp_amp();
///////////////////////////////////
void main()
{

//ext_int_edge(L_TO_H);      // init interrupt triggering for button press
//enable_interrupts(INT_EXT); //turn on interrupts
//enable_interrupts(GLOBAL);
delay_ms(500);

StartUP_amp();


while (1);
}

///////////
int StartUp_amp()
{
  
  OUTPUT_LOW(CLIP_DET);
  delay_ms(1000);
  I2c_start();
  i2c_write(AMP_ADD);            // I2C write address
  i2c_write(0x01|0x80);          //Ready Set pointer to control Byte 1, use Page write auto increment pointer
  i2c_write(0xff);               // Control byte 1 = 0xff Gain = 12dB, enable diagnostic
  i2c_write(0x10);               //control byte 2 = 0x10 to turn on Amplifier
  I2c_stop();
  
 // delay_ms(10);
 // I2c_start();
 // i2c_write(AMP_ADD);
 // i2c_write(0x01);             //Ready Set pointer to control Byte 1
 // i2c_write(0xff);               // Control byte 1 = 0xff Gain = 12dB, enable diagnostic
 // i2c_write(0x10); 
 // i2c_stop();
 OUTPUT_FLOAT(CLIP_DET);   // set CLIP_DET to High Z (INPUT)
return 0;
}


