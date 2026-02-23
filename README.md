## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:

### DESIGN STEPS:

#### STEP 1: Analyze the Python Function

#### STEP 2: Integrate LLM

#### STEP 3: Query Parsing

### STEP 4: Result

### PROGRAM:

### OUTPUT:
```py
import math
import os
from dotenv import load_dotenv, find_dotenv
import openai

_ = load_dotenv(find_dotenv())  
openai.api_key = os.environ['OPENAI_API_KEY']

def calculate_cylinder_volume(radius, height):

    if radius <= 0 or height <= 0:
        return "Radius and height must be positive numbers."
    
    volume = math.pi * (radius ** 2) * height
    return round(volume, 2)

def chat_with_openai(prompt):
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "You are an assistant that helps calculate the volume of a cylinder."},
            {"role": "user", "content": prompt},
        ],
        functions=[
            {
                "name": "calculate_cylinder_volume",
                "description": "Calculate the volume of a cylinder given radius and height.",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "radius": {"type": "number", "description": "Radius of the cylinder (in units)"},
                        "height": {"type": "number", "description": "Height of the cylinder (in units)"},
                    },
                    "required": ["radius", "height"],
                },
            }
        ],
        function_call="auto",  
    )
    
    if "function_call" in response["choices"][0]["message"]:
        function_name = response["choices"][0]["message"]["function_call"]["name"]
        arguments = eval(response["choices"][0]["message"]["function_call"]["arguments"])
        if function_name == "calculate_cylinder_volume":
            radius = arguments["radius"]
            height = arguments["height"]
            return calculate_cylinder_volume(radius, height)
    
    return response["choices"][0]["message"]["content"]


radius = float(input("Enter the radius of the cylinder: "))
height = float(input("Enter the height of the cylinder: "))

prompt = f"What is the volume of a cylinder with a radius of {radius} and a height of {height}?"
result = chat_with_openai(prompt)
print("Result:", result)

```
### RESULT:
<img width="437" height="105" alt="image" src="https://github.com/user-attachments/assets/5afb58a2-7ae0-4ee8-aa21-155edbdcb2ec" />

Thus, the program is executed successfully and got the desired output.
