# EXPERIMENT:06:SQUARE WAVE GENERATION AT THE OUTPUT PIN USING TIMER

### Aim:
To generate a PWM wave at the timer pin output and  simuate it on  proteus using an virtual oscilloscope  

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

The timer modules can operate a variety of modes one of which is the PWM mode. Where the timer gets clocked from an internal source and counts up to the auto-reload register value, then the output channel pin is driven HIGH. And it remains until the timer counts reach the CCRx register value, the match event causes the output channel pin to be driven LOW. And it remains until the timer counts up to the auto-reload register value, and so on.

The resulting waveform is called PWM (pulse-width modulated) signal. Whose frequency is determined by the internal clock, the Prescaler, and the ARRx register. And its duty cycle is defined by the channel CCRx register value. The PWM doesn’t always have to be following this exact same procedure for PWM generation, however, it’s the very basic one and the easier to understand the concept. It’s called the up-counting PWM mode. We’ll discuss further advanced PWM generation techniques as we go on in this series of tutorials.

The following diagram shows you how the ARR value affects the period (frequency) of the PWM signal. And how the CCRx value affects the corresponding PWM signal’s duty cycle. And illustrates the whole process of PWM signal generation in the up-counting normal mode.

STM32 Timers – PWM Output Channels

Each Capture/Compare channel is built around a capture/compare register (including a shadow register), an input stage for capture (with a digital filter, multiplexing, and Prescaler) and an output stage (with comparator and output control). The output stage generates an intermediate waveform which is then used for reference: OCxRef (active high). The polarity acts at the end of the chain.
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/87457b57-4311-440b-8cbe-a9d78db4335a)

STM32 Timers In PWM Mode

Pulse width modulation mode allows generating a signal with a frequency determined by the value of the TIMx_ARR register and a duty cycle determined by the value of the TIMx_CCRx register. The PWM mode can be selected independently on each channel (one PWM per OCx output) by writing 110 (PWM mode 1) or ‘111 (PWM mode 2) in the OCxM bits in the TIMx_CCMRx register. The user must enable the corresponding preload register by setting the OCxPE bit in the TIMx_CCMRx register, and eventually the auto-reload preload register by setting the ARPE bit in the TIMx_CR1 register.

OCx polarity is software programmable using the CCxP bit in the TIMx_CCER register. It can be programmed as active high or active low. For applications where you need to generate complementary PWM signals, this option will be suitable for you.

In PWM mode (1 or 2), TIMx_CNT and TIMx_CCRx are always compared to determine whether TIMx_CCRx≤TIMx_CNT or TIMx_CNT≤TIMx_CCRx (depending on the direction of the counter).

The timer is able to generate PWM in edge-aligned mode or center-aligned mode depending on the CMS bits in the TIMx_CR1 register.
STM32 PWM Frequency

In various applications, you’ll be in need to generate a PWM signal with a specific frequency. In servo motor control, LED drivers, motor drivers, and many more situations where you’ll be in need to set your desired frequency for the output PWM signal.

The PWM period (1/FPWM) is defined by the following parameters: ARR value, the Prescaler value, and the internal clock itself which drives the timer module FCLK. The formula down below is to be used for calculating the FPWM for the output. You can set the clock you’re using, the Prescaler, and solve for the ARR value in order to control the FPWM and get what you want.

STM32 PWM Frequency Formula - STM32 PWM Frequency Equation
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/aca8a20e-9b99-40c1-bada-f31accaa2ae9)

STM32 PWM Duty Cycle

In normal settings, assuming you’re using the timer module in PWM mode and generating PWM signal in edge-aligned mode up-counting configuration. The duty cycle percentage is controlled by changing the value of the CCRx register. And the duty cycle equals (CCRx/ARR) [%].
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/58ce0807-331e-49f7-bc8d-373f82592a92)



## Procedure:
Step1: Open CubeMX & Create New Project
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)


Step2: Choose The Target MCU & Double-Click Its Name select the target to be programmed  as shown below and click on next 

 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

Step3: Configure Timer2 Peripheral To Operate In PWM Mode With CH1 Output
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/682c851a-7dfe-4089-8395-f76088d43896)


