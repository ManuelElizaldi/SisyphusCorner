The message arrived on my phone at 4:42 on a Sunday afternoon:

```
Server Hard Drive Health:
Disk Usage: 1% 
```

Nothing after the colon. The script had run, curl had fired, Telegram had delivered. Every part of the system worked. The only thing missing was the answer to the question the whole thing existed to ask



Screen shot of my bot with the empty message

---

I have a 2TB SSD attached to a Raspberry Pi, shared across my network over Samba. It started as somewhere convenient to put things. Now it holds my coding projects, raw video files, and every scan from my film photography. None of that arrived through a decision. There was never a meeting where I designated it critical infrastructure. It accumulated, one directory at a time, until moving off it would cost me a weekend I do not want to spend.

Economists call this path dependence. Early choices constrain later ones, not because they were correct but because everything downstream got built on top of them. The classic example is US housing: timber was abundant when the building codes, the trade skills, and the mortgage underwriting all took shape, so wood-frame construction stayed dominant long after the original abundance stopped being the reason. The path held because the path was already there.

My SSD is a small version of the same thing. It became load-bearing while I was not paying attention. And the piece of my home lab I depend on most was the piece with no instrumentation on it at all. Everything else in the stack has monitoring. Prometheus scrapes the node, Grafana charts it, Uptime Kuma watches the services, and a Telegram bot tells me when something goes down. Earlier in that build I lost two hours to a web server that was not running, because I had assumed the wrong architecture. You can read more about that one here: [I Spent Two Hours Debugging a Web Server My System Didn't Need](https://www.linkedin.com/pulse/i-spent-two-hours-debugging-web-server-my-system-didnt-elizaldi-yvzdc/).

So the drive got a script.

### What the script needed to know

Two questions, and they are not the same question.

Is the hardware failing? That comes from SMART, the firmware inside the drive that tracks its own wear: reallocated sectors, power-on hours, write endurance consumed. The drive knows it is dying before the filesystem does. So we use smartctl, from the smartmontools package, to ask the drive how it is doing.

Is the volume full? SMART cannot give us the usage percentage, but df -h can. A drive at 99% capacity reports perfect health right up until writes start failing, so the two readings have to come from two different places.

Both answers, one message, sent by a bot I already had running for service uptime.

### The parts I did not expect to learn

I thought this was a simple project I could finish in an evening. Ten lines of bash, a curl command, done. It turned into a bash lecture.

**Cron runs your script in a different world than your shell does.** When you type a command, your shell finds it by walking PATH, a list of directories assembled at login by your profile scripts. Cron never logs in. It hands over a stripped environment, roughly /usr/bin:/bin and little else. smartctl lives in /usr/sbin, which is not on that list. So a script that runs perfectly by hand fails silently on schedule, and the fix is to declare PATH explicitly at the top and use absolute paths for the binaries that matter. Cron does not break absolute paths. Cron is the reason you need them.

Cron also has no terminal. Any echo you left in for debugging writes to nowhere. If you want to know what happened, you redirect to a log file, >> logfile 2>&1, where the 2>&1 folds stderr into the same stream.

**Sudo has a configuration file, and it can lock you out.** smartctl needs root to talk to the device, but cron cannot answer a password prompt. The answer is a sudoers rule granting passwordless execution of exactly the command you need:

```
manu ALL=(root) NOPASSWD: /usr/sbin/smartctl -H /dev/sda 
```

That is one read-only health check on one device, and nothing else. The tempting version is NOPASSWD: ALL, which means anything running as my user has silent root over the entire machine. Same instinct as scoping an IAM policy to one bucket instead of attaching AdministratorAccess and moving on.

The file gets edited with visudo rather than nano, because sudoers is parsed strictly and an invalid file means sudo refuses to run at all, including the sudo you would need to fix it. visudo validates before it saves. On a headless machine that check is the difference between a typo and a trip to find a monitor.

**Bash comparisons do not use the symbols.** Coming from Python I reached for > and >=. Inside [ ], > is output redirection. Writing [ "$USAGE" > 85 ] does not compare anything. It creates a file named 85 and the test passes unconditionally. Numeric comparison uses -gt, -ge, -lt, -le, -eq, -ne.

Underneath that is a stranger fact: bash has no types. Every variable is a string. There is no conversion step, no int(). What changes is the operator, which decides how to interpret the characters. -ge parses both sides as integers. = compares them alphabetically. Which is why I strip the percent sign off the df output at capture time rather than at comparison time, since [ "1%" -ge 85 ] throws an error instead of an answer.

**Functions exist, and they do not return values.** return in bash sends back an exit status, an integer from 0 to 255 where 0 means success. It is a status code, not data. To get data out of a function you print to stdout and capture it with command substitution, $( ). Which turns out to be the same mechanism I was already using to capture the output of smartctl and df. My own functions compose exactly the way the built-in tools do, using the same plumbing. That is the Unix design showing through, and it is more elegant than the limitation first appears.

### The blank value

Which brings me back to the message with nothing after the colon.

The cause was three characters. I had written the device path as dev/sda/ instead of /dev/sda. No leading slash makes it a relative path, so the script looked for the drive inside its own working directory and found nothing. smartctl errored out. The output it errored to was stderr, which command substitution does not capture. awk received an empty stream and matched nothing. The variable was assigned an empty string, and an empty string appended cleanly to my message.

Every step succeeded at its own job. The failure had nowhere to surface.

I caught it because I was sitting at the terminal watching the message land. Now move that same run to 8:00 on a Tuesday morning with cron executing it and me asleep. The message arrives, I glance at it over coffee, and the missing word after the colon reads as formatting rather than absence. A monitoring script that cannot determine the answer looks identical to a monitoring script delivering good news.

The fix is that the script now recognizes three states instead of two:

```
if [ -z "${SMARTMSG}" ]; then
  ALERT_MESSAGE+="ALERT: health check returned nothing"$'\n'
fi 
```

Healthy. Unhealthy. And unknown, which is its own alert, because "I could not determine the health of your drive" is not a quieter version of "your drive is fine." It is a different sentence entirely.

That distinction is not really about bash. I build reports against healthcare data for a living, and a dashboard showing zero records because the extract failed looks the same as a dashboard showing zero records because there were none. Same shape. Same silence. The number that is missing and the number that is genuinely zero render identically, and only one of them means you should be worried.

### What actually happened when it worked

The script runs daily now. Most days it says nothing, which is the point. Weekly it sends a digest, less because I need the reading and more because a message arriving proves the script is still alive. If anything crosses a threshold, it sends immediately with the specific condition named, not just the word "problem."

The part I did not expect was how it felt when the first real message came through. My phone is where I talk to people. The Pi is where I work. Those two things had never had anything to say to each other. Now the machine in the corner of my apartment tells me, unprompted, that the drive holding four years of my work is healthy, and it tells me on the same screen where my friends text me.

That connection is the thing that keeps pulling me forward on this build. I set out to make one project, a home lab. What I keep finding is that the project generates its own next projects. Monitoring the drive was never on a roadmap. It came out of building the thing, out of noticing what I had started to depend on. Terraform is next, and I suspect that one will spawn two more.

The drive is at 1%. I will find out about the other 99% one percentage point at a time.