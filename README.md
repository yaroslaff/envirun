# envirun

Load **environment** from file and **run** any program with this loaded environment.

This is useful if you want to easily run program with different environment, or troubleshoot systemd services which reads environment from /etc/default/ files.

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

/tmp/x1.env: `X=1`
/tmp/x2.env: `X=2`

~~~shell
$ envirun.py /tmp/x1.env /tmp/x.sh some args
X: 1
some args

$ envirun.py /tmp/x2.env /tmp/x.sh some other args --foo --bar
X: 2
some other args --foo --bar
~~~

## Source code
See environ.py, it's **very** simple. Main code is just three lines:

~~~python3
load_dotenv(dotenv_path=sys.argv[1], override=True)
rc = subprocess.run(sys.argv[2:])
sys.exit(rc.returncode)
~~~

## More details
Environment files are loaded using [dotenv](https://github.com/theskumar/python-dotenv) load_dotenv(), overriding existing env variables. Environment lines may start with `export`. See [dotenv](https://github.com/theskumar/python-dotenv) documentation if you want more details.

See also similar project: [envrun](https://github.com/JanLikar/envrun)

How to achieve same result without envirun in bash (with few more commands):

~~~shell
$ set -a
$ . /tmp/x1.env  # Load environment from /tmp/x1.env file
$ set +a
$ /tmp/x.sh some args
X: 1
some args
~~~