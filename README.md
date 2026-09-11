# robs

ini klo mo liat punyaku tdi

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int led = 13;  
const int btn = 4;       

int pwm = 0;
int tombolSekarang;
int tombolSebelumnya = HIGH;

void setup() {
  pinMode(led, OUTPUT);
  pinMode(btn, INPUT_PULLUP);
  lcd.init();
  lcd.backlight();
  analogWrite(led, pwm);
  lcd.setCursor(0, 0);
  lcd.print("PWM LED:");
  
  lcd.setCursor(0, 1);
  lcd.print(pwm);
}

void loop() {
  tombolSekarang = digitalRead(btn);

  if (tombolSebelumnya == HIGH && tombolSekarang == LOW) {
    pwm = pwm + 25;
    if (pwm > 255) {
      pwm = 0;
    }
    analogWrite(led, pwm);
    lcd.setCursor(0, 0);
    lcd.print("PWM LED:        ");
    lcd.setCursor(0, 1);
    lcd.print("Nilai: ");
    lcd.print(pwm);
    lcd.print("    ");
    delay(200);
  }
  tombolSebelumnya = tombolSekarang;
}

tp di modif sendiri yoe