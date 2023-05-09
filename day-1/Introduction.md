### Introduction 
Selenide is a framework for test automation powered by Selenium WebDriver. it brings some advantages:
- Consice fluent API for tests
- Stable tests
- Powerfull selector
- Simple Configuration

### Consice fluent API for tests
- This means Selenide help you write your test in a clear and readable way, using natural language assertion and powerful selectors, for example, you can write test like this:
```java
@Test
public void userCanLoginByUsername(){
    open("/login");
    $(By.name("user.name")).setValue("Johny");
    $("#submit").click();
    $("#loading_progress").should(disappear); // waits element to disappears
    $("#username").shouldHave(text("Hello, Johny!")); // Wait until element get text
}
```
- $ is about seletors, you find element first then do the action.
- You can pass `By` object, CSS selector, Xpath as an argument to work
- Fluent means after finding, do thing. Selenide provide build-in method to interact and assertion.

### Stable tests:
- Selenide can help you write stable tests by taking care of some common issues that can make tests flaky or unreliable. For example, Selenide can handle timeouts, stale elements, ajax calls, browser management, and other aspects of test automation, so you don’t need to worry about them
- Selenide has a built-in mechanism for waiting for elements to be visible, enabled, clickable, etc. before performing any actions or assertions on them. This way, you don’t need to use explicit waits or sleep statements in your tests
- As the above example, the test is stable and doesn't depend on any timing issues or external factors. Selenide will automatically wait for the elements to be in the expected state before proceeding with the test.

### Powerful selector:
- Powerful selectors is another feature of Selenide that allows you to find elements on the web page using different types of locators, such as CSS selectors, XPath expressions, ID, name, class, tag name, link text, partial link text, etc. 
- Selenide provides two methods for finding elements: `$` and `$$`
- - The `$` method returns the first element that matches the given locator -> imagine as findElement() method
- - the `$$` method returns a collection of all elements that match the given locator. -> imagine as findElements() in selenium
For example, you can write a test like this:
```java
@Test
public void userCanSearch() {
  open("https://google.com/ncr");
  $(By.name("q")).setValue("selenide").pressEnter();
  $$("#ires .g").shouldHave(size(10));
  $("#ires .g").shouldHave(text("Selenide: concise UI tests in Java"));
}
```
- You can use By class to specify the type of locator, such as `By.name("q")`
- You can use a shorthand notation with CSS selector, such as $("#ires .g")
- You can also use methods like `byText`, `byAttribute`, `byTitle`

- Selenide also supports finding elements inside shadow DOM using methods like `shadowCss` and `shadowDeepCss`. This way, you can access elements that are hidden inside web components or custom elements. For example, you can write a test like this:
```java
@Test
public void userCanSeeShadowDomElements() {
  open("https://example.com/shadow-dom");
  $(shadowCss("#name", "my-app")).shouldHave(text("John Doe"));
}
```
For more detail information, let check Selenide's Selectors [docs](https://selenide.org/javadoc/current/com/codeborne/selenide/Selectors.html) and [src](https://selenide.org/javadoc/current/com/codeborne/selenide/Selectors.html) 

#### Simple Configuration
- Simple configuration allows you to set up and run your tests with minimal effort and code. 
- You don’t need to write a lot of boilerplate code or use complex frameworks to configure your tests. 
- You can simply add selenide.jar (and its dependencies) to your project and you are done.
- Selenide also provides a Configuration class that contains different configuration options to customize the execution of your tests, such as timeout, browser, browser size, file download mode, etc... You can set these options either programmatically or via system properties or selenide.properties file2. For example, you can write a test like this:
```java
@Test
public void googleTest() {
  Configuration.browser = "firefox";
  Configuration.timeout = 10000;
  open("https://google.com");
  $(By.name("q")).setValue("selenide").pressEnter();
  $$("#res .g").shouldHave(size(10));
}
```
More detail in [javadoc](https://selenide.org/javadoc/current/com/codeborne/selenide/Configuration.html)
