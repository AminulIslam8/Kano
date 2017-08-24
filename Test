import org.junit.Assert;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.annotations.Test;
import java.util.List;

// You can take off the BaseTest as you will need to instantiate your own driver
public class Tests extends BaseTest {


    private static final String URL = "https://kano.me/";
    private static final String WORLD_URL = "https://world.kano.me/projects";

    // Please replace the browser with your own driver
    private Browser browser = DriverManager.getinstance();


    //Question 1
    @Test
    public void test_computer_kit_bundle_is_in_basket() {

        //GIVEN
        user_is_on_the_homepage(URL);

        //WHEN
        user_adds_a_computer_kit_bundle();

        //Then
        computer_kit_bundle_is_in_basket();
    }

    //Question 2
    @Test
    public void test_computer_kit_bundle_is_in_basket_in_another_country() {

        //GIVEN
        user_is_on_the_homepage(URL);

        //AND
        user_is_in_another_country();

        //WHEN
        user_adds_a_computer_kit_bundle();

        //Then
        computer_kit_bundle_is_in_basket();

    }

    //Question 3
    //Please note that this works only with firefox
    // Because of the shadow dom in the html
    // This has multiple lines of assertion, which is not the best way to structure our test
    // But for demo purposes this is the fastest way to write this.
    @Test
    public void test_header_and_footer_nav_items() {
        //GIVEN
        user_is_on_the_homepage(WORLD_URL);

        //WHEN
        String header_key = "kano-primary-links .nav-menu-items li";
        String footer_key = "div.stats .info p";
        final boolean world = user_verifies_nav_item(header_key, "World");
        final boolean make = user_verifies_nav_item(header_key, "Make");
        final boolean shop = user_verifies_nav_item(header_key, "Shop");
        final boolean connected_kanos = user_verifies_nav_item(footer_key, "Connected Kanos");
        final boolean online_today = user_verifies_nav_item(footer_key, "Online Today");
        final boolean lines_of_code = user_verifies_nav_item(footer_key, "Lines of code");


        //THEN
        Assert.assertTrue("World is not displayed on page", world);
        Assert.assertTrue("Make is not displayed on page", make);
        Assert.assertTrue("Shop is not displayed on page", shop);
        Assert.assertTrue("Connected Kanos is not displayed on page", connected_kanos);
        Assert.assertTrue("Lines of code is not displayed on page", lines_of_code);
        Assert.assertTrue("Online today is not displayed on page", online_today);
    }


    // Question 4
    /* After carefully studying question 4,
    I noticed that to be able to move the “Say” to the right side of the page to join the
    blocks, I may need to change the transform location.
    For example transform = “translate(255,157)” to transform = “translate(330,157)”.
    I did not go deeper into how I can insert this with selenium, but I think we can use
    the Action api for selenium to do this. I may be wrong.
*/


    private void user_is_on_the_homepage(String url) {
        browser.getDriver().get(url);
    }

    // I am not using page objects as this will be a lot of over head
    private void user_adds_a_computer_kit_bundle() {
        browser.getDriver().findElements(By.cssSelector("li.StickyHomeNav-item")).get(1).click();

        String buy_now_button = "BundleDisplay-actionPrimary--kano-complete";

        new WebDriverWait(browser.getDriver(), 30).until(ExpectedConditions.visibilityOfElementLocated(By.id(buy_now_button)));

        browser.getDriver().findElement(By.id(buy_now_button)).click();

    }

    private void computer_kit_bundle_is_in_basket() {
        new WebDriverWait(browser.getDriver(), 30).until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(".CartPage-title")));

        String actual_item_name = browser.getDriver().findElement(By.cssSelector(".CartPage-itemNameLink")).getText();

        String expected_item_name = "Computer Kit Bundle";

        Assert.assertEquals("Item Names do not match in Basket", expected_item_name, actual_item_name);
    }

    private void user_is_in_another_country() {
        browser.getDriver().findElement(By.id("region-pointer")).click();

        browser.getDriver().findElements(By.cssSelector("li.region.region--active.style-scope.kano-cart")).get(0).click();

        new WebDriverWait(browser.getDriver(), 30).until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(".LocationModal")));

        browser.getDriver().findElement(By.id("ButtonLink--127")).click();
    }


    private boolean user_verifies_nav_item(String key, String item) {
        final List<WebElement> menu_items_elements = browser.getDriver().findElements(By.cssSelector(key));

        for (WebElement menu_item : menu_items_elements) {
            if (menu_item.getText().equals(item)) {
                return true;
            }
        }
        return false;
    }
    
}
