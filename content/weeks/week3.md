---
title: "Week 3: Embedded Programming"
weight: 3
icon: "images/week1_icon.png"  # Optional: icon for this week
---

I chose to use this week to document my circuit and how I talk to my arduino :-) 

{{< image-figure src="images/w3_circuit.jpg" caption=" " size="80%" align="center" >}}

I used the simulation to learn how to add a button to my circuit. Here when the button press is detected by the arduino turns on the LED pin.  In my case, the button should open the solenoid for a fixed amount of time determined by the code onboard the arduino uno. I already have a pin sending to signal pin of relay that opens solenoid, so instead of changing LED_PIN i will change the SOLENOID_PIN when the button is pressed. 

{{< image-figure src="images/button_simulation.jpg" caption=" " size="50%" align="center" >}}

Video of button in action [here](https://youtube.com/shorts/toRzQ_8QJzU?feature=share). Note to self: make sure to add protection against long-button hold for solenoid control (ie no waterfalls). 
<!--{{< image-figure src="images/button.gif" caption=" " size="50%" align="center" >}}-->

Video of script in action [here](https://youtu.be/Zl2qq0PguPw)

Video of serial arduino communication in action [here](https://youtube.com/shorts/5qVZAUI8Hv8?feature=share) 

I will upload the example run with serial communication (from vscode) and the arduino probably with a youtube video when I get a chance. 

#### arduino script: button example
```cpp
#define LED_PIN 13
#define BUTTON_PIN 12
void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT);
}
void loop() {
  if (digitalRead(BUTTON_PIN) == HIGH) {
    digitalWrite(LED_PIN, HIGH);
    delay(300);
  }
  else {
    digitalWrite(LED_PIN, LOW);
  }
}
```

I use serial communication to send commands and read data from the arduino. 

Here's a snippet of the code: 
You can find the full notebook on [my GitHub](https://github.com/surlab/Behavior_Code_Emma/blob/main/python/rig_control.ipynb).

#### script for serial communication between arduino and personal computer
```python 
port = 'COM3'  # Replace with your Arduino's port
baudrate = 115200  # make sure this matches the baud rate in the Arduino sketch (.ino file)
#request user for identiying information
animal_ID = input("Enter Animal ID: ")
training_stage = input("Enter training stage: ")
min_ = float(input("Session length (min): "))
run_time = min_*60 #sec
#opn window to choose directory 
root = Tk()
root.withdraw()  # Hide the main tkinter window
save_directory = askdirectory(title="Select Directory to Save Data File")
data_filename = f"{animal_ID}_{training_stage}_{datetime.now().strftime('%Y%m%d_%H%M%S')}.txt"
data_filepath = os.path.join(save_directory, data_filename)
#initialize file to write to as 'file'
with open(data_filepath, 'w') as file:
    #initialize serial connection
    ser = serial.Serial(port, baudrate, timeout=1)
    time.sleep(2) 
    #send start command to Arduino
    start_time = time.time() #use for duration based arduino script start/stop
    ser.write(b'S') 
    behav_active = True
    timestamp = datetime.now().strftime('%Y-%m-%d %H:%M:%S.%f')[:-3]
    print(f'{timestamp} - Sent start command to Arduino.')
    file.write(f'{timestamp} - Sent start command to Arduino.\n')
    
    try:
        count = 0
        # Read data from Arduino
        while behav_active:
            if ser.in_waiting > 0:
                try:
                    line = ser.readline().decode('utf-8', errors='ignore').rstrip()
                    timestamp = datetime.now().strftime('%H:%M:%S.%f')[:-3]
                    log_line = f'{timestamp} - Arduino: {line}\n'
                    # Reduce print statements to every 10th message
                    count += 1
                    if count % 10 == 0:
                        print(log_line, end='')
                    file.write(log_line) 
                except UnicodeDecodeError:
                    print("Failed to decode serial data")
                    continue
    
            # Check if run_time seconds have passed to send the stop command
            if time.time() - start_time >= run_time:
                ser.write(b'X') 
                print('Sent stop command to Arduino.')
                timestamp = datetime.now().strftime('%Y-%m-%d %H:%M:%S.%f')[:-3]
                file.write(f'{timestamp} - Sent stop command to Arduino.')
                behav_active = False
    
    except KeyboardInterrupt:
        #see link for full 
    finally:
        ser.close()
#details ommitted, see link for full!!!
```

