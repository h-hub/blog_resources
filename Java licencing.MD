# What happened to java licence after JDK 11 ?

Simply,
  - Oracle’s JDK (commercial) – you can use this in development and testing for free, but if you use it in production you have to pay for it
  - Oracle’s OpenJDK (open source) – you can use this for free in any environment, like any open source library

That's it. You don't need to know anything else.

Anyway i have more to discuss here.
Starting with Java 11, Oracle will provide JDK releases under the open source GNU General Public License v2, with the Classpath Exception (GPLv2+CPE), and this is the Open JDK.From Java 11 this will be identical to the Oracle JDK with the exception of few cosmetic and packaging differences.

Those exceptions are:

 - -XX:+UnlockCommercialFeatures option not available in open jdk
 - Open JDk can not provide usage log data to the “Advanced Management Console” tool.
 - The output of the java --version and java -fullversion is different.
 - OpenJDK cryptography framework allowes either a valid signature or unsigned third party crypto provider.
 - Oracle OpenJDK builds are currently available as zip and tar.gz files.
 



references:
 - https://blogs.oracle.com/java-platform-group/oracle-jdk-releases-for-java-11-and-later
 - https://webcache.googleusercontent.com/search?q=cache:N8dVTNYsNHQJ:https://medium.com/%40javachampions/java-is-still-free-c02aef8c9e04+&cd=11&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:IPuWoW3U0FEJ:https://blog.jetbrains.com/idea/2018/09/using-java-11-in-production-important-things-to-know/+&cd=1&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:NeJDis-7-XYJ:https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html+&cd=1&hl=en&ct=clnk&gl=sg
 - https://developers.redhat.com/blog/2018/11/05/migrating-from-oracle-jdk-to-openjdk-on-red-hat-enterprise-linux-what-you-need-to-know/
 
