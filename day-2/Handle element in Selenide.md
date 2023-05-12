# Handle web elements:
- In selenium, if we want to perform action with an element, i need to catch it than do the action. so in selenide, everything would be more easier, and more fluent.
- Selenide provides smart waits that help element in perfect condition to do the action.
- Fisrt we go through the SelenideElement class in Selenide API, then apply it to handle elements types.
## SelenideElement
- This Class is a wrapper around Selenium's WebElement with additional methods for interact with web elements.
- It implements the SearchContext, WrapsDriver, WrapsElement, Locatable and TakesScreenshot interfaces.
- We have method to find element:
### Find element:
- Find single element that return `SelenideElement` Object\
- - find(By by|| String cssSelector):
- - findAll(By by, int index || String cssSelector, int index):
- - $(String cssSelector): 
- - $$(String cssSelector, int index || String By, int index): 
- - $x(String xpath):
- Find multiple elements and return `ElementsCollection` Object
- - $$x(String xpath):
- - $$(org.openqa.selenium.By selector || cssSelector)
- - findAll()
- Locate axis elements
- - ancestor(String selector): $("td").ancestor("table") will find the closest ancestor with tag table
- - ancestor(String selector, int index): $("td").ancestor("table", 1) will find the 2nd ancestor with tag table
- - closet(String seletor): $("td").closest("table") will find the closest ancestor with tag table
- - parent(): $("td").parent() could give some "tr".
- - lastChild():  $("tr").lastChild(); could give the last "td".
- - sibling(int index): $("td").sibling(0) will give the first following sibling element of "td"

### Interaction
#### click
- click(ClickOption ckickOption): 
