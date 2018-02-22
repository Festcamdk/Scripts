Adding a Shutdown Button to the Raspberry Pi

type:
sudo nano /etc/rc.local  

Find the line:
fi

enter:
sudo python /home/pi/Scripts/shutdown_pi.py &

before:
exit 0
