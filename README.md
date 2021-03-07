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


_______________________________________________________________________________________________________________________________________________________________________________
-SOFTWARE-
_______________________________________________________________________________________________________________________________________________________________________________

To reduce the load on the mobile application development we choose Firebase as a Mobile Backend. Firebase is a complete Package of products that allows one to build web and mobile apps. Firebase offers MBaaS or Mobile Backend as a Service and offers a method to link web and mobile applications to a cloud based backend storage and API.
Data is stored as JSON and synchronized continuously to each associated client. When any cross-platform application is developed with iOS, Android, and JavaScript SDKs, the greater part of the user’s demand is based on one Real-time database instance and this instance gets updated with each new data[2]. Firebase is NoSQL based. There are very few cloud based server available which are similar to firebase [4].


To begin creating a backend database we first need to create the project. We will use the default firebase account and this will provide us with a project ID. This ID is important as it will define the location of the storage of the project. After the project has been created on the firebase account we need to set up an Authentication method. It supports authentication using passwords, email id or username, phone number, etc. Users can be allowed to sign in to a Firebase app either by using FirebaseUI as a complete drop-in authentication solution or by using the SDK to manually integrate one or a few sign-in techniques [2]. 


 This will allows us to Authenticate and Manage users from a variety of providers without server side code. This Authentication is only for developers. It is a service that can authenticate users using only client-side code and it is a paid service. It also includes a user management system whereby developers can enable user authentication with email and password login stored with Firebase [4]. This will allow us to make a hierarchy and will allow us to manage different development teams to work on the project. This will also allow us to give permissions to read and write and edit security code form the server end. The user has to input the required credentials and the Firebase system checks whether these credentials are correct or not [2]. 

When a new user turn on the device, it will send notify to the smart phone using firebase notification to alert someone tried to access to the system. The owner will resend notify to device to give permission and store it in firebase database [7].

The next step would be to set up the Cloud Storage. We need to cloud storage to upload and download files directly from clients. Again for the Firebase SDK and the cloud storage to work seamlessly we need to provide a declarative security language that lets you set access controls on individual files or group of files, such that one can make files public or private. 

Firebase Storage was designed for application developers who need to store and serve user-generated content, for example photos or any other file. It is backed by Google Cloud Storage which is cost-effective object storage service [4]. It gives secure document transfers and download for Firebase applications, regardless of network quality. 

Firebase Storage is upheld by Google Cloud Storage, a capable, basic and cost-effective object storage service [2]. And because of cloud storage we need not migrate to any other provider as the storage scales automatically.

After this we need to set up the database. In real-time database we need to edit the default rules to suit our needs. These rules as mentioned before give permissions to developers to read and write. An API is provided to the application developer which allows application data to be synchronized across clients and stored on Firebase's cloud [4]. Lastly in the usage tab we can observe the usage statistics of the users and provide modifications when needed. The data stored is highly secured and is robust in nature means it resumes from the last point if any network error occurs [4].

For the development of the mobile application that can be very easily accessible as it would be based upon android OS. We will be using the Android Studio IDE for the development. We choose the android OS as it is more widely used and very easily accessible on various devices. It is also very easy to code, manage and update. It is also important to have JAVA installed on your development computer as it is required in some phases that will be discussed later in the upcoming parts. Flutter is an open-source UI software development kit created by Google.


First, we need to locate the SHA-1 and SHA-256 keys that are present in your java directory. SHA-1 is a unique key generated for your PC that can be used for signing/ it is mainly used for submitting the Google API in case of android. Every system with an active JDK installed on it will have a unique SHA-1 and SHA-256 key present. To obtain these keys we need to find the JDK directory in our system and open command prompt in that directory space. After doing so we need to input the following command:

key tool -exportcert -alias androiddebugkey -keystore [PATH_TO_.DIRECTORY] –listv

Upon replacing [PATH_TO_DIRECTORY] with the path present in your system we should be able to run the terminal command. In some cases you will be prompted with a password which you can enter (usually android) after which you the list of certificates will be printed on the screen. After this you can simply copy and paste the SHA-1 and SHA-256 keys in a separate word document or a notepad file

Next we need to specify an app file on the firebase page. This will be the link between our android application and our Firebase database. After making the app on firebase we provide a package name and note this package name in a doc as we will need to use the same package name for the application as well. Once we are done we will be required to download and save the google-services.json file in the root folder of your application development directory.

As we already have a backend due to the firebase database we are not required to specifically create a backend in the application so we can prevent a lot of complications in this phase. Now we need to add the required repositories and dependencies so that we can use the required functions and processes. Flutter has developed different dependencies that reduce the workload of generating extended process by just probating them as simple functions. When integrated with Firebase Authentication, developers can define who has access to what data, and how they can access it [8]. Then all we need to do is just call these functions to use the embedded processes. This makes the length of the code much shorter and is also much more helpful in debugging and post processing of the code. As the processes and embedded into the required functions they can be called repeatedly without the need to write the entire process over again. This again further simplifies the code although the processing is a bit more tedious, but due to our app being only front end it will not affect a lot.

