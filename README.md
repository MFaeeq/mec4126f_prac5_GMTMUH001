# mec4126f_prac5_GMTMUH001
prac5
// Description----------------------------------------------------------------|
/*
 *
 */
// DEFINES AND INCLUDES-------------------------------------------------------|

#define STM32F051												   //COMPULSORY
#include "stm32f0xx.h"											   //COMPULSORY
#include "lcd_stm32f0.c"
#include "lcd_stm32f0.h"
// GLOBAL VARIABLES ----------------------------------------------------------|



// FUNCTION DECLARATIONS -----------------------------------------------------|

void main(void);  //COMPULSORY
void display_on_LCD(uint8_t number);
void init_leds(void);
void display_on_LEDs(uint8_t num);
void init_switches(void);


// MAIN FUNCTION -------------------------------------------------------------|

void main(void)
{
init_lcd();
init LEDs();


unint8_t_result = 0;

while (1)
{
	while(result<=255 & result >= 0);
	
	if ((GPIOA -> IDR & GPIO_IDR_1)==0)
	{
		result = ++result;
		result = GPIOB -> ODR; 
		display_on_LCD(result);
		display_on_LEDs(result); 
		delay(8000000);
	}
	else if ((GPIOA -> IDR & GPIO_IDR_2)==0)
	{
		result = ++result;
		result = GPIOB -> ODR; 
		display_on_LCD(result);
		display_on_LEDs(result); 
		delay(8000000);
	}
	else if ((GPIOA -> IDR & GPIO_IDR_2)==0)
	{
		result = 0;
		result = GPIOB -> ODR; 
		display_on_LCD(result);
		display_on_LEDs(result); 
		delay(8000000);
	}
	else 
	{
		result = GPIOB -> ODR; 
		display_on_LCD(result);
		display_on_LEDs(result); 
		delay(8000000);
	}
}
}

// OTHER FUNCTIONS -----------------------------------------------------------|
void display_on_LCD(uint8_t number)
{
	char number_display[1];
	sprintf(number_display,"%d",number);
	lcd_command(CLEAR);
	lcd_putstring(number_display);
	delay(800000);	
}

void init_leds(void) 
{
       RCC->AHBENR |= RCC_AHBENR_GPIOBEN; 
       GPIOB->MODER |= GPIO_MODER_MODER0_0;
       GPIOB->MODER |= GPIO_MODER_MODER1_0;
       GPIOB->MODER |= GPIO_MODER_MODER2_0;
       GPIOB->MODER |= GPIO_MODER_MODER3_0;
       GPIOB->MODER |= GPIO_MODER_MODER4_0;
       GPIOB->MODER |= GPIO_MODER_MODER5_0;
       GPIOB->MODER |= GPIO_MODER_MODER6_0;
       GPIOB->MODER |= GPIO_MODER_MODER7_0;
}

void display_on_LEDs(uint8_t num)

{
GPIOB -> ODR = num;
}

void init_switches(void)
{
RCC -> AHBENR |= RCC_AHBENR_GPIOAEN;
GPIOA -> MODER &= ~ GPIO_MODER_MODER1;
GPIOA -> MODER &= ~ GPIO_MODER_MODER2;
GPIOA -> MODER &= ~ GPIO_MODER_MODER3;
GPIOA -> PUPDR |=GPIO_PUPDR_PUPDR1_0;
GPIOA -> PUPDR |=GPIO_PUPDR_PUPDR2_0;
GPIOA -> PUPDR |=GPIO_PUPDR_PUPDR3_0;
}

void init_external_interrupts(void)
{
	RCC -> APB2ENR |= RCC_APB2ENR_SYSCFGCOMPEN;
	SYSCFG -> EXITCR[0] |= SYSCFG_EXTICR1_EXTI3_PA;
	EXTI -> IMR |= EXTI_IMR_MR3;
	EXTI -> FTSR |= EXTI_FTSR_TR3;
	NVIC_EnableIRQ(EXTI2_3_IRQn);
}

