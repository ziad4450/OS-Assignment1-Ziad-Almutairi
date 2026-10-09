# 📝 MY_WORK: Student Information, Development Log, Reflection & Answers

---

## 👤 Student Information

| Field | Your Answer |
|-------|-------------|
| **Full Name** | Ziad Almutairi |
| **Student ID** | 445050300 |
| **University Email** | 445050300@std.psau.edu.sa |
| **GitHub Username** | ziad4450 |
| **Repository Link** | https://github.com/ziad4450/OS-Assignment1-Ziad-Almutairi |

---

## 🎥 Video Link

**Video Link**: `[ضع_رابط_فيديو_Google_Drive_هنا]`

> ⚠️ **Verification Note:** Ensure the video file is named `445050300_Assignment1_Demo.mp4`, lasts 2 to 3 minutes, and has permissions set to "Anyone with the link can view".

---

# Part A: Development Log (0.5 mark)

### Entry 1 - [October 2, 2026, 4:15 PM]
**What I did**: Forked the starter repository, renamed it, and set up my student ID in VS Code.

**Details**:
- Logged into GitHub using my university email.
- Forked `OS-Assignment1-Starter-481` and renamed it to `OS-Assignment1-Ziad-Almutairi`.
- Updated line 150 in `SchedulerSimulation.java` with my student ID (`445050300`).
- Tested the initial code compilation and verified output.

**Challenges**: Git user email was not set globally on VS Code initial setup.

**Solution**: Configured user credentials using `git config --global user.email`.

**Time spent**: 35 minutes

---

### Entry 2 - [October 4, 2026, 6:00 PM]
**What I did**: Implemented Feature 1 (Process Priority Field).

**Details**:
- Added an integer `priority` variable (1–10) in `Process` class.
- Generated random priority numbers during process generation.
- Updated `addProcessToQueue()` to display priority metadata when processes join the ready queue.

**Challenges**: Ensuring priority display did not break Round-Robin FIFO queue ordering.

**Solution**: Maintained strict FIFO queue structure while treating priority as informational attribute.

**Time spent**: 45 minutes

---

### Entry 3 - [October 6, 2026, 3:30 PM]
**What I did**: Implemented Feature 2 (Context Switch Counter).

**Details**:
- Declared `public static int contextSwitchCounter` inside `SchedulerSimulation`.
- Incremented the counter every time a thread is dispatched from the queue.
- Added code to display total context switches at simulation end.

**Challenges**: Avoiding overcounting context switches when a process runs to completion.

**Solution**: Incremented counter strictly inside the active scheduler loop execution step.

**Time spent**: 30 minutes

---

### Entry 4 - [October 8, 2026, 8:15 PM]
**What I did**: Implemented Feature 3 (Waiting Time Tracking and Formatted Summary Table).

**Details**:
- Tracked creation and completion timestamps using `System.currentTimeMillis()`.
- Computed `Turnaround Time` and `Waiting Time = Turnaround Time - Burst Time`.
- Added a formatted summary table at the end displaying all metrics per process.

**Challenges**: Calculating accurate waiting time with thread sleep pauses.

**Solution**: Captured lifecycle timestamps (`creationTime` and `finishTime`) per process object.

**Time spent**: 1 hour 15 minutes

---

### Entry 5 - [October 9, 2026, 5:00 PM]
**What I did**: Completed documentation, technical reflection, and recorded demo video.

**Details**:
- Completed all sections of `MY_WORK.md`.
- Screen-recorded VS Code showing student ID, features execution, and commit history.
- Uploaded demonstration video to Google Drive.

**Challenges**: Keeping video duration between 2 and 3 minutes.

**Solution**: Planned a concise script following the required 5-stage walkthrough.

**Time spent**: 1 hour 10 minutes

---

## Development Log Summary

**Total time spent on assignment**: 4 hours 15 minutes

**Most challenging part**: Calculating accurate waiting times across thread executions and formatting terminal output.

**Most interesting learning**: Seeing how Java threads simulate OS time-slicing and context switching mechanics.

**What I would do differently next time**: Create smaller modular helper functions for table formatting.

---

# Part B: Reflection (0.5 mark)

## Question 1: What did you learn about multithreading?
Working on this assignment provided me with practical understanding of thread management in Java and how operating systems handle CPU scheduling. I learned how threads transition through states using `Thread.start()`, `Thread.join()`, and `Thread.sleep()`. The simulation demonstrated how context switching enables concurrency by sharing CPU time slices among multiple tasks. I was surprised by the overhead introduced by frequent thread switches during time-quantum execution. Overall, this assignment helped connect theoretical OS concepts to actual Java code execution.

## Question 2: What was the most challenging part of this assignment?
The most challenging part was tracking individual process waiting times and turnaround times accurately in Feature 3. Since processes in Round-Robin are repeatedly paused, re-queued, and resumed, measuring waiting time required careful timestamp logging using `System.currentTimeMillis()`. Formatting the final summary table cleanly in console output without interfering with colored logs also required significant debugging. Resolving this helped me understand process life cycle tracking in CPU schedulers.

## Question 3: How did you overcome the challenges you faced?
I overcome these challenges by tracing the code execution line-by-line and testing modifications incrementally. I used debug print statements to monitor timestamp calculations during thread execution. I also referred back to assignment guidelines and Java documentation when handling thread synchronization methods like `join()`. Testing each feature before committing ensured that existing functionality remained intact.

## Question 4: How can you apply multithreading concepts in real-world applications?
Multithreading concepts are essential in modern software applications to maintain responsiveness and resource efficiency. For instance, web servers like Tomcat assign incoming user requests to individual worker threads to handle concurrent web traffic. In graphical user interface (GUI) and mobile applications, background threads handle network calls while keeping the main UI thread responsive. Game engines also use separate threads for physics, rendering, and audio processing. Understanding multithreading allows developers to build high-performance parallel systems.

---

# Part C: Technical Answers (0.5 mark)

## Question 1: Thread vs Process
A process is an independent program execution environment with its own isolated memory address space, whereas a thread is a lightweight execution unit operating within a process and sharing its memory. In this assignment, we used Java threads because spawning threads requires significantly lower creation overhead and allows direct access to shared data structures like `processQueue` and `processMap`. In our code, each simulated `Process` object is assigned to a Java thread via `new Thread(process)` in `addProcessToQueue()`, allowing the JVM to handle concurrent thread scheduling.

## Question 2: Ready Queue Behavior
When a process does not finish within its assigned time quantum, its remaining burst time is updated, and it yields the CPU to be re-enqueued at the back of the ready queue. In my program run with Student ID `445050300`, process **P2** had an initial burst time exceeding the quantum, requiring it to be re-queued twice before completion. Re-queueing ensures fairness by preventing long CPU-bound tasks from monopolizing processing time.

```text
[SCHEDULER] Dispatching process P2 (Remaining time: 7000ms)...
[P2] Executed for 3000ms. Remaining time: 4000ms.
[QUEUE] P2 (Priority: 5) added to ready queue