-Repositories and Dependancies used-

The following repositories were used in the project:

>cupertino_icons: ^0.1.2 – This is a repository which contains the default set of icons and assets that are required to make the user interface for the application.

>firebase_auth: ^0.15.4 – This is a futter plugin to use the Firebase Authenticaton API.

>firebase_database: ^3.1.1 – This is a flutter pugin to use the Firebase Realtime Database API.

>google_sign_in: ^4.1.1 – This is a flutter plugin for Google Sign In.

>provider: ^4.0.4 – 

>firebase_core: ^0.4.4 – This plugin enables the Flutter plugin to uses the Firebase Core API, which allows connections to multiple firebase applications.

>firebase:^7.2.1 – This package provides three libraries :
	-package:firebase/firebase.dart
	- package:firebase/firestore.dart
	- package:firebase/firebase_io.dart
	
>intl: ^0.15.8 – This package provides the internationalization and localization facilities like message translation, plurals and genders, date/time/number formatting and so on.

>percent_indicator: ^2.1.1 – This Package provides us with circular and linear percent indicators as a function.

>qr_flutter: ^3.2.0 – This is a simple library for simple and fast QR rendering via a widget/custom painter.

>barcode_scan: ^2.0.1 – Another simple library for barcode rendering.

>path_provider: ^1.6.4 – Flutter plugin for locating commonly used locations on the filesystem on android as well as IOS.


The following dependencies were used in the project:

>org.jetbrains.kotlin:kotlin-stdlib-jdk7  

>com.google.firebase:firebase-database:19.2.1

>com.google.firebase:firebase-database

>junit:junit:4.12

>androidx.test:runner:1.1.1

>androidx.test.espresso:espresso-core:3.1.1

>com.google.gms.google-services

-Flutter(Application Design)-

To simplify the process we will provide a separate page for each task. For every page that we need we will make a different code file and then piece them all together by calling them into a single main file. If we need to make a common function then we will create another file to develop the function. Keeping the function in separate files will allow us to call them when required without editing any variables and will also allow us to have a cleaner code and easier debugging. In case of running the application in debug mode we need a device to run the application on. Although we can emulate a device on the development PC itself it is better to have an external device, this will make the processing and the building of the application more efficient and faster. We can use external mobile phones running any recent version on android as an external device to run the application and test it.

-Login Method-

User will basically use their Google account to sign in. For the sign in method we will make a separate script and then call it into the main script in the end while building the application. In the sign in system we will have 2 separate methods consisting of sign in, sign out. Both these methods have a similar make and commands but their executions is mildly different. For the system we are required to use two packages:

>package:firebase_auth/firebase_auth.dart – This package has functions that will allow the online database to register and locate the specific user.
>package:google_sign_in/google_sign_in.dart – This package has methods that allow the use of android Google based sign in via their email and allow us to register the used id and email.

To begin we will have to run the following command:
		
>final FirebaseAuth _auth = FirebaseAuth.instance;
 		
This will authenticate the firebase to allocate users according to their email IDs. As soon as this command is called the application will await for a response from the google sign in method to allocate an email ID to the available string present.

To initiate the google sign in we need to create a function like the following:


