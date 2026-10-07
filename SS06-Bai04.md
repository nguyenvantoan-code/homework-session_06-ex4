root@103725795523314:~# cat <<'EOF' > loop-monitor.sh
#!/bin/bash
while true; do
    echo "System time: $(date)" >> /tmp/monitor.log
    sleep 5
done
EOF
root@103725795523314:~# cat loop-monitor.sh
#!/bin/bash
while true; do
    echo "System time: $(date)" >> /tmp/monitor.log
    sleep 5
done
root@103725795523314:~# chmod +x loop-monitor.sh
root@103725795523314:~# nohup ./loop-monitor.sh > /dev/null 2>&1 &
[1] 221641
root@103725795523314:~# pgrep -f loop-monitor.sh
221641
root@103725795523314:~# tail -n 10 /tmp/monitor.log
System time: Wed Oct  7 03:02:41 PM BST 2026
System time: Wed Oct  7 03:02:46 PM BST 2026
System time: Wed Oct  7 03:02:51 PM BST 2026
System time: Wed Oct  7 03:02:56 PM BST 2026
System time: Wed Oct  7 03:03:01 PM BST 2026
root@103725795523314:~# pgrep -f loop-monitor.sh
221641
root@103725795523314:~# kill -15 220500
-bash: kill: (220500) - No such process
root@103725795523314:~# ps aux | grep loop-monitor.sh
root      221641  0.0  0.0   7344  3712 pts/0    S    15:02   0:00 /bin/bash ./loop-monitor.sh
root      221692  0.0  0.0   6684  2304 pts/0    S+   15:04   0:00 grep --color=auto loop-monitor.sh
