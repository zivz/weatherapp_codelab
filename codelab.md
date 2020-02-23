author: Ziv Zalzstein
summary: Create iOS App
id: docs
categories: codelab, swift, ios
environments: ios
status: Published
feedback link: https://github.com/zivz/WeatherApp

# Creating your first iOS App

## First iOS App Overview
Duration: 0:01:30

In the following tutorial, we'll learn how to make an iOS app.  

**General**  
The app will show the user the current weather in its current location.  

**UI**  
The UI Will have a single view.  
The primary view will contain two subviews:  
* A view for the current weather
* A table view for the next 10 days forecast.

**API**  
The app will interact with Open Weather API, in order to fetch the current weather, and the forecast.  

**Location**  
The app will fetch the user's location, upon `When in use authorization` permission

**Notes:**
* The tutorial will focus on Storyboards, Autolayout and UIStackView.  
* The tutorial will include the current weather view only  
* Location Handler, Networking, Parsing code will be provided in order to provide the full capabilities of the app.  
* The app is extendable for further implementation of the next 10 days forecast.  
* Tableview displaying the forecast for the next 10 days implementation is still available in github.  
* The full code is available [here](https://github.com/zivz/WeatherApp).  

**Resources:**
* [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/overview/)
* [Autolayout](https://www.youtube.com/watch?v=emojd8GFB0o) and [StackView](https://www.youtube.com/watch?v=eF9Ut-VpdAI)
* [Open Weather API](https://openweathermap.org/api).

## Xcode New Project
Duration: 0:04:00

This tutorial assumes you have basic familiarity with Xcode, as provided in separate session.

**Resources:**
* [Xcode Essentials](https://www.youtube.com/watch?v=jniJeamcIUU)
* [Xcode AppStore](https://apps.apple.com/il/app/xcode/id497799835?mt=12)


#### Create a new Xcode Project

Open Xcode and select "Create a new Xcode Project"  
![Create a new Xcode Project](./assets/Create a new xcode project.png)

#### Choose a template for your new project with following options:
iOS | Single View App  
![Choose a template](./assets/Chosing template.png)

#### Choose options for your new project:
* Product Name - give a meaningful name such as `WeatherApp`
* Organization Name - give your Name or your organization Name
* Organization identifier will be constructed from Organization Name
* Bundle Identifier - will be constructed from your Product Name and Organization Name.
* Language - Swift
* User Interface - Choose Storyboard
* Leave `User Core Data, Include Unit Tests and Include UI Tests` **Unchecked**

![Template Options](./assets/Template options.png)

#### Verify and Edit Project Settings  
Once the project is created, The project file will appear on the screen.
**Under General tab verify the following:**  
* Verify `Display Name, Bundle Identifier` are correct under `identity`
* Check `iPhone` only, under `Deployment info`
* Verify `Portrait` only, under `Device Orientation`
![Project Settings](./assets/Project Settings.png)
