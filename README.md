# ESLint Rules and Javascript Coding Standards
This repo contains the ESLint file and explanations for the rule choices within. This setup is geared towards javascript best practices, with Sencha ExtJS in mind, though the ruleset is pretty much universal. 

## Table of Contents
1. [Global](#global)
2. [Best Practices](#best-practices)
5. [Complete Ruleset](#complete-ruleset)

## Global
<a name="env"></a><a name="1.1"></a>
  - [1.1](#env) **env**: This object should contain only one property, **browser**. It should be set to true. This allows browser to be treated as a global variable.
    > http://eslint.org/docs/user-guide/configuring#specifying-environments
    ```json
    "env": {
        "browser": true
    }
    ```
  
  - [1.2](#extends) **extends**: Use this property to set eslint:recommended. This setting automatically includes a set of recommended rules that ESLint has predetermined.
    > http://eslint.org/docs/user-guide/configuring#extending-configuration-files
    
  - [1.3](#rules) **rules**: This final object at the top level of the JSOn configuration file exists to house all of the necessary ESLint rules not included in the ```json eslint:recommended``` property.
    
## Best Practices
<a name="no--error"></a><a name="2.1"></a>
  - [2.1](#no--error) **NO-ERROR**: Use NO-ERROR only when you expect an error to occur, and if you use it, handle error appropriately

    > Why? NO-ERROR suppresses errors, which can cause database inconsistency issues, memory leaks, infinite loops and more...

    ```openedge
    /* bad (error is suppressed, cMemberName is never assigned */
    ASSIGN iMemberNumber = INTEGER("ABC")
           cMemberName   = 'ABC' NO-ERROR.
        
    /* good (ver 1) - using structured error handling */
    ASSIGN iMemberNumber = INTEGER("ABC")
           cMemberName   = 'ABC'.
    /* ... some code... */
    CATCH eExc AS Progress.Lang.ProError:
      MESSAGE "Error:" + eExc:GetMessage(1).
    END.
        
    /* good (ver 2) - classic error handling (split safe assignment from unsafe) */
    ASSIGN cMemberName   = 'ABC'.
    ASSIGN iMemberNumber = INTEGER("ABC") NO-ERROR.
    IF ERROR-STATUS:ERROR THEN DO:
        /* handle error here */
    END.
    ```
    
<a name="no--error"></a><a name="2.2"></a>
  - [2.2](#routine-level) **BLOCK-LEVEL THROW** Always use BLOCK-LEVEL ON ERROR UNDO, THROW statement

    > Why? It changes the default ON ERROR directive to UNDO, THROW for all blocks (from default UNDO, LEAVE or UNDO, RETRY)

    > Note: Use this parameter in legacy systems only. For new development use _-undothrow 2_ to set BLOCK-LEVEL ON ERROR UNDO, THROW everywhere

    > Note: Use in new modules or when you're confident that the change in existing code is not going to break error handling

    ```openedge
    /* bad (default ON ERROR directive used) */
    RUN internalProcedure.

    CATCH eExc AS Progress.Lang.AppError:
        /* this will never be executed */
    END.
        
    PROCEDURE internalProcedure:
        UNDO, THROW NEW Progress.Lang.AppError('Error String', 1000).
    END.

    /* good */
    BLOCK-LEVEL ON ERROR UNDO, THROW.

    RUN internalProcedure.

    CATCH eExc AS Progress.Lang.AppError:
        /* error will be caught here */
    END.

    PROCEDURE internalProcedure:
        UNDO, THROW NEW Progress.Lang.AppError('Error String', 1000).
    END.

    ```

    ```openedge
    /* bad (routine-level doesn't cover FOR loops) */
    ROUTINE-LEVEL ON ERROR UNDO, THROW.
    RUN internalProcedure.
        
    CATCH eExc AS Progress.Lang.AppError:
        /* this will never be executed */
    END.
        
    PROCEDURE internalProcedure:
        FOR EACH bMemberRecord NO-LOCK:
            IF bMemberRecord.memberDOB < 01/01/1910 THEN
                UNDO, THROW NEW Progress.Lang.AppError('Found member with invalid DOB', 1000).
        END.
    END.

    /* good */
    BLOCK-LEVEL ON ERROR UNDO, THROW.

    RUN internalProcedure.

    CATCH eExc AS Progress.Lang.AppError:
        /* error will be caught here */
    END.

    PROCEDURE internalProcedure:
        FOR EACH bMemberRecord NO-LOCK:
            IF bMemberRecord.memberDOB < 01/01/1910 THEN
                UNDO, THROW NEW Progress.Lang.AppError('Found member with invalid DOB', 1000).
        END.
    END.
    ```
## Complete Ruleset
<a name="complete-ruleset"></a><a name="5.1"></a>
```json
  {
      "env": {
          "browser": true
      },
      "extends": "eslint:recommended",
      "rules": {
          //Best Practices Section
          "accessor-pairs": "error",
          "array-callback-return": "error",
          "block-scoped-var": "error",
          "complexity": [
              "error",
              15
          ],
          "consistent-return": "error",
          "curly": "error",
          "default-case": "error",
          "dot-location": "error",
          "dot-notation": "error",
          "eqeqeq": [
              "error",
              "smart"
          ],
          "guard-for-in": "error",
          "no-alert": "error",
          "no-else-return": "error",
          "no-empty-function": "error",
          "no-eq-null": "warn",
          "no-eval": "error",
          "no-extend-native": "error",
          "no-floating-decimal": "error",
          "no-global-assign": "error",
          "no-implicit-coercion": "warn",
          "no-implicit-globals": "error",
          "no-implied-eval": "error",
          "no-iterator": "error",
          "no-labels": "error",
          "no-lone-blocks": "error",
          "no-loop-func": "error",
          "no-multi-spaces": "error",
          "no-multi-str": "error",
          "no-new": "error",
          "no-new-func": "error",
          "no-new-wrappers": "error",
          "no-param-reassign": "error",
          "no-return-assign": [
              "error",
              "always"
          ],
          "no-script-url": "error",
          "no-self-compare": "error",
          "no-sequences": "error",
          "no-throw-literal": "error",
          "no-unmodified-loop-condition": "error",
          "no-unused-expressions": "error",
          "no-useless-concat": "warn",
          "no-useless-escape": "error",
          "no-useless-return": "error",
          "no-void": "error",
          "require-await": "error",
          "wrap-iife": "error",
          "vars-on-top": "error",
          "strict": "error",

          //Variables Section
          "no-catch-shadow": "error",
          "no-shadow": "error",
          "no-shadow-restricted-names": "error",
          "no-use-before-define": "error",

          //Stylistic Issues Section
          "array-bracket-spacing": [
              "error",
              "always", {
                  "objectsInArrays": false
              }
          ],
          "block-spacing": "error",
          "brace-style": "error",
          "camelcase": "warn",
          "comma-dangle": "error",
          "comma-spacing": "error",
          "comma-style": "error",
          "computed-property-spacing": "error",
          "consistent-this": [
              "error",
              "me"
          ],
          "func-call-spacing": "error",
          "func-name-matching": "error",
          "id-length": [
              "error", {
                  "exceptions": ["e", "i", "j", "k"]
              }
          ],
          "indent": [
              "error",
              2, {
                  "SwitchCase": 1 //true
              }
          ],
          "key-spacing": "error",
          "keyword-spacing": "error",
          "max-len": [
              "error",
              120
          ],
          "max-lines": [
              "error",
              1000
          ],
          "max-nested-callbacks": "error",
          "max-params": [
              "warn",
              5
          ],
          "max-statements": [
              "error",
              50
          ],
          "max-statements-per-line": "error",
          "multiline-ternary": [
              "error",
              "never"
          ],
          "new-cap": "warn",
          "new-parens": "error",
          "no-array-constructor": "error",
          "no-lonely-if": "error",
          "no-mixed-operators": "warn",
          "no-multi-assign": "error",
          "no-multiple-empty-lines": "warn",
          "no-nested-ternary": "error",
          "no-new-object": "error",
          "no-trailing-spaces": "error",
          "no-unneeded-ternary": "warn",
          "no-whitespace-before-property": "error",
          "nonblock-statement-body-position": "error",
          "object-curly-newline": [
              "error", {
                  "minProperties": 2
              }
          ],
          "object-curly-spacing": "error",
          "object-property-newline": "error",
          "one-var-declaration-per-line": "warn",
          "operator-assignment": "error",
          "operator-linebreak": "error",
          "padded-blocks": [
              "warn",
              "never"
          ],
          "semi-spacing": "error",
          "space-before-blocks": "error",
          "space-before-function-paren": [
              "error",
              "always"
          ],
          "space-in-parens": "error",
          "space-infix-ops": "error",
          "wrap-regex": "error",
          "linebreak-style": [
              "error",
              "windows"
          ],
          "quotes": [
              "error",
              "single"
          ],
          "semi": [
              "error",
              "always"
          ]
      },
      "globals": {
          "Ext": false,
          "Atlas": false
      }
  }
  ```
