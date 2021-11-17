#include <ESP8266WiFi.h> 
#include <DHT.h>
#define DHT11PIN 4
#define DHTTYPE DHT11

//TANIMLAMALAR
const char* ssid = "wifiadı";  
const char* password = "şifre"; 
const char* host = "alanadiniz.com";
DHT dht(DHT11PIN, DHTTYPE);
float h,tc,tf;
// RGB LED Bacak Tanımlaması
int R=5;
int G=6;
int B=7;


void setup() { 
Serial.begin(115200); 
dht.begin();
delay(100);
Serial.println(); 
Serial.print("Baglaniyor..");
Serial.println(ssid);

WiFi.mode(WIFI_STA);
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED)
{
delay(500);
Serial.print("Wifiye Bağlanamıyor");
}
Serial.println("");
Serial.println("WiFi connected"); 
Serial.println("IP address: "); 
Serial.println(WiFi.localIP()); 
} 
int value = 0; 
void loop() { 

 double Sicaklik = sicaklik(); 
 double Nem = nemm();
 
delay(5000); ++value; 
Serial.print("connecting to ");
Serial.println(host); // Use WiFiClient class to create TCP connections
WiFiClient client;
const int httpPort = 80;
if (!client.connect(host, httpPort)) {
Serial.println("Bağlandı Hatası");
return;
}

String url = "/";
 url += "?nem=";
url += Nem;
url += "&sicaklik=";
url += Sicaklik;

Serial.print("Requesting URL: ");
Serial.println(url); 
client.print(String("GET ") + url + " HTTP/1.1\r\n" + "Host: " + host + "\r\n" + "Connection: close\r\n\r\n");
unsigned long timeout = millis();
while (client.available() == 0) {
if (millis() - timeout > 5000)
{ Serial.println(">>> Client Timeout !");
client.stop(); return; } } 
while (client.available())
{ String line = client.readStringUntil('\r'); 
Serial.print(line);
}
Serial.println();
Serial.println("Bağlandı Kapatıldı"); }

double nemm(){
    delay(2000);
   double nem = dht.readHumidity();
   return nem;
  }
  double sicaklik(){
    delay(2000);
  double sic = dht.readTemperature();
  return sic;
  }


  void sendSensor()
{
  float h = dht.readHumidity();  // nem ölçümü
  float t = dht.readTemperature(); // sıcaklık ölçümü
 
  if (isnan(h) || isnan(t)) {
    Serial.println("Sensöz Okuma yapamadı!");
    return;
  }
}
