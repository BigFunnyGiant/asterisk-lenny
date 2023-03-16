# Lenny
Telemarketers are the worst. They have no souls. They feed off of the misery of others. No one likes them. Luckily, a nice British gentleman by the name of Lenny has come to save the day.

Setting up Lenny with Asterisk is a pretty simple task, and is also a really nice primer into Asterisk custom contexts, and the power of scripting.

First, you will want to include the Lenny context in Asterisk. SSH into your Asterisk server and use your favorite editor to edit /etc/asterisk/extensions.conf. Add the following lines of code:

<pre>
 #include extensions_lenny.conf 
</pre>

You'll want to point it to where you have the file stored, or just copy and paste the file contents into your extensions.conf.

Next, use WinSCP to copy the Lenny sound files into /var/lib/asterisk/sounds/Lenny
(you may have to create the /Lenny directory).

On my system I send any incoming unauthorized calls to the [public] context like this, it's the same as what's suggested in the [PhreakNet docs](https://docs.phreaknet.org/), but I added Lenny.

<pre>
[public]
exten => _X!,1,Log(NOTICE, Unauthorized call: ${CALLERID(all)} at "${CHANNEL(peerip)}" to ${EXTEN})
  same => n,System(iptables -A INPUT -s ${CHANNEL(peerip)} -j DROP)
  same => n,Gosub(lenny,talk,1)
  same => n,Hangup()
</pre>

The original README had directions here for VitalPBX with screenshots. I use this on Vanilla Asterisk. The original README is still here. The filename is Original_Readme.md 
I will work on a new README soon. I also have some ideas for new recordings and some refinement of the code. 

:smile: :smile: **I hope you enjoy it.**

**Source of information:

[Crosstalk Solutions](https://crosstalksolutions.com/howto-pwn-telemarketers-with-lenny/)

[Original VitalPBX Repository](https://github.com/VitalPBX/Telemarketers-with-Lenny)

[HowTo: PWN Telemarketers with Lenny](https://www.youtube.com/watch?v=RRhRImp6kKQ)

[Pitch-perfect prank: 'Lenny' answers the campaign's call](https://ottawacitizen.com/news/local-news/pitch-perfect-prank-lenny-answers-the-politicians-call)
