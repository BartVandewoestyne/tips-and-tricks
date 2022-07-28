# GNU core utilities
These commands can be found on Unix operating systems and most Unix-like operating systems.

Getting the full path to a file:
```
readlink -f file.txt
```

List all .JPG and .jpg files:<br>
Method 1:
```
ls | grep -i \.jpg$
```
Method 2:
```
ls *.[jJ][pP][gG]
```

List only directories:
```
ls -d */
```

Finding the biggest directories in the current directory
```
du -s * | sort -n
du -s * .[a-zA-Z]* | sort -n
```

# Other GNU tools

???
```
sed -e '0,/\\begin\{document\}/d;s/\\begin\{[^}]*\}//g;s/\\[^{]*\{//g;s/\}//g'

sed -e 's/[ \t\n]/\n/g' | sed -e 's/[^0-9a-zA-Z]//g' | sort | uniq -c

file=$(cat inputfile); echo $file|sed -e 's/[\.!?] /\n/g' | wc -l
```

Get cpu frequency:
```
grep MHz /proc/cpuinfo | cut -d ":" -f 2
```

Grepping only in .tex files recursively:
```
grep -r '\$I\^.*\$' --include=*.tex .
```

Grep for a certain text in all non-binary files:
```
grep -rI "SomeText" .
```

Grep for multiple strings:
* Method 1
  ```
  grep 'pattern1\|pattern2' fileName_or_filePath
  ```
* Method 2
  ```
  grep -E 'pattern1|pattern2' fileName_or_filePath
  ```
* Method 3
  ```
  grep -e pattern1 -e pattern2 fileName_or_filePath
  ```

Grep but exclude .svn directories:
```
grep -rI --exclude-dir=".svn" "SomeText" .
```

Sending compressed data 'on the fly' over the network:
```
tar cjf - test.txt | ssh bartv@vonneumann.cs.kuleuven.be "cd /home/bartv/temp/ ;
tar xjf -"
```

Renaming a whole bunch of files using a regular expression:
```
rename 's/old/new/' *.tex
```

# Redirecting stdout and stderr

Example command that generates both stdout and stderr output:
```
ls . *.blah
```
Redirecting stdout and stderr to same file using tee:
```
ls . *.blah 2>&1 | tee output.txt
```
Redirecting stdout and stderr to separate files using tee:
```
ls . *.blah 1> >(tee stdout.txt) 2> >(tee stderr.txt >&2)
```

# Unknown
```
# mkdir -p /mnt/hda2
# mount -o dev /dev/hda2 /mnt/hda2
# chroot /mnt/hda2 /sbin/lilo
# exit
# sync; umount /dev/hda2
# reboot
```

# Image manipulation

Get EXIF data from a picture:
```
exif mypicture.jpg
exiftran -d kolonisten_van_catan_bus.jpg
```
Set EXIF data in a picture:
```
exif --output=myoutput.jpg -t 0x013b --ifd=0 --set-value='Foo Bar' --no-fixup myinput.jpg
```
To get the size or other info from an image:
```
identify -verbose sample.png
pnginfo sample.png
tiffinfo sample.tif
```
```
for d in `seq 1 15`;
do
  convert -append niederreiter_f_warnock01_1000000p_${d}d_none.jpg niederreiter_f_warnock01_1000000p_${d}d_Laurie.jpg - | display -
done

for d in `seq 1 15`;
do
  montage -geometry 640x480 niederreiter_f_warnock01_1000000p_${d}d_none.jpg niederreiter_f_warnock01_1000000p_${d}d_Laurie.jpg jpg:- | display -
done
```
Convert an EPS to a PNG:
* Method 1:
  ```
  mogrify -format png *.eps
  ```
* Method 2:
  ```
  convert foo.ps foo.png
  ```
Convert PDF to EPS
```
pdftops -eps file.pdf
```
Create a PDF file from an Asymptote script:
```
asy myfile.asy -f pdf
```

Convert pictures to a smaller format:
```
# For paraglide.be      -> 1600x1600 met -quality 80
# For parapentebelge.be -> 800x800
# Zie ook http://www.imagemagick.org/script/command-line-options.php
# Check also
#   -resize: http://www.imagemagick.org/script/command-line-options.php#resize
#   -scale: http://www.imagemagick.org/script/command-line-options.php#scale
#   -geometry: http://www.imagemagick.org/script/command-line-options.php#geometry
#   -size: http://www.imagemagick.org/script/command-line-options.php#size
# Image Geometry specification:
#   http://www.imagemagick.org/script/command-line-processing.php#geometry
#
for file in `ls *.JPG`
do
  echo -n "Converting $file to resized/$file... "
  convert -resize 1600x1600 -quality 80 $file resized/$file
  echo "done."
done
```

