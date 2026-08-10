# Assignment-6_Linux
# 📘 Linux Assignment — Process Management Utility

## 🎯 Objective

Practice **Linux process management, monitoring, scheduling, and service management** by creating shell-script based process management utilities.

The assignment is divided into three parts:

* 🔹 **Part A:** Process Management Utility
* 🔹 **Part B:** Process Manager Utility
* 🔹 **Part C:** Practical Process Management

---

# 📂 Part A: Process Management Utility

## 🎯 Objective

Create a process management utility named **`otProcessManager`** to monitor and manage processes running on a Linux system.

### 📌 Utility Syntax

```bash
./otProcessManager <operation> [arguments]
```

---

## 📊 Figure 1: Process Management Utility

```mermaid
flowchart TD
    A["otProcessManager"] --> B{"Select Operation"}

    B --> C["Top Process"]
    B --> D["Kill Least Priority"]
    B --> E["Running Duration"]
    B --> F["Orphan Process"]
    B --> G["Zombie Process"]
    B --> H["Kill Process"]
    B --> I["Waiting Process"]

    C --> C1["CPU"]
    C --> C2["Memory"]

    E --> E1["Process Name"]
    E --> E2["Process ID"]

    H --> H1["Process Name"]
    H --> H2["Process ID"]
```

---

## 📍 Task 1: Top N Processes by Memory

Find the top **N processes** based on memory consumption.

### 🔹 Command

```bash
./otProcessManager topProcess 5 memory
```

### 📝 Example

```text
Top 5 processes by memory
```

---

## 📍 Task 2: Top N Processes by CPU

Find the top **N processes** based on CPU consumption.

### 🔹 Command

```bash
./otProcessManager topProcess 10 cpu
```

### 📝 Example

```text
Top 10 processes by CPU
```

---

## 📍 Task 3: Kill Process Having Least Priority

Find and terminate the process having the lowest priority.

### 🔹 Command

```bash
./otProcessManager killLeastPriorityProcess
```

---

## 📍 Task 4: Find Running Duration of a Process

Find how long a particular process has been running.

### 🔹 Using Process Name

```bash
./otProcessManager RunningDurationProcess <processName>
```

### 🔹 Using Process ID

```bash
./otProcessManager RunningDurationProcess <processID>
```

### 📝 Example

```bash
./otProcessManager RunningDurationProcess nginx
```

or

```bash
./otProcessManager RunningDurationProcess 1234
```

---

## 📍 Task 5: List Orphan Processes

Find orphan processes running on the system.

### 🔹 Command

```bash
./otProcessManager listOrphanProcess
```

### 📖 Definition

An **orphan process** is a process whose parent process has terminated while the child process is still running.

---

## 📍 Task 6: List Zombie Processes

Find zombie processes running on the system.

### 🔹 Command

```bash
./otProcessManager listZoombieProcess
```

### 📖 Definition

A **zombie process** is a process that has completed execution but still has an entry in the process table because its parent has not collected its exit status.

---

## 📍 Task 7: Kill Process by Name or PID

Terminate a process using either its name or PID.

### 🔹 Using Process Name

```bash
./otProcessManager killProcess <processName>
```

### 🔹 Using Process ID

```bash
./otProcessManager killProcess <processID>
```

### 📝 Example

```bash
./otProcessManager killProcess nginx
```

or

```bash
./otProcessManager killProcess 1234
```

---

## 📍 Task 8: List Processes Waiting for Resources

Find processes that are currently waiting for resources.

### 🔹 Command

```bash
./otProcessManager ListWaitingProcess
```

---

## 📊 Figure 2: Part A Workflow

```mermaid
flowchart LR
    A["User"] --> B["otProcessManager"]

    B --> C["CPU Monitoring"]
    B --> D["Memory Monitoring"]
    B --> E["Process Duration"]
    B --> F["Process Killing"]
    B --> G["Orphan Detection"]
    B --> H["Zombie Detection"]
    B --> I["Waiting Process Detection"]

    C --> J["Process Information"]
    D --> J
    E --> J
    F --> J
    G --> J
    H --> J
    I --> J
```

---

# 📂 Part B: Process Manager Utility

## 🎯 Objective

Create a **`ProcessManager.sh`** utility that can register scripts as services and manage those services.

The utility should support:

* 📝 Register a service
* ▶️ Start a service as a daemon
* 🔍 Check service status
* 🛑 Stop a service
* ⚡ Change process priority
* 📋 List registered services
* 📊 Display process details

---

## 📊 Figure 3: Process Manager Architecture

```mermaid
flowchart TD
    A["ProcessManager.sh"] --> B["Service Registry"]

    B --> C["service1"]
    B --> D["service2"]
    B --> E["service3"]

    A --> F["Linux Process"]

    F --> G["PID"]
    F --> H["State"]
    F --> I["Priority"]
    F --> J["Script"]
```

