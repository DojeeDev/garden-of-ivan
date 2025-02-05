+++
title = "Selfhosting for School"
date = "2025-02-02T16:53:36-07:00"
draft = 'true'

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["selfhosting", "diy", "ai", "school"]
+++

### Motivation
Selfhosting has always been something I've enjoyed. While in lots of cases selfhosting gives you a better experience and not to mention privacy and security than your typical SaaS app, even when it doesn't the satisfaction in doing it yourself almost makes up for the hours sunk into trying to make it work.  

Recently I problem I've noticed is that professors will assign hours upon hours of lectures and reading ( okay maybe I'm exaggerating a bit but it still feels like it ). In any case regardless of your stance on using AI to summarize content or to even in some cases create content it's difficult to argue against at least having the option. One of my favorite tools is ~~Open~~ClosedAI's transcription model [Whisper](https://github.com/openai/whisper). It can run on almost anything and is quite accurate and fast. It's fairly easy to use from the terminal however for my girlfriend and roommate that's not an easy option. So I thought it would be a fun and (hopefully) useful project to run a web-ui for the model off of my home server so that they could used it to transcribe videos easily. 

### Searching for a solution
Easier said than done it turns out, most solutions I found online either were poorly documented or used out of date docker commands that made them hard to install and set up. Since none of them worked out of the box I just picked one and decided to work on it until I got it working. The one I chose was [Whisper-WebUI ](https://github.com/jhj0517/Whisper-WebUI). It has all the features I need and seems to be flexible enough to get working. 

### Installation and workarounds
1. Clone the repo
`git clone https://github.com/jhj0517/Whisper-WebUI.git`
1. run `chmod +x ./Install.sh` then ./Install.sh.  
I had to edit the sh file to change the `python` to `python3` but other than that it worked without many issues. Make sure you have git, python and FFmpeg installed.
1. Now for my purposes I wanted to used this on my LAN not just the machine I was running it on. To do that go to line 308 of `app.py` and edit the server_name and change it to "0.0.0.0"
1. Add the port to your firewall or disable it temporarily (just temporarily I'm not crazy!).
You can do this on fedora server with
```
sudo firewall-cmd --add-port=7860/tcp --permanent
sudo firewall-cmd --reload
```
1. Then just edit start-webui.sh to use python3 ( if needed ). And run it.
1. Then after it starts you should be able access at <your-machines-ip>:7860
  
You could set it up as a systemd service but for my purposes it's easier to just run it in a tmux session.