Find corrupted JPG files in a directory
```
find -iname "*.jpg" -print0 | xargs -0 jpeginfo -c | grep -e WARNING -e ERROR
```
See also http://watson-net.com/blog/checking-the-integrity-of-all-jpg-files-in-a-directory/

To find out what Linux distribution you have<br>
Method 1:
```
lsb_release -a
```
Method 2:
```
cat /etc/issue.net
```

# Audio

To get mp3-info and change it:
* For ID3 versions 1.0 and 1.1 only, not ID3V2:
  ```
  mp3info file.mp3
  ```
* For ID3 versions 1.0, 1.1, 2.3 and 2.4:
  ```
  eyeD3 file.mp3
  ```
For automated batch tagging, use the program easytag, btag or kid3 (on KDE) or kid3-qt (on Gnome).

Remark: Android Music Player should work with ID3v2.3.0, but not sure about ID3v2.4.0.

Convert .wav to .mp3
--------------------
# lame –h –b 192 Test.wav Test.mp3

$ for FILE in *.wav; do lame -h -b 192 "$FILE"; done

# for FILE in "`ls *.wav`"; do `which lame` –h –b 192 "$FILE" "${FILE//\.wav}.mp3"; done

#!/bin/sh
# name of this script: wav2mp3.sh
# wav to mp3
for i in *.wav; do
 if [ -e "$i" ]; then
   file=`basename "$i" .wav`
   lame -h -b 192 "$i" "$file.mp3"
 fi
done

# Video

## Downloading

Download a YouTube playlist:
```
youtube-dl -t http://www.youtube.com/view_play_list?p=PL03C3ABF4835B2C51
```
Downloading a stream:
```
ffmpeg -i videourl.m3u8 -c:v copy -c:a copy video.ts
```

## Getting info
To request codec info, similar as gspot for Windows:
```
mediainfo file.avi
avprobe file.avi
tcprobe -i file.avi
```
See also http://www.fourcc.org/codecs.php for a list of codecs and their four character code.

To get mpeg info:
```
mpgtx -i file.mpg
```
Checking if an mpg file is corrupt or not
-----------------------------------------
ffmpeg -v 5 -i file.avi -f null - 2>error.log

# Joining videos
* AVI files:
  ```
  mencoder -ovc copy -oac copy -o completevideos.avi video1.avi video2.avi
  ```
  Also checkout avimerge.
* MPEG:
  * Method 1:
    ```
    mpgjoin file1.mpg file2.mpg file3.mpg -o newfile.mpg
    ```
  * Method 2:
    ```
    mpgjoin *.mpg -o test.mpg
    ```
  * Method 3:
    ```
    cat file1.mpg file2.mpg file3.mpg > totalfile.mpg
    ```
  * Method 4:
    ```
    mencoder -of mpeg -ovc copy -oac copy *.mpg -o totalfile.mpg
    ```

# GPX related commands
gpx file in Google Earth bekijken met hoogte info
-------------------------------------------------
By default zet Google Earth de altitudemode op "clamped to ground".  Je kan
dat op "absolute" zetten via de opties van je tracks, of door je gpx file
naar een kml te converteren en daarbij de altitudemode op "absolute" te
zetten:

gpsbabel -i gpx -f myfile.gpx -o kml,floating=1 -F myfile.kml

http://www.gpsbabel.org/htmldoc-development/fmt_kml.html#fmt_kml_o_floating


# PDF and PostScript commands
PDF commands:
-------------
Paste together PDF's:

  method 1:
    pdfunite file1.pdf file2.pdf filen.pdf out.pdf

  method 1:
    pdftk file1.pdf file2.pdf cat output totaal.pdf

Extract pages from PDF:
* Method 1:
  ```
  gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dSAFER \
     -dFirstPage=22 -dLastPage=36 \
     -sOutputFile=outfile_p22-p36.pdf 100p-inputfile.pdf
```
* Method 2:
  ```
  pdftk inputfile.pdf cat 1-10 output outputfile.pdf
  ```
* Method 2 (pdftk with handles):
  ```
  pdftk A=100p-inputfile.pdf cat A22-36 output outfile_p22-p36.pdf
  ```
Rotating a PDF document:
```
  pdftk input.pdf cat 1-endwest output output.pdf
```

