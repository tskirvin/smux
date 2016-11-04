I like to use tmux in order to keep running sessions on my various hosts for
writing code, reading email, etc.  I have historically used
[mosh](https://mosh.org/) to connect to these sessions, but recently my place
of work has decided that udp is unacceptable.  And so I use `smux` instead.

There are three pieces to this code:

1.  tmux-session - a wrapper for tmux that makes it easy to manage 'named' 
    tmux sessions (e.g. `code`, `build`, `test`, `log`, etc) on a specific 
    host.  You can connect multiple times, create a session if it doesn't 
    yet exist, etc.

2.  smux - a version of <https://coderwall.com/p/aohfrg/smux-ssh-with-auto-reconnect-tmux-a-mosh-replacement> that is better
    suited to work with tmux-session.  Connections are kept open with
    autossh (which is tcp).

So now I can run, say, `smux ssiadmin1 code` and open a full session, which
will re-connect after a network connection goes down.
