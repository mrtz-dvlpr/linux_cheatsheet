# Linux Cheat Sheet

This is a comprehensive Linux command-line cheat sheet, designed for quick reference and use in a `README.md`. It includes commands, explanations, examples, and additional details for clarity. Commands are grouped by category for easy navigation.

---

## Environment Variables

- **`export`**: Export environment variables to make them available to child processes.
  - Example: `export MY_VAR="hello"` sets `MY_VAR` for the current session.
  - Example: `export PATH=$PATH:/usr/local/bin` appends a directory to the `PATH`.

- **`$USER`**: Displays the current user's username.
  - Example: `echo $USER` outputs the logged-in user (e.g., `jadi`).

- **`$HISTFILE`**: Path to the history file (usually `~/.bash_history`).
  - Example: `echo $HISTFILE` outputs `/home/jadi/.bash_history`.

- **`$PATH`**: Lists directories searched for executable files.
  - Example: `echo $PATH` outputs `/usr/local/bin:/usr/bin:/bin`.

- **`$PS1`**: Defines the primary prompt string for the shell.
  - Example: `echo $PS1` shows the current prompt format (e.g., `\u@\h:\w\$`).
  - Modify: `PS1='\u@\h:\w\$ '` to customize the prompt.

- **`unset PS1`**: Deletes an environment variable.
  - Example: `unset MY_VAR` removes `MY_VAR`.

---

## File and Directory Operations

- **`ls -ltrha`**: Lists files with details (long format, sorted by time, reverse order, including hidden files, human-readable sizes).
  - Example: `ls -ltrha` outputs:
    ```
    drwxr-xr-x  2 jadi jadi 4.0K Oct  6 2025 dir
    -rw-r--r--  1 jadi jadi  12K Oct  6 2025 file.txt
    ```

- **`cd`**: Changes the current directory.
  - Check type: `type cd` shows `cd is a shell builtin`.
  - Example: `cd /home/jadi` navigates to `/home/jadi`.

- **`mkdir -p one/two/three`**: Creates directories recursively, even if parent directories don't exist.
  - Example: Creates `one/two/three` in one command.

- **`touch`**: Creates empty files or updates file timestamps.
  - Examples:
    - `touch file.txt` creates an empty `file.txt`.
    - `touch -t 200908121510.59 file1` sets timestamp to Aug 12, 2009, 15:10:59.
    - `touch -d "11am" file2` sets timestamp to 11:00 today.
    - `touch -d "last fortnight" file3` sets timestamp to two weeks ago.
    - `touch -d "yesterday 6am" file4` sets timestamp to yesterday 6:00.
    - `touch -d "2 days ago 12:00" file5` sets timestamp to two days ago.
    - `touch -d "tomorrow 02:00" file6` sets timestamp to tomorrow 2:00.
    - `touch -d "5 Nov" file3` sets timestamp to Nov 5 of the current year.
  - Example output of `ls -ltrh file?`:
    ```
    -rw-rw-r-- 1 jadi jadi 0 Aug 12  2009 file1
    -rw-rw-r-- 1 jadi jadi 0 Aug 12 12:00 file5
    -rw-rw-r-- 1 jadi jadi 0 Aug 13 06:00 file4
    -rw-rw-r-- 1 jadi jadi 0 Aug 14  2022 file2
    -rw-rw-r-- 1 jadi jadi 0 Aug 15  2022 file6
    -rw-rw-r-- 1 jadi jadi 0 Nov  5  2022 file3
    ```

- **`rm -r test`**: Removes files or directories recursively (use with caution).
  - Example: `rm -r test` deletes the `test` directory and its contents.

---

## File Searching and Manipulation

- **`locate`**: Finds files by name using a pre-built database.
  - Example: `locate file.txt` finds all files named `file.txt`.
  - Note: Run `updatedb` as root to update the database.

- **`find`**: Searches for files in a directory hierarchy.
  - Examples:
    - `find . -iname "*png"` finds files ending in `.png` (case-insensitive).
    - `find . -type d -size +100k` finds directories larger than 100KB.
    - `find . -size 0` finds empty files.
    - `find . -empty` finds empty files or directories.

- **`cat test.txt test1.txt`**: Concatenates and displays file contents.
  - Example: `cat file1.txt file2.txt > combined.txt` combines files into `combined.txt`.

- **`head -n10 test.txt`**: Displays the first 10 lines of a file.
  - Example: `head -n5 file.txt` shows the first 5 lines.

