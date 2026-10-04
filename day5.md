Below is a complete submission covering **both A and B**. I chose **setting up a GitHub repository from scratch and making a first commit** for Part A because it is beginner-friendly and easy to demonstrate.

 A) User Manual Procedure — Setting Up a GitHub Repository and Making a First Commit

# A) User Manual Procedure: Setting Up a GitHub Repository from Scratch and Making a First Commit

 ## Prerequisites

 Before starting, the reader needs:

 - A computer with Windows, macOS, or Linux.
- A working internet connection.
- A web browser such as Chrome, Edge, Firefox, or Safari.
- A GitHub account.
- Git installed on the computer.
- Basic knowledge of creating and saving files.
- A text editor such as Visual Studio Code, Notepad, or another code editor.

 ## Procedure

 ### Step 1: Open GitHub

 **Action:** Open the GitHub website in a web browser.

 **Expected result:** The GitHub home page appears.

 ### Step 2: Sign in to GitHub

 **Action:** Sign in using your GitHub username and password.

 **Expected result:** Your GitHub account page or GitHub dashboard appears.

 ### Step 3: Create a new repository

 **Action:** Select **New repository** from the GitHub interface.

 **Expected result:** A page titled **Create a new repository** appears.

 ### Step 4: Enter the repository name

 **Action:** Enter `my-first-project` as the repository name.

 **Expected result:** The repository name is displayed in the repository-name field.

 ### Step 5: Set the repository visibility

 **Action:** Select **Public** as the repository visibility.

 **Expected result:** The Public option is selected, meaning other GitHub users can view the repository.

 ### Step 6: Create the repository

 **Action:** Select **Create repository**.

 **Expected result:** GitHub creates the repository and displays the new repository's page.

 ### Step 7: Create a project file

 **Action:** Create a text file named `README.md` containing the heading `# My First Project`.

 **Expected result:** A file named `README.md` containing the project heading exists on the computer.

 ### Step 8: Open the project folder in a terminal

 **Action:** Open a terminal inside the folder containing `README.md`.

 **Expected result:** The terminal opens with the project folder as its current working directory.

 ### Step 9: Initialize Git

 **Action:** Run the command `git init`.

 **Expected result:** Git creates a local repository in the project folder.

 ### Step 10: Connect the local repository to GitHub

 **Action:** Run `git remote add origin https://github.com/YOUR-USERNAME/my-first-project.git`, replacing `YOUR-USERNAME` with your GitHub username.

 **Expected result:** The local Git repository has a remote named `origin` pointing to the GitHub repository.

 ### Step 11: Add the project file to Git

 **Action:** Run `git add README.md`.

 **Expected result:** Git stages `README.md` for the next commit.

 ### Step 12: Create the first commit

 **Action:** Run `git commit -m "Initial commit"`.

 **Expected result:** Git creates a commit containing `README.md` with the message `Initial commit`.

 ### Step 13: Set the main branch name

 **Action:** Run `git branch -M main`.

 **Expected result:** The local branch is named `main`.

 ### Step 14: Upload the commit to GitHub

 **Action:** Run `git push -u origin main`.

 **Expected result:** The first commit is uploaded to the GitHub repository.

 ### Step 15: Verify the repository

 **Action:** Refresh the GitHub repository page in the web browser.

 **Expected result:** The `README.md` file appears in the GitHub repository, and the page shows the `Initial commit`.

 ## Screenshot Description

 **Screenshot:** A screenshot should show the GitHub repository page after the first commit has been pushed.

 The screenshot should clearly show:

 - The repository name `my-first-project`.
- The `README.md` file in the file list.
- The `Initial commit` message.
- The `main` branch.

 This screenshot demonstrates that the local Git repository was successfully connected to GitHub and that the first commit was uploaded.

 ## Troubleshooting

 ### Common error: `remote: Repository not found`

 This error usually occurs when the remote GitHub URL is incorrect or the repository name does not match the repository created on GitHub.

 **Solution:** Check the remote URL using `git remote -v`. Make sure the URL contains the correct GitHub username and repository name, then correct it with:

 `git remote set-url origin https://github.com/YOUR-USERNAME/my-first-project.git`

 After correcting the URL, run `git push -u origin main` again.

 ## B) API Reference Entry

 B) API Reference — Create a New Task

