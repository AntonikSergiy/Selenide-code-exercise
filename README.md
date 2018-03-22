***Exercise 1***
___Clicking on an element___
1. Open www.website.com page
2. Find „Sign in” button by class/title/withText and click
3. Find „Create anAcount” button by text/class,index and click
4. Find „Women” button by title/class/text and click
5. Scroll to the last dress on the page and click

***Visibility and existence assertions:***
___Text assertions:___
```sh
$(element).check(condition);
$("#element").shouldHave(text("CHEEZBURGER"));				//case insensitive, partial match
$("selector").shouldHave(exactText("DOUble CHeezBurGer")); 		//case insensitive, exact match
$("selector").shouldHave(textCaseSensitive("Cheezburger")); 		//case sensitive, partial match
$("selector").shouldHave(exactTextCaseSensitive("Double Cheezburger")); //case sensitive, exact match
$("#input").shouldHave(exactValue("John"));
$("selector").should(matchText("[A..Z]eezburger"));  			//regexp
Html.text.containsCaseSensitive(source(), "Text pattern From Page Source");
```    
___Other assertions:___
```sh
$("h1").shouldHave(css("font-size", "16px"));
$$("#mytable tbody tr").shouldHave(size(2));
$("#input").shouldHave(name("fname"));
$("#input").shouldHave(value("John"));
$("#input").shouldHave(type("checkbox"));
$("#input").shouldHave(id("myForm"));
$("#input").shouldNotHave(text("Hello"), text("World"));
$("selector").shouldHave(attribute("layout","row")); //with value
$("selector").shouldNotHave(attribute("href")); //any value
$("selector").shouldHave(cssClass(".class"));
$("[type=button]").shouldHave(type("button"));
$("[type=button]").shouldNotHave(id("idselector"));
```
```sh
$$(".errors").shouldHave(size(2));
$$(".errors").shouldHave(exactTexts("text 1", "text 2"));
$$(".errors").shouldHave(texts("text 1", "text 2"));
```    
___Positive assertions:___
```sh
$("input").shouldBe(visible, enabled);     //visible | appear 	// Same as $("selector").shouldBe(visible);
$("input").shouldBe(exist);                //present | exist  
```
```sh
$("input").shouldBe(readonly); 
$("input").shouldBe(focused);
$(".errors").shouldBe(empty);
$$(".errors").shouldBe(empty);
$("#element").should(exist);
```
___Negative assertions:___
```sh
$("input").shouldBe(hidden);			//hidden | disappear | not(visible) // Same as $("selector").should(disappear);
$("input").shouldNotBe(visible, enabled);
$("selector").shouldNot(exist); 	//element should not exist in DOM
```

***Querying***
```sh
$("#element").isDisplayed();
$("#element").exists(); 
```
```sh
$$("#multirowTable tr").findBy(text("Norris"));
$$("#multirowTable tr").filterBy(text("Norris"));
$$("#multirowTable tr").excludeWith(text("Chack"));    
    
$$(“#employees tbody tr”)
	.filter(visible)
	.shouldHave(size(4));
```
___Search for parents/children___
```sh
$(“td”).parent()
$(“td”).closest(“tr”)
$(“.btn”).closest(“.modal”)
$(“div”).find(By.name(“q”))
```

***Wait***

___with text/value/attribute___
```sh
$("#welcome").waitUntil(hasText("Hello, Johny!"), 2000);
$("#username").waitUntil(hasAttribute("name", "user.name"), 2000);
$("#username").waitUntil(hasClass("green-button"), 2000);
$("#username").waitUntil(hasValue("123"), 2000);
$("#username").waitUntil(matchesText("Johny"), 2000);
$("#username").waitUntil(not(matchesText("Noname")), 2000);
$("#username").waitUntil(matchText("^Johny$"), 2000);
```

***with Conditions***
```sh
$("#username").waitUntil(present, 5000); //enabled, disabled, visible appears, disappears;
```

***Exercise 2***
___Assert that element is visible/appears=23___
1. Find „Women” menu element by title and hover over it
2. Check that Evening Dresses element is visible/appears
3. Click on Evening Dresses
4. Check that product category image has „Evening Dresses” text and does not have text „Casual dresses”

***Collections***
	$$(selector)

***Collections basics:***
***Collections are iterable SelenideElements:***
```sh
ElementsCollection collection = $$("div");
$$("selector"); 					// doesn't search anything!
```
***They use the same Selectors as in $:***
```sh
$$(withText(„eezburger"));
```
***Operations on Collections:***
___Choosing an element:___
```sh
$$("div").first();
$$("div").last();
$$("div").get(2);			// get third element, index from 0
$$("div").findBy(text("123")); 		// finds the first element
```

