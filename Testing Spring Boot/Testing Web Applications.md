### Scenario
- Given a controller, how do you test any given endpoint?
- For example:
	- How do you assert the endpoint was triggered?
	- How do you assert the form fields are bound correctly?
	- etc.
- Follows up on [[Integration Testing]]
### Using the Full Application Context
* `@SpringBootTest` by default starts up a mock server
* `@AutoConfigureMockMvc` can be used to setup the `MockMvc`
	* You can then autowire the `MockMvc` as a parameter in your test function
* Alternatively: 
	* `WebTestClient` exists as a test client for `WebClient`
	* You can autowire this as well after annotating the class with `@AutoConfigureWebTestClient`
		* This is for a a mocked environment (only for WebFlux??)
* From there, you can write the tests as normal
### Using only the Web Layer
#### About
* For context, read [[Slices]]
#### MVC
* Use `@WebMvcTest` instead for just testing the web layer/MVC functionality
* This auto configures `MockMvc`
* For example:
```
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.mockito.BDDMockito.given;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@WebMvcTest(UserVehicleController.class)
class MyControllerTests {

	@Autowired
	private MockMvc mvc;

	@MockBean
	private UserVehicleService userVehicleService;

	@Test
	void testExample() throws Exception {
		given(this.userVehicleService.getVehicleDetails("sboot"))
			.willReturn(new VehicleDetails("Honda", "Civic"));
		this.mvc.perform(get("/sboot/vehicle").accept(MediaType.TEXT_PLAIN))
			.andExpect(status().isOk())
			.andExpect(content().string("Honda Civic"));
	}

}
```
##### Web Browser Functionality
* Need to test how your web app works in a browser?
* `WebMvcTest` comes with HtmlUnit `WebClient` bean and a Selenium `WebDriver` bean
#### WebFlux
* The Webflux equivalent annotation is `@WebFluxTest`
* Auto configures `WebTestClient` by default