# Todo-List.py
import json
import os

def load_todos():
    if os.path.exists("todos.json"):
        with open("todos.json", "r") as f:
            return json.load(f)
    return []

def save_todos(todos):
    with open("todos.json", "w") as f:
        json.dump(todos, f, indent=2)

todos = load_todos()

while True:
    print("=== TODO App ===")
    print("1. Add todo")
    print("2. View todos") 
    print("3. Delete todo")
    print("4. Quit")
    
    choice = input("Choose (1-4): ")
    
    if choice == "1":
        todo = input("Enter todo: ")
        todos.append({"task": todo, "done": False})
        save_todos(todos)
        print("✅ Added!")
        
    elif choice == "2":
        for i, todo in enumerate(todos, 1):
            status = "✅" if todo["done"] else "⏳"
            print(f"{i}. {status} {todo['task']}")
            
    elif choice == "3":
        try:
            index = int(input("Todo number to delete: ")) - 1
            if 0 <= index < len(todos):
                removed = todos.pop(index)
                save_todos(todos)
                print(f"🗑️ Removed: {removed['task']}")
            else:
                print("Invalid number!")
        except:
            print("Enter a number!")
            
    elif choice == "4":
        print("Bye!")
        break
