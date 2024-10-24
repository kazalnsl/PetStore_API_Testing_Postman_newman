# A Comprehensive Guide to Using Postman for API Testing (With Pet-store Examples)



![Postman displayed on computer screen](https://www.testdevlab.com/_next/image?url=https%3A%2F%2Fcms.testdevlab.com%2Fcontent%2Fimages%2F2023%2F02%2Fimage5-9.jpg&w=3840&q=75)

There are many useful libraries, like [REST assured](https://www.testdevlab.com/blog/an-introduction-to-testing-apis-using-rest-assured) which is a Java-based library, that can be used to automate API testing. These contain a few code snippets that can be reused in test cases. Although they’re very useful for automation engineers, there is another tool that can help you better understand API testing without having to know a programming language. [Postman](https://www.postman.com/api-platform/api-testing/) is an API testing tool that allows you to perform comprehensive testing faster. It offers:

- a simple user interface where each integral part of the API lifecycle can be easily visualized and understood.
- pre-built code snippets that can be used for verifying tests or for generating test data used in tests.
- a wide range of options, for example, testing on different environments, testing on different servers, documentation of the API, collaboration and sharing the API with teammates or with the world.

My aim in the blog post is to introduce Postman as a useful tool for API semi-automated testing. I will provide screenshots of practical examples in Postman using a test API. I assume that you’re already familiar with the API concept and understand the basics. If not, then I highly recommend reading one of my previous articles—[Understanding APIs: Simplified Guide for Beginners](https://www.testdevlab.com/blog/understanding-apis-simplified-guide-for-beginners), before proceeding with this one.

## What is Postman?

Abhinav Asthana, a software engineer who wanted to simplify API testing, started Postman as a side project in 2012. Postman is an API platform for engineers to design, build, and test their APIs. It simplifies each step of the API lifecycle and streamlines collaboration. As a result, teams in an organization can create better APIs in an easier and faster manner.

At its core, Postman allows users to easily store, catalog, and collaborate around all API artifacts on one central platform. Postman can store and manage API specifications, documentation, workflow recipes, test cases and results, metrics, and everything else related to APIs. Postman has over 20 million registered users as of today.

## Postman installation and user registration

Postman can be downloaded from [here](https://www.postman.com/downloads/). You should be able to select the correct operating system. If you’re using macOS, make sure to download Postman for the correct chip under which your laptop is running.

If you don’t want to install the app, Postman offers a [web version](https://go.postman.co/home) as well, but to access it you have to [create a Postman account](https://identity.getpostman.com/signup?continue=https%3A%2F%2Fgo.postman.co%2Fhome&_ga=2.206592400.2072758458.1669900429-2082066344.1669900429) first—if you don’t have one already.

To use the desktop app, you don’t have to be a registered user, however, not all features will be available.

## Getting started with Postman

Postman’s central view is the **workspace** where all the things we’re going to use are positioned. Workspaces help us organize our API work and collaborate with teams across the organization. Inside our workspace we can access collections, environments, mock servers, monitors and other Postman features. **Collection** is a group of saved API requests, while **environments** is a set of variables that we can use in the requests.

![Workspace, the overview screen of Postman](https://cms.testdevlab.com/content/images/2023/02/image16.png)Workspace - the overview screen of Postman

## How to structure a collection in Postman

As mentioned above, we group all API requests in a collection, but we also group our API tests in a collection. This means that the collection is a root folder of our project. Inside it we can organize our work in folders and subfolders. It is up to you to decide how you would like to structure the collection, however, the most common practice is that:

- Folders are created for every endpoint. The name of the folder is usually the name of the endpoint.
- An *Integration tests* folder can also be created where we can place API tests that test the connection between different API endpoints. Namely, when we want to chain multiple API requests to test, for example, if the data in one endpoint is present in the other related endpoint.

![Postman collection structure](https://cms.testdevlab.com/content/images/2023/02/image15.png)Postman collection structure

## Practical examples using Postman

I will use the [Petstore API](https://petstore.swagger.io/) from Swagger for the examples. I’d also like to encourage you to take the time to explore the documentation, if available, for every API you use. Exploring the documentation will give you a clear overview of the API, what is expected in each request, and what response you will receive for it. The documentation for Petstore API is available [here](https://petstore.swagger.io/).

![Exploring Petstore API documentation](https://lh5.googleusercontent.com/ZBti-pPicsKWBcKVQZt1tCWfYxM_pATPtYo3ZAczgVopX38NFw3R3NKXfW1rp8saii9rc55BEXvOm4zWSFeH-JBai-d4AOjjp9q-dBwhpuBLxRe-peDr-JYaK_vFfo3LUBsJb9N9MmuQQnupt0ELcu8)Exploring Petstore API documentation

In the documentation, the base URL of the API is written as: petstore.swagger.io/v2. Since the base URL is the same for every API request, it makes sense that we store it as a variable in our collection so that we can reuse it. To do that, follow these steps:

- Select the collection in **“Collections”** tab.
- In the collection’s view, select **“Variables”** tab.
- Populate “**Variable name**”, **“Initial value”** and **“Current value”** columns with respective values: *baseUrl* and *https://petstore.swagger.io/v2*.

![Create collection variable](https://lh3.googleusercontent.com/VkgUErIzxAHGEO1kHCcAAGxRJm0sJaG_ZlLuE0mf7nlFyhWvJ3bBQQxXgd1COLgJB9q8yYLDlurdDtbaI_Tsh1NhxqiVMyw_XsbJhoAvkoZLg6A8mblu8yL7dPjGFn3DuD9p7rQMyHHPyQYkq54JxVs)Create collection variable

### Create GET request and test for it

The first request we’re going to create in Postman is the GET request for finding pets by status. The endpoint for this request is */pet* and the request parameter is */findByStatus*. We can also observe from the documentation that this request requires a **status** query parameter and the values for the status that are accepted are: **available**, **pending** and **sold**.

![Documentation of /pet/findByStatus API request](https://lh4.googleusercontent.com/udRqli5burY_5qWQ_06LlyOJILCLGqzITOsBv23Y2VG_04CVRJjZA8Kf0zhlP90gDm5BDfaTc00khyn2lDL60qZsGsmM3nUZmNm61ZD3lWpO2FA4zI-o_aBxG-u9-2lqMTR6JXVz43SWDdfo8Hv4JX8)Documentation of /pet/findByStatus API request

To add the request in Postman, follow these steps:

- Right click on the collection in the **“Collections”** tab.
- Choose the **“Add folder”** option. Name the folder **“pet”** because we will place all requests for */pet* endpoint in this folder.
- Right click on the **“pet”** folder and choose the **“Add request”** option.
- The request view will be displayed. We should populate all the required information for the request here. For now, we will set just a name for the request.

![Adding a folder and request in Postman](https://lh3.googleusercontent.com/XOnW15NxqB17yDsxyFaa9QjgSEyl03bFgW2lWW507iUueIEhcvPcoTz247WhUDsqTWvh06czf3mpFkAtv2T5H4LVMNW6JtfQMd0RO8NCktEXWXj0C5O5ijbeq5FJC5tog_G6USX1nm_7KBayoK5SMtc)Adding a folder and request in Postman

GET is already set as the default option in the drop down for request method, therefore we don’t need to change it. We should enter the request URL, here we will insert *{{baseUrl}}/pet/findByStatus*. If you remember, we’ve already added *baseUrl* as a collection variable, so we can use its value by wrapping the variable name in curly brackets. This way, we don’t need to specify the full URL in every request. Under the **“Params”** tab, we can enter query parameters. For our request, we need to enter the **“status”** query parameter and any accepted status as value. We can use **“available”** as a status value for this example.

Now that we have entered all necessary data, we can hit the **“Send”** button to send the request and observe the response we receive from the server. The response is received in the **“Response”** section at the bottom of the view. The data is received in JSON format, and we can easily observe all the information of available pets, like name, photo URLs, categories, etc.

![Sending GET request in Postman and observing the response](https://lh3.googleusercontent.com/5mw9pDaXBJpvywxG4dnbYCm60ybob01eTiNelOVB3nV9aucpR1ijpuarFvIKZIGLC05cdG8NlutfK_zTr4ipeJOSDcoZotPMFihxC1wYxLplt_YefRE2s8VZfWJR-8QUgjOg80tThFbLnyV4w8vq0lQ)Sending GET request in Postman and observing the response

The next step is to add tests for the response we received. We want to test if we received a successful response (status code is 200) and if the data in the response body contains a pet with the name “doggie”. Tests can be added under the **“Tests”** tab. On the right side, next to the input field, we already have predefined JavaScript code snippets for most common test cases. Scroll down a bit, and look out for the snippets with names: **“Status code: Code is 200”** and **“Response body: JSON value check”**. These snippets can be used for our test cases. If you’re familiar with JavaScript, you can add more code here and test the response more thoroughly.

For our simple test we will modify the second code snippet, so that from the list of all available pets we will check if the first pet has the name “doggie”.

```postman
pm.test("First pet check name", function () {
   var jsonData = pm.response.json();
   pm.expect(jsonData[0].name).to.eql("doggie");
});
```

To run the tests, we have to send the request again. Test results will be available in the **“Response”** section under the **“Test Results”** tab. If you click on this tab, you can easily check which tests passed or if some tests failed.

![Adding and executing tests, and observing test results](https://lh5.googleusercontent.com/f5VP2MItoKYGUUF40h7JbzxRi53GZlnefpW-6I5jUElyErvmw_KdQJeWiB0G_TOo2NQIM0xNcA-mrlrRwj578Z4LzLbc6XnCqwY6lFG5vm-Cq2KzwnHFgm7RAnGUzca7O0TQ4F6MpuLK_XrHZVqD8WY)Adding and executing tests, and observing test results

Our second test case will fail sometimes because every time the request is sent, the API responds with available pets at that particular time. This means that “doggie” may not be available the next time we send the request and that’s why the test might fail. We should design our test cases to be better than the simple example above, they should always be consistent with the end use case we want to check and with the API state.

![Screen displaying test results](https://lh3.googleusercontent.com/EN1568BBfJXxLWiB1Gbjk3wVlT5Uw942N6TCEhWfmOO8tIySxEyXc7QQLUgr5damzFo1MY4LCyXELSDkSQ_RB9lDS-1zFasPwGYEySz6WCgQQ7Y_KN9_KG5Q8XXZp0mBGJc8yqK7mIbY216tsBlKpwg)Test might fail if you run it again after some time has passed

We can also check and test what happens when we pass invalid status value. The documentation states that in this case we should receive the 400 response status code. We can add this example in our request, also we can test this expectation. We can duplicate our existing request by right clicking on it and choosing the **“Duplicate”** option.

![Adding a duplicate request](https://lh3.googleusercontent.com/733L7gCxxBzLzBZ1iUBaSY7RSTdrm2laomzQ2WAhRk-XEss7L4FVQhw4u3x05yr125YaF_ye-BbohP8-CnZCuLJs0pHmAyRSSGk1RIiYJZCGikopsJ_Kd0TpbCncfpZJfrai6fz7Labs4DYiby4_NQ)Adding a duplicate request

We set a new name for the request so that we distinguish that it is for an invalid status code. Also, we modify the value of the “status” query parameter and add an arbitrary value. In the tests, we remove the second test case because we don’t need it for this request, but we also modify the first test case to check if we receive the 400 response status code.

```postman
pm.test("Status code is 400", function () {
   pm.response.to.have.status(400);
});
```

If we send the request, the test should pass.

### Create POST request and test for it

How about we add a new pet with the name Dogo to the pet store? For this we can use the POST request, which is the only request that changes the server by adding a new object. From the documentation, we can see that the endpoint for adding a new pet is just **/pet** without any request parameter. A request body is mandatory, as is with every POST request. We can see from the documentation that the body should be given in JSON format and the required data that should be provided is pet’s **name** and **photoUrls**.

![Documentation of POST /pet API request](https://lh6.googleusercontent.com/y9XGS__Evzu0d5X4ECsJFtaerex0ksk23jstLLME_uJ89k933xrFD11UWskyl1wN7s-ITKwOuTksWtQ7SVFq7TmtmhnFrpDTqxlCjneSMp1Kacy579y5Z2qDKyffjgvqwZt3-SVRPypfeBHU26p_pIo)Documentation of POST /pet API request

Similarly, as we did with the GET request, we will add the POST request under the **“pet” folder**:

- Select **“POST”** from the drop down menu.
- Enter *{{baseUrl}}/pet* in the request URL input field.
- Select the **“Body”** tab below the request URL input field to add the JSON request body.
- Choose the **“raw”** option and select **JSON** from the last drop down view in the row.
- In the input field below the body format options, we should enter the following body:

```postman
{
 "name": "Dogo",
 "photoUrls": [
   "https://www.akc.org/wp-content/uploads/2017/11/Dogo-puppy.jpg"
 ]
}
```



![Adding POST request in Postman](https://lh6.googleusercontent.com/u2aUTAHXEe0g2HsTvumph2zhqVJ8uGPPd4nvMLRHjRgBe9AuKrqX0WlVCFEmgH9QD4nkMbE3NY6u99pDKkUe2z9yQZnbBKsqwt514lCpPP_gl5jSz0zCz6ZafnJ_Dp5PVKCf4kUQPGp6HdElcAzql2s)Adding POST request in Postman

If we execute this request by pressing the **“Send”** button, we should receive a successful response. The response should contain data we already provided with additional information, like ID.

![The response from the request](https://lh3.googleusercontent.com/jx_UI93Vp2umBWmWc_oBqI_s-kRs6WiCP3T9D7D92tKUe6Nqvd6d54_kyspvq0QNPeXcr0jaILJgIV2E77OVSwIKX-hRPT4FN7eRL0u1X2pPeyMDxyFHWwFgjPL-gv5y7m0w4wWka9-kRMdccHGvfTk)The response from the request

It's fairly simple to construct a test for this response, we want to make sure that the added pet is indeed with the name Dogo and with the correct photo URL. Similarly as with the GET request, we can use already existing snippets for checking the response status code and values from the JSON response. Our tests should look like this:

```postman
pm.test("Status code is 200", function () {
   pm.response.to.have.status(200);
});
pm.test("New pet response check", function () {
   var jsonData = pm.response.json();
   pm.expect(jsonData.name).to.eql("Dogo");
pm.expect(jsonData.photoUrls[0]).to.eql("https://www.akc.org/wp-content/uploads/2017/11/Dogo-puppy.jpg");
});
```

If we run the tests, they should pass.

![Test results for adding new pet request](https://lh4.googleusercontent.com/W7sQLvy6zfpqcBrBD1pzd5tEB9fPJLsXTEy-X4RWjWNZdPecBATJdbM4YGHSdpuCMfp3X8-Z_qnxxdUAH7GZmxukGw8BBvyltrxGMdnQkBaqV3v-h4itoX3nCFdkqt-VqMtzb2LXIanf6cstFdr2XeU)Test results for adding new pet request

We can also play around with the request body and try to send invalid data or data without mandatory values. It’s recommended to construct tests with expected response codes, trying to cover as many negative and positive scenarios as possible.

### Create PUT request and test for it

What if you want to change the name of your pet and update the status to sold? We know that the PUT request can modify the server so that an existing object can be updated with new data. But from all the pets in the store, how will the server know which one is your pet? If you observe the response from above closely, where we added the pet to the store with the POST request, you’ll notice that there is an ID in the data. This ID is the identification of the pet whose data we want to update. We can use this ID in our request for updating the name of our pet and the status. However, it’s not optimal to copy and paste the ID. We want this ID to be stored as a variable and then used in our update request. Luckily, Postman allows us to store data from responses as variables too, just like we stored the base URL in collection variables. Let’s store the ID of the previously created pet. In Postman, follow these steps:

- Open the POST request you created previously.
- Go to the **“Tests”** tab.
- From the snippets on the right, choose the one with the name **“Set a collection variable”**.
- The snippet should be copied at the end of the test. Move the snippet in **“New pet response check”** test and modify it like so:

```postman
pm.collectionVariables.set("petId", jsonData.id);
```

- Run the tests again. This is important so that with the new code snippet, the ID can be saved to collection variables.

You can check if your ID is stored by clicking on the collection, then selecting the **“Variables”** tab. The *petId* variable should be listed below the *baseUrl* variable.

![petId saved as collection variable after test execution of adding new pet](https://lh6.googleusercontent.com/JYKXKN93qWZePce2g3Wzu1jJoPFWUMowWKKRsQVrDLhzIC17PyWz3jVNu1WRDAw9UB_b2IzCv9EdE7Lm0RRHkLMxg57c4ze-MfYoFWYkn6RvgekHiravJ1iu_ZjwM2fJ7cSbSxpSSI-wxjJ2OmpxjtY)petId saved as collection variable after test execution of adding new pet

Now that we have the identification of our pet we can update the name and status with the PUT request. From the documentation, we can see that everything is the same as with the POST request, the only difference is in the request method. Repeat the same steps as with the POST request, but make sure to select **“PUT”** from the drop down menu for the request method and send the following request body:

```postman
{
"id": {{petId}},
"name": "Lucky",
"status": "sold"
}
```

We wrapped our saved pet ID with curly brackets in the request body. The created request in Postman should like this:

![PUT request to update the data of our pet](https://lh5.googleusercontent.com/ToyH4kxGhqUsxTEcuk1P1SzXol_reDyF9n2I6iAo3aNq-56f1MImQMowo3Z5InClwlLC5tViqp4lrW67yH51_6W-R2Gbo6AUck9VJmhJMjQ3K9EC86sJ-WmZCKYqwob5_3cVVrVY2Sd-S_vw3AAjY8I)PUT request to update the data of our pet

Run the request and observe the response. New data should be visible in the response.

![The response of the PUT request](https://lh5.googleusercontent.com/VKCUaWGw3z8Si75DZImK7_MsZpqFZyw-ucVFlis_OD2Si2fHMXDOeZyDU6fAxDR-YdWdlFwwZlfz77Sbb79Hqlpetf3fKKSt_w3vjG0oUBQoywA3uU333wURykcBiz0PvNwj9L_JX0NyqvQI1UiZimA)The response of the PUT request

We can add similar tests as with the POST request to check if the pet’s name and status are updated. The tests should look like this:

```postman
pm.test("Status code is 200", function () {
   pm.response.to.have.status(200);
});
pm.test("Pet update check", function () {
   var jsonData = pm.response.json();
   pm.expect(jsonData.name).to.eql("Lucky");
   pm.expect(jsonData.status).to.eql("sold");
});
```

When we run the tests, they should pass.

### Create DELETE request and test for it

Now, let’s imagine that the pet store has sold the dog Lucky and he is now happily living with me. I can safely delete the data of my pet from the server by using the DELETE request. The documentation states that the pet ID should be provided as a request parameter to the endpoint.

![Documentation of DELETE /pet API request](https://lh5.googleusercontent.com/J6YTNJ1jCg7XmtbJ91ETsF-sO58mC4Qzb4-AF28A8CYzeArhaE6pY5mxHesxukxiH-EYD_bndoNt1PmjiqF1xk63hhlTHa5y2xJQ8xKdmQBj7yZxPV1XlvjMfBzCGiKR4TG7YFkcRonSxpiE0itp5gk)Documentation of DELETE /pet API request

We already have the ID stored in the collection variables, therefore we can use it for the DELETE request as well by wrapping it in curly brackets in the request URL. Here is what the request in Postman should look like:

![DELETE request to delete the data of a pet](https://lh4.googleusercontent.com/KwS4Wx0dyudbmI5TY7ZZZ0XBthoSIuyCgKCkU1bAAr_uHvzKEB36uRorTYLkeb3f5jIi1EicPOHahsKmsX5KJ9P_1LNwC4Z8HLAa-hCBly2MA_sBRuZj_9FZugGRe9mSlIsshII13_UfqTTnmJqTrg)DELETE request to delete the data of a pet

Before executing this request with the “Send” button, we should add tests first. This is because the DELETE request tests are more informative than the response body we receive. We can add one test to check if we receive the successful response status code 200. However, we can also check if the pet is actually deleted by using the GET request with the */pet/{petId}* endpoint, which gives us information about a given pet with a specific ID.

For this request we should receive a 404 (not found) response status code because we previously deleted the pet with the stored ID and it should no longer exist. We can check this by sending the request in code via an already existing code snippet. This code snippet can be found under **“Send a request”** name. In the test, for this request, we expect that the response has a 404 (not found) status code, so it should look like this:

```postman
pm.test("Status code is 200", function () {
   pm.response.to.have.status(200);
});


pm.sendRequest(pm.variables.get("baseUrl")+"/pet/" + pm.variables.get("petId"), function (err, response) {
   pm.test('Get pet data after deletion', function() {
       pm.expect(response.code).to.eql(404)
   });
});
```

Now we can execute the request and observe test results. Tests should have passed.

![Test results for deleting a pet request](https://lh5.googleusercontent.com/kXKV56QIMWr_TrfPsMFJo6JEGQFewKqvJ6LJMPkkruQES_V7i5BsrAIr_MD8TlN9bswLiZCX2y4w_JaCfGEtrYBPh-cc2OIufwhugtKqkMP_18fM_Byc9mMkIRNXH6g-NlGgG2xGssRJX1qrDD7uIA)Test results for deleting a pet request

## Wrapping it up

We covered the four most commonly used API requests (GET, POST, PUT, DELETE), added them in Postman, looked at responses, added tests for expected data from responses and analyzed the results. From our example test cases using the Petstore API, we can agree that Postman is a really simple and user-friendly tool to use when exploring and testing APIs.

Specifically, using Postman for API testing has many benefits:

- It has a **user-friendly interface** that is easy to use.
- **APIs can be visualized better**, making them simpler to understand.
- Stored API requests in a collection can be **easily exported** and afterwards **shared with the whole team.**
- Its pre-built JavaScript code snippets are very **useful for people with little to no knowledge of programming languages** and enable them to build effective tests.
- Automation engineers can construct more advanced tests relatively easily and can **fully automate the whole API** by generating test data in pre-request scripts for each request, storing variables in collections and environments.
- **Authorization and authentication of APIs** is also possible and easy to use.
- The same tests for the API can be run in **different environments.**
- The API can be **documented** as well as easily **monitored.**

As we mentioned earlier, the tests that we performed here are really simple, but in the real world they should be more comprehensive, the data should be tested more thoroughly, and the use case scenarios should be followed more precisely. If you want to learn more about how to write tests in Postman you can read [Postman’s documentation for writing tests](https://learning.postman.com/docs/writing-scripts/test-scripts/). Furthermore, you can explore their [learning center](https://learning.postman.com/docs/getting-started/introduction/) to find out what other features they offer for API exploring and testing.

Have fun learning and working with Postman.

*Need help testing your API using Postman? We have a dedicated team of API experts with experience using various tools and technologies.* [*Contact us*](https://www.testdevlab.com/contact-us) *to learn more about our API testing services and how they can benefit your organization.*

- Tags:
- [API](https://www.testdevlab.com/blog/tag/api)
- [API testing](https://www.testdevlab.com/blog/tag/api-testing)
- [Postman](https://www.testdevlab.com/blog/tag/postman)
- [quality assurance](https://www.testdevlab.com/blog/tag/quality-assurance)
- [quality assurance engineer](https://www.testdevlab.com/blog/tag/quality-assurance-engineer)
- [software testing](https://www.testdevlab.com/blog/tag/software-testing)