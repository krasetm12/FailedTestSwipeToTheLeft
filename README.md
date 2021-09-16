# FailedTestSwipeToTheLeft
 
import io.appium.java_client.AppiumDriver;
import io.appium.java_client.TouchAction;
import io.appium.java_client.android.AndroidDriver;
import org.junit.After;
import org.junit.Assert;
import org.junit.Before;
import org.junit.Test;
import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;

import java.net.URL;
import java.util.ArrayList;

public class FirstTest {

    private AppiumDriver driver;

    @Before
    public void setUp() throws Exception {
        DesiredCapabilities capabilities = new DesiredCapabilities();
        capabilities.setCapability("platformName", "Android");
        capabilities.setCapability("deviceName", "AndroidTestDevice");
        capabilities.setCapability("platformVersion", "9");
        capabilities.setCapability("automationName", "Appium");
        capabilities.setCapability("appPackage", "org.wikipedia");
        capabilities.setCapability("appActivity", ".main.MainActivity");
        capabilities.setCapability("app", "C:/Users/aleksey/Desktop/JavaAppiumAutomation/apks/org.wikipedia_50370_apps.evozi.com.apk");

        driver = new AndroidDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
    }

    @After
    public void tearDown() {
        driver.quit();
    }                                                                                                                                                                                                 
    @Test
    public void SaveFirstArticleForMyList()
    {
        waitForElementAndClick(
                By.xpath("//*[contains(@text,'SKIP')]"),
                "Cannot find Search Skip input",
                5
        );
        waitForElementAndClick(
                By.xpath("//*[contains(@text,'Search Wikipedia')]"),
                "Cannot find Search wiki input",
                5
        );
        waitForElementAndSendKeys(By.xpath("//*[contains(@text,'Search Wikipedia')]"),
                "java",
                "cannot find search input",
                5);
        waitForElementAndClick(By.xpath("//*[@text='Object-oriented programming language']"),
                "cannot find search java input",
                10

        );
        waitForElementPresent(
                By.id("pcs-edit-section-title-description"),
                "cannot find article title",
                15
        );
        waitForElementAndClick(By.xpath("//android.widget.TextView[@text='Save']"),
                "cannot find button to open article options",
                5);
        waitForElementAndClick(By.xpath("//*[@resource-id='org.wikipedia:id/snackbar_action'][@text='ADD TO LIST']"),
                "cannot find button Add to list",
                5);

        waitForElementAndSendKeys(By.id("org.wikipedia:id/textinput_placeholder"),
                "My first list",
                "cannot find element org.wikipedia:id/textinput_placeholder",
                5);
        waitForElementAndClick(By.id("android:id/button1"),
                "cannot find element android:id/button1",
                5) ;
        waitForElementAndClick(By.xpath(
                "//android.widget.ImageButton[@content-desc='Navigate up']"),
                "cannot find Navigate up",
                5);
        waitForElementAndClick(By.xpath(
                "//android.widget.ImageView[@content-desc='Clear query']"),
                "cannot find clear query",
                5);
        waitForElementAndClick(By.id(
                "org.wikipedia:id/recent_searches_delete_button"),
                "cannot find clear query",
                5);
        waitForElementAndClick(By.xpath("//*[@text='YES']"),
                "cannot find element YES",
                5);
        waitForElementAndClick(By.xpath("//*[@class='android.widget.ImageButton']"),
                "cannot find android.widget.ImageButton",
                5);

        waitForElementAndClick(By.xpath(
                "//*[@resource-id='org.wikipedia:id/navigation_bar_item_small_label_view'][@text='Saved']"),
                "cannot find button to open article  saveD",
                10);
        waitForElementAndClick(By.xpath("//*[@resource-id='org.wikipedia:id/item_title'][@text='My first list']"),
     "cannot find My first list",
     5);

        waitForElementPresent(By.xpath(
                "//*[@resource-id='org.wikipedia:id/page_list_item_title'][@text='Java (programming language)']"),
                "cannot find list Java (programming language) ",
                10);
        swipeElementToLeft(By.xpath(
                "//*[@text='Java (programming language)']"),
                "cannot swipe Java (programming language) ");
        waitForElementNotPresent(By.xpath(
                "//*[@text='Java (programming language)']"),
                "cannot delete save Java (programming language) ",
                5);
      
    }


    private WebElement waitForElementPresent(By by, String error_message, long timeoutInSeconds) {
        WebDriverWait wait = new WebDriverWait(driver, timeoutInSeconds);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.presenceOfElementLocated(by)
        );
    }

    private WebElement waitForElementPresent(By by, String error_message) {

        return waitForElementPresent(by, error_message, 5
        );
    }

    private WebElement waitForElementAndClick(By by, String error_message, long timeoutInSeconds) {
        WebElement element = waitForElementPresent(by, error_message, timeoutInSeconds);
        element.click();

        return element;

    }

    private WebElement waitForElementAndSendKeys(By by, String value, String error_message, long timeoutInSeconds) {
        WebElement element = waitForElementPresent(by, error_message, timeoutInSeconds);
        element.sendKeys(value);

        return element;

    }

    private boolean waitForElementNotPresent(By by, String error_message, long timeoutInSeconds) {
        WebDriverWait wait = new WebDriverWait(driver, timeoutInSeconds);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.invisibilityOfElementLocated(by)
        );
    }

    private WebElement waitForElementAndClear(By by, String error_message, long timeoutInSeconds) {
        WebElement element = waitForElementPresent(by, error_message, timeoutInSeconds);
        element.clear();
        return element;
    }

    private boolean assertElementHasText(By by, String expected_text, String error_message) {
        WebDriverWait wait = new WebDriverWait(driver, 5);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.textToBePresentInElementLocated(by, expected_text)
        );
    }

    private boolean assertElementHasValue(By by, String value, String error_message) {
        WebDriverWait wait = new WebDriverWait(driver, 5);
        wait.withMessage(error_message + "\n");

        return wait.until(
                ExpectedConditions.textToBePresentInElementLocated(by, value)
        );

    }

   

    protected void SwipeUp(int timeofSwipe) {
        TouchAction action = new TouchAction(driver);
        Dimension size = driver.manage().window().getSize();
        int x = size.width / 2;
        int start_y = (int) (size.height * 0.8);
        int end_y = (int) (size.height * 0.2);
        action
                .press(x, start_y)
                .waitAction(timeofSwipe)
                .moveTo(x, end_y)
                .release()
                .perform();
    }

    protected void SwipeUpQuick() {
        SwipeUp(200);
    }

    protected void SwipeUpFindElement(By by, String error_message, int max_swipes) {
        int all_swipes=0;
        while (driver.findElements(by).size() == 0) {
            if(all_swipes>max_swipes){
                waitForElementPresent(by,"not find element by swiping up.\n"+error_message,0);
                return;

            }
            SwipeUpQuick();
            ++all_swipes;
        }




    }
    protected void swipeElementToLeft(By by,String error_message)
    {
        WebElement element=waitForElementPresent(
                by,
                error_message,
                10
        );
        int left_x=element.getLocation().getX();
        int right_x=left_x+element.getSize().getWidth();
        int upper_y= element.getLocation().getY();
        int lower_y=upper_y+element.getSize().getHeight();
        int middle_y=(upper_y+lower_y)/2;

        TouchAction action=new TouchAction(driver);
        action
                .press(right_x,middle_y)
                .waitAction(500)
                .moveTo(left_x,middle_y)
                .release()
                .perform();
    }
}