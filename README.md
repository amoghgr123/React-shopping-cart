# React-shopping-cart

**Shopping application built with React/Typescript using the concepts of React Test Library, React Memo **

This React project implements a functional shopping cart application, utilizing various Redux Toolkit functionalities. It introduces React Memoization for handling asynchronous operations, enabling smooth data fetching from an API by mocing the Product Data. The main app features encompass essential functionalities such as displaying the products upon launching the application, adding products to the the cart, removing items from the cart, adjusting item quantities during add/remove items to/from the cart, calculating the total price of the products in the cart and search feature which demonstrates the search of phone related products from the store. With the power of Redux Toolkit, this application provides a seamless and efficient user experience for managing the cart's state and interactions.

**# Tech Stack**

Typecript: The extension of the foundational programming language for creating responsive and interactive features which is Javascript

React / Vite – for the UI library we're going again with a React and Vite development environment

Redux Toolkit: The core library for state management, offering features like Redux Memo  for handling asynchronous actions, and Reselect for simplifying reducer functions.

React Redux: The library that connects React components with the Redux store for managing application state.

React Icons: The popular library that offers a diverse collection of icons to enhance the user interface and improve user experience in the project.

SASS / CSS Modules – for styling our app, we'll bet on the battle-tested solution of CSS Modules with SASS/SCSS

react-testing-library / Vitest – for testing the app, we'll use react-testing-library and Vitest.


# Installation:

I assume we are starting from scratch. We are going to use Vite for scaffolding the project. I suggest that you update it to the latest stable version. And as a package manager you may go with either npm or yarn.

Once you have one of these installed on your system, open your Terminal app and run the following:

yarn create vite shopping-cart-app --template react-ts


This command will install the initial application files in a folder named 'your-app-name'. After that step you will be able to open it in your favorite IDE and start working on it.

One last thing you should do here is to install to additional packages I mentioned in the previous section. You can do that by running the following:

yarn add -D sass @testing-library/react use-local-storage-state


# Project Structure:

The root level of the app contains files related to configurations and setup, as well as the HTML index file. This is where the main JavaScript module is loaded and the app is launched.

**index.html:**

The src folder (short for "source") contains two sub-folders: one for assets and one for components.

The public and screenshots folders have straightforward purposes. The .github folder contains the YAML configuration file that is used by GitHub Actions.

**Components:**

App Components:

All components are organized into separate folders. Within each folder, you'll find an index.ts file that exports the component. This file uses named exports for each of the components.

# Named export - Header component:

We'll start by examining the components from a top-to-bottom approach, as they are seen and used within the application. To help clarify, let me provide a visualization.

Kindly find the details of the components as below

Header – holds the top part of the app. On the left side is the logo image, an SVG I have downloaded from Iconify. On the right side sits the CartWidget component.

CartWidget – renders a button composed of an SVG image depicting a shopping cart and a number value indicating the count of products currently added to the cart. When clicked, the button takes the user to the cart page.

Products – this component is responsible for rendering the main content of the page, which consists of a list of products. On larger viewports, the products are displayed in three columns per row. Each product is represented by a thumbnail image, a title, price information, and an "Add to Cart" button. The price of each product is formatted to GBP using the CurrencyFormatter component.

CurrencyFormatter – This formats given numeric amount to INR – that is, 499 would become 499.00.

Cart – this component is responsible for rendering the main content of the page. It displays one product per row and includes a quantifier component that allows the user to update the quantity of the product. At the bottom of the page, it also shows the total price of the selected products, which is formatted as GBP using the CurrencyFormatter component.

Quantifier – this component displays plus and minus buttons along with an input field positioned between them. It serves the purpose of indicating the current quantity of a product and enables the user to modify this value. 

Footer – this component is designed to provide a simple and visually representative way to display information about the author and copyrights.

Loader – this component is not visible on the screenshots above, but it represents a simple loading animation that becomes visible once the user opens the app for first time and the products data is still being loaded.


**Header Shrinking:**

There is a feature of smooth shrinking animation of the header that can be seen while scrolling down through the list of products in the Home Screen

To accomplish this, I have used React hooks along with a technique involving manual manipulation of styles for various DOM elements. I implemented this functionality within a component method called shrinkHeader, which is invoked whenever a user scrolls. Within this method, I check if the current vertical scroll position exceeds a specified threshold value, DISTANCE_FROM_TOP, and accordingly apply different styles based on the outcome of this comparison.

One interesting aspect of this component is that the Product List component handles sending a request to a REST API in order to fetch the product data. This is accomplished through the fetchData method, which is invoked within a useMemo hook which drives the optimization of the API processing thus making the fetch of data more quicker compared to useEffect hook.


To ensure that each row displays three items when viewed on large viewports, we utilize CSS (SCSS) styles. This is done by utilizing the capabilities of Flexbox.

In addition to these features, the component code also includes functionality for handling the "Add to Cart" button click event, specifically adding the selected item to the local storage.

