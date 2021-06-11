# SPI协议——寄存器读写分析
SPI协议是主从模式：从机不主动发起访问，总是被动执行操作。
CSN：片选信号。
SCK：时钟信号。
MOSI:master output slave input,即主机输出从机输入。可以理解主机写从设备。
MISO:master input slave output,即主机输入从机输出。可以理解主机读从设备。

SPI全称:Serial Peripheral interface,即串行外围设备接口。SPI协议自然是串行地传输数据，每次
按 1 bit读写设备，而不是像并行每次1byte(8bit)传输。

以FlightController项目中的nRF24L01模块为例进行进行程序的编写。

通过时序图分析得出，当SCK(时钟)引脚发生跳变时，产生数据的传输/发送过程，总结来说：MCU在时钟信号的上升沿时写(write),下降沿时读(read)。

## 根据协议单字节写入：
```C++
void SPI_Write(byte Byte)
{
  for(int i = 0; i < 8; i++)
  {
     if(Byte&0x80)
     {
      digitalWrite(MOSI,1);
     }
     else
     {
      digitalWrite(MOSI,0);
     }
     digitalWrite(SCK,1);
     Byte <<= 1;
     digitalWrite(SCK,0);
  }
}
```
## 根据协议单字节读取：
```C++
byte SPI_Read(byte address)
{
  byte dat = 0;
  SPI_Write(address);
  for(int i=0;i<8;i++)
  {
    dat <<= 1;
    digitalWrite(SCK,1);
    if(digitalRead(MISO))
    {
        dat|=1;
    }
    else
    {
        dat|=0;
    }
    digitalWrite(SCK,0);
  }

  return dat;
}
```
**使用基础协议的实现算法，便可以对nRF24L01模块进行读写操作**
## nRF24L01写寄存器
```C++
void SPI_Reg_Write(byte address, byte value)
{
  digitalWrite(CSN,0);
  SPI_Write(byte(address+WRITE_REG));
  SPI_Write(value);
  digitalWrite(CSN,1);
}
```
## nRF24L01读寄存器
```C++
byte SPI_Reg_Read(byte address)
{
  byte outputValue;
  digitalWrite(CSN,0);
  outputValue = SPI_Read(address);
  digitalWrite(CSN,1);

  return outputValue;
}
```