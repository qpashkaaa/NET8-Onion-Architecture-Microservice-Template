# What It This?
  **The template ASP.NET 8 Core API microservice which is built by Onion Architecture.**
  >*In this solution, dependencies between libraries are immediately set in accordance with Onion Architecture. This template makes it easy to deploy a microservice project with the name you choose. All you need to do is download the project and execute Initializer.exe - Python script to replace the tags in your name.*

# How do I deploy the template?
- Upload a project from *GitHub* (*git clone https://github.com/qpashkaaa/NET8-Onion-Architecture-Microservice-Template.git*).
- Go to the root of the uploaded project.
- Run the file ***Initializer.exe*** - a console application written in Python that allows you to replace the tag in the project name with your own name (the Python script code itself is presented below).
- Follow the instructions provided in the application.
- After a successful replacement, check the file names in the solution explorer.
- If everything went well, you can delete the file Initializer.exe, or leave it in case you need to change the name of the solution and related projects.

# Screenshots
![image](https://github.com/user-attachments/assets/586178e0-71f4-4112-870a-2672f84d416d)
_____
![image](https://github.com/user-attachments/assets/1382bcea-3dd8-4c4b-9714-e03cb1074939)
_____
![image](https://github.com/user-attachments/assets/4b66d246-630c-49c3-a454-b5ebb45403f5)
_____
![image](https://github.com/user-attachments/assets/dc7dc1a5-9225-4ea1-be43-fb7cdf8f30b2)
_____
![image](https://github.com/user-attachments/assets/dfbbeadb-2c2a-41b9-9c25-e5b69703258c)
_____
![image](https://github.com/user-attachments/assets/6208a29e-c93c-4d22-999d-cc332edb2884)
_____

## Additional features
- **With the help of *Initializer.exe* you can change the name of your project and solution to a new one, even if the tag in the names is no longer there. You need to select "Use your own tag to replace" when starting the application. and act according to the instructions.**
- **After changing the names of the projects, the file *Initializer.exe* you can delete it from the project if it is no longer needed.**

## About my library (NuGet)
> To make the deployment of the microservice even more enjoyable, you can use our library, which is located in NuGet - ***AspNetCoreMicroserviceInitializer.TradingDesk***.
- [Project on GitHub and docs](https://github.com/qpashkaaa/Asp-Net-Core-Microservice-Initializer)
- [NuGet link](https://www.nuget.org/packages/AspNetCoreMicroserviceInitializer.TradingDesk/1.0.0)

## Python script
```Python
import os
import sys
import shutil
import stat


def replace_in_filenames_and_content(directory, placeholder, clear_placeholder, new_name):
    for root, dirs, files in os.walk(directory):
        for i, dir_name in enumerate(dirs):
            if placeholder in dir_name:
                new_dir_name = dir_name.replace(placeholder, new_name)
                old_path = os.path.join(root, dir_name)
                new_path = os.path.join(root, new_dir_name)
                os.rename(old_path, new_path)
                dirs[i] = new_dir_name

        for file_name in files:
            old_file_path = os.path.join(root, file_name)

            with open(old_file_path, 'r', encoding='utf-8', errors='ignore') as file:
                content = file.read()
                new_content = content.replace(placeholder, new_name).replace(clear_placeholder, new_name)

            if content != new_content:
                with open(old_file_path, 'w', encoding='utf-8') as file:
                    file.write(new_content)

            if placeholder in file_name:
                new_file_name = file_name.replace(placeholder, new_name)
                new_file_path = os.path.join(root, new_file_name)
                os.rename(old_file_path, new_file_path)


def remove_readonly(func, path, excinfo):
    os.chmod(path, stat.S_IWRITE)
    func(path)


def remove_git_related_files(directory):
    git_dir = os.path.join(directory, ".git")
    files_to_remove = ["README.md", ".gitattributes", ".gitignore"]

    if os.path.exists(git_dir) and os.path.isdir(git_dir):
        shutil.rmtree(git_dir, onerror=remove_readonly)
        print(f"Removed directory: {git_dir}")

    for file_name in files_to_remove:
        file_path = os.path.join(directory, file_name)
        if os.path.exists(file_path) and os.path.isfile(file_path):
            os.remove(file_path)
            print(f"Removed file: {file_path}")


def error_handling(text):
    print("\n")
    print(text)
    input("Press any button to restart the program...")
    main()


def main():
    os.system('cls')

    placeholder = None
    current_directory = os.getcwd()

    print(f"Current directory: {current_directory}")
    print("\n")
    print("Select an action:")
    print("1. Use a standard tag to replace (Test).")
    print("2. Use your own tag to replace.")
    print("\n")

    choice = input("Enter your choice (1 or 2): ").strip()

    if choice == "1":
        placeholder = "Test"
    elif choice == "2":
        placeholder = input("Enter the replacement tag: ").strip()
        if not placeholder:
            error_handling("Error: the tag cannot be empty!")
    else:
        error_handling("Error: the wrong item is selected!")

    print("\n")
    new_name = input("Enter new project name: ").strip()

    if not new_name:
        error_handling("Error: the new name cannot be empty!")

    clear_placeholder = placeholder.replace('$', "")

    replace_in_filenames_and_content(current_directory, placeholder, clear_placeholder, new_name)

    print("\n")
    print("The replacement is complete. ")

    print("\n")
    delete_git_choice = input("Delete files related to .git (if available)? (y/n): ")

    if delete_git_choice == 'y':
        print("\n")
        remove_git_related_files(current_directory)

    print("\n")
    input("To finish, press any key...")

    sys.exit()


if __name__ == "__main__":
    main()
```

## Tech Stack
- **.NET 8**

## Authors
- [Pavel Roslyakov](https://github.com/qpashkaaa)

## Contacts
- [Portfolio Website](https://portfolio-website-qpashkaaa.vercel.app/)
- [Telegram](https://t.me/qpashkaaa)
- [VK](https://vk.com/qpashkaaa)
- [LinkedIN](https://www.linkedin.com/in/pavel-roslyakov-7b303928b/)

## Year of Development
> *2024*
  
