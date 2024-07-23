Statement
You attend an interview for a forensic investigator job and they give you a challenge to solve as quickly as possible (having the Internet).
They ask you to find the date of printing as well as the serial number of the printer in this document.
You remain dubitative and accept the challenge.

The answer is in the form:
hh:mm dd/mm/yyyy SSSSSSSS
with
 hh: the hour of the event
 mm: the minutes of the event
 dd: the day of the event
 MM: the month of the event
 yyyy: the year of the event
 SSSSSSSS: the serial number

[explanation]

When I checked the problem file, there were no hints to help me solve it.
If you Google "yellow dot," you can see that it is a technique for hiding data by inserting yellow dots into color printer output. If you search for methods to find yellow dots, you will find that you can check for yellow dots by changing the background to blue or by using a copy scanner.
+ So, when I changed the background to blue using the convert command in Ubuntu, I couldn't see anything. They said I could check it with Photoshop, but even when I changed it with Gimp, I couldn't find the yellow dot.
I was able to confirm the yellow dot by searching and using online sites mainly used for forensics.

http://fotoforensics.com/analysis.php?id=4fc1d07d5248bf5fcaa5697fafd22280c1d560e1.2149907

https://stegonline.georgeom.net/image

https://incoherency.co.uk/image-steganography/#unhide

https://aperisolve.fr/58bfea09dc12465442702f0ee180f54c

The above sites are said to be mainly used as forensic tools.

 

At first, I checked by changing LSB to half, and there was a white square box in the upper right corner. From here, I could guess that there would be a yellow dot.


If you check by changing the colors used in the file,


You can't see it very well in this photo, but there are some blue dots in the upper right corner.


If you zoom in on that part, it looks like this.

Now the key is interpretation. For information on how to interpret, please refer to the post below.

https://en.wikipedia.org/wiki/Machine_Identification_Code

https://www.cybrary.it/blog/0p3n/printer-steganography/

Here's a quick picture summary of the detox method:

 


Date, time, and serial values ​​can be expressed with yellow dots within the horizontal and vertical black lines, and the horizontal lines are divided into time (2-5), date (6-8), separator (10), and serial (11-14) as shown in the picture. Each value is determined by the vertical line, and each cell of the vertical line is expressed in the form of 2^n.

Let's explain the number 2 in the picture as an example. The yellow dots are printed at 32, 16, and 2, and if you add up all of these values, it's 50. In other words, 50 minutes in time is expressed by two yellow dots. If you add up the values ​​where the yellow dots are located in this way, you can obtain the date, time, and serial values.

Back to the problem, let's change it like the example picture above!

 


It can be expressed like this


If we add up the individual values, we get 5 11 27 7 14 30 29 92 6.

If we divide these values ​​into the appropriate ranges and organize them into a final summary, we can see that it is 11:05, 2014-07-27, 06922930.

If you write this in the form presented in the problem and authenticate it, you can solve the problem.

 

Issue
💡https://web.archive.org/web/20180305181029/https://w2.eff.org/Privacy/printers/docucolor/ They say you can decode yellow dots, but I don't know if it's just me, but they don't decode them👿

After verifying the answer, I looked at the solution and it said I could get it by writing a code, but I don't understand the code☹️
+ flag
🍒 11:05 27/07/2014 06922930