- **`tail -n10 test.txt`**: Displays the last 10 lines of a file.
  - Use `-f` for real-time updates: `tail -f test.txt` monitors changes.

- **`less`**: Views file contents with navigation.
  - Navigation:
    - `G`: Go to the end.
    - `nG`: Go to line `n`.
    - `n`: Next search result.
    - `?`: Search backward.
    - `/`: Search forward.
    - `PgUp`/`PgDn`: Scroll up/down.
  - Example: `less file.txt`

- **`nl`**: Numbers lines in a file.
  - Example: `nl file.txt` prefixes each line with a number.

- **`cut -f 1,2,4,7-9 -d ',' test.txt`**: Extracts columns from a delimited file.
  - Example: For a CSV file, extracts columns 1, 2, 4, and 7–9 using `,` as the delimiter.

- **`sort -n -r test.txt`**: Sorts lines numerically (`-n`) in reverse order (`-r`).
  - Use `-c` to check if the file is sorted: `sort -c test.txt`.
  - Example: `sort -n numbers.txt` sorts numbers in ascending order.

- **`paste test1.txt test2.txt`**: Merges lines from multiple files side by side.
  - Example: `paste file1.txt file2.txt` combines lines with tabs.

- **`tr 'JS' 'js' < test.txt`**: Translates characters (e.g., uppercase to lowercase).
  - Example: `cat test.txt | tr 'A-Z' 'a-z'` converts text to lowercase.

- **`sed 's/a/b/g' test.txt`**: Performs text substitutions.
  - Example: `sed 's/foo/bar/g' file.txt` replaces all `foo` with `bar`.

- **`wc`**: Counts lines, words, or characters.
  - Example: `wc -l file.txt` counts lines.
  - Example: `wc file.txt` outputs lines, words, and characters.

- **`sha256sum test.txt`**, **`md5sum test.txt`**, **`sha512sum test.txt`**: Computes file checksums.
  - Example: `sha256sum file.txt` outputs the SHA-256 hash.

- **`od -c test.txt`**, **`od -a test.txt`**: Displays file contents in octal, character, or ASCII format (useful for binary files).
  - Example: `od -c file.txt` shows characters with escape sequences.

- **`split -d -n 10 test.txt book`**: Splits a file into 10 parts with numeric suffixes (`book00`, `book01`, ..., `book09`).
  - Recombine: `cat book0* > originalfile`.

- **`dd if=~/test.txt of=~/dir/test1.txt`**: Copies files with low-level control.
  - Example: Copies `test.txt` to `~/dir/test1.txt`.

---

## Compression and Archiving

- **`gzip fileName.txt`**: Compresses a file to `fileName.txt.gz`.
- **`gunzip fileName.txt.gz`**: Decompresses back to `fileName.txt`.
- **`bzip2 fileName.txt`**: Compresses to `fileName.txt.bz2`.
- **`bunzip2 fileName.txt.bz2`**: Decompresses back to `fileName.txt`.
- **`xz fileName.txt`**: Compresses to `fileName.txt.xz`.
- **`unxz fileName.txt.xz`**: Decompresses back to `fileName.txt`.
- **`bzcat`**, **`xzcat`**, **`zcat`**, **`gzcat`**: Displays compressed file contents without decompressing.
  - Example: `zcat file.txt.gz` shows contents of a `.gz` file.

- **`tar cfz archive.tar.gz fileOne.txt fileTwo.txt`**: Creates a compressed tar archive.
- **`tar xf archive.tar.gz`**: Extracts a tar archive.

---

## History and Shell Navigation

- **`history`**: Displays command history.
  - Example: `history | tail -n 5` shows the last 5 commands.

- **`~/.bash_history`**: File storing command history.

- **`Ctrl+R`**: Searches command history interactively.
  - Example: Press `Ctrl+R`, type `ls`, and cycle through matching commands.

- **`$HISTSIZE`**: Sets the number of commands stored in memory.
  - Example: `echo $HISTSIZE` might output `1000`.

---

## Process Management

- **`ps -ef`**: Lists all processes with details.
- **`ps -aux`**: Lists processes with user-oriented format.
  - Example: `ps -ef | grep firefox` finds Firefox processes.

- **`pgrep <target>`**: Finds process IDs by name.
  - Example: `pgrep firefox` outputs Firefox PIDs.

