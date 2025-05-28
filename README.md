# EXPERIMENT-05-Data-Publishing-to-IoT-Broker-Using-MQTT3
 ### NAME:MATHAVAN V
 ### REGISTER NUMBER:212223110026
 ### DEPARTMENT: CSE IOT
 ### YEAR:II
 ## Aim:
To publish data to an IoT broker using the MQTT protocol.

 ## Apparatus Required:
MQTT Broker: An MQTT broker, such as HiveMQ or Mosquitto, for handling communication.
Python Environment: To run the script for publishing data to the broker.
Internet Connection: For connecting to the IoT broker.
Theory:
MQTT (Message Queuing Telemetry Transport) is a lightweight messaging protocol used in IoT applications. It allows devices to publish data to a broker, where other devices or applications can subscribe to receive updates. This experiment demonstrates how to use MQTT to send messages to an IoT broker using the paho-mqtt library in Python.

 ## Procedure:
Setup MQTT Broker:

You can use a public broker like broker.hivemq.com or set up your own broker using software like Mosquitto.
Choose a topic for the message, e.g., test/topic.
Install MQTT Client Library:

Install the paho-mqtt Python library to facilitate communication with the MQTT broker.
bash
Copy code
!pip install paho-mqtt
Write the Python Script to Publish Data:

Create a Python script to connect to the broker and publish a message to a specific topic.
Code Implementation: Here’s the Python code to publish data to the IoT broker using MQTT:

python
Copy code
import paho.mqtt.client as mqtt

### Broker details
broker_address = "broker.hivemq.com"  # Broker address
broker_port = 1883  # Broker port
topic = "test/topic"  # Topic to publish to

### Initialize the MQTT Client
client = mqtt.Client()

### Connect to the broker
client.connect(broker_address, broker_port, keepalive=60)

### Publish a message to the topic
message = "Hello, MQTT!"  # Message to be published
client.publish(topic, message)

### Disconnect from the broker
client.disconnect()

### Print confirmation message
print(f"Message '{message}' published to topic '{topic}'")
Run the Script:

Execute the script. It will connect to the MQTT broker, publish the message to the specified topic, and then disconnect.
Verify Message Publishing:

You can verify the message by subscribing to the same topic using an MQTT client, such as MQTT.fx or any other MQTT subscriber tool.
 ## Outputs:
Message Confirmation: The script will print a message confirming that the data has been successfully published to the topic.


## Python Code 
```
import paho.mqtt.client as mqtt
import time

# HiveMQ Cloud credentials
BROKER = "8a241b8176014661bed225153087deef.s1.eu.hivemq.cloud"  # Updated HiveMQ Cloud instance URL
PORT = 8884  # Secure WebSocket port
TOPIC = "sensor/temperature"
USERNAME = "beatricethomas13"  # Replace with your HiveMQ Cloud username
PASSWORD = "Deepbee_13"  # Replace with your HiveMQ Cloud password

# Fixed temperature value
TEMPERATURE_VALUE = 25.5

# Callback when the client connects to the broker
def on_connect(client, userdata, flags, rc, properties=None):
    if rc == 0:
        print("Connected to HiveMQ Cloud successfully")
    else:
        print(f"Connection failed with code {rc}")

# Create MQTT client and set WebSocket transport
client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION2, transport="websockets")
client.username_pw_set(USERNAME, PASSWORD)
client.tls_set()  # Enable TLS for secure WebSockets
client.on_connect = on_connect

# Connect to HiveMQ Cloud using WebSocket
client.connect(BROKER, PORT, 60)
client.loop_start()

# Publish temperature value repeatedly every 5 seconds
try:
    while True:
        client.publish(TOPIC, TEMPERATURE_VALUE)
        print(f"Published temperature: {TEMPERATURE_VALUE} to topic: {TOPIC}")
        time.sleep(5)  # Adjust interval as needed
except KeyboardInterrupt:
    print("Stopping MQTT client...")
    client.loop_stop()
    client.disconnect()
  
```

 ## Simulation Screenshots:
 
![image](https://github.com/user-attachments/assets/41c6f814-8fc5-4e6c-ac9e-3f088b21e8ce)

![image](https://github.com/user-attachments/assets/7406426d-0957-4d55-838a-7542422acca1)


 ## Results:
The data was successfully published to the MQTT broker. The experiment demonstrated how to use the MQTT protocol to transfer data to an IoT broker, enabling remote communication between devices or applications. The message was confirmed to be received by the topic, and this communication can be extended to more complex IoT systems.
