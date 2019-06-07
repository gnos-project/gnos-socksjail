# GNOS socksjail

SOCKSify using tun2socks & netns

-  netns isolation (Linux network namespaces)
-  DNS over HTTPS (dnscrypt-proxy)
-  profiles with command execution
-  polkit integration

## Usage

```
USAGE:
  socksjail [ -r ] [ -v ] [ PROFILE_NAME | PROFILE_PATH [ COMMAND [ ARGS ... ] ] ]
  socksjail -d PROFILE_NAME
  socksjail -l
  socksjail -h

ARGS:
  PROFILE_NAME    Profile name, stored in /home/user/.config/socksjail/
  PROFILE_PATH    Profile path
  COMMAND         Command to execute, or "null" to keep connected
  ARGS            Command arguments

OPTS:
  -d              Disconnect profile
  -l              List active profiles
  -h              Show help
  -r              Force reconnect
  -v              Verbose output
```

## Install

Put files somewhere, for example `/opt/gnos-socksjail`, symlink `socksjail` to `$PATH`.

## Configure

Profiles are stored in `~/.config/socksjail`.

Profiles files are simple `bash` declarations.

| Variable |             Description              |
|----------|--------------------------------------|
| `addr`   | SOCKS proxy address: [IP]:PORT       |
| `auth`   | SOCKS proxy credentials: USER[:PASS] |
| `cmd`    | Command to execute in jail           |
| `pre`    | Command to execute before            |
| `post`   | Command to execute after             |

Commands are executed using `eval` to prevent quoting madness.

Running profile uses cache in `~/.cache/socksjail/PROFILE/`.