- **`kill -15 <PID>`**: Sends SIGTERM to terminate a process gracefully.
- **`kill -9 <PID>`**: Sends SIGKILL to force-terminate a process.
  - Example: `kill -9 1234` kills process with PID 1234.

- **`killall <process name>`**: Kills all processes by name.
  - Example: `killall firefox` terminates all Firefox instances.

- **`pkill <pattern>`**: Kills processes matching a pattern.
  - Example: `pkill fire` kills processes with "fire" in their name.

- **`top`**: Displays real-time system processes.
  - Example: Press `q` to quit, `k` to kill a process.

- **`jobs`**: Lists background jobs.
- **`fg %<job number>`**: Brings a job to the foreground.
- **`bg %<job number>`**: Runs a job in the background.
  - Example: `jobs; fg %1` brings job 1 to the foreground.

- **`nohup xeyes &`**: Runs a command immune to hangups (e.g., terminal closure).
- **`^Z`**: Suspends a running process (sends to background).
- **`^C`**: Terminates a running process.

- **`nice -n 14 ls`**: Runs a command with adjusted priority (range: -20 to 19).
- **`renice -n 4 <PID>`**: Changes the priority of a running process.
  - Example: `renice -n 4 1234` adjusts priority for PID 1234.

---

## System Monitoring

- **`free -h`**: Displays memory usage in a human-readable format.
  - Example: `free -h` shows total, used, and free memory.

- **`uptime`**: Shows system uptime and load averages.
  - Example: `uptime` outputs `22:44:45 up 2 days, 3:15, 2 users, load average: 0.10, 0.12, 0.15`.

- **`watch uptime`**: Runs a command repeatedly, updating the output.
  - Example: `watch "df -h | grep sda1"` monitors disk usage for `sda1`.

---

## System Information

- **`uname -a`**: Displays system information (kernel, hostname, etc.).
  - Example: `uname -a` outputs `Linux hostname 5.15.0-73-generic x86_64 GNU/Linux`.

- **`file /bin/bash`**: Determines file type.
  - Example: `file /bin/bash` outputs:
    ```
    /bin/bash: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=33a5554034feb2af38e8c75872058883b2988bc5, for GNU/Linux 3.2.0, stripped
    ```

- **`lsusb`**: Lists USB devices.
- **`lspci`**: Lists PCI devices.
- **`lsblk`**: Lists block devices (e.g., disks).
- **`lshw`**: Lists hardware details.
  - Example: `lsblk` shows disk partitions and mount points.

---

## Kernel Modules

- **`lsmod`**: Lists loaded kernel modules.
- **`modprobe <module>`**: Loads a kernel module.
- **`rmmod <module>`**: Removes a kernel module.
  - Example: `rmmod -f snd_hda_intel` forcefully removes a sound module.
- **`insmod <module>`**: Inserts a kernel module.
- **Configuration files**:
  - `/etc/modules`: Lists modules to load at boot.
  - `/etc/modprobe.d/`: Stores module configuration.

---

## System Logs and Boot

- **`dmesg`**: Displays kernel ring buffer (boot and hardware messages).
- **`journalctl -k`**: Shows kernel logs.
- **`journalctl -b`**: Shows logs for the current boot.
- **Log files**:
  - `/var/log/boot` or `/var/log/boot.log`: Boot logs.
  - `/boot/efi/EFI/`: Bootloader files.

- **`systemctl`**: Manages system services.
  - Examples:
    - `systemctl list-units --type=target`: Lists boot targets.
    - `systemctl get-default`: Shows default boot target.
    - `systemctl cat sshd`: Displays `sshd` service configuration.
    - `systemctl stop/start/restart/reload sshd`: Controls `sshd` service.
    - `systemctl enable/disable sshd`: Enables/disables `sshd` at boot.
    - `systemctl status/is-active/is-failed sshd`: Checks `sshd` status.
    - `systemctl daemon-reload`: Reloads systemd configurations.

- **Runlevels/Boot Targets**:
  - `systemctl get-default`: Shows default target (e.g., `multi-user.target`).
  - `systemctl isolate emergency`: Switches to emergency mode.
  - `runlevel`: Displays current and previous runlevels.
  - `telinit`: Changes runlevel (e.g., `telinit 3` for multi-user mode).
  - `/etc/init.d/`: Init scripts for services.
  - `/etc/rc[0-6].d/`: Runlevel-specific scripts.

---

