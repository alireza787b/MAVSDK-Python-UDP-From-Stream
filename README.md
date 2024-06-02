
# MAVSDK-Python-UDP-From-Stream

Real-time offboard control commands to MAVSDK from external sources over UDP, including a Pygame GUI example for joystick-like drone control.

![image](https://github.com/alireza787b/MAVSDK-Python-UDP-From-Stream/assets/30341941/dc058fda-b39e-43f2-9151-16c9faf08789)


## Overview
This project simplifies and extends the offboard control capabilities of MAVSDK-Python by introducing an easy mechanism for receiving and processing drone control commands via UDP. The new `receiver.py` script and `ControlPacket` class facilitate the integration of control commands from external sources (even an Arduino), and even different languages or technologies (such as image processing systems). These enhancements are particularly useful in scenarios where MAVSDK does not directly manage the command generation process, allowing for a highly flexible, system-agnostic approach to drone command and control.

### Key Components
- **Universal Command Reception (`receiver.py`)**: Acts as a bridge to receive control commands via UDP, enabling integration with systems that do not natively interface with MAVSDK or are written in different programming languages.
- **Control Packet Class (`control_packet.py`)**: Ensures structured and efficient handling of incoming control data, allowing for clear and straightforward integration with external command sources.
- **Example Scripts**: Includes examples demonstrating various control modes (attitude, body velocity, attitude rate, position NED circle), providing a practical reference for developers to implement similar functionalities.

## Getting Started

### Prerequisites
- Python 3.7 or higher
- MAVSDK
- Pygame (for GUI examples)

### Installation
1. **Clone the Repository**:
    ```bash
    git clone https://github.com/alireza787b/MAVSDK-Python-UDP-From-Stream.git
    cd MAVSDK-Python-UDP-From-Stream
    ```

2. **Create a Virtual Environment (recommended)**:
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # For Windows: .\env\Scripts\activate
    ```
    Alternatively, you can use your global Python environment.

3. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

### Configuration
Configure the UDP IP and port settings in `receiver.py`. If using a real drone with a serial connection, enable the serial port and set the appropriate port on the companion computer connected to the Pixhawk board.

```python
# Global Defaults
DEFAULT_CONNECTION_TYPE = 'udp' or 'serial'
DEFAULT_PORT_UDP = '14540'
DEFAULT_PORT_SERIAL = '/dev/ttyS0'  # Raspberry Pi default TTL

UDP_IP = "0.0.0.0"
COMMAND_UDP_PORT = 5005
BUFFER_SIZE = 1024
```

### Running the Example Scripts
1. **Run `receiver.py`**:
    ```bash
    python3 receiver.py
    ```

2. **Send Commands**:
    - You can run one of the Pygame GUI examples or write your own script to send commands. Ensure the UDP IP and port match those configured in `receiver.py`.

    For example, to run the body velocity sender example:
    ```bash
    python3 examples/body_velocity_sender_example.py
    ```


### Simulation Testing
To test the setup, you will need a SITL (Software In The Loop) interface on your computer. You can use JMAVSim, Gazebo, AirSim, or X-Plane. For Windows users, it is recommended to use WSL2. 

- [Tutorial on using PX4 SITL with WSL2](https://www.youtube.com/watch?v=iVU8ZNoMn_U)
- [Official PX4 Documentation](https://docs.px4.io/main/en/simulation/)

### Writing Your Own Commands
You can write your own command scripts in any language that supports UDP. Just follow the protocol defined in `control_packet.py` for sending and handling commands.

### Safety Disclaimer
Testing on a real drone is risky in offboard mode. Do it at your own risk and only if you are sure your drone is perfectly tuned, flyable, failsafe logic is activated and tested, and you are in a safe environment.

## Future Enhancements
- Adding more control examples
- Improving the Pygame GUI
- Supporting additional communication protocols

## Additional Resources
For more MAVSDK tutorials and basics, check out my YouTube tutorial on the basics of MAVSDK:
[MAVSDK Introduction + GCS GUI App example using Python Tkinter](https://www.youtube.com/watch?v=SM0WtREzqqE)

## Contribution
Contributions are welcome! Please open issues or submit pull requests with your improvements.

## License
This project is licensed under the Apache-2.0 license.
