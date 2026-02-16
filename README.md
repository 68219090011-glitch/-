
วชิรวิชญ์ ดำช่วย 011  โครงงาน เปิดปิดไฟบ้านตอนกลางคืนด้วยอุณหภูมิ
https://app.cirkitdesigner.com/project/f0254c79-9fbd-488d-bd6b-a523974ec33a

code
#include <DHT.h>

#define DHTPIN 2        // ขา DATA ของ DHT11
#define DHTTYPE DHT11

#define LEDPIN 13       // LED ต่อที่ขา D13

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();

  pinMode(LEDPIN, OUTPUT);
}

void loop() {
  float temperature = dht.readTemperature(); // อ่านค่า °C

  // เช็กว่าอ่านค่าได้ไหม
  if (isnan(temperature)) {
    Serial.println("อ่านค่า DHT11 ไม่ได้");
    return;
  }

  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" C");

  // เงื่อนไข
  if (temperature > 15) {
    digitalWrite(LEDPIN, HIGH);   // LED ติด
  } else {
    digitalWrite(LEDPIN, LOW);    // LED ดับ
  }

  delay(1000); // หน่วง 1 วินาที
}