The basic error handling logic is implemented while fetching the product list to display an error message in case the request to the third-party API fails.


**Cart Component:**

This component bears some resemblance to the Product List component in that it also lists products, but in a different manner with only one item per row.

It also introduces additional functionality by incorporating another component for updating the quantity of selected products. And it calculates the total price of all products in the cart.


# Using local storage:

The main distinction here is that instead of fetching the product data from an API, we retrieve it from the local storage. This is where we store the data for each selected product from the product list component.

LocalStorage is a feature provided by web browsers that allows web applications to store data locally on the user's device. It provides a simple key-value storage mechanism, similar to a dictionary or associative array.

Unlike session storage, which is temporary and gets cleared when the browser session ends, local storage persists even after the browser is closed and reopened. The data stored in local storage remains available until explicitly removed by the application or cleared by the user.

Local storage is primarily used for client-side data storage, enabling web applications to save user preferences, session data, or any other relevant information. This makes it a useful tool for creating personalized experiences and maintaining state across multiple visits to a website.

To accomplish this, I utilized a React hook called use-local-storage-state.

In this case, we use the useEffect hook once again, but this time to reset the scroll position of the window whenever the user visits the page. This ensures that all relevant data is consistently visible to the user, regardless of how far they have scrolled on the product list page.

In the Product List component, we added products to the LocalStorage whenever the user clicked on the Add to Cart button for each item. This ensured that the selected products were stored persistently.

Then, when the user navigates to the cart page, we retrieve the stored data from the LocalStorage and render the products accordingly. By doing so, the user can easily view and interact with the products they previously added to their cart.

We can see that the methods for decreasing or increasing the quantity of a product are passed to the component as callbacks through its props. This approach is useful as it helps maintain a relatively clean component by elevating the responsibility of state management to a higher level.

By lifting the logic for managing the state outside of the component, it allows for better separation of concerns and promotes reusability.


**Footer:
**
The implementation of the footer component is relatively straightforward. It consists of two links to my GitHub and LinkedIn profile details.

# Running the App:

In order to run the application and launch the Home Screen, run the following command as below

**yarn dev**


# Testing the App:

In all components folders, except the Loader one, we have .test.tsx files. These are the files containing the component tests that we run on the front end.

In order to do a test run, open your CLI and run the following command from the root directory of your project:


**yarn test**

This should run all tests and give you the list of the test cases passed and failed accordingly. 


#Automate Unit Testing with GitHub Actions:

GitHub Actions is a powerful automation tool provided by GitHub. It allows us to define and execute workflows directly within your GitHub repository.

With GitHub Actions, you can automate various tasks and processes, such as building, testing, and deploying your code, as well as performing code analysis, generating documentation, and more.

GitHub Actions workflows are defined using YAML syntax. A workflow consists of one or more jobs, and each job consists of a series of steps to be executed. Steps can include actions (reusable units of code), shell commands, or scripts.

I have utilized GitHub Actions to create a workflow that automatically runs the unit test suite whenever a new change is committed to the main branch. This ensures that no production build is triggered in the event of a test failure.

Implementing this workflow is straightforward and highly beneficial. It provides the reassurance that any issues inadvertently introduced into the main branch will be caught before reaching production. This level of reliability and peace of mind is easily achieved by leveraging the capabilities of GitHub Actions.


# Summary:

To summarize the details of the implementation, the following features are implemented as below

1. Creation of shopping cart application with the following actions:

a) Display the list of products in the store
b) Add Items to the cart
c) Remove items from the cart
d) Dynamically modify the count of the cart as when the items are added/removed showing the real-time updates
e) Display the total price of the items in the cart
f) Search the store to fetch the phone related items using the Search icon
g) Adding/Removing multiple number of same items to the cart at once
h) Adjust the quantity of each product in the cart.

2. State Management demonstrated using the actions and reducers like useState and useEffect

3. Integration of mock API as a JSONPlaceholder to fetch the Product data using the API 'https://dummyjson.com/products'.

4. Search phone related products by mocking the API as JSONPlaceholder using the API 'https://dummyjson.com/products/search?q=phone'

5. Optimization of the application for performance improvement utlilizing memorization feature of components using the React Hook useMemo during the fetch of Products from the mocked API

6. Implementation of basic error handling for API failures, such as displaying a user-friendly 
error message when the product list fails to load.

7. Implementation of Unit Tests for each of the created components like App, Product, SearchWidget, Header, Footer, Cart, CartWidget, CurrencyFormatter, Quantifier and TotalPrice.

8. Supporting the Responsive Design behavior using the implementation of media queries in files like Products, Search Widgets, Cart so that they are displayed on both Web and Mobile screens appropriately.

9. Usage of Type Script to add type safety across the application.

10. Implementation of GitHub Actions for promoting the promoting your code to production.
react-testing-library / Vitest – for testing the app, we'll use react-testing-library and Vitest.

11. Header Shrinking option on the Home Screen and Search screen which helps us to seamlessly scroll down the list of products with the shrinking effect of the header


