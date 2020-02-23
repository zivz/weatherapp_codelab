author: Ziv Zalzstein
summary: Create iOS App
id: docs
categories: codelab, swift, ios
environments: ios
status: Published
feedback link: https://github.com/zivz/WeatherApp

# Creating first iOS App

## First iOS App Overview
Duration: 0:01:30

In the following tutorial, we'll learn how to make an iOS app.
The app will have a single view UI, introducing the Current Weather in the user's Current Location.
The app will interact with Open Weather API, in order to fetch the current weather.

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
*Put here an image caption*

#### Choose a template for your new project with following options:
* iOS | Single View App

#### Choose options for your new project:
* Product Name - give a meaningful name such as `WeatherApp`
* Organization Name - give your Name or your organization Name
* Organization identifier will be constructed from Organization Name
* Bundle Identifier - will be constructed from your Product Name and Organization Name.
* Language - Swift
* User Interface - Choose Storyboard
* Leave `User Core Data, Include Unit Tests and Include UI Tests` *Unchecked*

#### Setup Go Environment Variables
Below is what I set on mac, but instructions are [here](https://golang.org/doc/install) for other OS options

``` bash
$ export GOPATH=$HOME/Go
$ export GOROOT=/usr/local/opt/go/libexec
$ export PATH=$PATH:$GOPATH/bin
$ export PATH=$PATH:$GOROOT/bin
```

#### Install claat
Install claat
``` bash
$ go get -u -v -x github.com/googlecodelabs/tools/claat
```

You should now have the *claat* command available to you.
``` bash
$ claat
```

## Create your initial CodeLab
Duration: 0:05:00

Now that we have the environment setup let's go ahead and create a markdown file where we'll create the actual codelab.

Negative
: If you're using Windows make sure to set your text editor to use UNIX line endings!

####
``` bash
$ vim codelab.md
```

#### Fill-in the header metadata
Copy and paste the headers below into your markdown file and change the values appropriately.
Guidelines are available below the sample headers.

``` bash
author: Author Name
summary: Summary of your codelab that is human readable
id: unique-codelab-identifier
categories: codelab,markdown
environments: Web
status: Published
feedback link: A link where users can go to provide feedback (Maybe the git repo)
analytics account: Google Analytics ID
```

Metadata consists of key-value pairs of the form "key: value". Keys cannot
contain colons, and separate metadata fields must be separated by blank lines.
At present, values must all be on one line. All metadata must come before the
title. Any arbitrary keys and values may be used; however, only the following
will be understood by the renderer:

* Summary: A human-readable summary of the codelab. Defaults to blank.
* Id: An identifier composed of lowercase letters ideally describing the
  content of the codelab. This field should be unique among
  codelabs.
* Categories: A comma-separated list of the topics the codelab covers.
* Environments: A list of environments the codelab should be discoverable in.
  Codelabs marked "Web" will be visible at the codelabs index. Codelabs marked
  "Kiosk" will only be available at codelabs kiosks, which have special
  equipment attached.
* Status: The publication status of the codelab. Valid values are:
  - Draft: Codelab is not finished.
  - Published: Codelab is finished and visible.
  - Deprecated: Codelab is considered stale and should not be widely advertised.
  - Hidden: Codelab is not shown in index.
* Feedback Link: A link to send users to if they wish to leave feedback on the
  codelab.
* Analytics Account: A Google Analytics ID to include with all codelab pages.

#### Add the Title
Next add your title using a single '#' character
```
# Title of codelab
```

#### Add Sections and Durations
Then for each section use Header 2 or '##' and specify an optional duration beneath for time remaining calculations
Optional section times will be used to automatically total and remaining tutorial times
In markdown I've found that the time is formatted hh:mm:ss

Example
``` bash
## Section 1
Duration: 0:10:00

## Section 2
Duration: 0:05:00
```

#### Add Section Content
Now that we have 2 sections to our titled codelab let's go ahead and add some content to each section.
Make up your own or copy and paste the example below:

Copy into section 1 (Below Duration and above Section 2):
```
### Info Boxes
Plain Text followed by green and yellow info boxes

Negative
: This will appear in a yellow info box.

Positive
: This will appear in a green info box.

You created info boxes!

### Bullets
Plain Text followed by bullets
* Hello
* CodeLab
* World

You created bullets!

### Numbered List
1. List
1. Using
1. Numbers

You created a numbered list!

```

Copy into section 2 (Below Duration):
```
### Add a Link
Adding a link!
[Example of a Link](https://www.google.com)

### Add an Image
Adding an image!
![image_caption](https://googlecloud.tips/img/031/codelabs.png)

### Embed an iframe
![https://codepen.io/tzoght/embed/yRNZaP](https://en.wikipedia.org/wiki/File:Example.jpg "Try Me Publisher")
```

More Markdown Parser examples can be found [here](https://github.com/googlecodelabs/tools/tree/master/claat/parser/md).

## Export and Serve
Duration: 0:02:00

Now that you have an initial codelab defined in your markdown file let's go ahead and generate the static site content.
We can export and serve the content locally using the `claat` command that we installed earlier.

``` bash
$ claat export codelab.md
$ claat serve
```

* Your browser should have opened (if it doesn't then try going to localhost:9090 in your browser).
* Choose the directory that matches your "id" that you put in the headers.
* Viola! You should have your first codelab!

## Host Your CodeLab
Duration: 0:01:00

When you ran the `claat export` command you created the static web content needed to host your codelab.
It placed static web content in a directory specified by your unique "id" and you can view it locally by opening the index.html page.

Negative
: Note that when you view it locally by opening index.html some of the graphics may not show up (such as access_time, Next, Back), but they work once online.


Now that you have the static content you can host it however you want.
One option is pushing it to github and serving it up from Netlify.

If you'd like to create your own landing page for codelabs, [like this one](https://codelabs.developers.google.com), there is a tool to do that as well!
Check it out here: [CodeLabs Site](https://github.com/googlecodelabs/tools/blob/master/site/README.md)
