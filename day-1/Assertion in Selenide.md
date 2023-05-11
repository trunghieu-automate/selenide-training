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







