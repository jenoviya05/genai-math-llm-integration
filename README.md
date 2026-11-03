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
~~~
%pip install openai==0.28.1 python-dotenv

import os
import openai
import json
import math
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv())
openai.api_key = os.environ["OPENAI_API_KEY"]
print("Libraries imported successfully!")

def calculate_cylinder_volume(radius, height):
"""Calculate the volume of a cylinder."""
volume = math.pi * radius ** 2 * height
result = {
"radius": radius,
"height": height,
"volume": round(volume, 2)
    }
return json.dumps(result)
print(calculate_cylinder_volume(5, 16))

functions = [
    {
      "name": "calculate_cylinder_volume",
      "description": "Calculate the volume of a cylinder",
      "parameters": {
      "type": "object",
      "properties": {
      "radius": {
      "type": "number",
      "description": "Radius of the cylinder"
                      },
      "height": {
      "type": "number",
      "description": "Height of the cylinder"
                      }
                  },
      "required": ["radius", "height"]
              }
          }
]

messages = [
    {
      "role": "user",
      "content": "Calculate the volume of a cylinder with radius 5 and height 16"
    }
]
print(messages)

response = openai.ChatCompletion.create(
    model="gpt-4o-mini",
    messages=messages,
    functions=functions,
    function_call="auto"
)
 
print(response)

response_message = response["choices"][0]["message"]
 
print(response_message)

args = json.loads(
    response_message["function_call"]["arguments"]
)
 
print(args)

result = calculate_cylinder_volume(
args["radius"],
args["height"]
)
print(result)

messages.append(response_message)
messages.append({
"role": "function",
"name": "calculate_cylinder_volume",
"content": result
})
final_response = openai.ChatCompletion.create(
model="gpt-4o-mini",
messages=messages
)
print(final_response["choices"][0]["message"]["content"])

~~~


### OUTPUT:

<img width="963" height="712" alt="Screenshot 2026-11-03 161759" src="https://github.com/user-attachments/assets/ddc6b2e6-c618-408d-8c6e-752ea81ae0e8" />

<img width="886" height="340" alt="Screenshot 2026-11-03 161810" src="https://github.com/user-attachments/assets/46a27471-7a4d-41b8-81e3-3211fc00aa26" />

<img width="865" height="377" alt="Screenshot 2026-11-03 161823" src="https://github.com/user-attachments/assets/281b316f-bac8-4162-ac5d-29524f2ae122" />

<img width="895" height="717" alt="Screenshot 2026-11-03 161836" src="https://github.com/user-attachments/assets/c930ccf9-2337-494d-b516-8df7d15dc909" />

<img width="882" height="832" alt="Screenshot 2026-11-03 161917" src="https://github.com/user-attachments/assets/f2d96e95-696a-4229-a5f9-818679ab35e8" />

<img width="855" height="517" alt="Screenshot 2026-11-03 161927" src="https://github.com/user-attachments/assets/f70cc63c-8692-41b5-b46e-1a1321672380" />

<img width="902" height="592" alt="Screenshot 2026-11-03 161937" src="https://github.com/user-attachments/assets/84a0ed30-5264-4b6c-9f42-d236a740d87e" />


### RESULT:
Thus, the cylinder volume calculation was successfully implemented in Python and integrated with an LLM using function calling.
