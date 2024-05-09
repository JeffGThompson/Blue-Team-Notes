# Commands

## One liners



### Monitor folder size

Monitors a folder and checks if it increases or decreased since the last minute.

**Linux**

```
while true; do size=$(du -sh /root/ | awk '{print $1}'); echo "$size ($(echo $size - $prev | bc) change)"; prev=$size; sleep 60; done
```



## TMUX

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

### Search current pane

```
press Ctrl-b [ = to enter copy mode
press Ctrl-s = to start search
```

## vim

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

## ls

### Finds what directory someone ran a command in

**Linux**

```
ls -la /proc/$PID | grep cwd
```

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

## ps

### Process tree

A process tree shows how processes on the system are linked to each other; processes whose parents have been killed are adopted by the init (or systemd).&#x20;

**Linux**

```
ps -aef --forest
```

## journalctl

1. **Viewing Logs**:
   * `journalctl`: Displays logs from the current boot session.
   * `journalctl --boot=-1`: Displays logs from the previous boot session.
   * `journalctl --since "2024-05-01 00:00:00" --until "2024-05-02 23:59:59"`: Displays logs within a specific time range.
2. **Filtering Logs**:
   * `journalctl _SYSTEMD_UNIT=unit_name.service`: Displays logs for a specific systemd unit (service).
   * `journalctl _PID=1234`: Displays logs for a specific process ID (PID).
   * `journalctl -u unit_name.service`: Displays logs for a specific systemd unit (service).
   * `journalctl -p err`: Displays logs with a priority level of "err" (error) or higher.
3. **Output Formatting**:
   * `journalctl -o json`: Outputs logs in JSON format.
   * `journalctl -o short`: Outputs logs in a compact, human-readable format.
   * `journalctl -o verbose`: Outputs logs with additional metadata.
4. **Real-time Logging**:
   * `journalctl -f`: Displays logs in real-time, similar to `tail -f`.
5. **Displaying Additional Information**:
   * `journalctl --disk-usage`: Displays disk usage statistics of the journal.
   * `journalctl --list-boots`: Lists all available boot sessions and their respective IDs.
   * `journalctl --list-unit-files`: Lists available systemd unit files.
6. **Other Options**:
   * `journalctl --vacuum-size=1G`: Removes old journal files until the total disk space used by the journal is reduced to 1GB.
   * `journalctl --rotate`: Forces rotation of the journal files.
7. **Useful:**
   * `journalctl -u sshd --since "2024-05-08 16:00:00" --until "2024-05-08 18:30:00"`: Check who logged in between two times
   * `journalctl -u Splunkd --since "2024-05-08 17:00:00" --until "2024-05-08 18:30:00":` Check Splunk logs between two times



## Ansible

### **Run Adhoc Command on multiple servers**

inventory needs to be a list of hosts.

**Linux**

```
ansible -i inventory all -u $USERNAME --become -k -K -m shell -a 'sudo grep somestring /path/to/file/$FILE || echo "Not found"'
```

## tar

### Archive Folder&#x20;

**Linux**

```
tar -zcvf $tarName.tar.gz $folderName
```



## du

### Show biggest to smallest folders&#x20;

Below shows top 6 folders&#x20;

**Linux**

```
 du -ah /path/to/folder | sort -rh | head -6
```

## ln

### **The difference between a hard-link and a symbolic-link (soft-link)**

#### **Hard Link**

Hard link is a mirror copy of the original file. Deleting the original file will not impact anything, because the hard link file, will act as a mirror copy of the original file.

#### Symbolic Link

A symbolic link, also known as symlink or soft link, is a special type of file that points to source file or directory in Linux. It is like a shortcut in Windows which contains the path of the original file and not the contents. In general, Symbolic links are used to link libraries and log files & folders on mounted NFS (Network File System) shares.

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Creates links to files and folders

#### Create a symbolic link to a file (or folder)

**Linux**

```
ln -s path/to/file path/to/symlink
```

#### Overwrite an existing symbolic to point to a different file

**Linux**

```
ln -sf path/to/new_file path/to/symlink
```

#### Create a hard link to a file

**Linux**

```
ln path/to/file path/to/hardlink
```



## grep

### Grep OR Statement&#x20;

**Linux**

```
grep "Eps=| HT=" /opt/splunk/superconnector/current/logs/agent.out.wrapper.log 
grep "Eps=|HT=|C=" /opt/arcsight/smartconnector/2pcc_wuc_2k12_srv_64bit_01/current/logs/agent.out.wrapper.log
```



### GREP Number Range

**Linux**

```
grep -E 'M1CacheDropped=[0-9]{3}' agent.log*
```

### GREP with Square Brackets in string

**Linux**

```
grep -i "No Smb Transports found for the host \[someText\]"
```

### Grep Recursive and Ignore Folders&#x20;

**Linux**

```
grep -R --exclude-dir=node_modules 'some pattern' /path/to/search
```



## dig

### Check if DNS is resolving host

**Linux**

```
dig @$DNS_Server_You_Want_To_Test $Server_Your_Looking_Up
```



## scp

### Receive folder from external machine to local machine

**Linux**

```
scp $USERNAME@$LOCAL_IP:$/$FOLDER/ $FILE
```

### Send local folder on local machine to external machine

**Linux**

```
scp $LOCAL_FOLDER $USERNAME@$EXTERNAL_IP:$FOLDER/
```

## git

### Squash commits before making merge request

**Linux**

```
git rebase -I HEAD~4 = 4 commits
git rebase -I sdds8e3esd 
```

## telnet

### Testing if SMTP works

```
telnet $SMTP_SERVER 25

ehlo mydomain.com 
mail from:<joe@myemail.com> 
rcpt to:<jim@youremail.com> 
data 
This is a test, please do not respond 
. 
quit
```















