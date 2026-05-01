# Surya
Projects
import json
import os

FILE = "tasks.json"

def load_tasks():
    if os.path.exists(FILE):
        with open(FILE, "r") as f:
            return json.load(f)
    return []

def save_tasks(tasks):
    with open(FILE, "w") as f:
        json.dump(tasks, f)

def show_tasks(tasks):
    if not tasks:
        print("No tasks yet!")
    else:
        for i, task in enumerate(tasks):
            status = "✔️" if task["done"] else "❌"
            print(f"{i+1}. {task['task']} [{status}]")

def add_task(tasks):
    task = input("Enter task: ")
    tasks.append({"task": task, "done": False})

def mark_done(tasks):
    show_tasks(tasks)
    num = int(input("Enter task number to mark done: "))
    if 0 < num <= len(tasks):
        tasks[num-1]["done"] = True

def delete_task(tasks):
    show_tasks(tasks)
    num = int(input("Enter task number to delete: "))
    if 0 < num <= len(tasks):
        tasks.pop(num-1)

def main():
    tasks = load_tasks()

    while True:
        print("\n1. Show Tasks")
        print("2. Add Task")
        print("3. Mark Done")
        print("4. Delete Task")
        print("5. Exit")

        choice = input("Choose: ")

        if choice == "1":
            show_tasks(tasks)
        elif choice == "2":
            add_task(tasks)
        elif choice == "3":
            mark_done(tasks)
        elif choice == "4":
            delete_task(tasks)
        elif choice == "5":
            save_tasks(tasks)
            print("Goodbye!")
            break
        else:
            print("Invalid choice!")

if __name__ == "__main__":
    main()
    
    
