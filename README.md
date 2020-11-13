# cpulimit-all

cpulimit wrapper for limiting CPU of multiple processes

Example usage:
```sh
./cpulimit-all.sh --limit=1 -e firefox -e firefox-esr -e chromium -e chrome\
    --watch-interval 0 --max-depth=1
```
Limit CPU of all currently running browser processes to 1%, but do not
watch for new processes.

```usage
Usage: ./cpulimit-all.sh [TARGET] [OPTIONS...] [-- PROGRAM]
   TARGET may be one or more of these (either TARGET or PROGRAM is required):
      -p, --pid=N        pid of a process
      -e, --exe=FILE     name of a executable program file
      -P, --path=PATH    absolute path name of a
                         executable program file
   OPTIONS for ./cpulimit-all.sh
          --max-depth=N  If 0, only target explicitly referenced processes.
                         Otherwise, target subprocesses up to N layers deep.
          --max-processes=N
                         Maximum number of processes to limit. After this
                         limit is reached, new processes will be limited
                         as old ones die.
          --watch-interval=INTERVAL
                         If 0, targets will be selected at setup. Otherwise,
                         every INTERVAL (argument to sleep(1)), search for
                         more possible targets.
          --subprocess-watch-interval=INTERVAL
                         During setup, delay INTERVAL (argument to sleep(1))
                         between searches for more subprocesses to avoid
                         spending 100% CPU searching for targets.
          --             This is the final ./cpulimit-all.sh option. All following
                         options are for another program we will launch.
      -h, --help         display this help and exit
   OPTIONS forwarded to CPUlimit
      -c, --cpu=N        override the detection of CPUs on the machine.
      -l, --limit=N      percentage of cpu allowed from 1 up.
                         Usually 1 - 800, but can be higher
                         on multi-core CPUs (mandatory)
      -q, --quiet        run in quiet mode (only print errors).
                         (Also suppresses messages from ./cpulimit-all.sh.)
      -k, --kill         kill processes going over their limit
                         instead of just throttling them.
      -r, --restore      Restore processes after they have
                         been killed. Works with the -k flag.
      -s, --signal=SIG   Send this signal to the watched process when cpulimit exits.
                         Signal should be specificed as a number or
                         SIGTERM, SIGCONT, SIGSTOP, etc. SIGCONT is the default.
      -v, --verbose      show control statistics
```
