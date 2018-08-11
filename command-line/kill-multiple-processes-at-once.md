### Kill multiple processes at once

Using pgrep it's possible to kill multiple processes at once. Passing the PIDs via xargs to kill is even better.

`pgrep docker | xargs kill -9`

Other example(s):

`a variation on above but with more advanced functionality`

- Source(s)
  - [1](https://unix.stackexchange.com/questions/138202/can-i-chain-pgrep-with-kill)
  - [2](https://www.linuxquestions.org/questions/linux-newbie-8/how-do-i-extract-the-pid-field-from-ps-aux-command-361150/)
