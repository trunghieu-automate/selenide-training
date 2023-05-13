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
#### Dropdown list:
Locate the parent then do these method to catch value, text, selecting a option or multiple options as you wish.
- selectOption(int index, int ...otherIndexes): select option from dropdown list, can pass another indexes from 2nd argument if you want to select multiple options
- selectOption(String text, String ...otherTexts): same as above
- selectOptionContainText(String text, String ...otherTexts): same as above but check the option's substring
- selectOptionByValue(String value, String ...othervalues): same as above but check the value attribute.
- getSelectedOption(): return SelenideElement Object that is the first option is selected.
- getSelectedoptions(): return ElementsCollection that are selected in the dropdown list.
- getSelectedOptionValue(): return String that is value of the selected option value
- getSelectedOptionText(): return String that is text of the selected option

#### Scroll
Selenide provides these method for scroll into selected element, adding some option for more reality as an end user.
- scrollTo(): scroll to element
- scrollIntoView(boolean alignToTop): If true: top of the element will be at the top of browser's view. Vice versal
- scrollIntoView(String scrollOptions): scroll that set by specific options
```java
scrollIntoViewOptions:
  * behavior (optional) - Defines the transition animation
    1. auto (default)
    2. instant
    3. smooth
  * block (optional)
    1. start
    2. center (default)
    3. end
    4. nearest
  * inline
    1. start
    2. center
    3. end
    4. nearest (default)
```
```java
   element.scrollIntoView("{block: \"end\"}");
   element.scrollIntoView("{behavior: \"instant\", block: \"end\", inline: \"nearest\"}");
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
##### upload file
SelenideElement can upload file to uploaded field (input='file') using uploadFile() method
- uploadFile(File ...file): take as many files as arguments as you wish..., return the first File object that you upload

##### SendKey
We have method setValue() to cover sendKey() of Selenium in Selenide. Selennide has more methods to interact with text and textarea:
- setValue(String text): use for <input> and <textarea>, means you can select radio/ checkbox by this method.
> If Configuration.fastInput = true, Selenide will use js input instead of selenium's sendKey method. If not, things will do the following: clear() -> sendKey() -> trigger change event
- append(): use for <text> and <textarea>, used for append text to selected text or textarea -> mean no clear()
- clear(): same as Selenium
- paste(): Append text from the clipboard to the text field and trigger change event.
##### Convert to Selenium WebELement
This method help convert SelenideElement to WebElement
- toWebElement() node that there are no waiting for this elements to convert
- getWrappedElement() 



