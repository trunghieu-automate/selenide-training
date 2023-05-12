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
#### Mouse action
- click(ClickOption ckickOption): Click the element using ClickOptions: `$("#username").click(ClickOptions.usingJavaScript())`, return SelenideElement but can be ignored
> You can specify a relative offset from the center of the element inside ClickOptions: e.g.
```java
$("#username").click(usingJavaScript().offset(123, 222))
````
- click(): simple click the element
- contextClick(): return SelenideElement but can be ignored
- doubleClick(): return SelenideElement but can be ignored
- hover(): Emulate "mouseOver" event, return SelenideElement but can be ignored
- dragAndDrop(DragAndDropOptions options): return SelenideElement but can be ignored, automatically wait for element get visible before acting.
```java
// Locate the source element using Selenide
SelenideElement source = $("#source");

// Locate the target element using Selenide
SelenideElement target = $("#target");

// Perform the drag and drop action using the dragAndDrop method
source.dragAndDrop(target);
```



#### Other:
##### download file
Selenide has download method that return File object, performing a click to the element
- download()
- download(long timeout)
- download(long timeout, FileFilter fileFilter):
- download(DownloadOption option): not performing a click
- download(Filefilter fileFilter)
##### screenshot
Perform screenshot to the elements
- screenshot(): return File object with png extension, or null if failed to take a screenshot.
- screenshotAsImage(): return [`BufferedImage`](https://docs.oracle.com/en/java/javase/17/docs/api/java.desktop/java/awt/image/BufferedImage.html)
- 
