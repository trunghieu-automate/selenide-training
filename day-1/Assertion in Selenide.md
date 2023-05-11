# Selenide Assertion:
- Selenide assertion is mainly based on should() and shouldNot() methods of SelenideElement class.
> When using should? and shouldNot(), examples for each
- Selenide assertion plays a role as explicit waits in Selenide. The wait of the conditions to be satisfied until a timeout come up.
> So you need to understand which conditions you are expected and [`Selenide's built-in condition`]().


## Question:
### When using should(), shouldNot()?
- We use them to check some condition of the element on the webpage. the condition is often visible, clickable, seleted,...
- We often use should() for positive conditions and shouldNot() for nagative conditions.
- They also known as assertions or verifications

### Examples:
```java
// Check if an element is visible
$("#submit").should(visible);

// Check if an element is hidden
$("#logout").shouldNot(visible);

// Check if an element has some text
$(".message").shouldHave(text("Hello"));

// Check if an element does not have some text
$(".error").shouldNotHave(text("Oops"));

// Check if an element has some attribute
$("img.logo").shouldHave(attribute("src", "logo.png"));

// Check if an element does not have some attribute
$("input.password").shouldNotHave(attribute("type", "text"));
```
## About condition
- Selenide team has a user guide for condition, that is very convenient and easy to understand, here is the [`link`](https://selenide.gitbooks.io/user-guide/content/en/selenide-api/condition.html), Note that, just take the key, and method has been updated, so the fully static method and static fields is in [`javadoc here`](https://selenide.org/javadoc/current/com/codeborne/selenide/Condition.html) 
- Should import each Condition statically for using
- Used in should, shouldNot, shouldHave, waitUntil, waitWhile from SelenideElement class

#### Building composite Conditions:
- We can import these static method to build a quick multiple condition: and(), or(), not()
```java
Condition clickable = and("element can be clicked", visible, enabled);
```

#### Assertion element text?
- We have many methods to do assertion the element's text, that divide into 2 types:
- First type is assertion the extract value of the element text:
- - exactOwnText(String text): Assert that element has given text (without checking child elements).
- - exactOwnTextCaseSensitive(String text): Assert that element has given text (without checking child elements).
- - exactText(String text): Assert that element has exactly (case-insensitive) given text
- - exactTextCaseSensitive(String text): Assert that element has exactly the given text
- - exactValue(String value)
```java
$("#input").shouldHave(exactValue("John"));
```
- Second is checking element text contains a subString, we have some method here:
- - text(String text): 
- - textCaseSensitive(String text): 
- - ownText(String text)
- - ownTextCaseSensitive(String text)

#### The built-in matchText and creating a customeMatch method:
- In some case we need to test element text should match an regex, so Selenide come with matchText() method that take regex as an argument
```java
Condition validEmail = matchText("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$");
Condition validPhone = matchText("^\\+\\d{1,3}\\s\\d{3}\\s\\d{3}\\s\\d{4}$");

// Usage
$("#email").shouldHave(validEmail);
$("#phone").shouldHave(validPhone);
```
- Selenide come with another way to build a custom condition that specify for matching values, `customMatch()` method
- This method take in an Predicate as an arguments, here is example:
```java
Condition validEmail = customMatch("valid email", text -> text.matches("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$"));
Condition validPhone = customMatch("valid phone", text -> text.matches("^\\+\\d{1,3}\\s\\d{3}\\s\\d{3}\\s\\d{4}$"));

// Usage
$("#email").shouldHave(validEmail);
$("#phone").shouldHave(validPhone);
```

#### Combining multiple conditions
You can combine multiple conditions in Selenide using the and and or methods. These methods allow you to check if an element matches all or any of the given conditions. For example, here are some combined conditions that check if an element is clickable or editable:
```java
// Using and
Condition clickable = and("can be clicked", visible, enabled);
Condition editable = and("can be edited", visible, enabled, not(readonly));

// Usage
$("#submit").shouldBe(clickable);
$("#name").shouldBe(editable);

// Using or
Condition clickableOrEditable = or("can be clicked or edited", clickable, editable);

// Usage
$("#button").shouldHave(clickableOrEditable);
$("#input").shouldHave(clickableOrEditable);
```
#### Creating custume and explainedCondition method
- You can use explainedCondition method in Selenide to wrap any condition with a custom explanation. This method allows you to provide a more meaningful error message when the condition fails. 
> For example, here is an explained condition that checks if an element has a valid email:
```java
public static Condition explainedCondition(String explanation, Condition delegate) {
  return new Condition(delegate.getName(), delegate.missingElementSatisfiesCondition()) {
    @Override
    public boolean apply(Driver driver, WebElement element) {
      return delegate.apply(driver, element);
    }

    @Override
    public String actualValue(Driver driver, WebElement element) {
      return delegate.actualValue(driver, element);
    }

    @Override
    public String toString() {
      return explanation + " " + delegate.toString();
    }
  };
}
```
```java
// Using explainedCondition
Condition validEmail = explainedCondition("valid email", matchText("^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$"));

// Usage
$("#email").shouldHave(validEmail);

// Error message
Element should have valid email {#email}
Element: '<input id="email" value="invalid.email.com">'
Actual value: invalid.email.com
```

#### Creating custom condition:
- To create a custom condition in Selenide since version 6.0.0, you need to extend the Condition class and override the check method. The check method takes a driver and an element as parameters and returns a CheckResult object that contains the verdict and the actual value of the condition. The verdict can be either ACCEPT or REJECT, depending on whether the element satisfies the condition or not. The actual value can be any string that represents the state of the element. For example, here is a custom condition that checks if an element has a specific CSS property and value:
```java
public static Condition css(final String propName, final String propValue) {
  return new Condition("css") {
    @Override
    public CheckResult check(Driver driver, WebElement element) {
      String actualValue = element.getCssValue(propName);
      boolean matches = propValue.equalsIgnoreCase(actualValue);
      return new CheckResult(matches, actualValue);
    }
  };
}

// Usage
$("h1").shouldHave(css("font-size", "16px"));
```
