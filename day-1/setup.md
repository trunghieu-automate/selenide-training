## How to setup Selenide
- It's simple, just adding the dependency to your pom or gradle....
- The harder work is how to integrate Selenide effectively.
- After having the required library, just add import method: import static com.codeborne.selenide.Selenide.*;

## Do we need selenium library while we already have Selenide?
- No, you don’t need to add selenium library while you already have Selenide. Selenide is a wrapper tool for the Selenium web driver. It has an API that connects with Selenium Web Driver and resolves the Ajax/Timeouts problems. Selenide is compatible with Selenium WebDriver 4.0+1. Therefore, you can use Selenide without adding selenium library to your project.

## Can we use Selenide with Cucumber?
Yes, You can use Selenide with Cucumber by following these steps:
- Add cucumber-java and cucumber-junit dependencies to your pom.xml file.
- Create a feature file with your scenarios written in Gherkin language.
- Create a runner class that specifies the feature file and step definitions locations.
- Create a step definitions class that implements the steps using Selenide methods.
- Run your tests using mvn test command or your IDE.

You can find a sample project demonstrating how to use Selenide with Cucumber and Maven on [GitHub](https://github.com/selenide-examples/cucumber)

## Basic setup for a Selenide UI Test framework following POM?
We can create a simple framework for UI testing with Selenide following POM by following instruction:
- Create Maven project then -> add Selenide dependency
- Create **src/test/java** folder and add your test classes
- Create **src/main/java/page** folder and create your page classes here.
- In your page class, you can declare locators and the page interaction here with help of Selenide's fluent API
```java
// sample LoginPage
public class LoginPage{
    private SelenideElement userNameField = $("#username");
    private SelenideElement passwordField = $("#password");
    private SelenideElement loginBtn = $("#login");

    // Page's method
    public void enterUsername(String username) {
        usernameField.setValue(username);
    }
  
    public void enterPassword(String password) {
        passwordField.setValue(password);
    }
  
    public void clickLogin() {
        loginBtn.click();
    }
}
```
- In your test classes, user `open()` method to navigate to the page URL and the `page()` method to create an instance of the page object.

```java
public class LoginTest {
    @Test
    public void testLogin() {
        open("https://example.com/login");
        LoginPage loginPage = page(LoginPage.class);
        loginPage.enterUsername("testuser");
        loginPage.enterPassword("testpass");
        loginPage.clickLogin();
        // verify login success
  }
}
```



