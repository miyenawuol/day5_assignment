# Exercise Answers

## A) User Manual Procedure: Creating and Activating a Python Virtual Environment & Installing a Package

### Prerequisites

Before starting this procedure, ensure you have:

* A computer running Windows, macOS, or Linux.
* Internet connectivity to download Python packages.
* Basic understanding of opening and typing commands into your terminal or command prompt.
* Python 3 installed on your computer (includes `pip` and the `venv` module by default).

---

### Step-by-Step Procedure

1. **Open your terminal or command prompt:** Prerequisite step before navigating directories.
Open your system's command line application (Terminal on macOS/Linux, or Command Prompt / PowerShell on Windows).

*Expected Result:* A command-line window opens displaying a text cursor waiting for input.


2. **Create a dedicated project directory:**
Type `mkdir my_python_project && cd my_python_project` and press **Enter**.

*Expected Result:* A folder named `my_python_project` is created, and your working directory changes to this folder.


3. **Create the virtual environment:**
Type `python3 -m venv myenv` (on macOS/Linux) or `python -m venv myenv` (on Windows) and press **Enter**.

*Expected Result:* A new subfolder named `myenv` appears inside your project directory containing an isolated Python installation.


4. **Activate the virtual environment:**
Type `source myenv/bin/activate` (macOS/Linux) or `myenv\Scripts\activate` (Windows) and press **Enter**.

*Expected Result:* The prefix `(myenv)` appears before your command prompt line, indicating the virtual environment is currently active.


5. **Install a target package using pip:**
Type `pip install requests` and press **Enter**.

*Expected Result:* Pip downloads and successfully installs the `requests` library and its dependencies inside `myenv`.


6. **Verify the package installation:**
Type `pip list` and press **Enter**.

*Expected Result:* Terminal outputs a list of installed packages in `myenv` showing `requests` along with its version number.


---

### Screenshot Description

> **Screenshot Name:** `activated_venv_confirmation.png`
> **Visual Description:** This screenshot should show a full terminal window after Step 4 execution. The top line displays the entered command (`source myenv/bin/activate` or `myenv\Scripts\activate`). Below it, a red callout circle highlights the new terminal prompt where `(myenv)` is prepended to the user path (e.g., `(myenv) user@computer:~/my_python_project$`). Annotations explain that `(myenv)` serves as visual verification that commands run inside the isolated environment.

---

### Troubleshooting Note

* **Common Error:** `command not found: python3` or `'python' is not recognized as an internal or external command`.
* **Cause:** Python is either not installed or its executable path was not added to your system environment variables (`PATH`) during installation.
* **Fix:** Re-run the Python installer, check the box labeled **"Add Python to PATH"** at the bottom of the first setup window, and restart your terminal.

---

## B) API Reference Entry

### HTTP Method & Endpoint Path

`POST /api/v1/projects/{project_id}/tasks`

---

### Overview

Creates a new task within a specified project. Requires authentication via a Bearer JWT token. On successful creation, the newly created task object is returned in the response payload.

---

### Request Headers

| Header Name | Type | Required | Description |
| --- | --- | --- | --- |
| `Authorization` | String | **Required** | OAuth 2.0 Bearer token in format `Bearer <token>` |
| `Content-Type` | String | **Required** | Must be set to `application/json` |

---

### Request Parameters

#### Path Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| `project_id` | String (UUID) | **Required** | Unique identifier of the project where the task will be created |

#### Body Parameters

| Name | Type | Required | Description |
| --- | --- | --- | --- |
| `title` | String | **Required** | The concise title of the task (1-255 characters). |
| `description` | String | Optional | Detailed text description of the task. |
| `assignee_id` | String (UUID) | Optional | User ID of the assigned team member. Must belong to the project. |
| `due_date` | String (ISO 8601) | Optional | Due date and time in format `YYYY-MM-DDTHH:mm:ssZ`. |
| `priority` | String | **Required** | Priority level. Accepted values: `"low"`, `"medium"`, `"high"`. |

---

### HTTP Response Codes

| Status Code | Description / Cause |
| --- | --- |
| `201 Created` | Task successfully created. Returns created task payload. |
| `400 Bad Request` | Missing required body fields, invalid payload format, or unknown enum values. |
| `401 Unauthorized` | Missing or invalid Authorization header/token. |
| `403 Forbidden` | Authenticated user lacks permission to create tasks in this project. |
| `404 Not Found` | Target `project_id` or specified `assignee_id` does not exist. |
| `422 Unprocessable Entity` | Business validation failed (e.g., `due_date` is in the past). |

---

### Example Request Body (JSON)

```json
{
  "title": "Set up CI/CD pipeline",
  "description": "Configure GitHub Actions workflow for automated testing and staging deployments.",
  "assignee_id": "9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d",
  "due_date": "2026-10-15T17:00:00Z",
  "priority": "high"
}

```

---

### Example Successful Response Body (`201 Created`)

```json
{
  "status": "success",
  "data": {
    "id": "e4f3a2b1-5c6d-7e8f-9a0b-1c2d3e4f5a6b",
    "project_id": "a1b2c3d4-e5f6-7a8b-9c0d-1e2f3a4b5c6d",
    "title": "Set up CI/CD pipeline",
    "description": "Configure GitHub Actions workflow for automated testing and staging deployments.",
    "assignee_id": "9b1deb4d-3b7d-4bad-9bdd-2b0d7b3dcb6d",
    "due_date": "2026-10-15T17:00:00Z",
    "priority": "high",
    "status": "todo",
    "created_by": "3c2b1a0f-9e8d-7c6b-5a4f-3e2d1c0b9a8f",
    "created_at": "2026-10-04T11:14:45Z",
    "updated_at": "2026-10-04T11:14:45Z"
  }
}

```