Release standards (RC bugs)
----------

[What they are for packages](testing/rc_policy.txt)
[What they are for architectures](testing/arch_policy.html)
[Which of them aren't being met](https://bugs.debian.org/release-critical)
[Architecture status](testing/arch_qualify.html)
[Freeze policy](testing/freeze_policy.html)
[Unblock requests FAQ](testing/FAQ.html)

Recent stable release updates
----------

* `[2025-08-09]` [Bits from the Stable Release Managers](https://lists.debian.org/aJe0GaBk6XYuZugI@powdarrmonkey.net)
* `[2019-08-04]` [Bits from the Stable Release Managers](https://lists.debian.org/1564950897.14830.21.camel@adam-barratt.org.uk)
* `[2018-04-16]` [Bits from the Stable Release Managers](https://lists.debian.org/debian-devel-announce/2018/04/msg00007.html)

Recent release updates
----------

* `[2025-08-09]` [Bits from the Release Team: checks, calendars, and cleanups](https://lists.debian.org/debian-devel-announce/2025/09/msg00001.html)
* `[2025-08-09]` [Bits from the Stable Release Managers](https://lists.debian.org/debian-devel-announce/2025/08/msg00003.html)
* `[2025-08-09]` [Bits from the Release Team: Let's Fork(y)!](https://lists.debian.org/debian-devel-announce/2025/08/msg00002.html)
* `[2025-07-19]` [trixie release planning](https://lists.debian.org/debian-devel-announce/2025/07/msg00003.html)
* `[2025-05-18]` [Bits from the Release Team: hard frozen trixie](https://lists.debian.org/debian-devel-announce/2025/05/msg00004.html)
* `[2025-03-29]` [Bits from the Release Team: trixie freeze started](https://lists.debian.org/debian-devel-announce/2025/03/msg00011.html)
* `[2025-01-22]` [Bits from the Release Team: trixie freeze dates](https://lists.debian.org/debian-devel-announce/2025/01/msg00004.html)
* `[2023-12-16]` [Bits from the Release Team: Cambridge sprint update](https://lists.debian.org/debian-devel-announce/2023/12/msg00003.html)
* `[2023-06-10]` [Bits from the Release Team: a trixie customer](https://lists.debian.org/debian-devel-announce/2023/06/msg00001.html)
* `[2023-06-04]` [Bits from the Release Team: bookworm nearly ready for release](https://lists.debian.org/debian-devel-announce/2023/06/msg00000.html)

Planned point releases
----------

Planned point releases to Q4 2026 are as follows:

|   Date    | Versions  |     Notes     |
|-----------|-----------|---------------|
|6 Sep 2025 |12.12, 13.1|               |
|15 Nov 2025|   13.2    |               |
|10 Jan 2026|12.13, 13.3|               |
|14 Mar 2026|   13.4    |               |
|16 May 2026|12.14, 13.5|               |
|11 Jul 2026|12.15, 13.6|bookworm to LTS|
|12 Sep 2026|   13.7    |               |

These dates are subject to change and the confirmed date for each version will be announced via [debian-stable-announce@lists.debian.org](https://lists.debian.org/debian-stable-announce).

Key release dates
----------

Debian 13 "trixie" was released on 9 August 2025.

Useful links
----------

* [Frozen packages](/britney/hints/freeze)
* [Removal and entering hints](/britney/hints/)
* [On the topic of key packages and autoremoval](/key-packages.html)
* [List of candidates for automatic removal from testing](https://udd.debian.org/cgi-bin/autoremovals.cgi)
* [List of key packages](https://udd.debian.org/cgi-bin/key_packages.yaml.cgi)
* [Packages blocked from uploads to unstable due to transitions](https://ftp-master.debian.org/transitions.yaml)
* [Transition tracker](/transitions/)
* [Documentation on requesting binNMUs and other wanna-build actions](/wanna-build.html)
* [NEW queue summary for stable-proposed-updates](/proposed-updates/stable.html)
* [NEW queue summary for oldstable-proposed-updates](/proposed-updates/oldstable.html)
* [Autopkgtest pseudo excuses for experimental](/britney/pseudo-excuses-experimental.html)
* [Our wiki site](https://wiki.debian.org/Teams/ReleaseTeam)
* [Our tools](tools.html)

Suite update policy
----------

[stable](https://www.debian.org/releases/stable/)Fast response for security updates. Minor updates include
security and other important fixes only. Major updates are sourced
from testing, and are infrequent, but large. [testing](https://www.debian.org/devel/testing)Security updates are irregular and unreliable. Release standards
are almost continually met. Updates are automatically sourced from
unstable, happen four times each day and are usually small. [unstable](https://www.debian.org/releases/sid/)Security updates are made by the maintainer; they may not be
effective on all architectures, and may be delayed. Packages uploaded
may not meet release standards, but any breakage is expected to be fixed
promptly. Updates are made by maintainers. experimentalPackages that are not suitable for widespread use yet. They may
or may not meet release standards, as it is commonly used as a staging area
for uploads to unstable. Updates are made by maintainers.