Convert a PDF file to booklet:<br>
* My method:
    ```
    pdftops file.pdf
    psbook file.ps | psnup -2 -pa4 | a2ps -1 -s tumble -o booklet.ps
    ```
  and then print on a duplex printer.

* Alternative 1:
    ```
    pdf2ps -spapersize=a4 file.pdf file.ps
    psbook file.ps | psnup -2 | a2ps -1 -s tumble -o booklet.ps
    ```
  and then print on both side with the option "long edge (standard)".

* Alternative 2: if the original document is not in the a4 format (for instance 14,88 cm x 20,98 cm),
we have to do:
    ```
    pdf2ps file.pdf file.ps
    psbook file.ps | psnup -2 -w18.88cm -h20.98cm -pa4 | a2ps -1 -s tumble -o booklet.ps
    ```

Selecting selected pages from a PostScript document:
```
psselect -p18,31,32 file_in.ps file_out.ps
```

Combining PostScript files into one document:
* Method 1:
  ```
  ghostscript -dNOPAUSE -sDEVICE=pswrite -dBATCH -sOutputFile=out.ps file1.ps file2.ps
  ```
* Method 2:
  ```
  psjoin
  ```
* Method 3
  ```
  psmerge -oout.ps file.ps
  ```
The above command only works if the files were created using the same application, with the
same device setup and resources (fonts, procsets, patterns, files, etc) loaded.

# Print commands

Print only odd sides pages in a certain range:
```
$ lp -o page-set=odd -o sides=two-sided-long-edge -o media=a4 -o fitplot -P 3-5 file.pdf
```
First uneven:
```
$ lp -o page-set=odd -o sides=two-sided-long-edge -o media=a4 -o fitplot -P 1-5
PaulVanHoutte.pdf
```
Then even (in reverse order):
```
$ lp -o page-set=even -o outputorder=reverse -o sides=two-sided-long-edge -o
media=a4 -o fitplot -P 2-6 PaulVanHoutte.pdf
```
`\linebreak` can help in LaTeX to break lines

# Text processing

Replacing a piece of text in a lot of files in the current directory:
* Method 1:
  ```
  for file in `ls *.tex`
  do
    sed -e "s/chapter/part/g" <$file >$file.new
    mv $file.new $file
  done
  ```
* Method 2:
  ```
  perl -pi.bak -e 's/foo/bar/g' *.whatever
  ```
* Method 3:
  ```
  sed -i.bak -e 's/foo/bar/g' *.whatever
  ```

Append a line after a certain matching line:
```
sed '/myregex/ a\myline' myfile.txt
```

Printing sourcecode in color:
* With `enscript`:
  ```
  enscript -Ec -G -U2 --color -Pkleur <file>

    -E            -> filter (autodetectie meestal, hier c-code)
    -G            -> fancy header 
    -U2           -> 2 paginas op bladzijde
    --color       -> kleur
  ```
* With `a2ps`:
  ```
  a2ps --prologue=color -2 <file>

    -> includes color.pro as PostScript prologue
    -> predefined font size and layout for 2 virtual
  ```

# gnuplot

Finding out what options gnuplot is built with:
```
gnuplot> show version long
```

Plotting points from sequences:
```
$ gnuplot
plot "filename.seq" using ($15):($16)

$ echo 'plot "filename.seq" using ($1):($2); pause 10' | gnuplot
```

Dictionary:
-----------
dict myword

# X Window System

Starting another X:
```
export WINDOWMANAGER=kde
startx -- :2
```
???:
```
als user: xhost +LOCAL:
als root: export DISPLAY=:0
          gq
```

# Maple input files
-----------------
1) start maple in console modus
2) read("myfile.mpl")


Add a graphicspath in LaTeX:

  \graphicspath{{<path_to_pictures>}}

Convert a latex file to Word or ODT:

  mk4ht oolatex file.tex
  http://johnmacfarlane.net/pandoc/
    pandoc -s math.tex -o math.docx
  http://dlmf.nist.gov/LaTeXML/

-------------------------------------------------------------------------------
ispell gebruikt by default american checking.  Als je british wil, dan gebruik
je
ispell -d british file.txt

\frac{-w_{N_s}f_k(s_{N_s})}{s_{N_s}-a_1} & \hdots & \frac{-w_{N_s}f_k(s_{N_s})}{s_{N_s}-a_N}
XFig figures met LaTeX fonts:
-----------------------------
* Create or open your .fig file in xfig.
* Add text with the Text Input tool (the same way you always add text). You
  can use mathematical formulas as in LaTeX, including the dollar sings (e.g.,
  $f(x)=x^3$).
