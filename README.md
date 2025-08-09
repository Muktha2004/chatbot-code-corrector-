# chatbot-code-corrector-
A simple command-line chatbot built in Python using the OpenAI API. 
Reads your API key securely from an environment variable (OPENAI_API_KEY).  
Supports interactive conversation with GPT models (gpt-3.5-turbo or gpt-4o).
Clean and modular code structure for easy customization.
Safe exit commands: quit, exit, or bye.


# Use the exclamation mark prefix to run shell commands in Jupyter
# Alternatively, you can use the system command
import sys
import subprocess
subprocess.check_call([sys.executable, '-m', 'pip', 'install', 'openai'])
import os
from openai import OpenAI

# Get API key from environment variable
# In terminal, run: export OPENAI_API_KEY="your_key_here"
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

def chat_with_gpt(prompt):
    response = client.chat.completions.create(
        model="gpt-3.5-turbo",  # or "gpt-4o"
        messages=[{"role": "user", "content": prompt}]
    )
    return response.choices[0].message.content.strip()

if __name__ == "__main__":
    while True:
        user_input = input("You: ")
        if user_input.lower() in ["quit", "exit", "bye"]:
            break
        response = chat_with_gpt(user_input)
        print("Chatbot:", response)
