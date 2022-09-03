---
layout: post
title: Testing SPI interface with STM32 Nucleo 
subtitle: Trying to interface with the BME280 sensor from Bosch
published: false
---

## Microcontroller - Showcase

Using BME280 in conjunction with the STM32 Nucleo-F072RB to learn the SPI interface 

### The Wiring 

Here is a picture of how I wired things up. I used the defualt SPI1 communication pins to hook everything up. I also used the digikey tutorial interfacing with rom from here [link](https://www.digikey.com/en/maker/projects/getting-started-with-stm32-how-to-use-spi/09eab3dfe74c4d0391aaaa99b0a8ee17)

![Nucleo Board hookup]()

### The Programming 

Here is the code I wrote for the STM32 
the Trickiest part for me was firguring out that the ctrl_meas needed to be set to extract any data 

![Output Screenshot]()

~~~
/* USER CODE BEGIN Header */
/**
  ******************************************************************************
  * @file           : main.c
  * @brief          : Main program body
  ******************************************************************************
  * @attention
  *
  * Copyright (c) 2022 STMicroelectronics.
  * All rights reserved.
  *
  * This software is licensed under terms that can be found in the LICENSE file
  * in the root directory of this software component.
  * If no LICENSE file comes with this software, it is provided AS-IS.
  *
  ******************************************************************************
  */
/* USER CODE END Header */
/* Includes ------------------------------------------------------------------*/
#include "main.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include <stdio.h>

/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */
/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/
SPI_HandleTypeDef hspi1;

UART_HandleTypeDef huart2;

/* USER CODE BEGIN PV */
//instructions for the sensor
//chip id register
const uint8_t BME_280_id_reg = 0xD0;
const uint8_t BME_280_temp_msb_reg = 0xFA;
const uint8_t BME_280_ctrl_meas = 0xF4; //read
const uint8_t BME_280_ctrl_meas_write = 0b01110100;

//instructions
const uint8_t TEMP_READ = 0b00100011;
/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MX_GPIO_Init(void);
static void MX_USART2_UART_Init(void);
static void MX_SPI1_Init(void);
/* USER CODE BEGIN PFP */

/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */

/* USER CODE END 0 */

/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{
  /* USER CODE BEGIN 1 */

	char uart_buf[50];
	int uart_buf_len;
	char spi_buf[20];

  /* USER CODE END 1 */

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  MX_USART2_UART_Init();
  MX_SPI1_Init();
  /* USER CODE BEGIN 2 */

  //setting the CS pin to high
  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_SET);

  //testing sending info over uart
  uart_buf_len = sprintf(uart_buf, "SPI Test\r\n");
  HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);

  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_RESET);
  HAL_SPI_Transmit(&hspi1, (uint8_t *)&BME_280_ctrl_meas_write,1,100);
  HAL_SPI_Transmit(&hspi1, (uint8_t *)&TEMP_READ,1,100);
  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_SET);

  //read the id register

//  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_RESET);
//  HAL_SPI_Transmit(&hspi1, (uint8_t *)&BME_280_id_reg,1,100);
//  HAL_SPI_Receive(&hspi1, (uint8_t *)spi_buf,1,100);
//  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_SET);
  /* USER CODE END 2 */

  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {

//	  uart_buf_len = sprintf(uart_buf, "The value of the id is: \r\n0x%x\r\n",(unsigned int)spi_buf[0]);
//	  HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);
//	  HAL_Delay(1000);

	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_RESET);
	  HAL_SPI_Transmit(&hspi1, (uint8_t *)&BME_280_temp_msb_reg,1,100);
	  HAL_SPI_Receive(&hspi1, (uint8_t *)spi_buf,2,100);
	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_SET);

	  uart_buf_len = sprintf(uart_buf, "The value temp major bit is: \r\n0x%x, 0x%x\r\n",
			  (unsigned int)spi_buf[0],
			  (unsigned int)spi_buf[1]);
	  HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);

	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_RESET);
	  HAL_SPI_Transmit(&hspi1, (uint8_t *)&BME_280_ctrl_meas,1,100);
	  HAL_SPI_Receive(&hspi1, (uint8_t *)spi_buf,1,100);
	  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_6, GPIO_PIN_SET);

	  uart_buf_len = sprintf(uart_buf, "here is where the control temp is at: 0x%x \r\n",
	  			  (unsigned int)spi_buf[0]);
	  HAL_UART_Transmit(&huart2, (uint8_t *)uart_buf, uart_buf_len, 100);

	  HAL_Delay(1000);

    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configuration
  * @retval None
  */

~~~


