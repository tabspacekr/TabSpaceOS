# TabSpaceOS
Armbian Based TabSpace Customized OS


# Prework Code

1. 업데이트 패키지의 빠른 다운로드를 위해 Kakao Apt Repository 추가

<pre>
sudo vi /etc/apt/sources.list
</pre>
adding
<pre>
deb http://mirror.kakao.com/debian buster main contrib non-free
#deb http://deb.debian.org/debian buster main contrib non-free
#deb-src http://deb.debian.org/debian buster main contrib non-free

deb http://mirror.kakao.com/debian buster-updates main contrib non-free
#deb http://deb.debian.org/debian buster-updates main contrib non-free
#deb-src http://deb.debian.org/debian buster-updates main contrib non-free

deb http://mirror.kakao.com/debian buster-backports main contrib non-free
#deb http://deb.debian.org/debian buster-backports main contrib non-free
#deb-src http://deb.debian.org/debian buster-backports main contrib non-free

deb http://mirror.kakao.com/debian buster/updates main contrib non-free
#deb http://security.debian.org/ buster/updates main contrib non-free
#deb-src http://security.debian.org/ buster/updates main contrib non-free
</pre>
