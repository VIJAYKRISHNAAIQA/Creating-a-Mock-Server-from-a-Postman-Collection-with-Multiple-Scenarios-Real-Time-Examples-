- **Creating a Mock Server from a Postman Collection with Multiple Scenarios (Real-Time Examples)**

**Mocking APIs in Postman** allows you to create simulated versions of real APIs for development and testing. This guide will show you how to create a Mock Server from a Postman collection and define various scenarios using real-time examples.

**Prerequisites:**
- Postman application installed

**Steps:**

1. **Build your Postman Collection:**
    - Start by creating a collection in Postman that represents the API you want to mock.
    - Add requests for different functionalities of the API, including details like:
        - Method: (GET, POST, PUT, etc.)
        - URL: The endpoint you want to target
        - Headers: Any required headers (e.g., authorization tokens)
        - Body: Request body data (if applicable)

2. **Capture Sample Responses (Optional):**
    - If you have access to a real API, send the requests and capture the responses. These will serve as a reference for your mocks.

3. **Create a Mock Server:**
    - In the Collections sidebar, select the three dots next to your collection and choose "Mock Collection."
    - Give your Mock Server a descriptive name and click "Create Mock Server."

4. **Configure Individual Mocks for Different Scenarios:**

    **Scenario 1: Mocked GET Request for a Product List (Success)**
    - In the "Mock" tab of your collection (or Mock Server), click "Create Mock."
    - Configure the mock details:
        - Method: Select "GET"
        - Path: Define the path for the product list endpoint (e.g., "/products")
        - Match: Choose "Exactly" for an exact match
    - Assign a Response Example:
        - Click "Save as Example" in the "Response" section.
        - Create a response body with sample product data in JSON format (e.g., product IDs, names, prices).
        - Name the example "product_list_success".
        - Select this example in the "Response" section.
    - Enable the Mock: Toggle the switch next to your mock to activate it.

    **Scenario 2: Mocked GET Request for a Specific Product (Success)**
    - Create another mock for a GET request to retrieve a specific product by ID.
    - Method: Select "GET"
    - Path: Define the path with a wildcard for the product ID (e.g., "/products/:id").
    - Match: Choose "Glob Pattern" for a flexible URL match.
    - Assign a Response Example:
        - Create a new example with sample data for a single product (e.g., "product_details_success").
        - Use environment variables to represent dynamic data like the product ID in the response body. You can access environment variables with double curly braces (e.g., {{ProductID}}).
    - Enable the Mock: Activate the switch for this mock as well.

    **Scenario 3: Mocked GET Request for a Non-Existent Product (Error)**
    - Create another mock to simulate an error for a non-existent product.
    - Method: Select "GET"
    - Path: Use the same path with the wildcard for the product ID (e.g., "/products/:id").
    - Match: Choose "Glob Pattern".
    - Customize Response:
        - Instead of an example, define a custom response directly in the editor.
        - Set the status code to an error code (e.g., 404 Not Found).
        - Include an error message in the response body (e.g., "Product not found").
    - Enable the Mock: Activate the switch for this error scenario mock.

5. **Test Your Mock Server:**
    - In a separate Postman tab, create requests that match the paths defined in your mocks.
    - Send the requests. Postman should return the corresponding mock responses you configured for each scenario (success responses, product details with dynamic IDs, and the error message for a non-existent product).

**Additional Tips:**
- Use environment variables to manage sensitive data like API keys within your mock responses.
- Leverage Postman scripting with JavaScript for more complex scenarios where you need to manipulate data or conditionally generate responses based on request parameters.
- Create additional mocks for different functionalities of your API, like user login, adding products to a cart, etc., following the same principles.

By following these steps and exploring the various configuration options, you can effectively create a Mock Server.

- **Configuring Mocks for Different Scenarios:**

    1. **Mock 1: GET /products (Success):**
        - Method: GET
        - Path: /products (Exactly match)
        - Response: Select the "products_list" example containing the list of products.

    2. **Mock 2: GET /products/:id (Success):**
        - Method: GET
        - Path: /products/:id (Exactly match) - This allows mocking responses for any product ID.
        - Response: Select the "product_details_success" example containing a single product object. Note: You can't dynamically insert the ID into the response path using mocks, but you can access it within the response body using environment variables (explained later).

    3. **Mock 3: GET /products/:id (Error):**
        - Method: GET
        - Path: /products/:id (Exactly match)
        - Response: Select the "product_details_error" example with the error code and message for a non-existent product.

- **Adding Complexity with Environment Variables:**

    - To dynamically insert the product ID into the response body for successful retrieval (Mock 2), you can leverage environment variables.
        1. Go to the Environments tab and create a new environment (or use an existing one).
        2. Define a variable named productId with a sample value (e.g., "123").
        3. In the "product_details_success" example body, access the environment variable using double curly braces: {id: {{ environment.productId }}}. This dynamically replaces the placeholder with the actual product ID from the environment variable.


