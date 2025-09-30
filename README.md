# Linux-Administration-Project
This repository contains the deliverables for a three-part Linux Administration project, covering:

Part 1: Advanced Bash Scripting for user/group management and file system operations.

Part 2: Software Build Systems using both Make and CMake for a modular cryptographic application.

Part 3: Process Management and Inter-OS Communication via SSH for a multi-process task manager.


# Part 1: Bash Scripting
  Script 1: userdef
  
    Creates a new user and group, configures them, and assigns the user to the group with specific UID/GID requirements.
    
    Usage: sudo ./userdef <username> <userpass> <groupname>
    

  Script 2: filesetup
  
    Automates directory creation, file population, archiving, and deployment to a specific user's home directory.
    
    Features:
    
      Creates a directory and files (main.c, main.h, hello.c, hello.h). 
      
      Writes custom content to each file.
      
      Archives the directory and copies it to another user's home.
      
      Extracts the archive and manages file permissions.
      
      
# Part 2: Makefiles & CMake

  A project demonstrating the build process for a cryptographic application using two different ciphers. 
  
  Build Instructions:
  
    Using Make:
    
      Navigate to the Makefile_Project directory.
      
      Run make all to build the project.
      
      Run ./output/output to execute the program.
      
    
    Using CMake:
    
      Navigate to the CMake_Project directory.
      
      Create a build directory: mkdir build && cd build
      
      Configure the project: cmake ..
      
      Build the project: make
      
      Run the executable: ./output
      
  
  Test Command:
  
  ./output 3 K "aaa"
  
  
  Expected Output:
  
  text encrypted with caesar: ddd
  
  text decrypted with caesar: aaa
  
  text encrypted with xor: ***
  
  text decrypted with xor: aaa
  


# Part 3: Process Management
  Establishes an SSH connection from a Windows host to a Linux VM/WSL and runs a multi-process task manager.
  
  Key Components:
  
  SSH Setup: Configures and enables the SSH daemon on Linux for access from Windows.
  
  Task Manager Application (task_manager.c):
  
  A parent process forks two child worker processes.
  
    Worker 1: Executes a command to monitor CPU usage (e.g., mystat or mpstat).
    
    Worker 2: Executes the ps command to list active processes.

