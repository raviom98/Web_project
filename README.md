# CSCI 5709: Tutorial 4 - Group 17

Moviesight is a react-based client application that enables users to find information on their favourite movies and TV shows from around the world. As part of the tutorial's requirements, the application features an auto-suggest component, react-router based routing, and asynchronous REST API requests using AXIOS.

* Date Created: 30 05 2020
* Last Modification Date: 02 06 2020

**Deployed Application**: You can find the application up and running on https://web-tutorial2.herokuapp.com/.

## Authors

If what is being submitted is an individual Lab or Assignment, you may simply include your name and email address. Otherwise list the members of your group.

* [Devarshi Pandya](devarshi.pandya@dal.ca) - (Maintainer)
```
Implemented the Header and App components.
```
* [Daksh Patel](dk792765@dal.ca) - (Maintainer)
```
Implemented the SuggestionsList component.
```
* [Karthik Tamil Mani](kr630601@dal.ca) - (Maintainer)
```
Implemented the Info component.
```
* [Ravi Patel](rv526909@dal.ca) - (Maintainer)
```
Implemented the Results component.
```
* [Mansoor Ghazi](mansoor.ghazi@dal.ca) - (Maintainer)
```
Implemented the Autosuggestion component and routing.
```


## Getting Started

Refer the following sections on how to install, run, and deploy the Moviesight application.

### Prerequisites

To have a local copy of this lab tutorial up and running on your local machine, you will first need to install various npm packages. Key packages are:

* Axios - for REST API requests
* Font Awesome - for icons

See the following section for detailed step-by-step instructions on how to install the dependencies and prepare the app for deployment.

### Installing

Follow the steps listed below to setup the app, and run it on your local machine / computer.

#### Step 1: Clone Repository

Run the following command from the terminal on your machine, to clone the repository:

```
git clone https://github.com/karthikktamilmani/Web_Tutorial.git
```

#### Step 2: Install Dependencies

Navigate into the `react-client` folder and run the following command to install the required dependencies:

```
npm install
```

#### Step 3: Start The Dev Server

To start the app, without any complicated build steps, simply start the development sever through the following command:

```
npm start
```

#### Step 4: The Application

In the last step, open your web browser, and navigate to `localhost:3000` to view a running instance of the application. If everything went fine, you should see the following page:

![Image of App Running](/deployed_app.png)


## Deployment

To deploy the app to Heroku, follow the ist 

## Built With

* [create-react-app](https://github.com/facebook/create-react-app) - React buildpack by facebook
* [npm](https://www.npmjs.com/) - Node Package Manager

## Sources Used

For the Autosuggestion component, some inspiration was taken from the semantics of [Mosh Hamedani's](https://programmingwithmosh.com/react/simple-react-autocomplete-component/) tutorial. However, our Autosuggestion component is drastically different. For example, we have used composition instead of inheritance. Also, the auto-suggestion filter was completely updated to suggest results that started with the user's input, instead of results that contain the user's input as a sub-string. Furthermore, unlike the referenced Auto-suggestion component, 

The Autosuggestion component's `onChange` event handler, with our own implementation, as well as Mosh's implementation is presented below.

### Autosuggestion.js

Lines 26 - 45
---------------

```
onChange = (event) => {
    let suggestions = [];
    const userInput = event.target.value;
    axios.get(this.baseURL + this.searchEndpoint + userInput).then((response) => {
        suggestions = response.data;
    }).then(() => {
        const filteredSuggestions = suggestions.filter((suggestion) => {
            return suggestion.title.substring(0, userInput.length).toLowerCase()=== userInput.toLowerCase();
        });
        console.log(filteredSuggestions);
        this.setState({
            activeSuggestion: 0,
            filteredSuggestions,
            showSuggestions: true,
            userInput
        });
    }).catch((err) => {
        console.log(err);
    });
}
```

The code above was created by adapting the code in [Mosh Hamedani's](https://programmingwithmosh.com/react/simple-react-autocomplete-component/) tutorial as shown below: 

```
onChange = (e) => {
    const { suggestions } = this.props;
    const userInput = e.currentTarget.value;

    const filteredSuggestions = suggestions.filter(
        (suggestion) =>
        suggestion.toLowerCase().indexOf(userInput.toLowerCase()) > -1
    );

    this.setState({
        activeSuggestion: 0,
        filteredSuggestions,
        showSuggestions: true,
        userInput: e.currentTarget.value
    });
};
```

- The code in [Mosh Hamedani's](https://programmingwithmosh.com/react/simple-react-autocomplete-component/) was implemented by Mosh Hamedani.
- [Mosh Hamedani's](https://programmingwithmosh.com/react/simple-react-autocomplete-component/) code was used to understand the semantics of syncrhonus auto-suggestion.
- [Mosh Hamedani's](https://programmingwithmosh.com/react/simple-react-autocomplete-component/) code was modified by Mansoor Ghazi to create an asynchronus auto-suggestion feature.

## Acknowledgments and References

* Thank you for the awesome React documentation at https://reactjs.org/ and react-router tutorial at https://blog.pshrmn.com/simple-react-router-v4-tutorial
* For the UI design inspiration: https://design-system.pluralsight.com/ 
* For the Input validation in Auto-suggestion component we took help from: http://web.stanford.edu/~mendel/cgi-bin/cs142-win16/slides/Input.pdf



