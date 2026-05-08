---
title: Error Handling
Date Created: 2024-09-08
Last Updated: 2025-09-28
tags:
  - CS2103
  - SWE
  - ErrorHandling
---
# Assertions
---
Unlike exceptions, <span style='color:var(--mk-color-turquoise)'>assertions</span> are used to identify **mistakes** made by the <b><span style='color:var(--mk-color-yellow)'>programmer</span></b> and not the user.

These <span style='color:var(--mk-color-turquoise)'>assertions</span> are also <b><mark style='background:var(--mk-color-yellow)'>different</mark></b> from the ones in <span style='color:var(--mk-color-purple)'>JUnit</span>, as these are for testing the code, while assertions are in the production code.

**Assertions** (`assert`)
>Define **assumptions about the program** state so that at **runtime it can be verified**

If an <span style='color:var(--mk-color-red)'>assertion failure</span> is detected at run time it will take some drastic actions (*Terminating / Error message*), since this <span style='color:var(--mk-color-yellow)'>indicate that there is a possible bug</span>.

In <span style='color:var(--mk-color-purple)'>Java</span> assertions are **disabled by default** and has to reenabled with `java -enableassertions Helloworld` or use `java -ea HelloWorld`. And to disable it again just change it to `disableassertions`.

However, <span style='color:var(--mk-color-purple)'>JUnit</span> and <span style='color:var(--mk-color-purple)'>Java</span> <span style='color:var(--mk-color-turquoise)'>assertions</span> though similar in functionality, the ones in <span style='color:var(--mk-color-purple)'>JUnit</span> are:
- **More powerful**
- **Customised for testing**
- **Not disabled by default**
## When to Use Assertions

Firstly <b><span style='color:var(--mk-color-red)'>do not use assertions as logic</span></b> for your code, because <span style='color:var(--mk-color-yellow)'>assertions can be disabled</span> while will render the code not to work. 

It is recommended to **use assertions** liberally as it as <span style='color:var(--mk-color-green)'>low impact on performance</span> and they <span style='color:var(--mk-color-green)'>provide additional safety features</span>.

Assertions are <span style='color:var(--mk-color-yellow)'>suitable for verifying assumptions</span> about:
- Internal Invariants
- Control-Flow Invariants
- Preconditions, Postconditions,
- Class Invariants
# Logging
---
<span style='color:var(--mk-color-turquoise)'>Logging</span> is the process of **recording certain information** <span style='color:var(--mk-color-yellow)'>during a program execution</span>.

The output can be **saved into a log file or other means for future reference**, and this can be used for troubleshooting.

> [!info] Black Box
> A log file is like a **black box**.
> 
> It <b><mark style='background:var(--mk-color-red)'>does not prevent problems</mark></b> or bugs from happening.
> 
> It can however help better <b><mark style='background:var(--mk-color-green)'>understand what went wrong</mark></b>.

<span style='color:var(--mk-color-yellow)'>Most environments have logging systems</span> that **allow sophisticated forms of logging** like logging intensity or enabling / disabling.

In <span style='color:var(--mk-color-purple)'>java</span> there is a logging package under utility (`import java.util.logging.*;`).

**How to use the logger in java**
```Java
import java.util.logging.*;
// Create the logger object
private static Logger logger = Logger.getLogger("Foo");

// log a message at INFO level
logger.log(Level.INFO, "going to start processing");
processInput();
if (error) {
    // log a message at WARNING level
    logger.log(Level.WARNING, "processing error", ex);
}
logger.log(Level.INFO, "end of processing");
```
# Defensive Programming
---
It is to code **under the assumption** that, if you <span style='color:var(--mk-color-yellow)'>leave room for things to go wrong they will go wrong</span>.

It is **always good to be defensive**? <b><mark style='background:var(--mk-color-yellow)'>No it is not necessary</mark></b>. While this practice is <span style='color:var(--mk-color-green)'>less prone to be misused or abused</span>, it can make the code <span style='color:var(--mk-color-red)'>more complex and slower to run</span>.

> [!question] When to be Defensive?
> There are **many factors to consider** but do <span style='color:var(--mk-color-orange)'>ask yourself these questions</span>:
> - How critical is the system?
> - Will the code be used by programmers other than the author?
> - The level of programming language support for defensive programming
> - The overhead of being defensive
## Enforcing Compulsory Association

Consider the following association where an `Account` **must have 1** `Guarantor`. Then we can enforce this with the following code:

```Java
class Account {
    private Guarantor guarantor;
    public Account(Guarantor g) {
        if (g == null) {
            stopSystemWithMessage(
                    "multiplicity violated. Null Guarantor");
        }
        guarantor = g;
    }
    public void setGuarantor(Guarantor g) {
        if (g == null) { // Without this the user can do .setGuarantor(Null) !!
            stopSystemWithMessage(
                    "multiplicity violated. Null Guarantor");
        }
        guarantor = g;
    }
    // ...
}
```
### Enforcing 1 to 1 Associations

We can enforce a 1 to 1 as such:

```Java
class MinedCell {
    private Mine mine;
    public MinedCell() {
        mine = new Mine();
    }
    // ...
}
```

Without the constructor called the `Mine` constructor, it will make a `MineCell` to have 0 `Mine` objects which will <span style='color:var(--mk-color-red)'>violate the association.</span>.
### Enforcing Referential Integrity

Lets take for instance a **bidirectional association**, `Man` and `Woman`, which can be a boyfriend or a girlfriend. If we have a `set` method which can just **change one object without changing the other** then we will have this **"love triangle"**, this means the <span style='color:var(--mk-color-red)'>referential integrity has been violated</span> and the<span style='color:var(--mk-color-red)'> object reference is inconsistent</span>.

We can <span style='color:var(--mk-color-orange)'>solve</span> this by doing the following:
```Java
public class Woman {
    private Man boyfriend;

    public void setBoyfriend(Man m) {
        if (boyfriend == m) {
            return;
        }
        if (boyfriend != null) {
            boyfriend.breakUp();
        }
        boyfriend = m;
        if (m != null) {
            m.setGirlfriend(this);
        }
    }

    public void breakUp() {
        boyfriend = null;
    }
    // ...
}
```

Essentially we just need to <span style='color:var(--mk-color-yellow)'>remember to update both objects</span> when one is being updated.
# Design by Contract
---
It is an approach that <span style='color:var(--mk-color-yellow)'>requires defining</span> **formal, precise and verifiable interface specifications for software components**.

Instead of asking the code to check if the preconditions are met, it assumes that the <span style='color:var(--mk-color-yellow)'>responsibility of the caller </span>to **ensure the preconditions are met**.

Only then the software will work as intended **if not then it will be "unspecified"**. <span style='color:var(--mk-color-purple)'>Eiffel</span> a language that **has inbuilt support for DbC**.

For other languages like <span style='color:var(--mk-color-purple)'>Java</span> or <span style='color:var(--mk-color-purple)'>C++</span>, there is no DbC support thus, <span style='color:var(--mk-color-teal)'>assertions</span> can be used to confirm pre-conditions.

