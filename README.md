<h1>Linux Handbook</h1>

This handbook serves as a comprehensive guide to understanding and using Linux commands effectively. It covers basic, advanced, and administrative commands, along with examples and outputs, to help users navigate and manage Linux systems efficiently.

---

<h2>Understanding Shell Commands</h2>

Most input lines entered at the shell prompt have three basic elements:

1. **Command**: The name of the program or utility you are executing.
2. **Options**: Usually starts with one or two dashes (e.g., `-p` or `--print`) and modifies the behavior of the command.
3. **Arguments**: Specifies the target or input for the command.

Some commands may not require options or arguments.

---

<details>
<summary><h2>Categorization of Commands</h2></summary>

<details>
<summary><h4><strong>1. Basic Commands</strong></h4></summary>

1. **`cat`**: Used to display the contents of a file or concatenate multiple files.

    - **Example**: `cat file.txt`
    - **Output**: Displays the content of `file.txt`.

2. **`head`**: Displays the first few lines of a file.

    - **Example**: `head file.txt`
    - **Output**: Shows the first 10 lines of `file.txt`.

3. **`tail`**: Displays the last few lines of a file.

    - **Example**: `tail file.txt`
    - **Output**: Shows the last 10 lines of `file.txt`.

4. **`man`**: Displays the manual or documentation for a command.

    - **Example**: `man ls`
    - **Output**: Opens the manual page for the `ls` command.

5. **`pwd`**: Prints the current working directory.

    - **Example**: `pwd`
    - **Output**: `/home/user`

6. **`ls`**: Lists the contents of the current directory.

    - **Example**: `ls`
    - **Output**: Lists files and directories in the current directory.

    - **Options**:
        - `-a`: Lists all files, including hidden files (those starting with `.`).
            - **Example**: `ls -a`
            - **Output**: `. .. file1 file2 .hiddenfile`
        - `-R`: Recursively lists directories and their contents.
            - **Example**: `ls -R`
            - **Output**: Displays all files and subdirectories.

7. **`tree`**: Displays the directory structure in a tree-like format.

    - **Example**: `tree`
    - **Output**:
        ```
        .
        ├── file1
        ├── file2
        └── file3
            └── subdir
        ```

8. **`cd`**: Changes the current directory.

    - **Example**: `cd /home/user`
    - **Output**: Changes the working directory to `/home/user`.

9. **`mkdir`**: Creates a new directory.

    - **Example**: `mkdir new_folder`
    - **Output**: Creates a directory named `new_folder`.

10. **`rmdir`**: Removes an empty directory.

    - **Example**: `rmdir empty_folder`
    - **Output**: Deletes the directory `empty_folder`.

11. **`touch`**: Creates an empty file.

    - **Example**: `touch file.txt`
    - **Output**: Creates a file named `file.txt`.

    - **Hidden File**: Prefix the filename with a dot (`.`) to create a hidden file.
        - **Example**: `touch .hiddenfile`
        - **Output**: Creates a hidden file named `.hiddenfile`.

12. **`mv`**: Moves or renames files.

    - **Example**: `mv file.txt /home/user`
    - **Output**: Moves `file.txt` to `/home/user`.

13. **`cp`**: Copies files.

    - **Example**: `cp file.txt /home/user`
    - **Output**: Copies `file.txt` to `/home/user`.

14. **`clear`**: Clears the terminal screen.

    - **Output**: Clears all text from the terminal.

15. **`history`**: Displays the list of previously executed commands.

    - **Output**:
        ```
        1  ls
        2  cd /home
        3  pwd
        ```

16. **`echo`**: Prints text to the terminal.

    - **Example**: `echo Hello`
    - **Output**: `Hello`

17. **`printf`**: Prints formatted text to the terminal. - **Example**: `printf "This is a ball.\n"` - **Output**: `This is a ball.`
</details>

<details>
<summary><h4><strong>2. Advanced Commands</strong></h4></summary>

