# iBoot Environment Variable Overflow
This write-up is an analysis of iOS 3.0 iBoot Environment Variable Overflow exploit. This bug in iBoot's parsing commands and environment variables has been used by PurpleRa1n jailbreak tool back to iOS 3.x era. Goals of this project are to learn about how an iOS low-level exploit works abd how to implement it properly in order to acheive unsigned code execution.

1. **Actual information about the exploit** 
First, since this is a public exploit, there is few information available on Internet. Here is few interesting links I found about.
https://www.theiphonewiki.com/wiki/Purplera1n
https://www.theiphonewiki.com/wiki/IBoot_Environment_Variable_Overflow


2. **Setting up work environment**
Apple usually respond quickly about reported bugs in their products by releasing software updates. That bug we are talking about was in iBoot, which is a software flashable component that can be easily updated. Since this iOS 3.0 iBoot bug has been publicly available, Apple soon released iOS 3.0.1 which patch it. So, that overflow is not possible in iOS 3.0.1 iBoot. Apple also implemented image validation also known as SHSH protocol at that time, which prevent unsigned downgrades. Since Apple closed iOS 3.0 signatures distribution, there is no way to downgrade back to iOS 3.0 without hack something early in the BootROM or in the actual signed iOS bootchain of trust.

In order to analyze and try to manually implement that bug, we have to reproduce that 2009 iOS 3.0 environment. According to reasons above, we need to run unsigned code in order to downgrade. Actually, there is few ways to acheive this.

1. Using Limera1n BootROM exploit :
We pwn the SecureROM using Limera1n, then directly upload a stock (not pactched) iBSS or iBEC. Interesting fact : In early 4.x builds and older, iBSS is actually a secondary stage bootloader, mostly identical as iBEC.
