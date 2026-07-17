# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

Add your screenshot here.
![Screenshot 1](<screenshots/Assignment 5/Task one/Screenshot 1 _assignment_5_task_1.png>)
#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![Evidence](<screenshots/Assignment 5/Task one/Screenshot 2_assignment_5_task_1 showing the scripts directory.png>)

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash (Bourne Again Shell) is a command-line interpreter that allows users to interact with the operating system by running commands and executing scripts. It is commonly used in Linux and macOS to automate tasks and manage systems.

**2. What is the difference between shell and Bash?**

A shell is a program that lets users communicate with the operating system. Bash is one specific type of shell. In other words, all Bash programs are shells, but not all shells are Bash.

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important to confirm the Bash version because some commands and features work only in certain versions of Bash. Checking the version helps ensure that your script is compatible and runs correctly without errors.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`
![Evidence](<screenshots/Assignment 5/Task two/Screenshot 1 — Content of `first-script.sh`.png>)

#### Screenshot 2 — Output of `./first-script.sh`
![Evidenace](<screenshots/Assignment 5/Task two/Screenshot 2 — Output of `.:first-script.sh`.png>)

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission
![Evidence](<screenshots/Assignment 5/Task two/Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission.png>)

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

Add your answer here.

#!/bin/bash is called a shebang. It tells the operating system to use the Bash shell to run the script, ensuring the commands are executed correctly.

**2. Why do we use `chmod +x` before running a script?**

Add your answer here.

We use chmod +x to make the script executable. Without this permission, the operating system will not allow the script to run directly.

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

Add your answer here.

./script.sh runs the script as an executable file and requires execute permission (chmod +x). It also uses the interpreter specified in the shebang (#!/bin/bash).
bash script.sh runs the script directly with the Bash interpreter, so it does not require execute permission.

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`
![Screenshot](<screenshots/Assignment 5/Task three/Screenshot 1 — Content of `user-info.sh`.png>)

#### Screenshot 2 — Output of `./user-info.sh`

![Screenshot](<screenshots/Assignment 5/Task three/Screenshot 2 — Output of `.:user-info.sh`.png>)

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

Add your answer here.

A variable in Bash is a named container used to store data such as text, numbers, or command outputs. It allows scripts to store and reuse values during execution.

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Add your answer here.

In Bash, spaces around the = sign are not allowed because Bash interprets the command differently. A space makes Bash think the variable name is a command and the value is an argument.

**3. How do you access the value stored inside a Bash variable?**

Add your answer here.

You access the value of a Bash variable by adding a $ symbol before the variable name.

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![Screenshot](<screenshots/Assignment 5/Task four/Screenshot 1 — Content of `tools-checklist.sh`.png>)

#### Screenshot 2 — Output of `./tools-checklist.sh`

![Screenshot](<screenshots/Assignment 5/Task four/Screenshot 2 — Output of `.:tools-checklist.sh`.png>)

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

Add your answer here.

An array in Bash is a variable that can store multiple values under a single name. Each value in the array is stored at a specific index position.

**2. Why are arrays useful in scripts?**

Add your answer here.

Arrays are useful because they allow scripts to store and manage multiple related values easily. They make it easier to process lists of items, such as filenames, usernames, servers, or software tools, using loops and other commands.

**3. What does `"${tools[@]}"` mean?**

Add your answer here.

"${tools[@]}" is used to access all elements in the Bash array named tools. The @ symbol represents all items in the array, and the quotes preserve each item as a separate value, even if it contains spaces.

**4. What is the purpose of the `for` loop in this script?**

Add your answer here.

The for loop is used to repeat a set of commands for each item in a list or array. In this script, it goes through each value in the tools array and performs an action on each tool individually.

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![Screenshot](<screenshots/Assignment 5/Task five/Screenshot 1 — Content of `counter.sh`.png>)

#### Screenshot 2 — Output of `./counter.sh`

![Screenshot](<screenshots/Assignment 5/Task five/Screenshot 2 — Output of `.:counter.sh`.png>)

### Notes

Answer the following in your own words:

**1. What is a loop?**

Add your answer here.

A loop is a programming structure that allows a set of commands to be executed repeatedly until a specific condition is met or for a defined number of times.

**2. Why do we use loops in Bash scripting?**

Add your answer here.

We use loops in Bash scripting to automate repetitive tasks, reduce the amount of code we write, and efficiently process multiple files, commands, or data items without running each command manually.

