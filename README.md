## ⚡ Code Runner

The **Code Runner** is a secure execution module that allows users to write and execute code directly inside the platform.

### Features

* 🧑‍💻 **Code Execution** — Run user-submitted code directly from the platform.
* 🔒 **Sandboxed Environment** — Execute code in an isolated environment to prevent it from affecting the main application.
* ⏱️ **Execution Time Limit** — Automatically stop programs that run for too long.
* 💾 **Resource Control** — Limit CPU, memory, and other resources available to each execution.
* 📤 **Input Support** — Provide custom input to programs.
* 📥 **Output Capture** — Capture and return standard output and errors.
* ❌ **Error Handling** — Clearly return compilation errors, runtime errors, and timeout errors.
* 🧹 **Automatic Cleanup** — Remove temporary execution files after the program finishes.

### Execution Flow

```text
User writes code
       ↓
Code Runner API
       ↓
Validate request
       ↓
Create isolated execution environment
       ↓
Compile / Execute code
       ↓
Capture output & errors
       ↓
Destroy execution environment
       ↓
Return result to user
```

### Security

The Code Runner should **never execute untrusted code directly on the host machine**.

Recommended security measures:

* Containerized execution
* CPU and memory limits
* Execution timeout
* Restricted filesystem access
* Restricted network access
* Non-root execution
* Temporary workspace for each execution
* Automatic cleanup after execution

### Example API

```http
POST /api/code/run
```

**Request:**

```json
{
  "language": "python",
  "code": "print('Hello World')",
  "input": ""
}
```

**Response:**

```json
{
  "status": "success",
  "output": "Hello World\n",
  "error": null,
  "execution_time": 0.12
}
```

### Supported Languages

The runner can be extended to support:

* Python
* JavaScript
* C
* C++
* Java
* Go
* Rust

### Error Types

| Error              | Description                       |
| ------------------ | --------------------------------- |
| `CompilationError` | Code failed during compilation    |
| `RuntimeError`     | Program crashed while running     |
| `TimeoutError`     | Execution exceeded the time limit |
| `MemoryLimitError` | Program exceeded memory limit     |
| `ValidationError`  | Invalid execution request         |

> **Important:** Security isolation is mandatory when executing user-generated code. Never use a simple `subprocess` call on the production host without proper sandboxing.