1.  **`chmod`**: Changes file permissions.

    The `chmod` command is used to modify the permissions of a file or directory. Permissions determine who can read, write, or execute a file.

    -   **Permission Breakdown**:

        -   Each file or directory has three permission groups:

            1. **Owner**: The user who owns the file.
            2. **Group**: Other users in the same group as the owner.
            3. **Others**: All other users.

        -   Each group has three types of permissions:

            -   `r` → Read (4 in binary).
            -   `w` → Write (2 in binary).
            -   `x` → Execute (1 in binary).
            -   `-` → No permission (0 in binary).

        -   Permissions are represented as a combination of these values:
            -   `rwx` → Read, Write, Execute (4 + 2 + 1 = 7).
            -   `rw-` → Read, Write (4 + 2 = 6).
            -   `r--` → Read only (4).

    -   **How the Permission Number is Generated**:

        -   Permissions are represented as a three-digit number, where:
            -   The **first digit** represents the owner's permissions.
            -   The **second digit** represents the group's permissions.
            -   The **third digit** represents others' permissions.
        -   Each digit is the sum of the binary values for `r`, `w`, and `x`.

        -   **Example**:
            -   `chmod 754 file.txt`:
                -   `7` → Owner: Read (4) + Write (2) + Execute (1) = `rwx`.
                -   `5` → Group: Read (4) + Execute (1) = `r-x`.
                -   `4` → Others: Read (4) = `r--`.

    -   **Example Command**:

        -   `chmod 755 file.txt`
            -   **Explanation**:
                -   Owner: `rwx` (7).
                -   Group: `r-x` (5).
                -   Others: `r-x` (5).
            -   **Output**: Updates the permissions of `file.txt` to allow the owner full access, while the group and others can only read and execute.

    -   **Special Cases**:

        -   If the file starts with `d`, it is a directory.

            -   **Example**:
                -   `ls -l`
                    ```
                    drwxr-xr-x 2 user group 4096 Oct 10 12:00 my_directory
                    ```
                -   The `d` at the beginning indicates that `my_directory` is a directory.
                -   To change the permissions of this directory:
                    -   `chmod 755 my_directory`
                    -   **Explanation**: Grants the owner full access (`rwx`), and read/execute permissions (`r-x`) to the group and others.

        -   If the file starts with `-`, it is a regular file.
            -   **Example**:
                -   `ls -l`
                    ```
                    -rw-r--r-- 1 user group 1024 Oct 10 12:00 my_file.txt
                    ```
                -   The `-` at the beginning indicates that `my_file.txt` is a regular file.
                -   To change the permissions of this file:
                    -   `chmod 644 my_file.txt`
                    -   **Explanation**: Grants the owner read/write permissions (`rw-`), and read-only permissions (`r--`) to the group and others.

    -   **Chmod Calculator**:
        -   Use [Chmod Calculator](https://chmod-calculator.com) to easily calculate permissions.

2.  **`top`**: Displays real-time system processes and resource usage.

    -   **Example**: `top`
    -   **Output**: Displays CPU, memory usage, and running processes.

3.  **`ps`**: Displays information about running processes.

    -   **Example**: `ps`
    -   **Output**:

        ```
          PID TTY          TIME CMD
         1234 pts/0    00:00:01 bash
         5678 pts/0    00:00:00 ps
        ```

    -   **Options**:

        -   `-a`: Shows all processes associated with terminals.

            -   **Example**: `ps -a`
            -   **Output**:
                ```
                  PID TTY          TIME CMD
                 1234 pts/0    00:00:01 bash
                 5678 pts/0    00:00:00 ps
                 9101 pts/1    00:00:02 vim
                ```

        -   `-ef`: Displays detailed information about all processes.
            -   **Example**: `ps -ef`
            -   **Output**:
                ```
                 UID        PID  PPID  C STIME TTY          TIME CMD
                 root         1     0  0 10:00 ?        00:00:01 init
                 user      1234     1  0 10:01 pts/0    00:00:01 bash
                 user      5678  1234  0 10:02 pts/0    00:00:00 ps
                ```

4.  **`kill`**: Terminates a process by its PID.

    -   **Example**: `kill 1234`
    -   **Explanation**: The PID (Process ID) can be obtained using commands like `ps` or `top`. For example, running `ps` will list the currently running processes along with their PIDs.
    -   **Output**: Terminates the process with PID `1234`.

5.  **`vim`**: Opens a file in the Vim text editor.

    -   **Description**: Vim (Vi IMproved) is a highly configurable and powerful text editor used for efficiently creating and editing text files. It is widely used by developers and system administrators due to its versatility and extensive features.
    -   **Note**: Vim needs to be installed before use.
        -   **Installation Command**: `sudo apt install vim`
    -   **Example**: `vim file.txt`
    -   **Usage**:
        -   Press `i` to enter insert mode.
        -   Press `Esc` to exit insert mode.
        -   Type `:wq` to save and exit.
        -   Type `:q` to exit without saving.

    </details>

<details>
<summary><h4><strong>3. Administrative Commands</strong></h4></summary>

1. **`sudo`**: Executes commands with administrative privileges.

    - **Example**: `sudo apt update`
    - **Output**: Updates the package index.

2. **`su`**: Switches to another user account.

    - **Example**: `su username`
    - **Output**: Switches to the specified user.

3. **`sudo su`**: Temporarily switches to the root user.

    - **Example**: `sudo su`
    - **Output**: Grants root access.

4. **`apt`**: Manages software packages.
    - **Examples**:
      - `sudo apt update`: Updates the package index.
      - `sudo apt upgrade`: Upgrades all installed packages.
      - `sudo apt install packageName`: Installs the specified package.
      - `sudo apt remove packageName`: Removes the specified package.
      - `sudo apt purge packageName`: Removes the package and its configuration files.
      - `sudo apt autoremove`: Removes unnecessary dependencies.

 </details>

<details>
<summary><h4><strong>4. Networking Commands</strong></h4></summary>

1. **`ping`**: Tests the reachability of a host on a network.
   - **Example**: `ping google.com`
   - **Output**:
     ```
     PING google.com (142.250.190.78): 56 data bytes
     64 bytes from 142.250.190.78: icmp_seq=0 ttl=118 time=14.2 ms
     ```
   - **Explanation**: Sends ICMP echo requests to the specified host and measures the response time.

2. **`ifconfig`**: Displays or configures network interfaces.
   - **Example**: `ifconfig`
   - **Output**:
     ```
     eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
           inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
     ```
   - **Explanation**: Shows details about the network interfaces, such as IP address and netmask.

3. **`netstat`**: Displays network connections, routing tables, and interface statistics.
   - **Example**: `netstat -tuln`
   - **Output**:
     ```
     Proto Recv-Q Send-Q Local Address           Foreign Address         State
     tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
     udp        0      0 0.0.0.0:68              0.0.0.0:*
     ```
   - **Explanation**: Lists active network connections and listening ports.

4. **`curl`**: Transfers data from or to a server using various protocols.
   - **Example**: `curl http://example.com`
   - **Output**: Displays the HTML content of the specified URL.

5. **`wget`**: Downloads files from the web.
   - **Example**: `wget http://example.com/file.zip`
   - **Output**: Downloads `file.zip` to the current directory.

</details>

<details>
<summary><h4><strong>5. Disk and Filesystem Management</strong></h4></summary>

1. **`df`**: Displays disk space usage.
   - **Example**: `df -h`
   - **Output**:
     ```
     Filesystem      Size  Used Avail Use% Mounted on
     /dev/sda1        50G   20G   30G  40% /
     ```
   - **Explanation**: Shows the available and used disk space in a human-readable format.

2. **`du`**: Displays disk usage of files and directories.
   - **Example**: `du -sh /home/user`
   - **Output**:
     ```
     1.2G    /home/user
     ```
   - **Explanation**: Shows the total size of the specified directory.

3. **`mount`**: Mounts a filesystem.
   - **Example**: `mount /dev/sdb1 /mnt`
   - **Output**: Mounts the device `/dev/sdb1` to the `/mnt` directory.

4. **`umount`**: Unmounts a filesystem.
   - **Example**: `umount /mnt`
   - **Output**: Unmounts the filesystem mounted at `/mnt`.

5. **`fdisk`**: Partition management tool.
   - **Example**: `fdisk /dev/sda`
   - **Output**: Opens an interactive session to manage partitions on `/dev/sda`.

</details>

<details>
<summary><h4><strong>6. Archiving and Compression</strong></h4></summary>

1. **`tar`**: Archives files into a single file.
   - **Example**: `tar -cvf archive.tar file1 file2`
   - **Output**: Creates an archive named `archive.tar` containing `file1` and `file2`.

2. **`gzip`**: Compresses files.
   - **Example**: `gzip file.txt`
   - **Output**: Compresses `file.txt` into `file.txt.gz`.

3. **`zip`**: Compresses files into a zip archive.
   - **Example**: `zip archive.zip file1 file2`
   - **Output**: Creates a zip archive named `archive.zip` containing `file1` and `file2`.

4. **`unzip`**: Extracts files from a zip archive.
   - **Example**: `unzip archive.zip`
   - **Output**: Extracts the contents of `archive.zip` into the current directory.

</details>

<details>
<summary><h4><strong>7. System Monitoring</strong></h4></summary>

1. **`uptime`**: Displays system uptime and load average.
   - **Example**: `uptime`
   - **Output**:
     ```
     10:00:00 up 5 days,  3:42,  2 users,  load average: 0.00, 0.01, 0.05
     ```
   - **Explanation**: Shows how long the system has been running and the average system load.

2. **`free`**: Displays memory usage.
   - **Example**: `free -h`
   - **Output**:
     ```
                   total        used        free      shared  buff/cache   available
     Mem:           8.0G        2.5G        4.0G        500M        1.5G        5.0G
     Swap:          2.0G        0.5G        1.5G
     ```
   - **Explanation**: Shows the total, used, and available memory in a human-readable format.

3. **`vmstat`**: Displays system performance statistics.
   - **Example**: `vmstat 1`
   - **Output**:
     ```
     procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
      r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
      1  0      0  4000M  1000M  2000M    0    0     0     0  100  200  5  1 94  0  0
     ```
   - **Explanation**: Provides real-time statistics on CPU, memory, and I/O usage.

</details>

</details>

---

<h2>File Paths</h2>

1. **Absolute Path**: Starts with `/` and specifies the full path.

    - **Example**: `/home/user/file.txt`

2. **Relative Path**: Does not start with `/` and is relative to the current directory.
    - **Example**: `file.txt`

---

<h2>User Prompts</h2>

-   `$`: Represents a regular user.
-   `#`: Represents a super user (root user).
