DIGITAL CLOCK USING ARDUINO UNO 
#include <Wire.h>
#include <RTClib.h>
#include <LiquidCrystal_I2C.h>

RTC_DS3231 rtc;
LiquidCrystal_I2C lcd(0x27, 16, 2);

void setup() {
  lcd.init();
  lcd.backlight();

  if (!rtc.begin()) {
    lcd.setCursor(0, 0);
    lcd.print("RTC NOT FOUND");
    while (1);
  }

  // RTC ka time computer ke current time se set karega
  rtc.adjust(DateTime(F(__DATE__), F(__TIME__)));
}

void loop() {
  DateTime now = rtc.now();

  lcd.setCursor(0, 0);
  lcd.print("Time: ");

  if (now.hour() < 10) lcd.print("0");
  lcd.print(now.hour());
  lcd.print(":");

  if (now.minute() < 10) lcd.print("0");
  lcd.print(now.minute());
  lcd.print(":");

  if (now.second() < 10) lcd.print("0");
  lcd.print(now.second());

  lcd.setCursor(0, 1);
  lcd.print("Date: ");

  if (now.day() < 10) lcd.print("0");
  lcd.print(now.day());
  lcd.print("/");

  if (now.month() < 10) lcd.print("0");
  lcd.print(now.month());
  lcd.print("/");

  lcd.print(now.year());

  delay(1000);
}
