# file-unchanged-alert

[![CI](https://github.com/andornaut/file-unchanged-alert/actions/workflows/test.yml/badge.svg)](https://github.com/andornaut/file-unchanged-alert/actions/workflows/test.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Send an email if a file hasn't changed within a given number of seconds.

## Usage

```bash
# Send an email if /var/log/messages hasn't changed in the last 2 minutes
./file-unchanged-alert /var/log/messages 120 admin@example.com
```

## Alert on Docker logs

```bash
containerName=example
containerId=$(docker ps --filter "name=${containerName}" --quiet)
containerLogPath=$(docker inspect ${containerId} --format='{{.LogPath}}')
sudo file-unchanged-alert "${containerLogPath}"
```

## Example crontab entry

Output a warning message to stdout when a file hasn't changed in 6 minutes (the default).
You can [configure cron](https://man7.org/linux/man-pages/man5/crontab.5.html)
to send an email when this occurs.

```text
5 * * * * root /usr/local/bin/file-unchanged-alert  /file/path
```