>Future<String> signInWithGoogle() async {
>  final GoogleSignInAccount =await googleSignIn.signIn();
>  finalGoogleSignInAuthenticationgoogleSignInAuthentication=await GoogleSignInAccount.authentication;
>  final AuthCredential credential = GoogleAuthProvider.getCredential(
>    accessToken: googleSignInAuthentication.accessToken,
>    idToken: googleSignInAuthentication.idToken,);
>assert(user.email != null);
>  assert(user.displayName != null);
>  assert(user.photoUrl != null);

>  assert(!user.isAnonymous);
>  assert(await user.getIdToken() != null);

The async statement allows the application to await reply from the user and the above statement will create a pop up that will allow the user to login to their gmail account. Once the user logs in to their account their email, display name and their profile photo is acquired and stored. It is checked that these are not null or empty. In case it is empty the method will send the process back to the top at the beginning of the process. Once the sign in is complete the process will have a user ID token, which will be unique to each user. We will assign the profile details to separate strings which will allow us to use them as text files.

>final FirebaseUser currentUser = await _auth.currentUser(); 
>assert(user.uid == currentUser.uid);

The above statements will take the user ID and the ID token generated are set to the firebase statement which was awaiting before and will send the data to the database server. The second method that we need to implicate is the sign out method. This is a fairly simple method as compared to the sign in method. 

>void signOutGoogle() async{await googleSignIn.signOut();

The above statement will simply sign you out and clear the profile strings and basically reset the application. This will create our login/logout method. 

-Profile Page-

We will not discuss the planning of the application but rather we will talk about the important points like using the profile strings and connecting the sign out methods to the page and create a page switch in case of log out. After the planning and the basic page layout is created we can begin developing the page specific parts. First need to extract the image from the string. The image_URL string only provides us with a link to the image provided in the actual Gmail profile picture present in the users Gmail account. We can access that image via the URL and then flutter will build the application while down loading the image from the Gmail server. We need to following command to make the display widget.



>CircleAvatar(
>                backgroundImage: NetworkImage(
>                  imageUrl,
>                ),
>                radius: 60,
>                backgroundColor: Colors.transparent,
>              ),

Next, we need to use the other profile strings specifically the user name and the email strings. We got the information during log in and saved it in strings. To use these string its fairly simple as they can be simply considered as text files. This means we can create simple text widgets and just use the string and we will acquire the required output. We need the following command for that widget.

>Text(
>                name, //string name
>                style: TextStyle(
>                    fontSize: 25,
>                    color: Colors.deepPurple,
>                    fontWeight: FontWeight.bold),
>              ),

>Text(
>                email, //text email
>                style: TextStyle(
>                    fontSize: 25,
>                    color: Colors.deepPurple,
>                    fontWeight: FontWeight.bold),
>              ),


To create the sign out button we need to create a button widget and give it and action effect and link it to the sign out method that we created before on the login method and then the application should push the user screen back to the login page We will use the following set of code for to create the button.

>RaisedButton(
                onPressed: () {
	signOutGoogle(); 
Navigator.of(context).pushAndRemoveUntil(MaterialPageRoute(builder: (context) {return LoginPage();}), ModalRoute.withName('/'));
                },

Once we create this it will create a loop between the login and profile page. This will allow the user to login and logout safely and successfully and will allow the user to safely login and log out through the application itself and will not have to do it manually via their gmail. This finishes the Profile page


-Login Page-

We have created the methods for login in another dart file before so we will only have to call the method and design the UI for the login page the login page will be linked to the data page and the profile page has a push method. This page will not need many widgets, only the login option. The page can have other widgets and options but for the simplicity of the app we will give it a simple UI.

>Widget _signInButton() {
    return OutlineButton(
      splashColor: Colors.grey,
      onPressed: () {
        signInWithGoogle().whenComplete(() {
          Navigator.of(context).push(
            MaterialPageRoute(
              builder: (context) {
                return DataPage2();
              },
	     
When the Log in method returns true the above method will push the page in view to the datapage. We will later add a side drawer which will send us to the profile page and hence the log out button. And in case the log in is a failure a simple message will pop up stating the same.

-Data Page-

For the data page we will have a decent UI made up of circular progress indicators and Bar Progress indicators. As a repository for these types of indicators is already available there is no need to create them from scratch using the paint creator methods. We can simply add the repository can call these functions to use them. As this page will be a little more complex as compared to the other pages we will need to plan the design properly or else the system will not be able to compile the application due to the parameters not being aligned properly with the desired screen size if this occurs there will be a red screen showing the error code and description on the device. First we need to set up a basic layout of the page

>return MaterialApp(home: Scaffold(
      appBar:  AppBar(title: Text('Datapage'),),
      body: ListView(
	Container(
            height: 1,
            color: Colors.grey,
          ), //divider
	Container(
            height: 110,
            child: Row(
                children:[
                  Container(
                      width: 350,
                      padding: EdgeInsets.fromLTRB(20, 0, 0, 0),
                      child: Text('Container 2',
                        style: TextStyle(
                            color: Colors.black,
                            fontWeight: FontWeight.w400,
                            fontSize: 30
                        ),
                      )
                  ),
                  CircularPercentIndicator(
                    progressColor: Colors.amber,
                    percent: meso,
                    animation: true,
                    radius: 100,
		    lineWidth: 10,
                    circularStrokeCap: CircularStrokeCap.round,
                    center: Text(d2),
                  ),	
                ]
            )
          ),


The container is an outline widget that surrounds the main widget. We can provide specifications to the container by tweaking its property values. Inside the container we will have a second contaioner that will contain the label of the quantity under measure. Outside that container we will have the circular progress indicator method to keep track of the values and proportions. To position these widgets properly we can provide edge insets that will allow us to accurately position all the widgets properly with respect to the screen. These methods can be repeated multiple times as per the required amount to display all the data over the application. 

>Drawer(
            child: ListView(
              padding: EdgeInsets.zero,
              children:  <Widget>[
                DrawerHeader(
                  decoration: BoxDecoration(
                    color: Colors.orange,
                  ),
                  child: Text(
                    'Drawer Header',
                    style: TextStyle(
                      color: Colors.white,
                      fontSize: 24,
                    ),
                  ),
                ),
                ListTile(
                  leading: Icon(Icons.message),
			title: Text('Messages'),
                ),
                ListTile(
                  leading: Icon(Icons.account_circle),
                  title: Text('Profile'),
                  onTap: () {
                    Navigator.push(
                        context,
                        MaterialPageRoute(
                          builder:(context) => ProfileScreen(),
                      )
                    ); // close the drawer
                  },
                ),
                ListTile(
                  leading: Icon(Icons.center_focus_weak),
                  title: Text('scan'),
                  onTap: () {
                    Navigator.push(context,
                        MaterialPageRoute(
                          builder: (context) => ScanScreen(),
                        )

This method will create a drawer and will also create buttons with which we can navigate to the other pages of the application. 

			
