# Tiny13_HV_resetter
Attiny13, reset fuse and the chip, uses High Voltage (HV) Serial programming mode

Uses 5V-12V booster circuit to provide 12V+/-0.5V VPP to enter HV mode. no 12V supply available around

revised firmware, enable reset swtich working alone to reset fuse, LED blinking fast at the end to singal job done.


2020-JUN-08 update, 5v-12V boost design  

```

procedure

�i�J ���� PROGRAMMER �N�g����k

1) SDI, SII, SDO, RESET, VCC ���a
2) VCC ���� 4.5V - 5.5V, �O�� VCC �b20us ���W�L 1.8V
3) ���� 20 - 60us, �M�� RESET �� 12V +/-0.5V) (�̤� 100ns)
4) �����H�W���A�̤� 10us (�������Ӥw�g�i�J�F�����Ҧ�)
5) �_�} SDO �����a, �קK�m��, �u��
6) ���ݳ̤� 300us, �M��~�ާ@ SDI �M SII �� ATTINY13 Ū�g
7) �_�q���}�� RESET ���a�K�i���������Ҧ�
```  
.  
.  
.  
```
code

    pinMode(SDO, OUTPUT);     // Set SDO to output
    digitalWrite(SDI, LOW);
    digitalWrite(SII, LOW);
    digitalWrite(SDO, LOW);
    digitalWrite(RST, HIGH);  // 12v Off
    digitalWrite(VCC, HIGH);  // Vcc On
    delayMicroseconds(60);    // wait 20-60us
    digitalWrite(RST, LOW);   // 12v On
    delayMicroseconds(10);    // keep the state for at least 10us
                              // should be entered HV Programming mode
    pinMode(SDO, INPUT);      // Set SDO to input, relase
    delayMicroseconds(300);   // wait for 300us before giving instruction to SDI/SII
```
.
.
.  
Atmel Data sheet of how to,  
![alt text](Attiny13_HV_reset_fuse1.jpg)  
    
Atmel Data sheet of how to,  
![alt text](Attiny13_HV_reset_fuse2.jpg)  
    
chip, no ISP capable before the fuse rest.  
![alt text](Attiny13_HV_reset_fuse3.jpg)  
.  
.  
soruce code

![Tiny13_HV_resetter_12V_boost.ino](Tiny13_HV_resetter_12V_boost.ino)






### the old design
2018-MAR-07

schematic & physical connection
![alt text](Attiny13_reset_schematic_breadbroad.JPG)

reset and done  
![alt text](Attiny13_reset_Termnial.JPG)

source code  
https://github.com/xiaolaba/Tiny13_HV_resetter/blob/master/Tiny13_HV_resetter.ino

hex files  
https://github.com/xiaolaba/Tiny13_HV_resetter/blob/master/Tiny13_HV_resetter.ino.hex   
https://github.com/xiaolaba/Tiny13_HV_resetter/blob/master/Tiny13_HV_resetter.ino.with_bootloader.hex    

To embeds image to this read.me
.  
.  
.  
.  
.  
.  
.   
