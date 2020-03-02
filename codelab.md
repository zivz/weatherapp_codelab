author: Ziv Zalzstein
summary: Create iOS App
id: docs
categories: codelab, swift, ios
environments: ios
status: Published
feedback link: https://github.com/zivz/weatherapp_codelab

# Creating your first iOS App

## First iOS App Overview
Duration: 0:01:30

In the following tutorial, we'll learn how to make an iOS app.  

**General**  
The app will show the user the current weather in his current location.  

**UI**  
The UI Will have a single view.  
The primary view will contain two subviews:  
* A view for the current weather
* A table view for the next 10 day forecast.

![WeatherApp](./assets/WeatherApp.png)

**API**  
The app will interact with Open Weather API, in order to fetch the current weather, and the forecast.  

**Location**  
The app will fetch the user's location, upon `When-in-use` authorization permission.

**Notes:**
* The tutorial will focus on `Storyboards`, `Autolayout` and `UIStackView`.  
* The tutorial **will include the current weather view only**.  
* Location Handler, Networking, Parsing code will be provided in order to provide the full capabilities of the app.  
* The app is extendable for further implementation of the next 10 day forecast.  
* Tableview displaying the forecast for the next 10 day implementation is still available in [Github](https://github.com/zivz/WeatherApp).  

**Resources:**
* [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/overview/)
* [Autolayout](https://www.youtube.com/watch?v=emojd8GFB0o) and [StackView](https://www.youtube.com/watch?v=eF9Ut-VpdAI)
* [Open Weather API](https://openweathermap.org/api).
* The full code is available [here](https://github.com/zivz/WeatherApp).

## Xcode - New Project
Duration: 0:04:00

This tutorial assumes you have basic familiarity with Xcode, as provided in a separate session.

**Resources:**
* [Download Xcode from App Store](https://apps.apple.com/il/app/xcode/id497799835?mt=12)
* [Xcode Essentials](https://www.youtube.com/watch?v=jniJeamcIUU)

#### Create a new Xcode Project

Open Xcode and select "Create a new Xcode Project"  
![Create a new Xcode Project](./assets/Create_a_new_xcode_project.png)

#### Choose a template for your new project with following options:
iOS | Single View App  
![Choose a template](./assets/Choosing_a_template.png)

#### Choose options for your new project:
* Product Name - give a meaningful name such as `WeatherApp`
* Organization Name - give your Name or your organization Name
* Organization identifier will be constructed from Organization Name
* Bundle Identifier - will be constructed from your Product Name and Organization Name.
* Language - Swift
* User Interface - Choose Storyboard
* Leave `User Core Data, Include Unit Tests and Include UI Tests` **Unchecked**

![Template Options](./assets/Template_options.png)

#### Edit and Verify Project Settings  
Once the project is created, The project file will appear on the screen.
**Under General tab verify the following:**  
* Verify `Display Name, Bundle Identifier` are correct under `identity`
* Check `iPhone` only, under `Deployment info`
* Check `Portrait` only, under `Device Orientation`

![Project Settings](./assets/Project_Settings.png)

##[Weather App UI Overview]{#weather-app-ui-overview}

#### UI Components
Our Primary View will contain 2 subviews.  
* Current Weather view
* Table View with 10 day weather forecast, **which will not be part of this tutorial.**

![WeatherApp Subviews](./assets/TwoViews.png)

#### Current Weather view
Will be consisted of 2 parts:   
* **Part 1** - General Info
  * Current date
  * Current Temperature in Celsius
  * Current Location
* **Part 2** - Weather Description
  * An Image of Weather Type
  * Weather Description

![Current Weather View](./assets/CurrentWeatherView.png)

## Appendix - UI Terms in Xcode

In this section we'll get familiar with some terms related to UI in Xcode.

#### Storyboard
From [raywanderlich.com](https://www.raywenderlich.com/5055364-ios-storyboards-getting-started) - Storyboards are an exciting feature first introduced in iOS 5, which save time building user interfaces for your apps. Storyboards allow you to prototype and design multiple view controller views within one file, and also let you create transitions between view controllers.

From [apple.com](https://developer.apple.com/library/archive/documentation/General/Conceptual/Devpedia-CocoaApp/Storyboard.html) - A storyboard is a visual representation of the user interface of an iOS application, showing screens of content and the connections between those screens.

#### Autolayout

From [raywanderlich.com](https://www.raywenderlich.com/811496-auto-layout-tutorial-in-ios-getting-started) - At first, Apple made one screen size for the iPhone. Developers didn’t have to create flexible interfaces as they only had to fit that one size. Today, differently sized devices and more emphasis on landscape mode demand user interfaces of different sizes. Auto Layout is Apple’s solution to this problem, enabling UI elements to grow, shrink and move depending on screen size. Auto Layout makes it easy to support different screen sizes in your apps.

#### Constraints

From [SwiftLee](https://www.avanderlee.com/swift/auto-layout-programmatically/) - Auto Layout constraints allow us to create views that dynamically adjust to different size classes and positions. The constraints will make sure that your views adjust to any size changes without having to manually update frames or positions

#### UIStackview
From [apple.com](https://developer.apple.com/documentation/uikit/uistackview) - Stackviews let you leverage the power of Auto Layout, creating user interfaces that can dynamically adapt to the device’s orientation, screen size, and any changes in the available space.
The stack view manages the layout of all the views in its arranged subviews property. These views are arranged along the stack view’s axis, based on their order in the arranged subviews array. The exact layout varies depending on the stack view’s axis, distribution, alignment, spacing, and other properties.
![Stack view - Apple developer](./assets/Apple_StackView.png)

## Creating the basic view

As seen in the image capture below, **Current Weather View** and **Weather Forecast (table) view** are two separate views in the view held by the view controller.

![WeatherApp Subviews](./assets/TwoViews.png "Current Weather View and Forecast Table View")  
We'll create this view and later pile up our detailed UI Elements.  

We're basically going to add the blue view, holding our detailed UI Elements as in the 3D capture below.
![Current Weather 3D Capture](./assets/Current_Weather_3D.png "Current Weather 3D Capture")

In order to do so, follow these steps:
1. Open `Main.storyboard`
  1. You should currently see a View inside the View Controller hierarchy.  
  ![View Controller Scene](./assets/View_Controller_Scene.png "View Controller Scene")
2. Tap on the `+` Button in the right top corner, in order to reveal the `Object Library`  
  1. Search for `View/UIView` and drag it beneath the View.    
  ![View](./assets/ObjectLibrary-View.png)  
  2. You should currently have a view inside your previous view.  
  ![Adding a view](./assets/Adding_a_view.png "Adding a view")

### Setting our view constraints

**Before we continue, follow the steps below. These steps will help us differentiate the view we've just created from its parent view:**
* Go to the view attributes, and set its color to `System Teal Color`.  
![Current Weather View Teal Color](./assets/CurrentWeatherView_TealColor.png)
* Change the view name to a more meaningful name, such as `Current Weather View`.
![Current Weather View Rename](./assets/CurrentWeatherView_rename.png)
* Build and Run the application and verify your changes.

Negative
: **Notice**: there's a red arrow indicating a problem with your view since it has no set of rules,  
![Missing Constraints](./assets/Missing_Constraints.png "Missing Constraints")  
In other words we need to `Add constraints` so `Autolayout` will figure out where to position the Current weather view.

In order for our view to be adaptive, we need to set some rules so it will fit several devices:
* Click on Add New Constraints Button  
![Add New Constraints](./assets/add_new_constraints.png "Add New Constraints")
* Pin the view to the top, leading and trailing edges.
* Add a height of 300.
* Click on Add 4 New Constraints  
![Add 4 Constraints](./assets/add_4_constraints.png "Add 4 Constraints")
* Verify the "Missing Constraints" error is gone
* Build and run your app.

## Adding Current Weather - General Info UI Elements

We'll add the items as in the image below.  
![CurrentWeather-GeneralInfo](./assets/CurrentWeather-GeneralInfo.png)

Follow these steps in order to add the items:
* Step 1: In Object Library (`+` Button) Search For an Image:
![CurrentWeather-Image](./assets/Choosing_a_label.png)
* Step 2: Drag the label under the blue view we've previously created.
* Step 3: Copy and paste The label twice, so you'll end up with 3 labels.
* Step 4: By clicking on the labels give them more meaningful names:
  * `Current Date` for the top label
  * `Current Temp` for the middle Label
  * `Current Location` for the bottom Label
* Step 5: Your Interface builder should look like that  
![CurrentWeather-GeneralInfoItems](./assets/CurrentWeather-GeneralInfoItems.png)

## Creating Current Weather - General Info Stackview

As specified in [Weather App - UI Overview](#weather-app-ui-overview), the `Current Weather` UI view will be consisted of two views.  
Those views are marked in the image below in <font color="red">red</font>, and <font color="green">green</font>.
The red view refers to the `General Info View`, while the green view refers to the `Weather Description View`.

![Current Weather View](./assets/CurrentWeatherView.png "Current Weather View")

Using Stackviews will ease our development process, simplify our constraints logic and will be easier for maintenance if we'll want to make changes in our UI in the future.
Using Stackviews comes naturally as one view, can be "treated" as an array of 3 vertical elements, while the other has 2 vertical elements.

Negative
: As Stackviews are really confusing in the beginning, play with the different options  
other than those suggested in the paragraph below, In order to notice the difference.

#### The Current Weather General Info Stack View Properties
* **Axis** - As Our elements are stacked vertically, we'll choose `Vertical`.
* **Alignment** - We'd like our elements to fill the container, we'll choose `Fill`.
* **Distribution** - We'd like our elements to be distributed proportionally by their label size, hence we'll choose `Fill Proportionally`.
* **Spacing** - Is redundant here since **Distribution** defines the way the items will be spaced.

![Info Stack View](./assets/Info_Stack_View_Attributes.png)

## Adding Current Weather - Description UI Elements

We'll add the items as in the image below.  
![CurrentWeather-Description](./assets/CurrentWeather_DescriptionView.png)

Follow these steps in order to add the items:
* Step 1: In Object Library (`+` Button) Search For an Image:
![CurrentWeather-Image](./assets/Choosing_an_image.png)
* Step 2: Drag the image under the blue view we've previously created.
* Step 3: In Object Library (`+` Button) Search For a Label:
![CurrentWeather-Label](./assets/Choosing_a_label.png)
* Step 4: Drag the label under the blue view we've previously created.
* Step 5: By clicking on the items give them more meaningful names:
  * `Description Image` for the Image
  * `Description Label` for the middle Label
* Step 6: Your Interface builder should look like that  
![Description Interface Builder](./assets/Description_Interface_Builder.png)

## Creating Current Weather - Description Stackview

#### Current Weather Description Stackview properties
* **Axis** - As our elements are stacked vertically, we'll choose `Vertical`.
* **Alignment** - We'd like our elements to be in the Center of the container, we'll choose `Center`.
* **Distribution** - We'd like our elements to be vertically stretched in the container, hence, we'll choose `Fill`.
* **Spacing** - Is redundant here since **Distribution** defines the way the items will be spaced.

![Image Stack View](./assets/Image_Stack_View_Attributes.png)

## Setting constraints for our Stackviews
Now that we have two Stackviews, we need to constraint them to the view, and each other.

#### Adding constraints to the `Info Stackview`:
* Step 1: Click on the Info Stack View, then on `Add New Constraints`
  * Pin the stack view 20 pts to the top of the view
  * Pin the stack view 20 pts to the bottom of the view
  * Pin the stack view 20 pts to the leading edge of the view
* Step 2: We still need a constrain to the trailing edge,
  * We'll solve that by adding constraints to the Description stack view.

#### Adding constraints to the `Description Stack View`:
* Step 1: Click on the Description Stack View then on `Add New Constraints`
  * Pin the stack view 100 pts to the top of the view
  * Pin the stack view 20 pts to the bottom of the view
  * Pin the stack view 20 pts to the trailing of the view
* Step 2: Add a constrain related to the Info stack view:
  * The constrain should reflect that the leading Image Stack View will be 20 pts from the trailing edge of the Info Stackview.

Your constraints should look as following:  
![Stack View Constraints](./assets/StackViews_Constraints.png)

## Adding Assets to our Project
As part of our data model, we'll parse the weather description, and map it to a local asset.  
In order to do so, go ahead and
<a href="https://github.com/zivz/weatherapp_codelab/raw/master/resources/UI_Assets.zip" download>Download Image Assets</a>

Once a weather description will be parsed, it will be associated to a local image in our assets and then will be displayed to our user.

In order to import the resources to our project, simply go to `Assets.xcassets` folder and drag the images after being extracted from the attached zip.

## MVC Design Pattern
Apple's recommended architectural pattern, Model-View-Controller or MVC for short.  
MVC is a software development pattern made up of three main objects:
* The **Model** is where your data resides. in our case the model will be things like:
  * The networking code.
  * Managers like our location manager.
  * Model Objects, such as our CurrentWeather object.

* The **View** Layer is the face of our app. Its classes are reusable as they don't contain any domain-specific logic. For example, a `UILabel` is a view that represents a text on the screen, and it's reusable.
In our case, our view will be coupled with our controller.

* The **Controller** mediates between the view and the model.
In our case, we'll not have any user-interaction, but instead request for data from our API, use our model, and update the view, using our controller.

![MVC Diagram](./assets/MVC-Diagram.png)

Resources:
* [raywanderlich.com](https://www.raywenderlich.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach)
* [learnappmaking.com](https://learnappmaking.com/model-view-controller-mvc-swift/)  

## Preparing our Network Manager - Part 1
Before we begin go to our project navigator, and create a new group, named `Managers`.
In order to so, right click on Weather App Folder and Choose `Create New Group`
A group in Xcode was used to be a "FAKE" folder, but now a days a group is actually a folder.
A group without folder is used in order to organize files in your project without affecting the structure on the actual file system.  

You can read more about groups and folder in [stackoverflow.com](https://stackoverflow.com/questions/34207664/difference-between-folder-and-group-in-xcode)

Follow these steps in order to create our Network Manager file:
1. Right click our new group, named `Network Manager`
2. Choose `New File...`
3. Choose `Swift`
4. Name it `NetworkManager.swift`

#### Open Weather API
In order to fetch data from the network, we'll be using open weather api.
Feel free to self explore the API, but for now we'll use the `Current Weather API` only.  

In order to get the current weather, there are several options:
* Get the weather by city name
* Get the weather by city id
* Get the weather by geographic coordinates. **This is the request we'll be using**
* Get the weather by zip code

#### Getting weather by geographic coordinates
As specified in [Current Weather API](https://openweathermap.org/current)  
We'll need to pass the network call the latitude and longitude coordinates, as well as an api key.
In order to create an api key, you'll be required to [Subscribe](https://openweathermap.org/appid) to Open weather API.

The API call will look as so:  
`api.openweathermap.org/data/2.5/weather?lat={lat}&lon={lon}&appid={your api key}`

#### Creating a structure for our End Point
In `NetworkManager.swift` We'll insert a structure for our end point.
The structure is using URL Components, will save us typos, bugs and will be easier to use, later in our API Calls.
The structure is based on [Constructing URLs in Swift article](https://www.swiftbysundell.com/articles/constructing-urls-in-swift)

go ahead and copy these lines to our `NetworkManager.swift`  
```swift
private struct EndPoints {
    private struct Path {
        static let weather = "/data/2.5/weather"
    }

    private static let base_url = "api.openweathermap.org"

    private struct QueryParams {
        static let latitude = "lat"
        static let longitude = "lon"
        static let app_id = "appid"
        static let mode = "mode"
        static let units = "units"
    }

    private struct QueryValues {
        static let api_key = "insert your apikey"
        static let units = "metric"
        static let latitude = Location.shared.latitude!
        static let longitude = Location.shared.longitude!
    }

    static var currentWeatherURL: URL? {
        var components = URLComponents()
        components.scheme = "https"
        components.host = EndPoints.base_url
        components.path = Path.weather
        components.queryItems = [
            URLQueryItem(name: QueryParams.latitude, value: String(Location.shared.latitude!)),
            URLQueryItem(name: QueryParams.longitude, value: String(Location.shared.longitude!)),
            URLQueryItem(name: QueryParams.app_id, value: QueryValues.api_key),
            URLQueryItem(name: QueryParams.units, value: QueryValues.units)
        ]

        return components.url
    }
```

## Preparing our Network Manager - Part 2
Will now create our Network Manager, the Network Manager is a singleton.

#### Create our singleton
Copy these lines of code, under our EndPoints structure.
```swift
class NetworkManager {
  static let shared = NetworkManager()
  private init() {}
}
```

By using private init() our NetworkManager cannot be instantiated more than once, hence, it's a singleton.

#### Creating our currentWeather Network Call
Our network call will not get any outside parameters, but rather be using our location coordinates, which will be accessed through a singleton as well.
We'll use the enumeration to capture information about whether an asynchronous call succeeds or fails, and use the associated values for the `Result.success(_:)` and `Result.failure(_:)` cases to carry information about the result of the call.
To read more about using result, I've found [this article](https://www.hackingwithswift.com/articles/161/how-to-use-result-in-swift) very helpful.

Go ahead and declare our function under `private init() {}` declaration.
```Swift
func getCurrentWeather(completionHandler: @escaping (Result<CurrentWeather, WeatherError>) -> Void ) {

}
```

Notice that we're using our CurrentWeather, and WeatherError as the success and failure cases.
We'll create the `Current Weather` model and `WeatherError` very soon.

#### Creating our data task
Our data task, which will handle the api call will be consisted from constructing the url, firing the request and handling the response.

Let's create the url

in our function, copy and paste these lines of code:
```Swift
guard let url = EndPoints.currentWeatherURL else {
    completionHandler(.failure(.invalidURL))
    return
}
```

This part was easy, since we were using our EndPoints structure.
We also had to handle an error, since the url is optional and we don't want to continue if the url is `nil`.
In that case we'll return a failure case, the failure case is expecting an error, so we provided our WeatherError enum with invalidUrl.

Let's fire our task, will be using URLSession.  
URLSession provides and API for downloading data from and uploading data to endpoints indicated by URLs.
You can read more about URLSession [here](https://developer.apple.com/documentation/foundation/urlsession), [here](https://www.raywenderlich.com/3244963-urlsession-tutorial-getting-started) and [here](https://learnappmaking.com/urlsession-swift-networking-how-to/)

under our guard statement, copy and paste this line of code

```Swift
let task = URLSession.shared.dataTask(with: url) { data, response, error in

}
```

We now see that our dataTask, using the url we've created, the completionHandler of the task either returns us data, response and error.

#### Handling the error  
error means there was a transport error, either by sending the request, or receiving the response.

to handle the error copy and paste these lines of code:
```Swift
if let _ = error {
    completionHandler(.failure(.unableToComplete))
    return
}
```

#### Handling the response
We're expecting for response code of 200, so any other response code will indicate us an error.
to handle responses other than 200, copy and paste these lines of code:
```Swift
guard let response = response as? HTTPURLResponse, response.statusCode == 200 else {
    completionHandler(.failure(.unableToComplete))
    return
}
```

####Handling our data
We're expecting for data, so we'll again handle the case we don't get any data.
to handle corrupted data, copy and paste these lines of code:
```Swift
guard let data = data else {
    completionHandler(.failure(.invalidData))
    return
}
```
####Decoding our data
We'll be using JSONDecoder, since our data will be serialized to JSON,
Then we'd like to parse our JSON into an object, which will be our DecodedWeather structure.
We'll then map for our own convenience DecodedWeather to CurrentWeather which will contain the data in the structure we want.

go ahead and copy these lines of code under data closing braces:
```Swift
do {
    let decoder = JSONDecoder()
    let decodedWeather = try decoder.decode(DecodedWeather.self, from: data)
    let currentWeather = CurrentWeather(weather: decodedWeather)
    completionHandler(.success(currentWeather))
} catch {
    completionHandler(.failure(.invalidData))
}
```

####Firing the request
After the closing braces of our task, insert `task.resume()`
This line of code will fire our request.

## Preparing our Data model
After fetching our data, using the getCurrentWeather request, we'll be using JSON decoder and get our object in hand.
We'll use decodable for parsing our data.
Then map our structure to another structure, for our own convenience.

#### Creating a group for our data model
In order to so, right click on Weather App Folder and Choose `Create New Group`
Name the group `Model`

Follow these steps in order to create our Network Manager file:
1. Right click our new group, named `Model`
2. Choose `New file...`
3. Choose `Swift`
4. Name it `CurrentWeather.swift`

By examining our response, we need to decode the following pieces:
* From the first hierarchy we'll need:
  * "name" for the Location label
* From weather structure, we'll need:
  * "main" for weather description and image.
* From main structure, we'll need:
  * "temp" for weather description.

The current date label will not be taken from the network response.

```
{
    "coord": {
        "lon": 34.91,
        "lat": 31.99
    },
    "weather": [
        {
            "id": 802,
            "main": "Clouds",
            "description": "scattered clouds",
            "icon": "03d"
        }
    ],
    "base": "stations",
    "main": {
        "temp": 20.12,
        "feels_like": 16.12,
        "temp_min": 17.78,
        "temp_max": 21.67,
        "pressure": 1019,
        "humidity": 46
    },
    "visibility": 10000,
    "wind": {
        "speed": 5.1,
        "deg": 290
    },
    "clouds": {
        "all": 43
    },
    "dt": 1582806769,
    "sys": {
        "type": 1,
        "id": 6845,
        "country": "IL",
        "sunrise": 1582776663,
        "sunset": 1582817744
    },
    "timezone": 7200,
    "id": 294421,
    "name": "Lod",
    "cod": 200
}
```

#### Decoding the Current Weather
In `CurrentWeather.swift`, copy and paste.
```Swift
// MARK: - CurrentWeather
struct DecodedWeather: Decodable {

    let weather: [Weather]
    let main: Main
    let cityName: String

    enum CodingKeys: String, CodingKey {
        case weather, main
        case cityName = "name"
    }
}

// MARK: - Main
struct Main: Decodable {
    let temp: Double
}

// MARK: - Weather
struct Weather: Decodable {
    let type: String

    enum CodingKeys: String, CodingKey {
        case type = "main"
    }
}
```

#### Mapping DecodedWeather to CurrentWeather  
Let's go ahead and create  `CurrentWeather` structure, that will be used for mapping the decoded response for our convenience.
```Swift
struct CurrentWeather: Codable {

    let currentTemp: Int
    let weatherType: String
    let cityName: String

    init(weather: DecodedWeather) {
        self.currentTemp = Int(weather.main.temp.rounded(.toNearestOrEven))
        self.weatherType = weather.weather.first?.type ?? ""
        self.cityName = weather.cityName
    }
}
```

## Creating Location Model
In order to save the location, retrieved by `Core Location` and upon `When in use authorization` permission  
we'll create another file for saving the `Location` Model.

Follow these steps in order to create our Location file:
1. Right click our new group, named `Utilities`
2. Choose New file..
3. Choose `Swift`
4. Name it `Location.swift`

Add the following code, so we'll have Location as singleton, we'll also need to save only two attributes, which are the `latitude` and `longitude`.

```Swift
class Location {
    static var shared = Location()

    private init() {}

    var latitude: Double!
    var longitude: Double!
}
```

## Creating WeatherError
In order to handle the various cases of network errors, we'll create a new group, named `Utilities`.

Follow these steps in order to create our WeatherError file:
1. Right click our new group, named `Utilities`
2. Choose New file..
3. Choose `Swift`
4. Name it `WeatherError.swift`   

create the following cases by copy and pasting these lines of code:
```Swift
enum WeatherError: String, Error {
    case invalidResponse = "Invalid response from the server"
    case invalidURL = "Invalid url"
    case unableToComplete = "Unable to complete your request. Please check your internet connection"
    case invalidData = "The data received from the server was corrupted. Please try again"
}
```

## Date Formatting
`Swift` Foundation provides us to get the current date.
This is required in order to display the current date label, but the format we'll be using doesn't match our needs.

We'll create an extension for `Date` and use it to display the date in the format we want.

Create a new group, named `Extensions`
Follow these steps in order to create our Date+Ext file:
1. Right click our new group, named `Extensions`
2. Choose New file..
3. Choose `Swift`
4. Name it `Date+Ext.swift`   

Using [this web site](https://nsdateformatter.com), eases our life dealing with formatting.
Since we want our Date to Include Month, day and year we'll play with the format in the above link and copy the format.  
![Date Format](./assets/DateFormat.png)

in our file, insert the following code:
```Swift
func currentDate() -> String {
    let dateFormatter = DateFormatter()
    dateFormatter.dateFormat = "MMMM dd, yyyy"
    let currentDate = dateFormatter.string(from: Date())
    return "Today, \(currentDate)"
}
```

Alternatively we can use this code, I've found while searching in [stackoverflow](https://stackoverflow.com/questions/24100855/set-a-datestyle-in-swift)
```Swift
func currentDate() -> String {
    let dateFormatter = DateFormatter()
    dateFormatter.dateStyle = .long
    dateFormatter.timeStyle = .none
    let currentDate = dateFormatter.string(from: Date())
    return "Today, \(currentDate)"
}
```

## Connecting the UI To Our View controller

In order to control our UI elements and handle the logic related to them, we need to connect our UI to a View Controller.
Currently our `Main.storyboard` has a scene, named `View Controller Scene`, and by viewing its Identity Inspector we see its class is `ViewController.swift`.

Positive
: **Reminder:** Having Main.storyboard and a ViewController associated to it, came out of the box, since we created a `Single View` Template while we created the project.

Negative:
: `ViewController.swift` class has no code related to our logic, and even before we start writing any code in it, its name doesn't reflect its responsibility.  So before we start connecting our UI Elements to the ViewController we'll first rename it.

#### Renaming our View controller
In order to rename our view controller follows these steps:
1. In Project Navigator click on `ViewController.swift`
2. Click again, and rename to `WeatherVC.swift`
3. Open the file and change the class name:
  * In the description heather
  * In the class declaration
4. **Our Storyboard doesn't know who's WeatherVC**, Open `Main.storyboard`
  * Click on the View Controller Scene
  * In utilities pane click on `identity inspector`  
  ![Identity Inspector](./assets/Identity_Inspector.png)
  * Change the class in custom class to `WeatherVC`

## Connecting outlets from interface builder

#### Showing our View Controller Scene aside of our View Controller

In order that `WeatherVC` will handle the logic for our UI Elements we need to connect them to our class.  
Before we start doing that we'll prepare Xcode and change the layout so we can view the elements and the code side by side.

In order to view `WeatherVC` side by side with our storyboard, follow these steps:
* Open `Main.storyboard`
* In editor view - click on `Adjust Editor Options` button.  
![Adjust Editor Options](./assets/Adjust_Editor_Options.png)
* Choose `Assistant`
* Our `Main.storyboard` should open the View Controller associated with the scene that is currently in focus.
Since We have only one scene, and only one View Controller, it will open WeatherVC.Swift on the side.

#### Creating outlets for our UI Elements
Connecting our UI Elements in `WeatherVC Scene` to our `WeatherVC` class, requires an Interface Builder outlet.
Creating an outlet is simple as dragging our element to the code.

In order to create an outlet follow these steps:
* Open document outline and select the UI element, let's start with our `Date Label`.
* Drag the element when holding the `^`/`Ctrl` button to `WeatherVC.swift`
* When the dialog opens, choose connection as `Outlet`
* Give the outlet a meaningful name, such as `dateLabel`
* Verify the type is as expected UILabel for label, or UIImageView for Image view.
* Verify the reference is weak.  
![Outlet](./assets/CreatingOutlet.gif)
* **Repeat The steps above for all our elements** :
  * `Current Temp Label`
  * `Location Label`
  * `Current Weather Image`
  * `Current Weather Type Label`

#### Verify your connections
By using the `utilities`/`inspectors` pane, we can use the connections inspector to verify everything is in place:
* Choose our View Controller Scene, e.g, `WeatherVC Scene`   
* Reveal the Utilities pane by clicking on the right button.  
![UtilitiesPane](./assets/UtilitiesPane.png)
* Click on the right most button, which the connections inspector.
* You should see all our connections, I've marked those you should be familiar with in the rectangular area.
![ConnectionsInspector](./assets/ConnectionsInspector.png)
* verify that all your connections appears with a filled circle.  

## Location Manager

#### Location Permission
In order to fetch the user's location we'll first need the user's permission.

From [medium.com](https://medium.com/rakutenready/requesting-location-permissions-in-ios-9e5a3b814a8b)
iOS apps can support one of two levels of location access:
* **While using the app**  
  The app can access the device’s location when the app is in use. This is also known as “when-in-use authorization.”
* **Always**  
  The app can access the device’s location either when app is in use or in the background.

Since we don't need to Always use the user's location, we'll request the user to allow location `While using the app`.
`While using the app`, is also referred in Apple's Terminology as `when-in-use`.

#### Telling the user we need its permission
In order to tell the user we need its permission to access the location `when-in-use`, we need to display the user an alert.
As seen in the image below, the only thing we need to take care of is the `Message` body.
![LocationRequestAlert](./assets/LocationRequestAlert.png)  
The Title and Buttons are already taken care of by iOS.

Now, just another question is left an-unanswered. How do we edit the usage description?
* Open `info.plist`
* Add a new key named `Privacy - Location When In Use Usage Description`
* Add a value that will represent the message we want to show the user.  
"We need your location to give you relevant, up-to-date weather information."

#### Location Manager Delegate
Now, that we have the user's permission, how can we tell our `WeatherVC` that our location was authorized?
How can we tell our ViewController that our location has been updated and ready to be used?
That's where delegation comes in to place.

Delegation is a design pattern in swift, that you can further read in the resources below,  
In our case, we'll use the `Location Manager Delegate` in order to get updates related to the location.
By conforming to the delegate we'll be able to do actions related to the updates we want to get.

Resources:
[Delegation in swift](https://learnappmaking.com/delegation-swift-how-to/)
[Swift Delegate Protocol Pattern Tutorial - Sean Allen](https://www.youtube.com/watch?v=DBWu6TnhLeY)

#### Using extensions for cleaner code
Our `WeatherVC` will have to conform to `CLLocationManagerDelegate` protocol.
We can write an extension for our `WeatherVC`, using that approach will ease our code readability by knowing that the extension is responsible for location purposes only.

After the the closing braces of `WeatherVC` add the following line of code:
```Swift
extension WeatherVC: CLLocationManagerDelegate {

}
```

Resources:
[CLLocationManagerDelegate](https://www.google.com/search?client=safari&rls=en&q=CLLocationManagerDelegate&ie=UTF-8&oe=UTF-8)


### What information does "Location Manager Delegate" hold?
Let's ask ourselves what do we need to know?
* We basically need to update our `CurrentLocation` with you guessed, the Current Location.
* We also need to handle errors such as:
  * What happens if we asked for the users location but didn't get its permission?
  * What happens if we do have permission to access the location but its location services are disabled?
  * What happens if for some reason the location services are enabled, but there's no location?

#### Handling Authorization
CLocationManagerDelegate has a function named `func locationManager(_ manager: CLLocationManager, didChangeAuthorization status: CLAuthorizationStatus)`.
Go ahead and add the following lines of code to our extension:
```Swift
func locationManager(_ manager: CLLocationManager, didChangeAuthorization status: CLAuthorizationStatus) {
  if status == .authorizedWhenInUse {
      locationManager.startUpdatingLocation()
    } else {
      locationManager.requestWhenInUseAuthorization()
    }
}
```

Reading the function above makes lots of sense, but how does it work?
By conforming to the location manager delegate and using the function above, we get an update if the authorization has changed.
Now comes the `WeatherVC` part where by filling the function body we do what we want if this update occurs.
We want to start updating the location if the user's location is authorized.
In Any other case we want to nudge the user and ask for its permission so we can continue working.

Negative
: What happens if We do get authorization, but location services are disabled?
iOS already handled the work for us, no worries.

#### Updating the location upon authorization
In order to update our `Location` model with the location we need to use the delegates function related to updatingLocation.
This is where `func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation])` comes to help.

Go ahead and add the following lines of code to our extension:
```Swift
func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
    guard let currentLocation: CLLocationCoordinate2D = locationManager.location?.coordinate else {
        return }
    Location.shared.latitude = currentLocation.latitude
    Location.shared.longitude = currentLocation.longitude
    fetchData()
}
```

Negative
: `fetchData()` is a function in our WeatherVC we'll handle later. no worries.

#### Dealing with Errors
Checking our errors handling in the beginning, we already took care of:
* No authorization, in that case we ask again for the user's permission.
* Authorized but Location Services are disabled, iOS is taking care of that.

We just need to take care of a case I was able to simulate in the simulator.
What happens if Location When-In-Use is authorized, Location services are enabled, but location is none.

Go ahead and add the following lines of code to our extension:
```Swift
func locationManager(_ manager: CLLocationManager, didFailWithError error: Error) {
    self.showAlertOnMain(title: "Check your location", message: "Your location seems to be none")
}
```

Negative
: `showAlertOnMain` is an extension we'll later add for our ViewController in order to handle alerts

#### Adding the missing parts in WeatherVC
We just miss some parts so we can tell the CLLocationManagerDelegate that we'll do the work for me.
Remember, the delegate knows the information, and we do the rest of the work for him.

Follow these steps in order to fully conform to `CLLocationManagerDelegate`:
* After `import UIKit`, add `import CoreLocation`
* After declaring all our outlets, add this line of code:
  ```Swift
  let locationManager = CLLocationManager()
  ```
* In `viewDidLoad()`, and after `super.viewDidLoad()` add these lines of code:
```Swift
locationManager.delegate = self
locationManager.desiredAccuracy = kCLLocationAccuracyBest
locationManager.requestWhenInUseAuthorization()
```

What did we do above?
* `locationManager` is an instance of `CLLocationManager()`
* We told `locationManager` that `WeatherVC` is its delegate and waiting for orders.
* We told `locationManager` that accuracy of location we want to have.
* We told `locationManager` to request for the location permission after the view has loaded.
  This is the first thing the user will see when launching the app.


## Using Location in Our Network Request
Now that we have our latitude and longitude coordinates, we're finally ready to retrieve the weather in the given location.
We can now add to `WeatherVC` our `fetchData` function.
We use fetchData and not `getCurrentWeather` since our app is open for extensions, and we might want to do more than just getting the current weather upon location retrieval.

Before getting the current weather, let's declare a variable that will hold our current weather information.
Add this line of code, after declaring the `locationManager`.
```Swift
var currentWeather: CurrentWeather!
```

After `func viewDidLoad`, add:
```Swift
private func fetchData() {
    getCurrentWeather()
}
```

Now let's write the code for `getCurrentWeather`, add the following lines of code after `fetchData()`:
```Swift
private func getCurrentWeather() {
    NetworkManager.shared.getCurrentWeather { [weak self] result in
        guard let self = self else { return }

        switch result {
            case .success(let currentWeather):
              self.currentWeather = currentWeather
              DispatchQueue.main.async {
                  self.updateMainUI()
              }
            case .failure(let error):
              self.showAlertOnMain(title: "Something went wrong", message: error.rawValue)
            }
        }
}
```

Let's explain we wrote above:
* We first called our NetworkManager to get the current weather
* We're guarding self as precaution of memory leaks
* Upon getting the result, we're expecting `.success` or `.failure`
  * In case of `success` we'll call a function that will update our currentWeather instance.
    * We'll then do the UI Updates on the main threads, that's why we used `DispatchQueue.main.async`
    * We'll call a function name updateMainUI(), that will update our UI using the currentWeather obj
  * In case of `failure` we'll Show an Alert with a relevant error.

We now have to add our `updateMainUI` function
Add the following lines of code after `getCurrentWeather` function.
```Swift
func updateMainUI() {
    dateLabel.text = Date().currentDate()
    currentTempLabel.text = "\(currentWeather.currentTemp)°"
    currentWeatherTypeLabel.text = currentWeather.weatherType
    locationLabel.text = currentWeather.cityName
    currentWeatherImage.image = UIImage(named: currentWeather.weatherType)
}
```

Let's explain the code above:
* Our date label will use the currentDate we wrote as an extension to `Date`
* All other labels are pretty much declarative, notice that `currentTempLabel` is using a `concatenation` of the `Degree` symbol.
* In `currentWeatherImage.image` we we'll use an image from our `Assets.xcassets`
  The image will be based on the weatherType we get from our network call.

#### Writing an extension for alerts
We already came across some cases where we had present the user alerts.
The first alert we were showing was related to location permission, but that was handled by adding a key-value pair in our `info.plist`
The two other alerts we were showing, were in the case were no location is available and were there was a failure with our Network call.

Instead of writing an alert every time we need one, we can write an extension to UIViewController, since our ViewController is UIViewController, we can use this extension by calling `self`.

Follow these steps in order to add extension for UIViewController:
1. Go to Project Navigator
1. Right click  `Extensions`
2. Choose New file..
3. Choose `Swift`
4. Name it `UIViewController+Ext.swift`

Now, open `UIViewController+Ext`, instead of importing `Foundation`, import `UIKit` since we're going to deal with UI.

Add the following lines of code.
```Swift
extension UIViewController {
    func showAlertOnMain(title: String, message: String, style: UIAlertController.Style = .alert) {
        let alertController = UIAlertController(title: title, message: message, preferredStyle: style)
        alertController.addAction(UIAlertAction(title: "Ok", style: .default, handler: nil))

        DispatchQueue.main.async {
            self.present(alertController, animated: true, completion: nil)
        }
    }
}
```

Let's explain what we just wrote.
* Our function expects a title and message for our alert
* Our alert style defaults to .alert
* We create an instance of alertController with the provided info above.
* Then we add an action, with a button name "Ok".
* Since no handler is needed upon pressing the button, we leave the handler as `nil`.
* Then we use the Main Queue for UI Updates and present the alert.

## Are we there yet?
We just need to think about edge cases and some tweaks.
These tweaks are totally up to you, but you should consider them.

* What happens with the UI Elements before we get any network response.
  * Do we want to change our view's background according to the weather type?
  * Do we want to show some placeholder text before we receive the data from the network?
  * Do we want to hide the elements and show them when we get the response?
  * Do we want to show an activity indicator when our network call begins?
  * Do we want to have a placeholder image in case where unknown weather type is received in the response?

#### Adding table views
You can review the full code in [github.com](https://github.com/zivz/WeatherApp) in order to add the table view and the activity indicator code.

For that you'll need to:
* Add table view in our `WeatherVC` scene.
* Add a custom class representing the forecast cell.
* Add a network call to get the forecast
* Conform to UITableViewDataSource in order to feed the table with data.
* Set `WeatherVC` as the Tableview data source.

Good Luck!

#### Adding more features
In order to complete the app, you can add a table view representing the forecast for the next 10 days.
You can also add more screens that will display the user weather in different locations.
You can persist the data,
You can add a settings button that will change the units to Fahrenheit.
