# Purpose

Creating and sharing documents on Google Drive to collect students
homework for grading.

# Command Line Parameters

* `-a` or `--affix`: a mnemonic affix that will end the name of the document for the student (e.g., `cmputXYZ-wTT-hwN`)
* `-f` or `--folder`: the name of the folder in drive where the documents are stored
* `-s` or `--students`: JSON file with three fields per student: prename, surname, and email, which are used to name the document
* `-t` or `--type`: type of artifact to be created (i.e., `document`, `spreadsheet`, or `folder`), `document` as default
* `-i` or `--instructors`: JSON file with one email field per member of the instructional team, which is used to share the document


Sample JSON file with student list:

```
[
  {"prename": "Alice", "surname": "Wonderland", "email": "alice@wonderland"},
  {"prename": "Bob", "surname": "Builder", "email": "bob@builder"}
]
```

Sample JSON file with instructional team list:

```
[
  {"email": "white@rabbit"},
  {"email": "cheshire@cat"}
]
```
##Note
After downloading the namelist json file, remove the outermost square brackets of the code.

#Scripts
create_and_share_google_docs.py: creating a file or folder for each students.

create_teams_file.py: creating a file or folder for a group.

add_permissions.py : adding the permission.

change_permissions.py : changing the permission so that only the own can edit it, after deadlines.

# Initial Setup

1. Enable the Drive API for the institutional account used on the course (follow the [Python Quickstart](https://developers.google.com/drive/api/v3/quickstart/python))
2. Download the credentials and put them on the same folder as the script.

# Naming of Folders and Documents

Folders and files on Google Drive are accessed via internal identifiers (instead of paths). The program first searches for a directory (anywhere) in the Google Drive corresponding to the provided access token matching the parameter `folder`. Note: make sure the folder name is identical (Tip: rename the folder name before running this code and change it back after)

If the folder is found, the program creates a blank document for each student listed in the student file, naming each file with the prefix (so that the student knows what the document is about) followed by the student name and the provided student id in parenthesis.

Example:
```
python create_and_share_google_docs.py -f cmput123 -a Project1 -s students.json -t document
```

Would create documents `Project1_Wonderland` and `Project1_Builder_Bob` inside folder with name **cmput123**.

It might be best to test everything with an empty student file.

### Python Quickstar

This code wad produced by modifying the [Python Quickstart](https://developers.google.com/drive/api/v3/quickstart/python).

