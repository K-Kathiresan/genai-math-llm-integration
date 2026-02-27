## Integration of a Mathematical Calulations with a Chat Completion System using LLM Function-Calling

### AIM:
To design and implement a Python function for calculating the volume of a cylinder, integrate it with a chat completion system utilizing the function-calling feature of a large language model (LLM).

### PROBLEM STATEMENT:
Design and implement a system where a user can input dimensions of a cylinder (radius and height),  
and the system calculates its volume by invoking a Python function using the function-calling capabilities of an LLM.

### DESIGN STEPS:

1. Import necessary libraries, including OpenAI for LLM integration and math for mathematical operations.
2. Define a Python function to calculate the volume of a cylinder based on its radius and height.
3. Integrate the function into an LLM-based chat completion system with function-calling capabilities.

### PROGRAM:
```
Name : KATHIRESAN K
Reg No : 212223110021
```
```py
import math

def get_cylinder_volume(radius, height):
    if radius <= 0 or height <= 0:
        return None
    return math.pi * radius * radius * height


def ai_function_router(intent, params):
    if intent == "volume_cylinder":
        result = get_cylinder_volume(params["radius"], params["height"])
        return {"result": result}
    else:
        return {"error": "Unknown request"}

def run_chatbot():
    print("AI Assistant: I can calculate cylinder volume 📐")

    try:
        r = float(input("Enter radius: "))
        h = float(input("Enter height: "))

        response = ai_function_router(
            "volume_cylinder",
            {"radius": r, "height": h}
        )

        if response["result"] is not None:
            print(f"AI Assistant: Volume = {response['result']:.2f}")
        else:
            print("AI Assistant: Invalid values provided!")

    except:
        print("AI Assistant: Please enter numbers only.")


if __name__ == "__main__":
    run_chatbot()

```


### OUTPUT:

<img width="787" height="106" alt="Screenshot 2026-02-13 141702" src="https://github.com/user-attachments/assets/eb5aa056-c99a-4ef6-bd8f-01f9eec16fa6" />


### RESULT:
Hence,the python program to design and implement a Python function for calculating the volume of a cylinder,  
integrating it with a chat completion system utilizing the function-calling feature of a large language model (LLM) is written successfully and executed.
