# 3xWords

Lord Polonius: What do you read, my lord?

Hamlet: Words, words, words.

— *Hamlet*, Act 2, Scene 2

3xWords is a PyQt5 application for simplifying the process of creating, editing, and deleting posts on a Jekyll-based website hosted on GitHub Pages. This version of the application is specifically meant to be used for Shakespeare in Bengal (SiB), an archival project that deals with Bengali negotiations with William Shakespeare. The purpose of this application is to make the content writing and publishing process easy and accessible through automation.

## Key Features
3xWords features three different tabs for three different actions:
- Through the **Create** tab, the user can provide the title, date, tags, category, and content for a new post.
- The **Edit** tab is nearly identical to the Create tab, except that it allows the user to select an existing post to modify the aforementioned elements.
- The **Delete** tab simply lets the user choose an existing post for deletion.

## Project Organization
The project directory has been organized into the following structure:
```cmd
3xwords/
    ├── 3xwords.py
    ├── LICENSE
    ├── README.md
    ├── requirements.txt
    └── ui/
    	├── 3xwords-setup-window.ui
    	└── 3xwords.ui
```
- `3xwords.py` contains the Python code for the application. The code in the script will be described in detail later.
- The `LICENSE` file outlines the legal terms and conditions under which the project is distributed.
- `requirements.txt` lists the external dependencies that are required for the project to work.
- The `ui` directory contains the .ui files generated by Qt Designer. Inside the directory, there are two files:
	- `3xwords-setup-window.ui` includes the graphical components for the setup window that opens up during the initial setup.
	- `3xwords.ui` holds the rest of the GUI elements for the application.

## How the App Works
The entire application was built using Python. The graphical user interface (GUI) was created with PyQt5. `3xwords.py` contains all the code that is needed for the application to run. The GUI for the application was initially made with Qt Designer, and then the .ui files were converted to Python scripts using pyuic5. The resulting code was combined with custom Python logic in a single script, `3xwords.py`.

Opening the application for the first time, the user will be prompted to provide the web URL and the name of the GitHub repository in which the files and directories related to their website exist. The user-provided data will be stored in a JSON file named `repo.json`. After that, the remote repository will be cloned to the local machine in the same directory. It should be noted that the application cannot run without `repo.json`. If the user fails to provide the required data, they will be warned, and if the data is still not provided, the application will close. Once the initial setup is successfully completed, the main features of the application will be accessible. The setup window can be reopened by pressing Ctrl+S on Windows.

The main window of the application contains various fields or input boxes in the three tabs (mentioned in the “Key Features” section) to provide the required data for the post that the user wants to create, edit, or delete. These fields have different characteristics:
- The **Title** field holds a maximum of 190 characters.
- In the **Date** field, the input is stored in DD/MM/YYYY format.
- Comma-separated values in the **Tags** field are treated as different tags.
- In the **Content** field, the text can be formatted using Markdown syntax.
- The **Select Post** field offers autocomplete suggestions for user input, based on the names of the files in the `_posts` directory of the Jekyll repository. Specifically in the Edit tab, the data from an existing post is loaded once the user presses the Enter key after providing a valid file name.

Apart from these fields, the **Category** menu, which can be found in both the Create tab and the Edit tab, features a drop-down list of categories, specifically included for the SiB website.

Once **the Publish/Edit button** is clicked in the application, a series of automated processes are executed in the following order:
- At first, the local Jekyll repository is updated through a pull operation (or the repository is cloned if it does not exist locally).
- If a file is being edited, the program checks whether it is a valid markdown file.
- The data in the fields are stored in appropriate variables and combined to create a properly formatted Jekyll post or overwrite an existing one.
- The post is saved in the `_posts` directory.
- As multiple users might end up working on the same file, the changes are not immediately pushed to the main branch. Instead, a new branch is created, and the changes are committed locally and then pushed to that branch.
- After checking for conflicts, the new branch is merged into the main branch.
- Finally, the changes are pushed to the main branch.

If **the Delete button** is clicked, the program deletes a file locally from the `_posts` directory based on the valid file name in the Select Post field and sequentially completes the last three steps listed above. The changes made in the `_posts` directory should appear on the user’s website.

## Acknowledgements
This application was developed as the final project for the CS50x course. I would like to thank Prof. David J. Malan and his team for providing an invaluable introduction to computer science, which made this project possible.
