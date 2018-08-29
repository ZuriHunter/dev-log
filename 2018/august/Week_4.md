```
/^                                         /^^
/^ ^^                                       /^^
/^  /^^    /^^  /^^   /^^   /^^  /^^ /^^^^ /^/^ /^
/^^   /^^   /^^  /^^ /^^  /^^/^^  /^^/^^      /^^
/^^^^^^ /^^  /^^  /^^/^^   /^^/^^  /^^  /^^^   /^^
/^^       /^^ /^^  /^^ /^^  /^^/^^  /^^    /^^  /^^
/^^         /^^  /^^/^^     /^^   /^^/^^/^^ /^^   /^^
                   /^^
```
#### 2018-08-20

- Unity is going to discontinue support for MonoDevelop. MonoDevelop is an IDE for C#, F# and many more languages.  They are going to switch to having developers use their preferred IDE or Visual Studio.  I am not too much of fan. But I will have to tailor the tutorial for anyone who wants to make a change to the unity-sdk to whatever they wish.

#### 2018-08-24
- **QT**
  - I don't have Atlas installed on here but I want to look into using QT with Atlas...for fun.
  - It is a cross-platform application framework and widget toolkit for creating classic and embedded graphical user interfaces and application that run on various software and hardware platforms with little or no change in the underlying codebase.  It remains as a native application with native capabilities and speed.
  - Open Source and Commercial are offered.

    | Features   |      Commercial      |  Open Source |
    |----------|:-------------:|:------:|
    | Rights & Obligations|  X |GNU Lesser General Public License v.3  |
    |Essential libraries and APIs |    X   |   X |
    | Full Features | X |    X|
    | All Tools | X |    |
    | Embedded Tooling & Solutions | X |    |
    | QT Support | X |   X|
    | Company Relationship w/ QT | X |   |
  - Features
    - 3D/2D Graphics & Image Processing
    - Data Storage
    - Mobility & Mapping
    - Networking & Connectivity
    - Platform Extras
    - QT Concurrent (Multi-Threading)
    - SCXML State Machine
    - UI technologies
    - Wayland Compositor
    - Web Technologies
  - Tools
    - QT Creator Identifiers
    - Integrated Tooling
    - UI Design Tools
    - SCXML State Chart Editor
    - Qt VS Tools
  - Tooling & Solutions
    - Direct on-device Debugging
    - One-click Deployment
    - Qt Virtual Keyboard
    - Reference software stack
    - Qt sources for DIY embedded software stack
    - Qt Configuration tool
    - Real-time operating system
    - One-click deployment
  - I need Xcode to use QT....I guess thats the same with most languages and frameworks.
- **The Bison Project**
  - The idea is to have three services
    - User Management
    - UI
    - LinkedIn API
- **Splunk**
  - In a nutshell Splunk is basically a tool that allows for us to look at machine data smoothly.
  - Three themes PinPoint <> Correlate <> Alert base off events occuring within the database that records all information.
  - Records structured and unstructured data. Give insights on Security, User Behavior, Hardware and Financial transactions
  - Downloaded Splunk locally and it spun up within the terminal, setup password and then I can log in the GUI.

#### 2018-08-25
- QT installation was long as hell.  To resolve it from not recognizing the latest version of Xcode run this line. `sudo /usr/bin/xcode-select -switch /Applications/Xcode.app/Contents/Developer`
- **Splunk**
  - Index Data
    - Reads data and determine what it is an assign a `source type` to it. The worker then comes in and break the data into `events` with timestamps that are then indexed.
  - Search & Investigate
    - Entering a query you look for the data
  - Add Knowledge
    - Add labels to help give further information on the infor
  - Monitor & Alert
    - Create alerts on certain sourcetypes, labels and events.
  - Report & Analyze
  - Under the hood there is a Indexer, Search Head and Forwarder. Indexer breaks things up into folders base off of time. Search Head providers dashboards.  Forwarder consume data, lives on machine that sends the data to the Splunk Indexer. (Input, Parsing, Indexing, Searching)
  - Three ways to input data: File Upload, Monitory Files and Directories, Forwarders which have Splunk client installed on it.

- **The Bison Project**
- Stop PG `brew services stop postgresql`
- Start PG `brew services start postgresql`
- In the PG shell to list DBs `\list`
- Creating DBs. All done in the regular terminal
```
# Change the user to Postgres
su - thestrugglingblack

# Create DB
createdb DATABASE_NAME
```
- The user that created the DB is the user that puts its name in the section where Postico asks for user...and if you didn't specify a password thats it.
- After changing the database.yml, spinning up the Postgres and Postico instance, had to run `rake db:setup`

#### 2018-08-26
- QT finally finished installing. Only install the latest for Qt and not the others. Lost two days on downloading and installing the software
- `CSS Houdini` gives access to lower level of CSS
- The CSS Paint API allows you to call the `paint()` function instead and pass in a paint worklet that you have defined through JavaScript. It kind of operates like `<canvas>`
- CSS Paint API is only supported on Chrome 65, Opera 52, Android 67 and Android Chrome 67...not many browsers at the end of the day.
- Name the worklet and call it within the CSS
```
# .css
section {
  background-image: paint(awesomeSauce)
}

# .js
CSS.paintWorklet.addModule('patternWorklet.js');

# patternWorklet.js
registerPaint('awesomeSauce', Shape); // call and define first

class Shape {
  paint(ctx, geom, properties) {

    ctx.strokeStyle = 'white';
    ctx.lineWidth = 4;
    ctx.beginPath();
    ctx.arc( 200, 200, 50, 0, 2*Math.PI);
    ctx.stroke();
    ctx.closePath();

  }
}
```
- **Kubernetes Up and Running**
  - `Healthchecks`
    - ensures that the main process of your application is always running. It was introduced to check on application liveliness.
    ```
    apiVersion: v1
    kind: Pod
    metadata:
      name: kuard
    spec:
      containers:
        - image: gcr.io/kuar-demo/kuard-amd64:1
          name: kuard
          livenessProbe:
            httpGet:
              path: /healthy
              port: 8080
            initialDelaySeconds: 5
            timeoutSeconds: 1
            periodSeconds: 10
            failureThreshold: 3
          ports:
            - containerPort: 8080
              name: http
              protocol: TCP
    ```
    - In the example above the probing is being done as a HTTP GET probe, hence to `httpGet`.  The HTTP GET probe hits the endpoint at `/healthy` which lies on the port 8080. So it would unravel as `GET http://localhost:8080/healthy`.
    - The probe wont kick off until 5 seconds since the container opens up base off this property `initialDelaySeconds`.
    -  The probe must respond within 1 second base off of `timeSeconds` property.
    - The response from the probe must be above 200 but less than 400 to be considered a successful response.  
    - `periodSeconds` means that the healthcheck probe will kick offevery 10 seconds to see if the container is still in good standing.  
    - The `failureThreshold` will say if the probe fails more than three times restart the container.
    - **Readiness**
      - `Liveness` determines if an application is running properly.
      - `Readiness` describes when a container is ready to serve user requests.
    - **Types of Checks**
      - `tcpSocket` and `exec` are examples
      - TCP can be for databases probing and exec for running scripts.
      - For scripts if it exits zero then it would be classified as a successful probe.
  - `Resource Management`
    - `Utilization` is defined as the amount of a resource actively being used divided by the amount of resource that has been purchased.
    - Two Metrics
      - 
