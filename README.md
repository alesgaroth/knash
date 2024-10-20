KNASH  Kloud Network Application SHell

In Summer 1998, during my last term of my Computer Science degree, I had the idea of a command
line shell that would run programs on any computer on the network.   We only had a couple of
computers in our home network, and I didn't really get a chance to try it out.

2024 October 19 (over 26 years later) I finally recognized that the idea might work on a kubernetes cluster, or cloud cluster.

The general idea is that if I wrote
```
./long_running_process &
```
it would that process "somewhere" and not necessarily on the same machine that's receiving my
typed commands.  If I wrote
```
for i in 1000; do
   ./long_running_process &
done
```
it would run 1000 processes across as many machines as made sense, and I, as user, wouldn't think about where they ran.

```
./one_long_running_process | ./second_long_running_process | ./third_long_running_process
```
might run the processes on three different machines in the same cluster, pre-connecting the stdin and stdout between them, and stderr to my terminal.

A more interesting version would be:
```
./one_long_running_process |4 ./second_long_running_process | ./third_long_running_process
```
which cause 4 copies of second_long_running_process to be run (on 1 to 4 different machines)
where the copies take turns reading from the queue.  This implies that each line of the output can be considered as a separate record.
