### #PICProje.org
##### K�t�phaneyi h�zl�ca kullanmaya ba�lamak i�in a�a��daki uyar�lar� dikkate almal�s�n�z.

Bu k�t�phane CubeMX yard�mc� program� ile olu�turulacak projelere 
h�zl�ca entegre edilebilecek �ekilde optimize edilmi�tir. 

Projenizi CubeMX'te olu�tururken bir adet SPI birimini, Full-Duplex modda, 
Hardware nSS deste�i olmaks�z�n, en fazla 10Mbit h�z�nda olacak �ekilde aktif etmelisiniz. Buna ek olarak iki adet GPIO pinini m�mk�n olan en y�ksek h�z� se�erek Output Push-Pull modda aktif etmelisiniz. 

Bu pinlerden birinin kullan�c� tan�ml� etiketi (User Label) xxx_CE, di�erinin ise xxx_nSS olmal�. 

**Not: Etiketlerin bir �nemi yok ancak kar���kl�k yaratmamak ad�na _nSS ve _CE eklemelerini yap�n�z.**

Ayr�ca bir adet GPIO_EXTIx (External Interrupt) pini aktif etmelisiniz. 

�nemli Not: CubeMX Code Generation safhas�nda "Generate peripheral initialization as a pair of '.c/.h' files per peripheral" se�ene�i aktif olmal�.

# �rnek CubeMX Konfigurasyonu:
## GPIO
#### xxx_CE ve xxx_nSS i�in;
    -GPIO Output Level	    : High
    -GPIO Mode		        : Output Push Pull
    -GPIO Pull-up/Pull-down	: No pull-up and no pull-down
    -Maximum output speed	: Very High (veya m�mk�n olan en y�ksek h�z)
    -User Label		        : nRF24L01P_CE (ve _nSS)

#### -GPIO_EXTIx i�in;
    -GPIO Mode		        : External Interrupt Mode with Rising edge...
    -GPIO Pull-up/Pull-down	: No pull-up and no pull-down
    -User Label		        : Don't Matter...

## NVIC
    -EXTI xxx [xx xx]       : Enabled ? Yes.

## SPIx
    -Frame Format	        : Motorola
    -Data Size		        : 8 Bits
    -First Bit              : MSB First
	
	-Prescaler		        : 256 (10MBit'i ge�meyecek herhangi bir de�er.)
    -BaudRate*	            : 175.781 KBits/s (Test ama�l� d���k h�z)
	-Clock Polarity (CPOL)	: Low
	-Clock Phase (CPHA)	    : 1 Edge
	
	-CRC Calculation	    : Disabled
	-nSS Signal Type	    : Software