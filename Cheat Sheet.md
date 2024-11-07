# Table of contents
- [Table of contents](#table-of-contents)
- [Components](#components)
- [In- and Outputs](#in--and-outputs)
  - [Enable Ports](#enable-ports)
    - [Port A](#port-a)
    - [Port B](#port-b)
    - [Port C](#port-c)
    - [Port A, B \& C](#port-a-b--c)
  - [Set mode of pins](#set-mode-of-pins)
    - [LED0 (PB5)](#led0-pb5)
    - [LED1 (PB10)](#led1-pb10)
    - [LED2 (PC7)](#led2-pc7)
    - [LED3 (PB9)](#led3-pb9)
    - [LED4 (PB8)](#led4-pb8)
    - [SW1 (PA10)](#sw1-pa10)
    - [SW2 (PB3)](#sw2-pb3)
  - [Turn on, turn off \& toggle LEDs](#turn-on-turn-off--toggle-leds)
    - [LED0 (PB5)](#led0-pb5-1)
    - [LED1 (PB10)](#led1-pb10-1)
    - [LED2 (PC7)](#led2-pc7-1)
    - [LED3 (PB9)](#led3-pb9-1)
    - [LED4 (PB8)](#led4-pb8-1)
  - [Check if button is pressed](#check-if-button-is-pressed)
    - [SW1 (PA10)](#sw1-pa10-1)
    - [SW2 (PB3)](#sw2-pb3-1)


# Components
| Name in circuit diagram | Name on Board | Port & Pin |
| - | - | - |
| LED0 | D0 | PB5 |
| LED1 | D1 | PB10 |
| LED2 | D2 | PC7 |
| LED3 | D3 | PB9 |
| LED4 | D4 | PB8 |
| SW1 | SW1 | PA10 |
| SW2 | SW2 | PB3 |

&nbsp;

# In- and Outputs

## Enable Ports

### Port A
```
RCC->APB2ENR |= (0x01 << 2); // enable PortA
```

### Port B
```
RCC->APB2ENR |= (0x01 << 3); // enable PortB
```

Fix PB3, disable configuration for Debug:
```
RCC->APB2ENR |= RCC_APB2ENR_AFIOEN;
AFIO->MAPR &= ~AFIO_MAPR_SWJ_CFG;
AFIO->MAPR |= AFIO_MAPR_SWJ_CFG_JTAGDISABLE;
```

### Port C
```
RCC->APB2ENR |= (0x01 << 4); // enable PortC
```

### Port A, B & C
```
RCC->APB2ENR |= 0x1C; // enable Port A, B & C
```
&nbsp;


## Set mode of pins

### LED0 (PB5)
```
GPIOB->CRL &= ~(0x0F << (4 * 5)); // clear control register of PB5
GPIOB->CRL |= (0x02 << (4 * 5)); // set PB5 as output Push-pull, 2MHz
```

### LED1 (PB10)
```
GPIOB->CRH &= ~(0x0F << (4 * 2)); // clear control register of PB10
GPIOB->CRH |= (0x02 << (4 * 2)); // set PB10 as output Push-pull, 2MHz
```

### LED2 (PC7)
```
GPIOC->CRL &= ~(0x0F << (4 * 7)); // clear control register of PC7
GPIOC->CRL |= (0x02 << (4 * 7)); // set PC7 as output Push-pull, 2MHz
```

### LED3 (PB9)
```
GPIOB->CRH &= ~(0x0F << (4 * 1)); // clear control register of PB9
GPIOB->CRH |= (0x02 << (4 * 1)); // set PB9 as output Push-pull, 2MHz
```

### LED4 (PB8)
```
GPIOB->CRH &= ~(0x0F << (4 * 0)); // clear control register of PB8
GPIOB->CRH |= (0x02 << (4 * 0)); // set PB8 as output Push-pull, 2MHz
```

### SW1 (PA10)
```
GPIOA->CRH &= ~(0x0F << (4 * 2)); // clear control register of PA10
GPIOA->CRH |= (0x08 << (4 * 2)); // set PA10 as input with pull-up / pull-down
GPIOA->ODR |= (0x01 << 10); // set PA10 to pull-up
```

### SW2 (PB3)
```
GPIOB->CRL &= ~(0x0F << (4 * 3)); // clear control register of PB3
GPIOB->CRL |= (0x08 << (4 * 3)); // set PB3 as input with pull-up / pull-down
GPIOB->ODR |= (0x01 << 3); // set PB3 to pull-up
```
&nbsp;


## Turn on, turn off & toggle LEDs

### LED0 (PB5)
```
GPIOB->ODR |= (0x01 << 5); // turn LED0 on
```
```
GPIOB->ODR &= ~(0x01 << 5); // turn LED0 off
```
```
GPIOB->ODR ^= (0x01 << 5); // toggle LED0
```

### LED1 (PB10)
```
GPIOB->ODR |= (0x01 << 10); // turn LED1 on
```
```
GPIOB->ODR &= ~(0x01 << 10); // turn LED1 off
```
```
GPIOB->ODR ^= (0x01 << 10); // toggle LED1
```

### LED2 (PC7)
```
GPIOC->ODR |= (0x01 << 7); // turn LED2 on
```
```
GPIOC->ODR &= ~(0x01 << 7); // turn LED2 off
```
```
GPIOC->ODR ^= (0x01 << 7); // toggle LED2
```

### LED3 (PB9)
```
GPIOB->ODR |= (0x01 << 9); // turn LED3 on
```
```
GPIOB->ODR &= ~(0x01 << 9); // turn LED3 off
```
```
GPIOB->ODR ^= (0x01 << 9); // toggle LED3
```

### LED4 (PB8)
```
GPIOB->ODR |= (0x01 << 8); // turn LED4 on
```
```
GPIOB->ODR &= ~(0x01 << 8); // turn LED4 off
```
```
GPIOB->ODR ^= (0x01 << 8); // toggle LED4
```
&nbsp;

## Check if button is pressed

### SW1 (PA10)
```
if ((GPIOA->IDR & (0x01 << 10)) == 0) // Check if SW1 is pressed
{

}
```

### SW2 (PB3)
```
//	if ((GPIOB->IDR & (0x01 << 3)) == 0)  // Check if SWe is pressed
{

}
```
&nbsp;