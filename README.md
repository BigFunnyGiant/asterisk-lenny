# Lenny
Telemarketers are the worst. They have no souls. They feed off of the misery of others. No one likes them. Luckily, a nice British gentleman by the name of Lenny has come to save the day.

Setting up Lenny with Asterisk is a pretty simple task, and is also a really nice primer into Asterisk custom contexts, and the power of scripting.

First, you will want to create the Lenny context in Asterisk. SSH into your Asterisk server and use your favorite editor to edit /etc/asterisk/vitalpbx/extensions__80_lenny.conf. Add the following lines of code:

<pre>
vi /etc/asterisk/extensions__80_lenny.conf

[Lenny]
exten => talk,1,Set(i=${IF($["0${i}"="016"]?7:$[0${i}+1])})
same => n,ExecIf($[${i}=1]?MixMonitor(${UNIQUEID}.wav))
same => n,Playback(Lenny/Lenny${i})
same => n,BackgroundDetect(Lenny/backgroundnoise,1500)
</pre>

Next, use WinSCP to copy the Lenny sound files into /var/lib/asterisk/sounds/Lenny
(you may have to create the /Lenny directory).

The original README had directions here for VitalPBX with screenshots. I use this on Vanilla Asterisk. The original README is still here. The filename is Original_Readme.md 
I will work on a new README soon. I also have some ideas for new recordings and some refinement of the code. 

:smile: :smile: **I hope you enjoy it.**

**Source of information:

[Crosstalk Solutions](https://crosstalksolutions.com/howto-pwn-telemarketers-with-lenny/)

[HowTo: PWN Telemarketers with Lenny](https://www.youtube.com/watch?v=RRhRImp6kKQ)

[Pitch-perfect prank: 'Lenny' answers the campaign's call](https://ottawacitizen.com/news/local-news/pitch-perfect-prank-lenny-answers-the-politicians-call)
