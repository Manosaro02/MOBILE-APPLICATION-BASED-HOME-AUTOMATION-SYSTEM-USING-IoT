#include <WiFi.h>
#include <Wire.h>
#include<DHT.h>
#define DHTPIN 14 //dht pin defined
#define DHTTYPE DHT11 //dht type defined
WiFiClient client;
DHT dht(DHTPIN,DHTTYPE);
#define ssid "Wifi"
#define password "`12367dh"
17
WiFiServer server(80);
IPAddress local_IP(192,168,1,112);
IPAddress gateway(192,168,1,1);
IPAddress subnet(255, 255, 0, 0);
void setup()
{
Serial.begin(115200);
dht.begin();
WiFi.begin(ssid,pass);
Serial.println("Connecting");
while(WiFi.status()!=WL_CONNECTED)
{
Serial.print(".");
delay(100);
}
Serial.println("Connected");
}
 Serial.begin(115200);
 pinMode(14, OUTPUT); // set the LED pin mode
 delay(10);
 // We start by connecting to a WiFi network
 WiFi.config(local_IP,gateway,subnet);
 Serial.println();
18
 Serial.println();
 Serial.print("Connecting to ");
 Serial.println(ssid);
 WiFi.begin( ssid,password);
// WiFi.config(local_IP,gateway);
 while (WiFi.status() != WL_CONNECTED) {
 delay(500);
 Serial.print(".");
 }
 Serial.println("");
 Serial.println("WiFi connected.");
 Serial.println("IP address: ");
 Serial.println(WiFi.localIP());

 server.begin();
}
int value = 0;
void loop(){
// put your main code here, to run repeatedly:
float temperature = dht.readTemperature();
float humidity = dht.readHumidity();
Serial.println("Temperature:" + String(temperature) + " " +
19
"Humidity:" + String(humidity));
client.stop();
if(client.connect(server,80))
WiFiClient client = server.available(); // listen for incoming
clients
 if (client) { // if you get a client,
 Serial.println("New Client."); // print a message out
the serial port
 String currentLine = ""; // make a String to hold
incoming data from the client
 while (client.connected()) { // loop while the client's
connected
 if (client.available()) { // if there's bytes to
read from the client,
 char c = client.read(); // read a byte, then
 Serial.write(c); // print it out the serial
monitor
 if (c == '\n') { // if the byte is a
newline character
 // if the current line is blank, you got two newline
characters in a row.
 // that's the end of the client HTTP request, so send a
response:
 if (currentLine.length() == 0) {
 // HTTP headers always start with a response code (e.g.
HTTP/1.1 200 OK)
 // and a content-type so the client knows what's coming,
then a blank line:
 client.println("HTTP/1.1 200 OK");
20
 client.println("Content-type:text/html");
 client.println();
 // the content of the HTTP response follows the header:
 client.print("Click <a href=\"/H\">here</a> to turn the
LED on pin 14 on.<br>");
 client.print("Click <a href=\"/L\">here</a> to turn the
LED on pin 14 off.<br>");
 // The HTTP response ends with another blank line:
 client.println();
 // break out of the while loop:
 break;
 } else { // if you got a newline, then clear currentLine:
 currentLine = "";
 }
 } else if (c != '\r') { // if you got anything else but a
carriage return character,
 currentLine += c; // add it to the end of the
currentLine
 }
 // Check to see if the client request was "GET /H" or "GET
/L":
 if (currentLine.endsWith("GET /H")) {
 digitalWrite(14, HIGH); // GET /H turns the
LED on
 }
 if (currentLine.endsWith("GET /L")) {
21
 digitalWrite(14, LOW); // GET /L turns the
LED off}
 }
 // close the connection:
 client.stop();
 Serial.println("Client Disconnected.");
 }
}
