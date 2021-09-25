# envirun

Load **Envi**ronment from file and **run** any program with this environment.

This is useful if you want to easily run program with different environment, or troubleshoot systemd services which reads /etc/

## Installation
~~~shell
pip3 install envirun
~~~

## Example Usage
/tmp/x.sh:
~~~shell
#!/bin/sh

echo X: $X
echo $*
~~~

/tmp/x1: `X=1`
/tmp/x2: `X=2`

~~~shell
$ envirun.py /tmp/x1 /tmp/x.sh 1 2 3
X: 1
1 2 3

$ envirun.py /tmp/x2 /tmp/x.sh 1 2 3
X: 2
1 2 3
~~~