* Using the Edit tool, edit the properties of the text field you have just
  added. Set the following properties:

    * Special Flag: special
    * Font: use LaTex fonts (bottom of dialog), Default

* fig2eps --bbox=dvips test.fig

Cancellen print jobs
--------------------
Precies is het cancellen van jobs op p1c alleen mogelijk op scorpius
(=cups-server2.cs.kueluven.be) met lprm

Rasterizing an EPS figure
------------------------
gs -r300 -dEPSCrop -dTextAlphaBits=4 -sDEVICE=png16m -sOutputFile=fig.png -dBATCH -dNOPAUSE fig.eps
(wel uitvoeren op archimedes met gs versie 8.61, versie 7.07.1 cropte niet...)
(-r300 is de resolutie)

Pasting together rar files
--------------------------
If you have a bunch of files like

  file.r00
  ...
  file.r25
  file.rar

then you can stitch them together with

  unrar e file.rar

Check if your processor supports 64-bit
---------------------------------------
-> Look at /proc/cpuinfo and see if the 'lm' flag is present.
   If it is, then your CPU supports 64 bits and you can run a
   64 bit kernel if you'd like to. If doesn't have lm, but it supports cmov
   (Conditional move instruction), then it's only a 32 bit cpu, but you can run
   a i686 kernel. If you don't even see cmov, then it's a fairly old / basic cpu
   (eg an older low power via), and you'll need to run an i386 / i486 kernel

Is the running kernel 32 bit or 64 bit?
---------------------------------------

If we do find the lm flag, then how do we tell if the running kernel is 32 bit
or 64 bit? Possibly uname -a will give us a hint, but alas not always (look for
x86_64 in the output for 64 bit, or i686 for 32 bit). If that isn't conclusive,
then run getconf LONG_BIT - that should return either 64 or 32, that being your
answer.

Other method:

  file /sbin/init

GUI-method:

  Hit Windows key and search for 'Details', then see under 'OS type'

Mail versturen vanaf de command line
------------------------------------
mail -a "From: Bart.Vandewoestyne@telenet.be" -a "Reply-To: test@test.com" -s
"Een subject" foo@bar.com < body.txt

Compare two directories
-----------------------
See http://linuxcommando.blogspot.com/2008/05/compare-directories-using-diff-in-linux.html

Best method I have found so far:

  diff -qr dir1 dir2 | tee dir_cmps.txt
  
  -> This also shows if symlinks in dir1 and dir2 are different.

Other possibilities:

  rsync -avnc --delete dir1/ dir2/

    -a        archive mode; equals -rlptgoD (no -H,-A,-X)
              -r        recurse into directories
              -l        copy symlinks as symlinks
              -p        preserve permissions
              -t        preserve modification times
              -g        preserve group
              -o        preserve owner (super-user only)
              -D        same as --devices --specials
                         --devices  recreate character and block devices
                         --specials transfer special files such as named
                                    sockets and fifos
    -v        increase verbosity
    -n        perform a trial run with no changes made
    -c        skip based on checksum, not mod-time & size
              (this option seems better than mod-time & size to me...)
    --delete  delete extraneous files from dest dirs

Backups with rsync
------------------
First test with a dry-run to see what files are going to be deleted in dest:

  rsync -avzn --delete src_dir/ dest_dir

Then do the real work:

  rsync -avz --delete src_dir/ dest_dir


Foto-album maken
----------------
photon --sizelist=640x480 --resize-plugin=gimp -o myoutputdir mypicturesdir/

Having two versions of gcc side by side
---------------------------------------
sudo apt-get install gcc-4.3 g++-4.3

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.3 40 --slave /usr/bin/g++ g++ /usr/bin/g++-4.3
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.4 60 --slave /usr/bin/g++ g++ /usr/bin/g++-4.4

Now, if you want to change between gcc versions, simply run
sudo update-alternatives --config gcc

tcpdump commands
----------------
capture all sip traffic
  tcpdump -pi eth1 -n -s 0 port 5060 and host 192.168.1.138 -w mydump.pcap

sniff network
  tcpdump -pi eth1 -n -s 0 net 10.1.176.0/24 and not host 10.1.176.41 -w mydump.pcap

Terminal weer goed krijgen als hij fucked up is
-----------------------------------------------
tset
tput init
tput reset

Pretty print JSON
-----------------
cat file.json | python -mjson.tool
