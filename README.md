# ESLint Rules and Javascript Coding Standards
This repo contains the ESLint file and explanations for the rule choices within. This setup is geared towards javascript best practices, with Sencha ExtJS in mind, though the ruleset is pretty much universal. All of the rules below are linked to their corresponding ESLint documentation page.

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
  - [1.1](#env) <a href="http://eslint.org/docs/user-guide/configuring#specifying-environments">**env**</a>: This object should contain only one property,`browser`. It should be set to true. This allows browser to be treated as a global variable.
  
  - [1.2](#extends) <a href="http://eslint.org/docs/user-guide/configuring#extending-configuration-files">**extends**</a>: Use this property to set eslint:recommended. This setting automatically includes a set of recommended rules that ESLint has predetermined.
  
  - [1.3](#globals) <a href="http://eslint.org/docs/user-guide/configuring#specifying-globals">**globals**</a>: Use this property to define the remaining global objects that your project needs. We created one for Ext due to framework requirements, and one that was the name of our project, Atlas, for project-specific data.
  
  - [1.4](#rules) <a href="http://eslint.org/docs/rules/">**rules**</a>: This final object at the top level of the JSOn configuration file exists to house all of the necessary ESLint rules not included in the `eslint:recommended` property.
    
## Best Practices
  - [2.1](#accessor-pairs) <a href="http://eslint.org/docs/rules/accessor-pairs">**accessor-pairs**</a>: Enforces getter/setter pairs in objects

    > It’s a common mistake in JavaScript to create an object with just a setter for a property but never have a corresponding getter defined for it. Without a getter, you cannot read the property, so it ends up not being used.

    ```js
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
    ```
    
  - [2.2](#array-callback-return) <a href="http://eslint.org/docs/rules/array-callback-return">**array-callback-return**</a>: Enforces return statements in callbacks of array’s methods
  
    > `Array` has several methods for filtering, mapping, and folding. If we forget to write `return` statement in a callback of those, it’s probably a mistake.
    
  - [2.3](#block-scoped-var) <a href="http://eslint.org/docs/rules/block-scoped-var">**block-scoped-var**: Treat var as Block Scoped
  
  - [2.4](#complexity) **complexity**: Limit Cyclomatic Complexity
    > Cyclomatic complexity measures the number of linearly independent paths through a program’s source code. This rule allows setting a cyclomatic complexity threshold.
    ```js
    "complexity": [
      "error",
      15
    ],
    ```
    
  - [2.5](#consistent-return) **consistent-return**: require `return` statements to either always or never specify values
  
  - [2.6](#curly) **curly**: Require Following Curly Brace Conventions
  
  - [2.7](#default-case) **default-case**: Require Default Case in Switch Statements
  
  - [2.8](#dot-location) **dot-location**: Enforce newline before and after dot
  
  - [2.9](#dot-notation) **dot-notation**: Require Dot Notation
  
  - [2.10](#eqeqeq) **eqeqeq**: Require `===` and `!==`
  
  - [2.11](#guard-for-in) **guard-for-in**: Require Guarding for-in
  
  - [2.12](#no-alert) **no-alert**: Disallow Use of Alert
  
  - [2.13](#no-else-return) **no-else-return**: Disallow return before else
  
  - [2.14](#no-empty-function) **no-empty-function**: Disallow empty functions
  
  - [2.15](#no-eq-null) **no-eq-null**: Disallow Null Comparisons
  
  - [2.16](#no-eval) **no-eval**: Disallow eval()
  
  - [2.17](#no-extend-native) **no-extend-native**: Disallow Extending of Native Objects
  
  - [2.18](#no-floating-decimal) **no-floating-decimal**: Disallow Floating Decimals
  
  - [2.19](#no-global-assign) **no-global-assign**: Disallow assignment to native objects or read-only global variables
  
  - [2.20](#no-implicit-coercion) **no-implicit-coercion**: Disallow the type conversion with shorter notations
  
  - [2.21](#no-implicit-globals) **no-implicit-globals**: Disallow variable and function declarations in the global scope
  
  - [2.22](#no-implied-eval) **no-implied-eval**: Disallow Implied eval()
  
  - [2.23](#no-iterator) **no-iterator**: Disallow Iterator
  
  - [2.24](#no-labels) **no-labels**: Disallow Labeled Statements
  
  - [2.25](#no-lone-blocks) **no-lone-blocks**: Disallow Unnecessary Nested Blocks
  
  - [2.26](#no-loop-func) **no-loop-func**: Disallow `function` declarations and expressions inside loop statements
  
  - [2.27](#no-multi-spaces) **no-multi-spaces**: disallow multiple spaces

  - [2.28](#no-multi-str) **no-multi-str**: disallow multiline strings
  
  - [2.29](#no-new) **no-new**: disallow `new` operators outside of assignments or comparisons
  
  - [2.30](#no-new-func) **no-new-func**: disallow `new` operators with the `Function` object
  
  - [2.31](#no-new-wrappers) **no-new-wrappers**: disallow `new` operators with the `String`, `Number`, and `Boolean` objects
  
  - [2.32](#no-param-reassign) **no-param-reassign**: disallow reassigning `function` parameters
  
  - [2.33](#no-return-assign) **no-return-assign**: disallow assignment operators in `return` statements
  
  - [2.34](#no-script-url) **no-script-url**: disallow `javascript:` urls
  
  - [2.35](#no-self-compare) **no-self-compare**: disallow comparisons where both sides are exactly the same
  
  - [2.36](#no-sequences) **no-sequences**: disallow comma operators
  
  - [2.37](#no-throw-literal) **no-throw-literal**: disallow throwing literals as exceptions
  
  - [2.38](#no-unmodified-loop-condition) **no-unmodified-loop-condition**: disallow unmodified loop conditions
  
  - [2.39](#no-unused-expressions) **no-unused-expressions**: disallow unused expressions
  
  - [2.40](#no-useless-concat) **no-useless-concat**: disallow unnecessary concatenation of literals or template literals
  
  - [2.41](#no-useless-escape) **no-useless-escape**: disallow unnecessary escape characters
  
  - [2.42](#no-useless-return) **no-useless-return**: disallow redundant return statements
  
  - [2.43](#no-void) **no-void**: disallow void operators
  
  - [2.44](#require-await) **require-await**: disallow async functions which have no await expression
  
  - [2.45](#vars-on-top) **vars-on-top**: require var declarations be placed at the top of their containing scope
  
  - [2.46](#wrap-iife) **wrap-iife**: require parentheses around immediate function invocations
  
  - [2.47](#strict) **strict**: require or disallow strict mode directives
  
## Variables
  
  - [3.1](#no-catch-shadow) **no-catch-shadow**: disallow catch clause parameters from shadowing variables in the outer scope
  
  - [3.2](#no-shadow) **no-shadow**: disallow variable declarations from shadowing variables declared in the outer scope
  
  - [3.3](#no-shadow-restricted-names) **no-shadow-restricted-names**: disallow identifiers from shadowing restricted names
  
  - [3.4](#no-use-before-define) **no-use-before-define**: disallow the use of variables before they are defined

## Styling Choices

  - [4.1](#array-bracket-spacing) **array-bracket-spacing**: enforce consistent spacing inside array brackets
  
  - [4.2](#block-spacing) **block-spacing**: enforce consistent spacing inside single-line blocks
  
  - [4.3](#brace-style) **brace-style**: enforce consistent brace style for blocks
  
  - [4.4](#camelcase) **camelcase**: enforce camelcase naming convention
  
  - [4.5](#comma-dangle) **comma-dangle**: require or disallow trailing commas
  
  - [4.6](#comma-spacing) **comma-spacing**: enforce consistent spacing before and after commas
  
  - [4.7](#comma-style) **comma-style**: enforce consistent comma style
  
  - [4.8](#computed-property-spacing) **computed-property-spacing**: enforce consistent spacing inside computed property brackets
  
  - [4.9](#consistent-this) **consistent-this**: enforce consistent naming when capturing the current execution context
  
  - [4.10](#func-call-spacing) **func-call-spacing**: require or disallow spacing between function identifiers and their invocations
  
  - [4.11](#func-name-matching) **func-name-matching**: require function names to match the name of the variable or property to which they are assigned
  
  - [4.12](#id-length) **id-length**: enforce minimum and maximum identifier lengths
  
  - [4.13](#key-spacing) **key-spacing**: enforce consistent spacing between keys and values in object literal properties
  
  - [4.14](#keyword-spacing) **keyword-spacing**: enforce consistent spacing before and after keywords
  
  - [4.15](#linebreak-style) **linebreak-style**: enforce consistent linebreak style
  
  - [4.16](#max-len) **max-len**: enforce a maximum line length
  
  - [4.17](#max-lines) **max-lines**: enforce a maximum number of lines per file
  
  - [4.18](#max-nested-callbacks) **max-nested-callbacks**: enforce a maximum depth that callbacks can be nested
  
  - [4.19](#max-params) **max-params**: enforce a maximum number of parameters in function definitions
  
  - [4.20](#max-statements) **max-statements**: enforce a maximum number of statements allowed in function blocks
  
  - [4.21](#max-statements-per-line) **max-statements-per-line**: enforce a maximum number of statements allowed per line
  
  - [4.22](#multiline-ternary) **multiline-ternary**: enforce newlines between operands of ternary expressions
  
  - [4.23](#new-cap) **new-cap**: require constructor names to begin with a capital letter
  
  - [4.24](#new-parens) **new-parens**: require parentheses when invoking a constructor with no arguments
  
  - [4.25](#no-array-constructor) **no-array-constructor**: disallow Array constructors
  
  - [4.26](#no-lonely-if) **no-lonely-if**: disallow if statements as the only statement in else blocks
  
  - [4.27](#no-mixed-operators) **no-mixed-operators**: disallow mixed binary operators
  
  - [4.28](#no-multi-assign) **no-multi-assign**: disallow use of chained assignment expressions
  
  - [4.29](#no-multiple-empty-lines) **no-multiple-empty-lines**: disallow multiple empty lines
  
  - [4.30](#no-nested-ternary) **no-nested-ternary**: disallow nested ternary expressions
  
  - [4.31](#no-new-object) **no-new-object**: disallow Object constructors
  
  - [4.32](#no-trailing-spaces) **no-trailing-spaces**: disallow trailing whitespace at the end of lines
  
  - [4.33](#no-unneeded-ternary) **no-unneeded-ternary**: disallow ternary operators when simpler alternatives exist
  
  - [4.34](#no-whitespace-before-property) **no-whitespace-before-property**: disallow whitespace before properties
  
  - [4.35](#nonblock-statement-body-position) **nonblock-statement-body-position**: enforce the location of single-line statements
  
  - [4.36](#object-curly-newline) **object-curly-newline**: enforce consistent line breaks inside braces
  
  - [4.37](#object-curly-spacing) **object-curly-spacing**: enforce consistent spacing inside braces
  
  - [4.38](#object-property-newline) **object-property-newline**: enforce placing object properties on separate lines
  
  - [4.39](#one-var-declaration-per-line) **one-var-declaration-per-line**: require or disallow newlines around variable declarations
  
  - [4.40](#operator-assignment) **operator-assignment**: require or disallow assignment operator shorthand where possible
  
  - [4.41](#operator-linebreak) **operator-linebreak**: enforce consistent linebreak style for operators
  
  - [4.42](#padded-blocks) **padded-blocks**: require or disallow padding within blocks
  
  - [4.43](#quotes) **quotes**: enforce the consistent use of either backticks, double, or single quotes
  
  - [4.44](#semi) **semi**: require or disallow semicolons instead of ASI
  
  - [4.45](#semi-spacing) **semi-spacing**: enforce consistent spacing before and after semicolons
  
  - [4.46](#space-before-blocks) **space-before-blocks**: enforce consistent spacing before blocks
  
  - [4.47](#space-before-function-paren) **space-before-function-paren**: enforce consistent spacing before function definition opening parenthesis
  
  - [4.48](#space-in-parens) **space-in-parens**: enforce consistent spacing inside parentheses
  
  - [4.49](#space-infix-ops) **space-infix-ops**: require spacing around infix operators
  
  - [4.50](#wrap-regex) **wrap-regex**: require parenthesis around regex literals
