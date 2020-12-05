# mac_changer
print("mac changer by md bvb ")

import subprocess
import re
import optparse


def change_mac(interface, new_mac):
    subprocess.run(["ifconfig", interface, "down"])
    subprocess.run(["ifconfig", interface, "hw", "ether", new_mac])
    subprocess.run(["ifconfig", interface, "up"])
    print("(+) change the mac address of " + interface + " to " + new_mac)



def argement():
    parser = optparse.OptionParser()
    parser.add_option("-i", "--interface", dest="interface", help="please enter interface")
    parser.add_option("-m", "--new_mac", dest="new_mac", help="please enter new_mac")
    option = parser.parse_args()
    return option


(options, arg) = argement()
change_mac(options.interface, options.new_mac)
ifconfig = subprocess.check_output(["ifconfig"])
ifconfig_serch = re.search(r"\w\w:\w\w:\w\w:\w\w:\w\w:\w\w", str(ifconfig))
if ifconfig_serch:
    print("the mac_address has been change to  " +  ifconfig_serch.group(0))
if not ifconfig_serch:
    print("(-)could not find mac address")

