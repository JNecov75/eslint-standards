# ESLint Rules and Javascript Coding Standards
This repo contains the ESLint file and explanations for the rule choices within. This setup is geared towards javascript best practices, with Sencha ExtJS in mind, though the ruleset is pretty much universal. 

## Table of Contents
1. [Best Practices](#best-practices)

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