---

## 📍 Task 1: Register a Service

Register a script with a service alias.

### 🔹 Command

```bash
./ProcessManager.sh -o register -s <path> -a <alias>
```

### 📝 Example

```bash
./ProcessManager.sh -o register -s /home/user/service1.sh -a service1
```

### 📖 Explanation

* `-o register` → Register operation
* `-s` → Script path
* `-a` → Service alias

---

## 📍 Task 2: Start a Service

Start the registered service as a daemon/background process.

### 🔹 Command

```bash
./ProcessManager.sh -o start -a <alias>
```

### 📝 Example

```bash
./ProcessManager.sh -o start -a service1
```

---

## 📊 Figure 4: Service Start Flow

```mermaid
flowchart TD
    A["Start Service"] --> B["Enter Alias"]
    B --> C["Find Registered Service"]
    C --> D{"Service Exists?"}

    D -->|No| E["Display Error"]
    D -->|Yes| F["Get Script Path"]

    F --> G["Start Script"]
    G --> H["Run as Daemon"]
    H --> I["Store PID"]
```

---

## 📍 Task 3: Check Service Status

Check whether a particular service is running.

### 🔹 Command

```bash
./ProcessManager.sh -o status -a <alias>
```

### 📝 Example

```bash
./ProcessManager.sh -o status -a service1
```

### 💡 Expected Output

```text
service1 is running
PID: 2456
```

If the service is stopped:

```text
service1 is not running
```

---

## 📍 Task 4: Stop a Service

Stop a particular service.

### 🔹 Command

```bash
./ProcessManager.sh -o kill -a <alias>
```

### 📝 Example

```bash
./ProcessManager.sh -o kill -a service1
```

---

## 📍 Task 5: Change Process Priority

Change the priority of a service.

### 🔹 Command

```bash
./ProcessManager.sh -o priority -p <low/med/high> -a <alias>
```

### 📝 Examples

```bash
./ProcessManager.sh -o priority -p low -a service1
```

```bash
./ProcessManager.sh -o priority -p med -a service1
```

```bash
./ProcessManager.sh -o priority -p high -a service1
```

---

## 📊 Figure 5: Process Priority

```mermaid
flowchart LR
    A["Service Process"] --> B{"Priority"}

    B --> C["Low"]
    B --> D["Medium"]
    B --> E["High"]

    C --> F["Lower Scheduling Preference"]
    D --> G["Normal Scheduling Preference"]
    E --> H["Higher Scheduling Preference"]
```

> 💡 Linux process priority is commonly controlled using the **nice value**. A lower nice value generally gives a process a higher scheduling priority.

---

## 📍 Task 6: List Registered Services

Display all services registered with the utility.

### 🔹 Command

```bash
./ProcessManager.sh -o list
```

### 📝 Example Output

```text
service2
service1
service3
```

---

## 📍 Task 7: Display Process Details

Display details of all processes started by the utility.

### 🔹 Command

```bash
./ProcessManager.sh -o top
```

To display details of a particular service:

```bash
./ProcessManager.sh -o top -a <alias>
```

### 📝 Expected Output

```text
Alias     PID     State      Priority     Script
service1  2456    Running    10           /home/user/service1.sh
service2  2461    Sleeping   15           /home/user/service2.sh
service3  2470    Running    5            /home/user/service3.sh
```

---

## 📊 Figure 6: Process Details

```mermaid
flowchart TD
    A["Process Details"] --> B["Alias"]
    A --> C["PID"]
    A --> D["State"]
    A --> E["Priority"]
    A --> F["Script"]

    B --> G["Service Information"]
    C --> G
    D --> G
    E --> G
    F --> G
```

---

# 📂 Part C: Play Around With Processes

## 🎯 Objective

Perform practical experiments to understand how Linux handles processes, log files, file descriptors, and process priorities.

---

## 📍 Task 1: Clear a Log File of a Running Process

First identify the running process:

```bash
ps -ef
```

Clear the contents of the log file:

```bash
> application.log
```

or:

```bash
truncate -s 0 application.log
```

### 📖 Observation

The process continues running because only the **contents of the log file** are cleared.

---

## 📊 Figure 7: Clearing Log File

```mermaid
flowchart LR
    A["Running Process"] --> B["application.log"]

    C["Clear File"] --> B

    B --> D["File Becomes Empty"]
    A --> E["Process Continues Running"]
```

---

## 📍 Task 2: Delete a Log File of a Running Process

Delete the log file:

```bash
rm application.log
```

Check whether the running process still has the deleted file open:

```bash
lsof | grep deleted
```

### 📖 Observation

If a running process has the file open, deleting the file name does not immediately terminate the process.

The process can continue using its open file descriptor.

---

## 📊 Figure 8: Delete Log File