# B) API Reference: Create a New Task

 ## Endpoint

 **Method:** `POST`

 **Endpoint:** `/api/v1/projects/{projectId}/tasks`

 ## Description

 This endpoint creates a new task inside a specified project.

 The request must be made by an authenticated user. The task includes a required title, an optional description, an assignee, a due date, and a priority level.

 When the task is successfully created, the API returns the newly created task together with its unique ID and creation timestamp.

 ## Path Parameters

 | Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `projectId` | string | Yes | The unique ID of the project where the new task will be created. |

## Query Parameters

 This endpoint does not require any query parameters.

 ## Request Body

 The request body must be formatted as JSON.

 | Field | Type | Required | Description |
| --- | --- | --- | --- |
| `title` | string | Yes | The name or short title of the task. |
| `description` | string | No | Additional information about the task. |
| `assigneeId` | string | Yes | The unique ID of the user who will be assigned the task. |
| `dueDate` | string | Yes | The date on which the task is due, using the `YYYY-MM-DD` format. |
| `priority` | string | Yes | The priority of the task. Allowed values are `low`, `medium`, or `high`. |

## Request Headers

 | Header | Required | Description |
| --- | --- | --- |
| `Authorization` | Yes | Contains the user's access token in the format `Bearer <token>`. |
| `Content-Type` | Yes | Must be `application/json` because the request body is JSON. |
| `Accept` | Yes | Indicates that the client expects a JSON response. |

## Example Request

```
POST /api/v1/projects/proj_1001/tasks HTTP/1.1
Host: api.example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.example
Content-Type: application/json
Accept: application/json
```

 ### Example JSON Request Body

```
{
  "title": "Prepare database documentation",
  "description": "Write documentation for the project's database tables and relationships.",
  "assigneeId": "usr_2045",
  "dueDate": "2026-10-15",
  "priority": "high"
}
```

 ## HTTP Response Codes

 ### `201 Created`

 The task was successfully created.

 ### `400 Bad Request`

 The request contains invalid data, such as a missing required field, an invalid date format, or an unsupported priority value.

 ### `401 Unauthorized`

 The request does not contain a valid authentication token.

 ### `403 Forbidden`

 The user is authenticated but does not have permission to create tasks in the specified project.

 ### `404 Not Found`

 The specified project or assignee does not exist.

 ### `409 Conflict`

 The request conflicts with the current project state, such as attempting to create a task that violates a project-specific uniqueness rule.

 ### `422 Unprocessable Entity`

 The JSON structure is valid, but one or more values fail the application's validation rules.

 ### `500 Internal Server Error`

 An unexpected error occurred on the server while processing the request.

 ## Successful Response

 **HTTP status:** `201 Created`

```
{
  "id": "task_7842",
  "projectId": "proj_1001",
  "title": "Prepare database documentation",
  "description": "Write documentation for the project's database tables and relationships.",
  "assignee": {
    "id": "usr_2045",
    "name": "Amina Otieno"
  },
  "dueDate": "2026-10-15",
  "priority": "high",
  "status": "todo",
  "createdAt": "2026-10-04T11:42:18Z",
  "createdBy": {
    "id": "usr_1007",
    "name": "David Kamau"
  }
}
```

 ## Example Error Response

 For example, if the client provides an invalid priority:

```
{
  "error": {
    "code": "INVALID_PRIORITY",
    "message": "Priority must be one of: low, medium, high."
  }
}
```

 ## Summary

 The `POST /api/v1/projects/{projectId}/tasks` endpoint allows an authenticated user to create a task within a project. The client must provide a project ID, title, assignee ID, due date, and priority. The description is optional. A successful request returns HTTP `201 Created` and the details of the newly created task.

 This version is structured to meet the stated requirements: Part A has prerequisites, one-action-per-step instructions with expected results, a screenshot description, and troubleshooting; Part B defines the endpoint, parameters, headers, response codes, and consistent JSON examples.