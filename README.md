# Escrowredme
Setup WebDriver:

System Property Setup:


System.setProperty("webdriver.chrome.driver", "path_to_chromedriver");
This line sets the system property for the Chrome WebDriver, allowing Selenium to interface with the Chrome browser. Replace "path_to_chromedriver" with the actual path to your ChromeDriver executable.
Instantiate WebDriver:



WebDriver driver = new ChromeDriver();
Creates a new instance of the ChromeDriver, which will launch a new Chrome browser window.
Maximize Browser Window:



driver.manage().window().maximize();
Maximizes the browser window for better visibility and to ensure all elements are accessible.
Navigate to Amazon:


driver.get("https://www.amazon.in");
Opens the Amazon India website.
Search for Products:


WebElement searchBox = driver.findElement(By.id("twotabsearchtextbox"));
searchBox.sendKeys("Wrist Watches");
searchBox.submit();
Locates the search box element using its ID and inputs the text "Wrist Watches", then submits the search form.
Wait for Results to Load:


WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//span[contains(text(), 'results')]")));
Initializes a WebDriverWait object to wait for up to 10 seconds until the results are visible.
Apply Leather Filter:


WebElement leatherFilter = driver.findElement(By.xpath("//li[@aria-label='Leather']//span[@class='a-list-item']"));
leatherFilter.click();
Locates the filter for leather watches and clicks it.
Wait for Leather Filter to be Clickable:

wait.until(ExpectedConditions.elementToBeClickable(By.xpath("//li[@aria-label='Leather']//span[@class='a-list-item']")));
Waits until the leather filter is clickable, ensuring the page has updated correctly.
Apply Fastrack Filter:


WebElement fastrackFilter = driver.findElement(By.xpath("//li[@aria-label='Fastrack']//span[@class='a-list-item']"));
fastrackFilter.click();
Locates and clicks the Fastrack filter.
Wait for Fastrack Filter to be Clickable:


wait.until(ExpectedConditions.elementToBeClickable(By.xpath("//li[@aria-label='Fastrack']//span[@class='a-list-item']")));
Waits until the Fastrack filter is clickable.
Navigate to the Next Page:


WebElement nextPageButton = driver.findElement(By.xpath("//a[contains(text(), '2')]"));
nextPageButton.click();
Clicks on the button to go to the next page of search results.
Wait for the Next Page to Load:


wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//div[@data-index]")));
Waits for any product on the next page to be visible, confirming that the page has loaded.
Select the First Product:


WebElement firstProduct = driver.findElement(By.xpath("(//div[@data-index='1']//h2/a)[1]"));
firstProduct.click();
Locates the first product in the search results and clicks on it to view its details.
Switch to the New Window:


String originalWindow = driver.getWindowHandle();
for (String handle : driver.getWindowHandles()) {
    if (!handle.equals(originalWindow)) {
        driver.switchTo().window(handle);
        break;
    }
}
After clicking the product, a new window opens. This code snippet saves the original window handle and switches to the new window.
Add Product to Cart:


WebElement addToCartButton = wait.until(ExpectedConditions.elementToBeClickable(By.id("add-to-cart-button")));
addToCartButton.click();
Waits for the "Add to Cart" button to become clickable and then clicks it to add the product to the shopping cart.
Quit the Driver:


driver.quit();
Closes the browser and ends the WebDriver session, releasing all resources.
