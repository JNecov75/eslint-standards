# ESLint Rules and Javascript Coding Standards
This repo contains the ESLint file and explanations for the rule choices within. This setup is geared towards javascript best practices, with Sencha ExtJS in mind, though the ruleset is pretty much universal. 

## Table of Contents
1. [Global](#global)
2. [Best Practices](#best-practices)
3. [Variables](#variables)
4. [Styling Choices](#styling-choices)

## Global
  ```json
    "env": {
        "browser": true
    },
    "extends": "eslint:recommended",
    "globals": {
        "Ext": false,
        "Atlas": false
    }
  ```
  - [1.1](#env) **env**: This object should contain only one property, **browser**. It should be set to true. This allows browser to be treated as a global variable.
    > http://eslint.org/docs/user-guide/configuring#specifying-environments
  
  - [1.2](#extends) **extends**: Use this property to set eslint:recommended. This setting automatically includes a set of recommended rules that ESLint has predetermined.
    > http://eslint.org/docs/user-guide/configuring#extending-configuration-files
  - [1.3](#globals) **globals**: Use this property to define the remaining global objects that your project needs. We created one for Ext due to framework requirements, and one that was the name of our project, Atlas, for project-specific data.
  
  - [1.4](#rules) **rules**: This final object at the top level of the JSOn configuration file exists to house all of the necessary ESLint rules not included in the ```json eslint:recommended``` property.
    
## Best Practices
  - [2.1](#accessor-pairs) **accessor-pairs**: Enforces getter/setter pairs in objects

    > http://eslint.org/docs/rules/accessor-pairs 
    It’s a common mistake in JavaScript to create an object with just a setter for a property but never have a corresponding getter defined for it. Without a getter, you cannot read the property, so it ends up not being used.

    `js
    // Bad
    var o = {
        set a(value) {
            this.val = value;
        }
    };

    // Good
    var o = {
        set a(value) {
            this.val = value;
        },
        get a() {
            return this.val;
        }
    };
    `
    
  - [2.2](#array-callback-return) **array-callback-return**: Enforces return statements in callbacks of array’s methods
  
    > `Array` has several methods for filtering, mapping, and folding. If we forget to write `return` statement in a callback of those, it’s probably a mistake.


## Variables

## Styling Choices
