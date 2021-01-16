# Upgrading simple shells

### Spawning TTY

If Python is present on the target machine, the first method below is very reliable.  Otherwise, the other options are worth trying but don't always work.

```text
python -c "import pty; pty.spawn('/bin/bash')"
```

{% hint style="info" %}
Be sure to check for other versions of Python!
{% endhint %}

```text
echo os.system('/bin/bash')
```

```text
/bin/sh -i
```

### Tab auto completion

The following commands will give tab autocompletion, but other features such as SIGINT, history, and clear screen will not work.

```text
CTRL + Z (background the session)
stty raw -echo 
fg
reset
```

### Full TTY

The following commands will correct formatting errors and provide the remaining features including SIGINT, history, and the ability to clear your screen.

```text
# on attack machine
stty -a (note number of rows and columns)
echo $TERM

#on target machine
export TERM=xterm-256color (match term from attack machine)
stty row XX columns XXX (match from attack machine)

echo $SHELL -- if not bash, export SHELL=bash
```

