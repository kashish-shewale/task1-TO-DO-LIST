# task1-TO-DO-LIST
import json

class TodoApp:
    def __init__(self):
        self.todo_file = "todos.json"
        self.load_tasks()

    def load_tasks(self):
        """Load the tasks from a JSON file."""
        try:
            with open(self.todo_file, "r") as file:
                self.tasks = json.load(file)
        except (FileNotFoundError, json.JSONDecodeError):
            self.tasks = []

    def save_tasks(self):
        """Save the tasks to a JSON file."""
        with open(self.todo_file, "w") as file:
            json.dump(self.tasks, file, indent=4)

    def add_task(self, task):
        """Add a new task to the to-do list."""
        self.tasks.append({"task": task, "completed": False})
        self.save_tasks()

    def list_tasks(self):
        """List all tasks in the to-do list."""
        if not self.tasks:
            print("Your to-do list is empty.")
        else:
            print("\nTo-Do List:")
            for index, task in enumerate(self.tasks, start=1):
                status = "Completed" if task["completed"] else "Pending"
                print(f"{index}. {task['task']} - {status}")
            print()

    def update_task(self, task_number, status):
        """Update the status of a specific task."""
        if 0 < task_number <= len(self.tasks):
            self.tasks[task_number - 1]["completed"] = status
            self.save_tasks()
        else:
            print("Invalid task number!")

    def delete_task(self, task_number):
        """Delete a task from the to-do list."""
        if 0 < task_number <= len(self.tasks):
            self.tasks.pop(task_number - 1)
            self.save_tasks()
        else:
            print("Invalid task number!")

    def run(self):
        """Main function to run the to-do app."""
        while True:
            print("1. Add a task")
            print("2. List tasks")
            print("3. Update a task status")
            print("4. Delete a task")
            print("5. Exit")

            choice = input("Choose an option: ")

            if choice == "1":
                task = input("Enter the task: ")
                self.add_task(task)
            elif choice == "2":
                self.list_tasks()
            elif choice == "3":
                self.list_tasks()
                task_number = int(input("Enter the task number to update: "))
                status = input("Is the task completed? (y/n): ").strip().lower() == "y"
                self.update_task(task_number, status)
            elif choice == "4":
                self.list_tasks()
                task_number = int(input("Enter the task number to delete: "))
                self.delete_task(task_number)
            elif choice == "5":
                print("Exiting the To-Do App. Goodbye!")
                break
            else:
                print("Invalid choice! Please try again.")

if __name__ == "__main__":
    app = TodoApp()
    app.run()

OUTPUT:1. Add a task
2. List tasks
3. Update a task status
4. Delete a task
5. Exit
Choose an option: 1
Enter the task: PYTHON
1. Add a task
2. List tasks
3. Update a task status
4. Delete a task
5. Exit
Choose an option: 3

To-Do List:
1. python - Pending
2. PYTHON - Pending

Enter the task number to update: 1
Is the task completed? (y/n): NO
