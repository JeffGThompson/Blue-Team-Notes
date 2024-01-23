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



