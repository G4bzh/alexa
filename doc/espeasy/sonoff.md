# Connect

SSID: ESP_EASY_0
Pass: configesp


Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::c86c:2772:f053:c004%6
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.4.100
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : 192.168.4.1


Go to http://192.168.4.1

Select your own SSID and set the password.
The IP should appear. If not, look for a device named 'ESP-Easy' in your router DHCP leases
Go to http://<IP>


# Config

## Config tab

Set the hostname, wifi config and  IP config (static vs DHCP) if needed

## Controllers

Set here your Controllers like Jeedom or Domoticz. Here, we won't use any controller.

## Hardware

Let you define GPIO affectation and behaviour (in/out)

## Devices

(https://www.letscontrolit.com/wiki/index.php/Sonoff_basic)
Sonoff has 2 devices: a relay and a button. Let's create them

### Relay

A relay is a switch in esp-easy terminology.
Click on "Edit" in the first row then choose "Switch input - Switch" as a device
Set a name like "Relay" and tick "Enabled"
tick "Internal PullUp"
Set GPIO-12 in GPIO field

Let the rest by default
Submit then close

### Button

A button is also a switch in esp-easy terminology.
Click on "Edit" in the second row then choose "Switch input - Switch" as a device
Set a name like "Button" and tick "Enabled"
tick "Internal PullUp"
Set GPIO-0 in GPIO field
Change switch button type to "Push Button Active High"

Let the rest by default
Submit then close

The devices page should display the button state. Push it then refresh the page. The state should change.

## Tools

### Advanced

Check "Rules"
Message Interval: 200ms
Check Use NTP
Set a NTP server (0.fr.pool.ntp.org)
Set a Timezone accordingly (60mn for France)

Submit

A new menu named "Rules" should now be available.


## Rules

On "rules set 1",paste the following:

on Button#state do
  if [Button#state]=1
   gpio,12,1
  else
   gpio,12,0
  endif
 endon

 on Relay#state do
 if [Relay#state]=1
  gpio,13,1
 else
  gpio,13,0
 endif
endon


The fisrt snippet change relay state accoding to button state
The second change LED state (GPIO 13) according to relay state (1 == relay closed )

Go to Tools->Save to save the config (we will import into the other sonoff)


# Test it

http://<espeasyip>/control?cmd=<command>

command
 - Status,GPIO,<pin number>
 - GPIO,<gpio>,<value>
