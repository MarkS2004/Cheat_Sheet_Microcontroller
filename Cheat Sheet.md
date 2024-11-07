# Table of contents
- [Table of contents](#table-of-contents)
- [Quicklinks](#quicklinks)
- [Overview of components](#overview-of-components)
- [Enable Ports](#enable-ports)
  - [Enable Port A](#enable-port-a)
  - [Enable Port B](#enable-port-b)
  - [Enable Port C](#enable-port-c)
- [Cofigure pins (setup)](#cofigure-pins-setup)
  - [Configure LED0 (PB5)](#configure-led0-pb5)
  - [Configure LED1 (PB10)](#configure-led1-pb10)
  - [Configure LED2 (PC7)](#configure-led2-pc7)
  - [Configure LED3 (PB9)](#configure-led3-pb9)
  - [Configure LED4 (PB8)](#configure-led4-pb8)
  - [Configure SW1 (PA10)](#configure-sw1-pa10)
  - [Configure SW2 (PB3)](#configure-sw2-pb3)
- [Controll LEDs](#controll-leds)
  - [Controll LED0 (PB5)](#controll-led0-pb5)
  - [Controll LED1 (PB10)](#controll-led1-pb10)
  - [Controll LED2 (PC7)](#controll-led2-pc7)
  - [Controll LED3 (PB9)](#controll-led3-pb9)
  - [Controll LED4 (PB8)](#controll-led4-pb8)
- [Check button inputs](#check-button-inputs)
  - [Check SW1 (PA10)](#check-sw1-pa10)
  - [Check SW2 (PB3)](#check-sw2-pb3)

# Quicklinks
- [GitLab-Wiki](https://gitlab.com/HaraldLytentec/ucdhbwfn23/-/wikis/home) (Authentication required)
- [Reference Manual](https://www.st.com/resource/en/reference_manual/cd00171190.pdf)
- [Datasheet](https://www.st.com/resource/en/datasheet/stm32f103rb.pdf)
- [Notes on the development system](https://gitlab.com/HaraldLytentec/ucdhbwfn23/-/wikis/Hinweise%20zum%20Entwicklungssystem) (Authentication required)
&nbsp;

# Overview of components
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


# Enable Ports

## Enable Port A
```
RCC->APB2ENR |= (0x01 << 2); // enable PortA
```

## Enable Port B
```
RCC->APB2ENR |= (0x01 << 3); // enable PortB
```

Fix PB3, disable configuration for Debug:
```
RCC->APB2ENR |= RCC_APB2ENR_AFIOEN;
AFIO->MAPR &= ~AFIO_MAPR_SWJ_CFG;
AFIO->MAPR |= AFIO_MAPR_SWJ_CFG_JTAGDISABLE;
```

## Enable Port C
```
RCC->APB2ENR |= (0x01 << 4); // enable PortC
```


# Cofigure pins (setup)

## Configure LED0 (PB5)
```
GPIOB->CRL &= ~(0x0F << (4 * 5)); // clear control register of PB5
GPIOB->CRL |= (0x02 << (4 * 5)); // set PB5 as output Push-pull, 2MHz
```

## Configure LED1 (PB10)
```
GPIOB->CRH &= ~(0x0F << (4 * 2)); // clear control register of PB10
GPIOB->CRH |= (0x02 << (4 * 2)); // set PB10 as output Push-pull, 2MHz
```

## Configure LED2 (PC7)
```
GPIOC->CRL &= ~(0x0F << (4 * 7)); // clear control register of PC7
GPIOC->CRL |= (0x02 << (4 * 7)); // set PC7 as output Push-pull, 2MHz
```

## Configure LED3 (PB9)
```
GPIOB->CRH &= ~(0x0F << (4 * 1)); // clear control register of PB9
GPIOB->CRH |= (0x02 << (4 * 1)); // set PB9 as output Push-pull, 2MHz
```

## Configure LED4 (PB8)
```
GPIOB->CRH &= ~(0x0F << (4 * 0)); // clear control register of PB8
GPIOB->CRH |= (0x02 << (4 * 0)); // set PB8 as output Push-pull, 2MHz
```

## Configure SW1 (PA10)
```
GPIOA->CRH &= ~(0x0F << (4 * 2)); // clear control register of PA10
GPIOA->CRH |= (0x08 << (4 * 2)); // set PA10 as input with pull-up / pull-down
GPIOA->ODR |= (0x01 << 10); // set PA10 to pull-up
```

## Configure SW2 (PB3)
```
GPIOB->CRL &= ~(0x0F << (4 * 3)); // clear control register of PB3
GPIOB->CRL |= (0x08 << (4 * 3)); // set PB3 as input with pull-up / pull-down
GPIOB->ODR |= (0x01 << 3); // set PB3 to pull-up
```
&nbsp;


# Controll LEDs

## Controll LED0 (PB5)
```
GPIOB->ODR |= (0x01 << 5); // turn LED0 on
```
```
GPIOB->ODR &= ~(0x01 << 5); // turn LED0 off
```
```
GPIOB->ODR ^= (0x01 << 5); // toggle LED0
```

## Controll LED1 (PB10)
```
GPIOB->ODR |= (0x01 << 10); // turn LED1 on
```
```
GPIOB->ODR &= ~(0x01 << 10); // turn LED1 off
```
```
GPIOB->ODR ^= (0x01 << 10); // toggle LED1
```

## Controll LED2 (PC7)
```
GPIOC->ODR |= (0x01 << 7); // turn LED2 on
```
```
GPIOC->ODR &= ~(0x01 << 7); // turn LED2 off
```
```
GPIOC->ODR ^= (0x01 << 7); // toggle LED2
```

## Controll LED3 (PB9)
```
GPIOB->ODR |= (0x01 << 9); // turn LED3 on
```
```
GPIOB->ODR &= ~(0x01 << 9); // turn LED3 off
```
```
GPIOB->ODR ^= (0x01 << 9); // toggle LED3
```

## Controll LED4 (PB8)
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

# Check button inputs

## Check SW1 (PA10)
```
if ((GPIOA->IDR & (0x01 << 10)) == 0) // Check if SW1 is pressed
{

}
```

## Check SW2 (PB3)
```
//	if ((GPIOB->IDR & (0x01 << 3)) == 0)  // Check if SWe is pressed
{

}
```
&nbsp;