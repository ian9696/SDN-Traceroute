# SDN Traceroute
Ryu Controller Application with binary search traceroute functionality in Software-Defined Networking (SDN) with OpenFlow 1.3, implemented using Python, RYU SDN Framework, Dragon Knight, Mininet.

# Usage
1. Install [RYU SDN Framework](https://github.com/faucetsdn/ryu), [Dragon Knight](https://github.com/Ryu-Dragon-Knight/Dragon-Knight), [Mininet](https://github.com/mininet/mininet)(for testing).
2. Copy simple_switch_13_5.py to /usr/lib/python3/dist-packages/ryu/app/.
3. Copy dk_plugin.py and rest.py to /usr/local/lib/python3.8/dist-packages/Dragon_Knight-1.1.0-py3.8.egg/dragon_knight/.
4. Run Dragon Knight daemon (dragon-knightd or daemon.py).
```
$ python3 /usr/local/lib/python3.8/dist-packages/Dragon_Knight-1.1.0-py3.8.egg/dragon_knight/daemon.py
```
5. Run Dragon Knight CLI (dragon-knight or cli.py).
```
$ python3 /usr/local/lib/python3.8/dist-packages/Dragon_Knight-1.1.0-py3.8.egg/dragon_knight/cli.py
```
6. Install simple_switch_13_5.py in Dragon Knight CLI.
```
$ install /usr/lib/python3/dist-packages/ryu/app/simple_switch_13_5.py
```
Dragon Knight daemon will run controller application automatically after installation.
7. Run Mininet and create 10 switches in linear topology.
```
$ sudo mn --clean
$ sudo mn --topo=linear,10 --mac --controller=remote
```
Switches will connect to Ryu controller application automatically.
8. Test network reachability in Mininet
```
$ pingall
```
9. Disconnect links between switches.
```
$ link s3 s4 down
$ link s4 s5 down
$ link s9 s10 down
```
10. Run traceroute command in Dragon Knight CLI.
```
$ custom tr h1 h10
```

# Why dragon-knight
We need to commuicate with controller via command line. We try to create a thread to implement this function, but it seems doesn't work in Python. However, dragon-knight provide a UI to solve this problem.

# Demo example
By simple, we can test linear topology in mininet.
```
sudo mn --topo linear,5 --mac --switch ovsk,protocols=OpenFlow13 --controller remote
```
Now, linear topology is build. Then type the following in dragon-knight command line.
```
tr h3 h5
```
It will show the result in dragon-knight daemon.
