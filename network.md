# tools to monitor network connections

## definitions
* Listening: If data travels from computer A to B, ports that are in waiting state
in computer B to receive data from computer A in the network are called the
listening ports.

* Netstat
```
netstat -c
```
To continuously monitor (-c) hosts and available ports. Or use -tulpnc flag to
show all TCP and UDP (-t -u) stats along with listening ports (-l) and processes (-p)
Problem is that this moves a bit fast for the eye to catch up with.

* Iftop
Is a what `top` is for processor usage. Similar to `top`, `iftop` displays network
traffic by means of a much simpler graph. `iftop` can listen to a specific device
if we use it with the -i flag.
```
sudo iftop -i enp4s0f2
```
But `iftop` requires root access AFAIU.
Three columns at the end denotes 2s, 10s and 40s averages of data exchanged.
Pressing `s` or `d` can hide the source and destination displays respectively.
By hiding the inward or outward traffic, we can see who is who is receiving or
sending data across. Ports can be switched on by pressing `p`. pressing `t` can
show the direction of traffic (`=>` data sent, `<=` data received) in different
formats. This can also tell us whch user is using up most data.
To carefully look at some suspicious data, type `P`, and then `l`. This freezes
the screen and we can now search specifically for a particular IP address. Press
`P` again to unpause and to continue monitoring the filtered IP.

## source:
1) Humble Bundle/Practical Linux Topics
