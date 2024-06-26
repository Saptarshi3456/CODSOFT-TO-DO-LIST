# CODSOFT-TO-DO-LIST
Write a C++ program to build a console-based To-Do-List to add task , view task, mark as complete , remove task and exit.

#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Task
{
public:
    string name;
    bool completed;

    Task(string name) : name(name), completed(false) {}
};

class TaskManager
{
private:
    vector<Task> tasks;

public:
    void addTask(string name)
    {
        tasks.push_back(Task(name));
    }

    void viewTasks()
    {
        cout << "Tasks: \n";
        for (size_t i = 0; i < tasks.size(); ++i)
        {
            cout << i + 1 << ". " << tasks[i].name;
            if (tasks[i].completed)
            {
                cout << " (Completed)";
            }
            else
            {
                cout << " (pending)";
            }
            cout << "\n";
        }
        cout << endl;
    }

    void markTaskAsCompleted(int index)
    {
        if (index > 0 && index <= static_cast<int>(tasks.size()))
        {
            tasks[index - 1].completed = true;
        }
        else
        {
            cout << "Invalid task index.\n";
        }
    }

    void removeTask(int index)
    {
        if (index > 0 && index <= static_cast<int>(tasks.size()))
        {
            tasks.erase(tasks.begin() + index - 1);
        }
        else
        {
            cout << "Invalid task index.\n";
        }
    }
};

int main()
{
    TaskManager manager;

    while (true)
    {
        int choice;
        cout << "1. Add Task\n";
        cout << "2. View Tasks\n";
        cout << "3. Mark Task as Completed\n";
        cout << "4. Remove Task\n";
        cout << "5. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
        {
            char ch;
            do
            {

                string taskName;
                cout << "Enter task name: ";
                cin >> taskName;
                manager.addTask(taskName);
                cout << "Do you want to add more task (y/n)? ";
                cin >> ch;
            } while (ch == 'y');
            cout << "Task has been added successfully!!\n"
                 << endl;
            break;
        }
        case 2:
            manager.viewTasks();
            break;
        case 3:
        {
            int taskIndex;
            cout << "Enter task index: ";
            cin >> taskIndex;
            manager.markTaskAsCompleted(taskIndex);
            break;
        }
        case 4:
        {
            int taskIndex;
            cout << "Enter task index: ";
            cin >> taskIndex;
            manager.removeTask(taskIndex);
            break;
        }
        case 5:
            return 0;
        default:
            cout << "Invalid choice. Please enter again.\n";
        }
    }

    return 0;
}
