### Web Integration Test
- `@WebIntegrationTest` will boot up an embedded servlet container
- You can issue real http requests, no need for a `MockMvc`
### Ports
- Runs on 8080, but if you set `server.port=0` it can run on a randomized port
- Ex: `@WebIntegrationTest("server.port=0")`
	- or use `randomPort=true`
- To get the port, inject it onto an instance variable
	- `@Value(${local.server.port})`
### Selenium
- Use selenium to spin up a web browser and see the contents of the page
- As close as possible to manual testing