___Filtering:___
```sh
$$("div").filterBy(text("123"));	//only with text 123
$$("div").excludeWith(text("123"));	// all except with text 123
```
***Collection assertions:***
___Size assertion:___
```sh
$$("div").shouldBe(CollectionCondition.empty);
$$("div").shouldHave(size(5)); / or $$("div").shouldHaveSize(5);
$$("div").shouldHave(sizeGreaterThan(1));
$$("div").shouldHave(sizeGreaterThanOrEqual(1));
$$("div").shouldHave(sizeLessThan(100));
$$("div").shouldHave(sizeLessThanOrEqual(100));
$$("div").shouldHave(sizeNotEqual(1984));
```
___Text assertions (case sensitive):___
```sh
$$("div").shouldHave(texts(”kjlj", ”TTHT")); 			//partial matches of every single text
$$("div").shouldHave(exactTexts(”Here is your", ”Hamburger"));
```
___Operations returns:___
```sh
ElementsCollection collection = $$("div").filterBy(text("123")); 	// even when filters to a single element!
ElementsCollection collection2 = $$("div").filterBy(text("xyz")); 	// empty collection!
SelenideElement element = $$("div").get(2);
SelenideElement element2 = $$("div").find(text("xyz")); // null?
```
***Exercise 3***
1. Click on „Dresses” buton
2. Find collection of all dresses and filter them by text to find „Printed Summer Dress” .
Then use get(index) and click first element
3. Assert that there is the correct numer of colors available to choose for this dress

***Inputs, dropdowns and checkboxes***
___Inputs:___
```sh
$("#name").setValue(„Aleks");
$("#name").shouldHave(value(„Aleks"));
$("input[ng-model='user.company']").shouldBe(disabled);
$("input[ng-model='user.firstName']").shouldBe(enabled);
$("input[ng-model='user.firstName']").shouldBe(empty);
$("input[ng-model='user.company']").shouldHave(value("Goo")); //partial match
$("input[ng-model='user.company']").shouldHave(exactValue("Google"));
```
___Checkboxes:___
```sh
$("input[type=checkbox]").click();
$("input[type=checkbox]").shouldBe(checked);
```
or
```sh
$("input[type=checkbox]").setSelected(true);
$("input[type=checkbox]").shouldBe(checked);
$("input[type=checkbox]", 1).setSelected(false);
$("input[type=checkbox]", 1).shouldNotBe(checked);
```
***Dropdown menu:***
___Only standard HTML selects___
```sh
$("#dropdown").selectOption("Option 2"); 		//exact text match
$("#dropdown").selectOptionContainingText("ption 1"); 	//partial match
$("#dropdown").selectOption(3); 			//starting from 0, fourth option
$("#dropdown").selectOptionByValue("1");
$("#dropdown").getSelectedOption().shouldBe(disabled);
$("#dropdown").getSelectedOption().shouldHave(text("Option 1"), value("1"));
```
	
___What is NOT Page Object___
```sh
public class GoogleTest {
    @BeforeClass
    public static void setup() {
    Configuration.baseUrl = "http://google.com/ncr"
    }
	
	@Test
	public void userCanSearch() {
	open("/");
	$(By.name("q")).val("selenide").pressEnter();
	$$(".srg .g").shouldHave(size(10));
	$$(".srg .g").get(0).shouldHave(text("Selenide: concise UI tests in Java"));
	}
}
```

***POP Mid-level encapsulation***
```sh
public class GoogleTest {
    @BeforeClass
    public static void setup() {
    Configuration.baseUrl = "http://google.com/ncr"
    }

	@Test
	public void userCanSearch() {
	GooglePage google = new GooglePage();
	google.open().searchFor("selenide");
	google.results().shouldHave(size(10));
	google.results().get(0).shouldHave(text("Selenide: concise UI tests in Java"));
	}
}
```

***POP Mid-level encapsulation***
```sh
public class GoogleTest {
    @BeforeClass
    public static void setup() {
    Configuration.baseUrl = "http://google.com/ncr"
    }

	@Test
	public void userCanSearch() {
	GooglePage google = new GooglePage();
	google.open().searchFor("selenide");
	google.results().shouldHave(size(10));
	google.results().get(0).shouldHave(text("Selenide:concise UI tests in Java"));
	}
}
```

***POP higher-level encapsulation***
```sh
public class GoogleTest {
    GooglePage google = new GooglePage();
    SearchResults results = new SearchResults();

    @BeforeClass
    public static void setup() {
    Configuration.baseUrl = "http://google.com/ncr"}

	@Test
	public void userCanSearch() {
	GooglePage google = new GooglePage();
	google.open().searchFor("selenide");
	results.shouldHaveSize(10).shouldHaveResult(0, "Selenide: concise UI tests in Java");
	}
}
```

***POP higher-level encapsulation***
```sh
public class GooglePage {
	
    public GooglePage open() {
    Selenide.open("/");
    return this;
    }

	public SearchResults searchFor(String text) {
	$(By.name("q")).val(text).pressEnter();
	return new SearchResults();
	}
}
```

***POP higher-level encapsulation***
```sh
public class SearchResults {
   private final ElementsCollection elements = $$(".srg .g");
	
        public SearchResults shouldHaveSize(int size) {
	elements.shouldHaveSize(size);
	return this;
	}
	
	public SearchResults shouldHaveResult(int index, String text) {
	elements.shouldHave(text(text));
	return this;
	}
}
```
