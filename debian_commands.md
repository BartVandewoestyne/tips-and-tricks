# Debian GNU/Linux commands

To see what packages are the biggest:<br>
Method 1:
```
wajig size
```
Method 2:
```
dpkg-query -W --showformat='${Installed-Size} ${Package}\n' | sort -n
```
Method 3:
```
dpkg-query -W --showformat='${Installed-Size} ${Package} ${Status}\n' | sort -n | grep installed
```

To see to what package a file belongs:
```
$ dpkg -S /my/file
```

Search for packages and fetch info from a package:
```
$ aptitude search <packages>
```
The above command only searches in package names.
```
$ aptitude search ~d"RegEx"
```
The above command matches packages whose description matches the regular expression RegEx. 
See also http://algebraicthunk.net/~dburrows/projects/aptitude/doc/en/ch02s03s05.html.
```
$ apt-cache search zoekterm
$ apt-cache search "een zoekterm"
```

to see the description of on or more packages:
```
$ aptitide show <packages>
```

## Cleaning up a Debian system

To remove all packages of which the system can detect that they are no longer necessary:
```
# apt-get autoremove --purge
```

To remove packages (libs and data) that are no longe rused or that are in the rc-state:
```
# deborphan --find-config | xargs aptitude -y purge
# dpkg -l | grep ^rc | cut -d' ' -f3 | xargs aptitude -y purge
# deborphan | xargs aptitude -y purge
# deborphan --guess-data | xargs aptitude -y purge
```

To remove transitional Debian packages:
```
# dpkg -l | grep transitional | cut -c5-39 | xargs aptitude -y purge
```

In all the above, you can also change `aptitude -y purge` by `dpkg --purge`.

To set packages on 'unhold' via aptitude:
```
# aptitude hold packagename
# aptitude unhold packagename
# aptitude search ~ahold
```

To set packages on 'unhold' via dpkg/apt-get:
```
# echo 'packagename hold' | dpkg --set-selections       -> op hold zetten
# echo 'packagename install' | dpkg --set-selections    -> op unhold zetten
# dpkg --get-selections | grep hold                     -> lijst hold packages
```