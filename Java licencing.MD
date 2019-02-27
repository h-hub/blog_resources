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
 
Oracle JDK and Open JDK will be fucntionally equal.We can run our applications without any changes or loosing any features.
Oracle JDK can be used with a commercial licence while Open JDK can be used as a open source software.

## Support and Updates

If you are a paid Oracle JDK customer you will get support and updates as per the licence. But if your are using Open JDK, you won't get updates for the past versions. You will have to use the latest JDKs as they come out or run the old JDK without updates.
However, there are other vendor such as  Azul, IBM and Red Hat which provide JKD (Paid and free plans).

On 08/17/2018 05:36 PM, Stephen Colebourne has said
> OpenJDK is a community project. It's up to the community to support
> it. In practice this means that a group of organizations and
> individuals will maintain each OpenJDK LTS release for some period
> (TBA for 11, but it's sure to be a *lot* longer than six months.) I am
> certain that there will be a jdk11u project, and it will be properly
> and professionally run. I think it's likely that I'll be leading the
> project, but someone else may be chosen. Given that we don't know when
> Oracle will end their support it's hard to say any more.

Oracle will lead the first 6 month of the Open JDK LTS. But after wards updates will only be provided to Oracle JDK. At this point oracle will hand over the work to other providers and those vendors as i have mentioned ealier will have the options provide updates and support.

These other JDKs could difere from Oracle JDKs, but Technology Compatibility Kit will ensure that binaries of those JDKs are compatible with the Java SE standard


references:
 - https://blogs.oracle.com/java-platform-group/oracle-jdk-releases-for-java-11-and-later
 - https://webcache.googleusercontent.com/search?q=cache:N8dVTNYsNHQJ:https://medium.com/%40javachampions/java-is-still-free-c02aef8c9e04+&cd=11&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:IPuWoW3U0FEJ:https://blog.jetbrains.com/idea/2018/09/using-java-11-in-production-important-things-to-know/+&cd=1&hl=en&ct=clnk&gl=sg
 - https://webcache.googleusercontent.com/search?q=cache:NeJDis-7-XYJ:https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html+&cd=1&hl=en&ct=clnk&gl=sg
 - https://developers.redhat.com/blog/2018/11/05/migrating-from-oracle-jdk-to-openjdk-on-red-hat-enterprise-linux-what-you-need-to-know/
 - http://webcache.googleusercontent.com/search?q=cache:NL9mRCAp6p8J:mail.openjdk.java.net/pipermail/jdk-dev/2018-August/001830.html+&cd=1&hl=en&ct=clnk&gl=sg
 
