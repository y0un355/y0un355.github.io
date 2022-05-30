# yys.github.io :
DevOps Best Practices 

## What are Coding Standards?
Think of coding standards as a set of rules, techniques, and best practices to create cleaner, more readable, more efficient code with minimal errors. They offer a uniform format by which software engineers can use to build sophisticated and highly functional code.

## Advantages of implementing Coding Standards
 - Offers uniformity to the code created by different engineers.
 - Enables the creation of reusable code.
 - Makes it easier to detect errors.
 - Make code simpler, more readable, and easier to maintain.
 - Boost programmer efficiency and generates faster results.
## Glossary :

<details>
  <summary>
    <a href="#1-nodejs-best-practices">1. NodeJS Best Practices</a>
  </summary>

- [1.1 Structure your solution by components ](#11-structure-your-solution-by-components)</br>
- [1.2 Layer your components, keep the web layer within its boundaries ](#12-layer-your-components-keep-the-web-layer-within-its-boundaries)</br>
- [1.3 Wrap common utilities as npm packages](#13-wrap-common-utilities-as-npm-packages)</br>
- [1.4 Separate Express 'app' and 'server'](#14-separate-express-app-and-server)</br>
- [1.5 Use environment aware, secure and hierarchical config ](#15-use-environment-aware-secure-and-hierarchical-config)</br>

</details>
<details>
  <summary>
    <a href="#2-reactjs-best-practices">2. ReactJS Best Practices</a>
  </summary>

- [2.1 Keep component creation to a minimum](#21-keep-component-creation-to-a-minimum)</br>
- [2.2 Use a linter](#22-use-a-linter)</br>
- [2.3 The code should be testable](#23-the-code-should-be-testable)
- [2.4 DRY your code](#24-dry-your-code)
- [2.5 Use more robust managers to manage application state, such as Redux](#25-use-more-robust-managers-to-manage-application-state-such-as-redux)
- [2.6 Use defaultProps and propTypes](#26-use-defaultprops-and-proptypes)
- [2.7 File structure](#27-file-structure)
- [2.8 Use stateful function-based components by starting to use React Hooks](#28-use-stateful-function-based-components-by-starting-to-use-react-hooks)</br>

</details>

## 1.1 Structure your solution by components
The worst large applications pitfall is maintaining a huge code base with hundreds of dependencies - such a monolith slows down developers as they try to incorporate new features. Instead, partition your code into components, each gets its folder or a dedicated codebase, and ensure that each unit is kept small and simple. Visit 'Read More' below to see examples of correct project structure

Otherwise: When developers who code new features struggle to realize the impact of their change and fear to break other dependent components - deployments become slower and riskier. It's also considered harder to scale-out when all the business units are not separated



## 1.2 Layer your components, keep the web layer within its boundaries
Each component should contain 'layers' - a dedicated object for the web, logic, and data access code. This not only draws a clean separation of concerns but also significantly eases mocking and testing the system. Though this is a very common pattern, API developers tend to mix layers by passing the web layer objects (e.g. Express req, res) to business logic and data layers - this makes your application dependent on and accessible only by specific web frameworks

Otherwise: App that mixes web objects with other layers cannot be accessed by testing code, CRON jobs, triggers from message queues, etc




## 1.3 Wrap common utilities as npm packages
In a large app that constitutes a large codebase, cross-cutting-concern utilities like a logger, encryption and alike, should be wrapped by your code and exposed as private npm packages. This allows sharing them among multiple codebases and projects

Otherwise: You'll have to invent your deployment and the dependency wheel




## 1.4 Separate Express 'app' and 'server'
Avoid the nasty habit of defining the entire Express app in a single huge file - separate your 'Express' definition to at least two files: the API declaration (app.js) and the networking concerns (WWW). For even better structure, locate your API declaration within components

Otherwise: Your API will be accessible for testing via HTTP calls only (slower and much harder to generate coverage reports). It probably won't be a big pleasure to maintain hundreds of lines of code in a single file


## 1.5 Use environment aware, secure and hierarchical config
A perfect and flawless configuration setup should ensure (a) keys can be read from file AND from environment variable (b) secrets are kept outside committed code (c) config is hierarchical for easier findability. There are a few packages that can help tick most of those boxes like rc, nconf, config, and convict.

Otherwise: Failing to satisfy any of the config requirements will simply bog down the development or DevOps team. Probably both


## 2. ReactJS Best Practices :

## 2.1 Keep component creation to a minimum
You can always improve the reusability of components, by sticking to the rule of one function = one component. This means that you should skip trying to build a new component for a function if there already exists one for that function.

By reusing not only will you keep up with consistency, but you will also contribute to the community.

On the other hand, if a component becomes large or difficult to maintain, it’s better to break it up into a few smaller components.

For example, you can even go further and create a Button component that can handle icons. Then, each time you need a button, you’ll have a component to use. Making it more modular will allow you to cover many cases with the same piece of code. The best way is to aim somewhere in the middle. Your components should be abstract enough, yet not overly complex.

     `const BaseButton = props => {
         const { loading, color, visible, ...rest } = props;
         if (visible === false) {
           return null;
         }
         const content = (
           <StyledButton disabled={loading} color={color || 'default'} {...rest}>
             {props.children || props.text}
             {props.loading && <CircularProgress size={14} />}
           </StyledButton>
         );
       };`
 
 ## 2.2 Use a linter
 Linting is a process where we run a program that analyses code for potential errors.
 
 Mostly, we use it for language-related issues. But it can also fix many other issues automatically – particularly code style. Using a linter in your React code will help you keep your code relatively error- and bug-free.
 
 ## 2.3 The code should be testable
 The code you write should be easily and quickly testable. It’s a good practice to name your test files identically to the source files with a ‘.test’ suffix. It’ll then be a lot easier to find the files you’ve tested.
 
 You can use Cypress.io, and or JEST to test your React code.
 
 ## 2.4 DRY your code
 A common rule for all code is to keep it as brief as possible.
 
 You can achieve this by inspecting the code for patterns. If you find any, it’s possible you are repeating some code and there’s scope to eliminate duplication. A bit of rewriting might make it more concise.
 
 
 This relies on the reusability principle in React. Let’s say you want to add multiple buttons that contain icons. So, instead of adding the markup for each button, you can simply use the Button component that we made earlier. You could even go further by mapping everything into an array.
 
 ## 2.5 Use more robust managers to manage application state, such as Redux
 Redux is a popular JavaScript library for managing the state of your application. It is very common and – if you are working with React – you’ve probably already heard about it.
 
 For those of you who have no idea what an application state is: it is like a global object which holds information that you use for various purposes later in the app (e.g. making decisions on which components to render and when, rendering the stored data etc).
 
 Big applications have big application states so managing them gets more and more inconvenient as your app grows.
 
 That’s why we need state management libraries like Redux.
 
 One of the patterns that Redux follows is called “Single Source of Truth” – which means we have only one place (called Store) where we store the only state for the whole application.
 
 In other words, one app – one store – one state.
 
 ## 2.6 Use defaultProps and propTypes
 As your app grows, you can catch a lot of bugs with type-checking. For some applications, you can use JavaScript extensions like Flow or TypeScript to type-check your whole application. But even if you don’t use those, React has some built-in type-checking abilities. To run type-checking on the props for a component, you can assign the special propTypes property:
 
    `import PropTypes from 'prop-types';
     
     class Greeting extends React.Component {
       render() {
         return (
           <h1>Hello, {this.props.name}</h1>
         );
       }
     }
     
     Greeting.propTypes = {
       name: PropTypes.string
     };
     Greeting.defaultProps = {
         name: 'stranger'
     };`
     
 ## 2.7 File structure
   React doesn’t have preferences on how you should put files into folders. That being said, there are a few common approaches popular in the ecosystem you may want to consider.
   
   Grouping by features or routes – one common way to structure projects is to locate CSS, JS, and tests together inside folders grouped by feature or route.
   
      `api/
         APIUtils.js
         APIUtils.test.js
         ProfileAPI.js
         UserAPI.js
        components/
         Avatar.js
         Avatar.css
         Feed.js
         Feed.css
         FeedStory.js
         FeedStory.test.js
         Profile.js
         ProfileHeader.js
         ProfileHeader.css`

   Grouping by file type – another popular way to structure projects is to group similar files together, for example:
   
    `common/
       Avatar.js
       Avatar.css
       APIUtils.js
       APIUtils.test.js
     feed/
       index.js
       Feed.js
       Feed.css
       FeedStory.js
       FeedStory.test.js
       FeedAPI.js
     profile/
       index.js
       Profile.js
       ProfileHeader.js
       ProfileHeader.css
       ProfileAPI.js`
## 2.8 Use stateful function-based components by starting to use React Hooks
   Hooks are easier to work with and to test (as separated functions from React components*). Also, they make the code look cleaner and easier to read — a related logic can be tightly coupled in a custom hook. A code that uses hooks is easily readable and has fewer lines of code.
   
   You can also define several separated lifecycle methods instead of having all in one method (so you can split componentDidMount() logic with ease).
   
## 3. Flutter Best Practices :
to be added
## Definition of done :


We will keep adding detail and examples to this as we gain understanding of any ambiguities that come up.

For clarity, a task/pull request will not be considered to be complete until all these items can be checked off.

 - Task has its own GitHub issue (something it is solving)
 - Estimate of expected time required to complete task was agreed with all present and recorded before starting the task
 - Issue number is included in the commit messages for traceability
 - Record actual time taken for the task in the PR
 - Update the README.md with any changes/additions made
 - Your code follows the dwyl style guide
 - 100% test coverage
 - All tests pass