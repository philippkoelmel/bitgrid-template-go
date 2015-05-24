
# Enable Docker Compose on Windows

I am using [Console2](http://http://sourceforge.net/projects/console/) with [Git's ssh.exe](https://msysgit.github.io/).

Use this to make your own docker-compose command:

	alias docker-compose="boot2docker.exe ssh -t \"docker run -v "$(pwd)":/app -v /var/run/docker.sock:/var/run/docker.sock -t -i dduportal/docker-compose:latest\""

To avoid this exception (see below), this had to be done:

1.  Use boot2docker ssh
1.  Give this ssh a fake tty
1.  Tell docker to run in interactive mode (-i)
1.  Give docker a tty (-t)

If you don't set these flags, you will spam docker containers (docker ps) and some log buffering will occure.

Here is that nasty exception:

	Traceback (most recent call last):
	  File "<string>", line 3, in <module>
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.main", line 31, in main
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.docopt_command", line 21, in sys_dispatch
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.command", line 27, in dispatch
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.docopt_command", line 24, in dispatch
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.command", line 59, in perform_command
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.cli.main", line 155, in logs
	  File "/code/build/docker-compose/out00-PYZ.pyz/compose.project", line 229, in containers
	  File "/code/build/docker-compose/out00-PYZ.pyz/docker.client", line 385, in containers
	  File "/code/build/docker-compose/out00-PYZ.pyz/docker.client", line 102, in _result
	  File "/code/build/docker-compose/out00-PYZ.pyz/requests.models", line 741, in json
	  File "/code/build/docker-compose/out00-PYZ.pyz/json", line 326, in loads
	  File "/code/build/docker-compose/out00-PYZ.pyz/json.decoder", line 365, in decode
	  File "/code/build/docker-compose/out00-PYZ.pyz/json.decoder", line 383, in raw_decode
	ValueError: No JSON object could be decoded