This is a steps to customize Raspberry Pi’s boot up screen, specifically to change the splash image and remove unwanted images and texts. By default, Raspbian Jessie Desktop displays below during boot up before starting desktop GUI.

(1) Rainbow image
(2) Raspberry Pi Logo (image of four raspberries in the top left corner)
(3) Boot message log
(4) Blinking cursor for boot message logs (at the top left corner)
(5) Splash Image (“Welcome to pixel”)
(6) One-line text under splash image

By following the steps below, we’ll remove (1)-(4) and (6), then replace the default splash image with whatever you want to display at (5).

 

Assumption:
You should have your own splash image somewhere. In the steps below, assuming that the file name of the splash image is “my_splash.png” and it’s located home directory. (i.e. “~/my_splash.png”)

 

Here are the steps:

Remove Rainbow Screen
sudo nano /boot/config.txt

Then add below line at the end of the file.
disable_splash=1
 

Remove text message under splash image:
sudo nano /usr/share/plymouth/themes/pix/pix.script

Then, remove (or comment out) four lines below:
message_sprite = Sprite();
message_sprite.SetPosition(screen_width * 0.1, screen_height * 0.9, 10000);
       my_image = Image.Text(text, 1, 1, 1);
       message_sprite.SetImage(my_image);
Note : This is a quick and dirty method I found. It works, but there might be better way.
 

Remove Boot Messages
sudo nano /boot/cmdline.txt

Then, replace “console=tty1” with “console=tty3”. This redirects boot messages to tty3.

 
Remove other things
Still in “/boot/cmdline.txt”, add below at the end of the line

splash quiet plymouth.ignore-serial-consoles logo.nologo vt.global_cursor_default=0
Here are brief explanations.
‘splash’ : enables splash image
‘quiet’ : disable boot message texts
‘plymouth.ignore-serial-consoles’ : not sure about this but seems it’s required when use Plymouth.
‘logo.nologo’ : removes Raspberry Pi logo in top left corner.
‘vt.global_cursor_default=0’ : removes blinking cursor.

Note : The first three should be there by default, but make sure if those exist.

Replace Splash Image
Now, everything unwanted images and texts are gone. Let’s replace the default splash image (/usr/share/plymouth/themes/pix/splash.png) with your own splash image.

sudo cp ~/my_splash.png /usr/share/plymouth/themes/pix/splash.png
Note : As described in above assumption, “my_splash.png” should be your new splash image.
 

Verify the costumed boot up screen
Check the boot up screen by simply rebooting.

sudo reboot
