## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:

To develop a Python program that calculates the volume of a cylinder using its radius and height, and integrates the function with an LLM chat completion system. The LLM identifies the required parameters from the user's query, calls the appropriate function, and returns the calculated volume as output.

### DESIGN STEPS:

#### STEP 1: Define the Python Function
- Import the required Python libraries, such as math and json.
- Define a function named calculate_cylinder_volume() that accepts the radius and height of the cylinder.
- Calculate the volume using the formula for a cylinder.
- Return the radius, height, and calculated volume as a JSON-formatted result.

#### STEP 2: Define the Function-Calling Schema
- Define the function name, description, and parameters.
- Specify radius and height as numeric inputs.
- Mark both parameters as required.
- Provide the function schema to the LLM so it can identify when to call the Python function based on the user's query.

#### STEP 3: Integrate with the Chat Completion System
- Send the user's message and function schema to the LLM using the chat completion API.
- Allow the LLM to identify the function call and extract the required arguments.
- Execute the Python function using those arguments.
- Return the calculated volume to the user through the chat completion system.

### PROGRAM:

### OUTPUT:

### RESULT:
Thus, the cylinder volume calculation was successfully implemented in Python and integrated with an LLM using function calling.