**3. How many times did the loop run in your script?**

Add your answer here.

The loop ran 5 times in the script (assuming the script was configured to repeat the command from 1 to 5).

**4. What would you change if you wanted the loop to run 10 times?**

Add your answer here.

I would change the loop condition or range from 5 to 10.
for i in {1..10}
do
    echo "Run number: $i"
done

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

![Screenshot](<screenshots/Assignment 5/Task six/Screenshot 1 — Output of `ls -lah ..:test-folder`.png>)

#### Screenshot 2 — Content of `file-check.sh`

![Screenshot](<screenshots/Assignment 5/Task six/Screenshot 2 — Content of `file-check.sh`.png>)

#### Screenshot 3 — Output of `./file-check.sh`
![Screenshot](<screenshots/Assignment 5/Task six/Screenshot 3 — Output of `.:file-check.sh`.png>)

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

Add your answer here.

The -d test checks whether a specified path exists and is a directory.

**2. What does `-f` check in Bash?**

Add your answer here.

The -f test checks whether a specified path exists and is a regular file.

**3. Why should file and directory paths be stored in variables?**

Add your answer here.

Storing file and directory paths in variables makes scripts easier to read, maintain, and update. If the path changes, you only need to update the variable instead of changing it throughout the entire script.

**4. What happens if the file does not exist?**

Add your answer here.

If the file does not exist, the -f test returns false, and the script executes the else block (if one is provided). This allows the script to handle the missing file gracefully, such as by displaying an error message or taking another action.

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

![Screenshot](<screenshots/Assignment 5/Task Seven/Screenshot 1 — Content of `score-check.sh` with `score=85`.png>)

#### Screenshot 2 — Output showing `Result: Pass`

![Screenshot](<screenshots/Assignment 5/Task Seven/Screenshot 2 — Output showing .png>)

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

![Screenshot](<screenshots/Assignment 5/Task Seven/Screenshot 3 — Content of `score-check.sh` with `score=55`.png>)

#### Screenshot 4 — Output showing `Result: Retry`

![Screenshot](<screenshots/Assignment 5/Task Seven/Screenshot 4 — Output showing.png>)
### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

Add your answer here.

The if-else statement is used to make decisions in a Bash script. It allows the script to execute different commands depending on whether a condition is true or false.

**2. What does `-ge` mean?**

Add your answer here.

-ge means greater than or equal to. It is used to compare two integer values in Bash.

**3. Why should conditions be tested with different values?**

Add your answer here.

Testing conditions with different values helps ensure the script works correctly in all scenarios. It verifies that both the true and false branches of the condition behave as expected.

**4. How can conditionals help in automation scripts?**

Add your answer here.

Conditionals help automation scripts make decisions based on different situations, such as checking if a file exists, verifying user input, or handling errors. This makes scripts more flexible, reliable, and capable of responding to different conditions automatically.

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

![Screenshot](<screenshots/Assignment 5/Task Eight/Screenshot 1 — Content of `final-automation.sh`.png>)

#### Screenshot 2 — Output of `./final-automation.sh`

![Screenshot](<screenshots/Assignment 5/Task Eight/Screenshot 2 — Output of `.:final-automation.sh`.png>)

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

![Screenshot](<screenshots/Assignment 5/Task Eight/Screenshot 3 — Output of `ls -lah` showing all created scripts.png>)

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

Add your answer here.

A function in Bash is a reusable block of code that performs a specific task. It can be called multiple times within a script, which helps avoid repeating the same code.

**2. Why are functions useful in scripts?**

Add your answer here.

Functions make scripts easier to read, maintain, and reuse. They reduce code duplication, organize related commands into logical sections, and simplify troubleshooting.

**3. Which functions did you create in this script?**

Add your answer here.

The script includes functions to perform different tasks, such as displaying messages, checking files or directories, and organizing the script into reusable sections. (Replace this with the actual function names from your script if they are different.)

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

Add your answer here.

The final script uses variables to store values, arrays to manage multiple items, loops to repeat tasks, conditionals (if-else) to make decisions, file checks to verify whether files or directories exist, and functions to organize related commands into reusable blocks. Together, these features make the script more efficient, organized, and easier to maintain.

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`


#### Screenshot — Published LinkedIn post

![LinkedIn](<screenshots/Assignment 5/Task Eight/LinkedIn.png>)

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*