# FoodLogging

### Acknowledgements
This version of code is based of an existing project with an MIT license
Site: https://www.foodleh.app/
Git Repo: https://github.com/limyifan1/hawkercentral 

### URL as there are multiple variations
original: http://cs4249-ay2020.surge.sh/?iv2=static&iv3=none&iv1=1&task=1
Modified: http://cs4249-ay2020.surge.sh/?iv2=dynamic&iv3=short&iv1=1&task=1

All variations of the website can be found in foodlehURL.xlsx

### Libraries and programs used in Project

- npm to install required libraries
- npm surge for site hosting
- Reactjs
- Bootstrap
- Firebase (for database)

### Folders
- functions: misc functions and test scripts
- public: index files required for a react website
- src
	- assets: images and other assets
	- Components: Main source files
	- Helpers: files for email function and list categories.

### Key Files of intrerst
- src/Components/Home.js
  Home.js creates the home page as well as reads the resets sessionStorage variables and initialise the IVs basd on the URL(HTML GET). It also gets the current date time and saves it as the start time. An event is also sent to logging.js to indicate that this is the start of a new task attempt. 
  
 ```
  //handle onPageLoad
  componentDidMount() {
    window.addEventListener('load', this.handleLoad);
 }

 handleLoad() {
	const queryParams = new URLSearchParams(window.location.search);
	console.log("loaded");
	
	
	//reset each time homepage is loaded
	sessionStorage["timeStart"] =new Date().getTime();
	sessionStorage["clickCount"]=0;
	sessionStorage["errorCount"]=0;
	sessionStorage["task"]=queryParams.get("task");
	sessionStorage["iv1"]=queryParams.get("iv1");
	sessionStorage["iv2"]=queryParams.get("iv2");
	sessionStorage["iv3"]=queryParams.get("iv3");
	sendEvent("HomePageLoad");
 }
 //end handle onPageLoad
  ```
  
- src/Components/Search.js
	Search.js disaplays and manages the search button shown on the home page. When the search button is clicked the user is redirected to SearchAll,SearchAll_iv2,SearchAll_iv3 or SearchAll_modified based on the iv2,iv3. iv3 details will still be added into the URL when redirecting to control the grouping(basket) size; 3 or 6 km.
	
- src/Components/Item.js
	Item.js controls the design of the restaurants item cards. It also handles what happens when a user clicks on an itemcard. Checks are done based on the sessionStorage["task"] to decide if the user has completed the required task.
	
- src/Components/Logging.js
	Contains a function to convert the taskID gotten from the URL to string. It also includes error count function that increments when the user selects a restaurant differenet from what is required by the task. The remaing functions are used to trigger events and send details about the event to googleforms.
	Details of the click count, error count, start time, and endtime(the current time) are sent at each click. This is used in an event users fail to complete the required task, but we will still have an approximate data.

- src/Components/SearchAll.js
	Design of original site
- src/Components/SearchAll_iv2.js
	Design of original site with changes for IV2(fixed search bar)
- src/Components/SearchAll_iv3.js
	Design of original site with changes for IV3(Distance grouping)
- src/Components/SearchAll_modified.js
	The modified version of the UI containing both IV2 and IV3 changes. The changes are indicated with comments indicating sections for IV2 or IV3
	
	IV2: Encompass the search bar with a div and set it the be fixed position with a higher z-index. Additonal margins were add around the code to ensure the design looks similar to the original.
	
	IV3: Read IV3 details from URL. initialise distance variable accordingly. Get screen width divided by width of restaurant item card to decide how many to show initially before the show more button is clicked. 
	Divide the list of restaurants into groups, adding a gradient image overlay and show more button for each group.
	Added a function to handle DOM when the showmore button is clicked.
	
- src/App.css
	General css used throughout the site
- src/App.js
	Controls reactjs pathing


### Setup
- install npm
- open cmd
- cd to directory where the codes are
- run `npm install`
- run `npm start`


