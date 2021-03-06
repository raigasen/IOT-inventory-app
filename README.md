# IOT-inventory-app
Inventory tracker with a mobile application as a front end
Cloud-based inventory management is the monitoring and maintenance of a business’s inventory levels using online software. Enabling businesses to avoid many of the errors and issues that arise with traditional methods of measuring stock levels, Cloud-based inventory management seamlessly keeps track of inventory coming in and going out of your business.Traditionally, inventory management has been one of the most time-consuming and least popular tasks carried out by ecommerce businesses to keep their business running. It can be painstakingly boring and diverts resources from more important facets of the business, like growing the brand, improving efficiencies and adding new product lines.By contrast, Cloud-based inventory management performs the same function, but with greater efficiency and effectiveness. As well as giving businesses back their time and resources; Cloud-based stock management systems reduce the likelihood of human error.When it comes to inventory management, it pays to be precise. Stock is the lifeblood of your business so maintaining the right stock levels is crucial to your operations.
A cloud-based system can accurately inform you how much stock you have on hand. Cloud-based inventory management software can tell you whether you have enough stock for your demand forecast or whether you need to order more. This is an essential metric for customer satisfaction so you can avoid stock outs. It offers flexibility for you to implement customizations and business rules that support your unique requirements. The optimal cloud architecture preserves these customizations for you, so that they remain intact even as the cloud provider periodically upgrades your system to the latest release. Unlike spreadsheets or desktop applications, the cloud doesn't tether you to a desk. Web-based inventory management gives your personnel anywhere, anytime access to real-time data, whether on the road with a mobile device or receiving alerts on the warehouse floor. Metrics-driven dashboards let your managers continuously monitor and improve performance.



-HARDWARE PHASE-

The Arduino Yun is a hybrid Arduino consisting of ATmega32u4 and Atheros AR9331 Thus it supports a Linux distribution based on Openwork named Linino OS. Since we are using the Arduino Yun, this enables us to use the Wi-Fi feature to enable the wireless communication btw the Arduino and the IDE software on a system, thus allowing to update the software on the Yun remotely without having to connect the Arduino to the system. This Ultrasonic sensor are connected to the Arduino Yun which are used as the sensors to collect information from the containers. This sensor information is sent to the online server i.e. the Firebase. Furthermore, the information is sent to the online server in the form of percentage, where the container size is taken into consideration and the fill rate is converted to its percentage format, which results in easier display of the information in percentage format and in a donut graph.

-CODE-

---------------Initialization done for ‘.jason’ and the Ultrasonic Sensor:----------------

#include <Bridge.h>   //bridge library - for bridge communication between the server and Arduino
#include <Process.h>   //process library - for the online communication
#include <Console.h> //console library - Wi-Fi communication

Const char *FIREBASE = "https://fir-ee534.firebaseio.com/"; // declaring firebase server
Const char *NODE = ".json"; //'json declaration for online server communication extension

Const int UPDATE_RATE = 1000; //update delay rate
Const int trigPin3 = 6; //trigger pin used in the Arduino to connect the US sensor
Const int echoPin3 = 11; //echo pin connection



----------------Ultrasonic sensor coding and conversion to centimetres-----------------------

PinMode (trigPin3, OUTPUT); // Sets the trigPin as an Output  
PinMode (echoPin3, INPUT);    // Sets the echoPin as an Input

// Clears the trigPin
DigitalWrite (trigPin3, LOW);
delayMicroseconds(2);
// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin3, HIGH);
delayMicroseconds (10);
digitalWrite (trigPin3, LOW);
// Reads the echoPin, returns the sound wave travel time in microseconds
long duration3 = pulseIn (echoPin3, HIGH);
// calculating the distance
Double distance3= duration3*0.034/2;




------------Updating Information on the cloud server--------------

//Call used in main function
// Update value on Firebase
      request (distance3);
      wait ();
      response ();
// defining the function outside the main
void request (double distance3) {
char per3 [10];
dtostrf (distance3, 3, 2, per3); // distance is converted to string
// Build curl command line
  // Includes HTTPS support
  // PATCH
  // Single value so no JSON
  process.begin (“curl”);
  process.addParameter (“-k”);
  process.addParameter (“-X”);
  process.addParameter (“PATCH”);
  // Body
  // Value to update
  process.addParameter (“-d”);
  Sprintf (
    Buffer,
    "{\"distance1\": %s}",
    per3	
   );
  process.addParameter (buffer);
	 
  // URI
  Sprintf (
    Buffer,
    "%s%s",
    FIREBASE,
    NODE
  );
  process.addParameter (buffer);  
	
  // Run the command
  // Synchronous
  Process. Run ();
}
	
Void response ()
{
  Bool print = true;
  Char c;
	 
  // While there is data to read
  while (process.available ())
  {
    // Get character
    c = process.read();
	   
    // Debugging
    #ifdef DEBUG
      Console.print( c );
    #endif
  }
}
	
void wait()
{
  // periodically check curl process
  while( !process.available() )
  {
    delay( 100 );
  }
}
