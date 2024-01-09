#include <SPI.h>
#include <Wire.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <Adafruit_BME280.h>
#include <Adafruit_MPU6050.h>

// For OLED
#define SCREEN_WIDTH 128 
#define SCREEN_HEIGHT 64 
#define SCREEN_ADDRESS 0x3C
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire);

// For BME
Adafruit_BME280 bme; // I2C

// For MPU
Adafruit_MPU6050 mpu;

// Ace Shot Variables
float aceShotThreshold = 20.0; // 阈值，可根据需要调整
int aceShotCount = 0;
int buzzerPin = 0;

// Start
void setup() {
  Serial.begin(9600);
  // Initialize OLED
  if(!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    Serial.println(F("SSD1306 allocation failed"));
    for(;;); 
  }
  display.display();
  delay(2000); 
  display.clearDisplay();

  // Initialize BME
  if (!bme.begin(0x76)) {
    Serial.println("Could not find a valid BME280 sensor, check wiring!");
    while (1);
  }

  // Initialize MPU
  if (!mpu.begin()) {
    Serial.println("Failed to find MPU6050 chip");
    while (1) {
      delay(10);
    }
  }
  mpu.setAccelerometerRange(MPU6050_RANGE_8_G);
  mpu.setFilterBandwidth(MPU6050_BAND_21_HZ);

  pinMode(buzzerPin, OUTPUT);
}

void loop() {
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);

  // 显示 AceTennis 和网球图标
  display.setCursor(32, 52); // 居中位置
  display.print("AceTennis ");
  // 网球图标可以使用一个小图形来表示，这里用一个简单的圆形代替
  display.fillCircle(92, 55, 4, SSD1306_WHITE);

  // 显示 Ace Shot 数量
  display.setCursor(18, 28);
  display.setTextSize(2);
  display.print("Shots:");
  display.print(aceShotCount);

  // 显示温度和湿度
  display.setCursor(30, 0);
  display.setTextSize(1);
  display.print("Tem: ");
  display.print(bme.readTemperature());
  display.println(" C");
  display.setCursor(30, 8);
  display.print("Hum: ");
  display.print(bme.readHumidity());
  display.println(" %");
  display.display();

  // 检测 Ace Shot
  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);
  float accMagnitude = sqrt(a.acceleration.x * a.acceleration.x +
                            a.acceleration.y * a.acceleration.y +
                            a.acceleration.z * a.acceleration.z);

  if (accMagnitude > aceShotThreshold) { 
    aceShotCount++; // 增加 Ace Shot 计数
    display.setCursor(30, 16); // 临时显示位置
    display.print("Perfect Shot!");
    digitalWrite(buzzerPin, HIGH);
    display.display();
    delay(500);
    digitalWrite(buzzerPin, LOW);
    // delay(1000);
  }
  delay(100);
}