## Filesystem and Partitions

- **Standard Directories**:
  - `/bin`: Essential command binaries.
  - `/boot`: Boot loader files.
  - `/dev`: Device files.
  - `/etc`: System configuration.
  - `/home`: User home directories.
  - `/lib`: Shared libraries and kernel modules.
  - `/media`: Mount point for removable media.
  - `/mnt`: Temporary filesystem mounts.
  - `/opt`: Add-on software packages.
  - `/root`: Root user’s home.
  - `/sbin`: System binaries.
  - `/srv`: Service data.
  - `/tmp`: Temporary files (may be purged on boot).
  - `/usr`: Secondary hierarchy (binaries, libraries, etc.).
  - `/var`: Variable data (logs, etc.).

- **`mount | grep /dev/sda`**: Lists mounted partitions for `/dev/sda`.
- **`lsblk`**: Displays block devices and partitions.
- **`fdisk /dev/sda`**: Manages disk partitions (BIOS systems).
  - Example: `fdisk /dev/sda -l` lists partitions.
  - Commands: `p` (print partition table).
- **`gdisk /dev/sda`**: Manages partitions for UEFI systems.
- **`parted /dev/sda p`**: Displays partition information.
- **`gparted`**: GUI partition editor.

- **`mkfs.ext4 /dev/sda6`**: Formats a partition as ext4.
- **`mkswap /dev/sda6`**: Creates a swap partition.
- **`swapon /dev/sda6`**: Activates a swap partition.

---

## Bootloader (GRUB)

- **Configuration**:
  - `/boot/grub/grub.cfg`: Main GRUB configuration.
  - `/etc/grub.d/`: Scripts to generate `grub.cfg`.
  - `/etc/default/grub`: Global GRUB settings.
  - Update GRUB:
    - `grub2-mkconfig -o /boot/grub/grub.cfg`
    - `update-grub` (alias for above).
  - Install GRUB: `grub-install /dev/sda`.

- **GRUB Settings**:
  - `color`: Sets menu colors.
  - `default`: Default boot entry.
  - `fallback`: Fallback boot entry.
  - `hiddenmenu`: Hides the GRUB menu.
  - `splashimage`: Sets background image.
  - `timeout`: Menu timeout duration.
  - `password`: Sets a boot password.
  - `savedefault`: Remembers the last booted entry.
  - `root`: Defines `/boot` partition (e.g., `(hd0,1)` or `(hd0,msdos1)`).
  - `kernel`: Specifies kernel image.
  - `initrd`: Specifies initramfs image.
  - `rootnoverify`: Non-Linux root partition.
  - `chainloader`: Boots another loader (e.g., for Windows).
  - `menuentry`: Defines a menu entry.
  - `linux`/`linux16`: Linux kernel for BIOS.
  - `linuxefi`: Linux kernel for UEFI.
  - `initrdefi`: Initramfs for UEFI.

- **Notes**:
  - GRUB uses Linux-style numbering: `(hd0,1)` for first partition on first disk.
  - For GPT drives: `(hd0,gpt1)`.

---

## Shared Libraries

- **`ldd /bin/bash`**: Lists shared library dependencies.
- **`ldconfig`**: Updates the shared library cache.
- **Configuration**:
  - `/etc/ld.so.conf`: Library paths.
  - `/etc/ld.so.conf.d/`: Additional library path configurations.
  - `LD_LIBRARY_PATH`: Environment variable for custom library paths.
  - Example: `export LD_LIBRARY_PATH=/usr/local/lib`.

---

## Miscellaneous

- **`echo "hello" | xargs -I E echo morhza E`**: Passes input to a command with a placeholder.
  - Output: `morhza hello`.

- **`ls -1 | tee allfiles myfiles`**: Writes output to both a file and stdout.
  - Example: Saves `ls -1` output to `allfiles` and `myfiles`.

- **`tr ' ' '.' << END_OF_DATA`**: Translates spaces to dots in input.
  - Example:
    ```
    tr ' ' '.' << END_OF_DATA
    this is a line
    and then this
    we'll still type
    and,
    done!
    END_OF_DATA
    ```
    Output: `this.is.a.line`

- **`/dev/null`**: Discards output (black hole).
  - Example: `ls > /dev/null` suppresses output.

---

This cheat sheet is designed to be concise yet comprehensive, with examples and explanations for quick reference in a Linux environment. Save it in your `README.md` for easy access!