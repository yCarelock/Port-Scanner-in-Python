# Port-Scanner-in-Python
Overview
In this project, you’ll build a simple port scanner that checks a range of TCP ports on a target system to identify which ones are open. This project uses Python’s built-in socket module to attempt connections and will introduce you to basic network communication.

Software 
Pyhton 
Visual Code Studio 

Create the Python Script
File Creation: Create a new file named port_scanner.py.

3. Write the Code
Copy and paste the following code into your file:
import socket
import sys

def scan_ports(target, start_port, end_port):
    """
    Scans a range of TCP ports on the specified target to check if they are open.
    
    Parameters:
        target (str): Target hostname or IP address.
        start_port (int): Starting port number.
        end_port (int): Ending port number.
    """
    # Resolve the target's hostname to an IP address
    try:
        target_ip = socket.gethostbyname(target)
    except socket.gaierror:
        print("Error: Unable to resolve hostname.")
        sys.exit()

    print(f"Scanning {target} ({target_ip}) from port {start_port} to {end_port}:\n")
    
    for port in range(start_port, end_port + 1):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)  # Set a timeout of 1 second for each connection attempt
        result = s.connect_ex((target_ip, port))
        if result == 0:
            print(f"Port {port}: Open")
        s.close()

if __name__ == '__main__':
    # Get target and port range from the user
    target = input("Enter the target hostname or IP address: ")
    try:
        start_port = int(input("Enter the starting port number: "))
        end_port = int(input("Enter the ending port number: "))
    except ValueError:
        print("Error: Please enter valid numbers for the ports.")
        sys.exit()
    
    scan_ports(target, start_port, end_port)
Code Explanation:

Imports:

socket: Provides low-level network interactions to create connections.

sys: Allows the script to exit if a problem arises.

scan_ports Function:

Target Resolution: Converts the target hostname into an IP address.

Port Scanning Loop: Iterates through the given port range; for each port:

Creates a new socket.

Uses socket.connect_ex() to attempt a connection (which returns 0 if successful).

Prints the port as open if the connection is established.

Closes the socket after each attempt.

Main Block:

Prompts the user for a target and the range of ports to scan.

Calls the scan_ports() function with the provided parameters.

4. Run Your Script
Navigate to the Script’s Directory:

In my case I will be opening visual code studio 
Follow On-Screen Prompts:

You’ll be asked to enter the target hostname/IP address and the port range (for example, ports 1 to 100).

The script will then display which ports within that range are open.
![2025-04-10 21_52_53-port_scanner py - Visual Studio Code](https://github.com/user-attachments/assets/5291b750-18be-4970-b3ca-af27ebae8150)
After running the script and waiting approx 5 mins I did get results. 
Keep in mind the wider the range there will be a wait time. 
