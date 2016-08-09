# InterceptSQL
This powershell script is able to capture, extract and reconstruct sql statements that go through the network card, without needing access to database credetials, nor password to the encrypted scripts. The idea is very simple: if we have sql statements being sent from a client to a remote sql server, these should/will have to travel through the network. There are several technologies in the market to capture network traffic, so can we not use these technologies, to capture our sql statements? The answer is: YES, WE CAN, and this script is part of this process.

There are two phases to the whole thing:
1. Enable tracing on the network card;
2. Analyse the trace.

1. Enable tracing...
Microsoft was so kind to introduce a tool with Windows server 2008 onwards called "netsh" which in essence is a cmd/powershell
command. The great potential of this methodology is that we don't need to install anything on the customer's environment;

So, all we have to do is:
a. Open powershell on the client machine and type: netsh trace start capture=yes IPv4.Address=<ip address of the db server>. This will enable tracing of any traffic leaving our client, going to the db server;
b. Reproduce a problem that we know will issue sql statements to the db;
c. Type Netsh trace stop, into the powershell console
d. Collect the *.etl file from the location stated on the powershell console, right after executing step a.

From here all is left to do is to analyze the trace using our script... BUT... at this momentt(and I'm working on this) our script doesn't understand *.etl files so we will need to convert it to *.cap. This can be done with an app called Microsoft Message analyzer, by following the steps documented here: https://blogs.technet.microsoft.com/yongrhee/2013/08/16/so-you-want-to-use-wireshark-to-read-the-netsh-trace-output-etl/

2. Analyze the trace
We need to set up our machine to analyse the trace. The good news is that this set up only needs to be done once and we will be able to run our script without any further steps. So, you will need to download a file called tshark, from here maybe:

Almost fun time!!! Type this to powershsell:
cd <location of your powershell script>


Open cmd and run: netsh trace start capture=yes IPv4.Address=<here goes the IP you want to monitor>. Th