Step4: Set The RCC External Clock Source
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/8888af3b-63e2-4760-a51b-17b477763941)


STM32 RCC External Clock Selection CubeMX

Step5: Go To The Clock Configuration

Step6: Set The System Clock To Be 72MHz
![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4ea03faa-fb90-4b31-8079-3db5f959f2c3)


Step7: Name & Generate The Project Initialization Code For CubeIDE or The IDE You’re Using



Step8.  Creating Proteus project and running the simulation
We are now at the last part of step by step guide on how to simulate STM32 project in Proteus.

Step9. Create a new Proteus project and place STM32F40xx i.e. the same MCU for which the project was created in STM32Cube IDE. 
14. After creation of the circuit as per requirement as shown below 

 ![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/4f377f5e-bdda-489e-a416-c712c893831d)

Step10. Double click on the the MCU part to open settings. Next to the Program File option, give full path to the Hex file generated using STM32Cube IDE. Then set the external crystal frequency to 8M (i.e. 8 MHz). Click OK to save the changes.

 
Step14. click on debug and simulate using simulation as shown below 
 ![image](https://github.com/vasanthkumarch/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/36288975/b8efbfc2-f0c5-4106-8117-3a6e7ac87f6c)


 

  

## STM 32 CUBE PROGRAM :
```
#include "main.h"


void SystemClock_Config(void);
static void MX_GPIO_Init(void);
static void MX_TIM2_Init(void);

int main(void)
{
 
  MX_TIM2_Init();

  HAL_TIM_Base_Start(&htim2);
  HAL_TIM_PWM_Init(&htim2);
  HAL_TIM_PWM_Start(&htim2,TIM_CHANNEL_1);

  while (1)
{

}

}
```




## Output screen shots of proteus  :
## For Pulse at 5000:
![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/7b19a717-b2ca-4b69-935e-99ec4b839e57)
## For Pulse at 7500:
![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/d57b04cc-ad73-437b-a89c-13692b2f803d)
## For Pulse at 2500:

![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/89114289-7738-4039-b52b-fc0c4619fc3b)
 
## CIRCUIT DIAGRAM (EXPORT THE GRAPHICS TO PDF AND ADD THE SCREEN SHOT HERE): 
 ![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/ebf9951c-276c-4e0a-bc43-931e89b61124)


## DUTY CYCLE AND FREQUENCY CALCULATION: 
## FOR PULSE AT 5000:
```
TON =1.5*0.2m = 0.3ms 
TOFF=1.5*0.2m = 0.3ms
TOTAL TIME = 0.3ms + 0.3ms = 0.6ms
FREQUENCY = 1/(TOTAL TIME)
F=1/0.6ms = 1.66*10^3Hz
F = 1.6 KHz
Duty = 0.3ms/0.6ms = 1/2 = 0.5*100 = 50%
```
![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/7b19a717-b2ca-4b69-935e-99ec4b839e57)

## FOR PULSE AT 7500:
```
TON = 2.2*0.2m = 0.44ms
TOFF = 0.8*0.2m = 0.16ms 
TOTAL TIME = 0.44ms + 0.16ms = 0.6ms
FREQUENCY = 1/(TOTAL TIME)
F=1/0.6ms = 1.666*10^3Hz
F = 1.6 KHz
Duty = 0.44ms/0.6ms = 0.73*100 = 73%
```
![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/d57b04cc-ad73-437b-a89c-13692b2f803d)

## FOR PULSE AT 2500:
```
TON = 0.8*0.2m = 0.16ms
TOFF= 2.2*0.2m = 0.44ms
TOTAL TIME = 0.16ms + 0.44ms = 0.6ms
FREQUENCY = 1/(TOTAL TIME)
F=1/0.6ms = 1.666*10^3Hz
F = 1.6KHz
Duty = 0.16ms/0.6ms = 0.26*100 = 26%
```
![image](https://github.com/SOMEASVAR/EXPERIMENT--07-SQUARE-WAVE-GENERATION-AT-THE-OUTPUT-PIN-USING-TIMER/assets/93434149/89114289-7738-4039-b52b-fc0c4619fc3b)

## Result :
A PWM Signal is generated using the following frequency and various duty cycles are simulated 