```mermaid
flowchart TD
    A["Running Process"] --> B["Open File Descriptor"]
    B --> C["application.log"]

    D["rm application.log"] --> E["Directory Entry Removed"]

    B --> F["File Descriptor Still Open"]
    F --> G["Process Continues Running"]
```

---

## 📍 Task 3: Elevate the Priority of a Process

Check the running processes:

```bash
ps -eo pid,ni,comm
```

Check the priority/nice value of a particular process:

```bash
ps -o pid,ni,comm -p <PID>
```

Change the nice value:

```bash
sudo renice -n -5 -p <PID>
```

Verify the change:

```bash
ps -o pid,ni,comm -p <PID>
```

---

## 📊 Figure 9: Changing Process Priority

```mermaid
flowchart LR
    A["Running Process"] --> B["Check Nice Value"]
    B --> C["renice"]
    C --> D["New Nice Value"]
    D --> E["Changed Scheduling Priority"]
```

---

# 🛠️ Useful Linux Commands

The following Linux commands can be useful while implementing this assignment:

```bash
ps
top
pgrep
pkill
kill
killall
nice
renice
pstree
lsof
awk
grep
```

### 🔹 Display Processes

```bash
ps -ef
```

### 🔹 Display Detailed Process Information

```bash
ps -eo pid,ppid,user,%cpu,%mem,stat,ni,comm
```

### 🔹 Find Process by Name

```bash
pgrep <process-name>
```

### 🔹 Kill Process

```bash
kill <PID>
```

### 🔹 Kill Process by Name

```bash
pkill -f <process-name>
```

### 🔹 Change Process Priority

```bash
renice -n <value> -p <PID>
```

---

# 📁 Suggested Project Structure

```text
ProcessManagement/
│
├── README.md
│
├── Part-A/
│   └── otProcessManager
│
├── Part-B/
│   ├── ProcessManager.sh
│   └── services/
│       ├── service1.sh
│       ├── service2.sh
│       └── service3.sh
│
└── Part-C/
    └── process-experiments.txt
```

---

## 📊 Figure 10: Project Structure

```mermaid
flowchart TD
    A["ProcessManagement"] --> B["README.md"]
    A --> C["Part-A"]
    A --> D["Part-B"]
    A --> E["Part-C"]

    C --> C1["otProcessManager"]

    D --> D1["ProcessManager.sh"]
    D --> D2["services"]
    D2 --> D3["service1.sh"]
    D2 --> D4["service2.sh"]
    D2 --> D5["service3.sh"]

    E --> E1["process-experiments.txt"]
```

---

# ▶️ Execution

## 🔹 Give Execute Permission

```bash
chmod +x otProcessManager
chmod +x ProcessManager.sh
```

## 🔹 Run Part A

```bash
./otProcessManager topProcess 5 memory
```

## 🔹 Register a Service

```bash
./ProcessManager.sh -o register -s /path/to/service.sh -a service1
```

## 🔹 Start the Service

```bash
./ProcessManager.sh -o start -a service1
```

## 🔹 Check Status

```bash
./ProcessManager.sh -o status -a service1
```

## 🔹 Display Process Details

```bash
./ProcessManager.sh -o top
```

## 🔹 Stop the Service

```bash
./ProcessManager.sh -o kill -a service1
```

---

# 🎓 Learning Outcomes

After completing this assignment, you will be able to:

* ✅ Monitor CPU and memory usage of processes.
* ✅ Find and manage processes using PID and process name.
* ✅ Identify orphan processes.
* ✅ Identify zombie processes.
* ✅ Find processes waiting for resources.
* ✅ Understand process priority and nice values.
* ✅ Start and manage daemon processes.
* ✅ Register and manage services using a Bash utility.
* ✅ Check process status.
* ✅ Change process priority.
* ✅ Understand Linux file descriptors.
* ✅ Understand the effect of clearing and deleting files used by running processes.

---

# 🚫 Important Notes

* 🐧 The assignment should be performed on a Linux system.
* 🔐 Some process-management operations may require `sudo`.
* ⚡ Be careful while using `kill` and `renice` on system processes.
* 📝 Test process-management commands on safe/user-created processes whenever possible.

---

# 🏁 Assignment Summary

| Part      | Topic                           | Utility             |
| --------- | ------------------------------- | ------------------- |
| 📌 Part A | Process Monitoring & Management | `otProcessManager`  |
| 📌 Part B | Service Management              | `ProcessManager.sh` |
| 📌 Part C | Process Experiments             | Linux Commands      |

---

## 🏆 Final Outcome

By completing this assignment, you will gain practical knowledge of:

**Linux Processes → Process Monitoring → Process Priority → Process Control → Daemons → Service Management → File Descriptors**

---

**CC:** @Aditya Kaushik Sir, @Faisal Sir

## 🏁 Happy Learning! 🚀
