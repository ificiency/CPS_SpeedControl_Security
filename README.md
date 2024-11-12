README.md: To provides an overview of the project, usage instructions, and an explanation of the model.


# CPS Speed Control Project

This project demonstrates a basic Cyber-Physical System (CPS) model of an autonomous vehicle’s speed control system using Simulink. The model includes a PID controller that adjusts the vehicle’s speed to meet a desired setpoint, simulating real-world CPS control and stability.


## Project Structure
- `CPS_SpeedControlModel.slx`: Simulink model file containing the CPS speed control model.
- `README.md`: Project description and usage information.
- `LICENSE`: License information for the project.
- `.gitignore`: Specifies files and folders to be ignored by Git.



## Model Description
The model consists of:
- A **Constant** block to set the target speed.
- A **Sum** block to calculate the error between the target speed and actual speed.
- A **PID Controller** to adjust the throttle based on the error.
- A **Transfer Function** block to simulate vehicle response.
- A **Scope** block to visualize the vehicle's speed over time.
- A ** Manual Switch** to toogle between real feedback and spoofed feedback
- A ** Constant Block (Spoofed Speed) ** 





## Complete Procedure


   # Step 1: Set Up the Speed Control System

  
	1.	Open Simulink: Launch Matlab, then open Simulink from the toolbar.

	2.	Create a New Model: In Simulink, create a new blank model. This will be the basic control system of an autonomous vehicle.
		


Diagram Setup:

			1.	Constant Block (Desired Speed):
				o	Label: Desired Speed
				o	Value: Set to 50 (this represents the target speed, in km/h or other units).
				o	Connection: Connect the output of this block to the positive input (+) of the Sum block.

    
			2.	Sum Block (Error Calculation):
				o	Configuration: Set this block to have one positive (+) input and one negative (−) input.
				o	Function: This block will calculate the error between the desired speed and the actual/feedback speed.
				o	Inputs:
						Positive Input (+): Connect to the output of the Desired Speed Constant block (target speed).
						Negative Input (−): Connect to the output of the Manual Switch (feedback loop).
				o	Output: Connect the output of the Sum block to the input of the PID Controller.
    
    
			3.	PID Controller:
				o	Function: Adjusts the throttle based on the error signal from the Sum block.
				o	Input: Connect to the output of the Sum block.
				o	Output: Connect to the Transfer Function block.

    
			4.	Transfer Function (Vehicle Dynamics):
				o	Label: Transfer Function
				o	Configuration: Use a simple first-order transfer function (e.g., 1/(s+1)) to simulate the vehicle’s speed response.
				o	Input: Connect to the output of the PID Controller.
				o	Output: Connect to one input of the Manual Switch and also to the Scope block to visualize the speed.

    
			5.	Constant Block (Spoofed Speed):
				o	Label: Spoofed Speed
				o	Value: Set to 30 (or a value lower than the desired speed to simulate an attack).
				o	Output: Connect to one input of the Manual Switch.

    
			6.	Manual Switch (Select Feedback):
				o	Function: Allows you to toggle between real feedback (from the Transfer Function) and spoofed feedback (from the Spoofed Speed Constant block).
				o	Inputs:
						Input 1: Connect to the output of the Transfer Function (real speed feedback).
						Input 2: Connect to the output of the Spoofed Speed Constant block.
				o	Output: Connect the output of the Manual Switch to the negative input (−) of the Sum block (this acts as the feedback input in the control loop).

    
			7.	Scope (Visualization):
				o	Function: Displays the actual speed of the vehicle over time.
				o	Input: Connect the output of the Transfer Function to the Scope block to observe the system’s response.



    
Summary of Connections:
	•	Desired Speed Constant → Positive Input (+) of Sum Block
	•	Output of Sum Block (Error) → PID Controller
	•	PID Controller Output → Transfer Function
	•	Transfer Function Output (Real Speed):
			o	Connect to Input 1 of Manual Switch
			o	Connect to Scope (to visualize speed)
	•	Spoofed Speed Constant → Input 2 of Manual Switch
	•	Manual Switch Output (Feedback) → Negative Input (−) of Sum Block

 
This layout provides a structured flow where:
•	The Sum block calculates the error by subtracting the feedback speed (real or spoofed) from the desired speed.
•	The PID controller adjusts the control based on the error.
•	The Transfer Function simulates the vehicle dynamics.
•	The Manual Switch allows toggling between real and spoofed feedback to observe the impact on system behavior in the Scope.





Set Parameters:
	In the Constant block, set the desired speed (e.g., 50 km/h).
	Configure the PID Controller parameters as needed (e.g., P=1, I=0.5, D=0.1).
	Set the Transfer Function’s parameters to simulate the vehicle dynamics.



 #Step 3: Run and Observe the Results

	1.	Run the Simulation: Start the simulation and observe the output on the Scope.

	2.	Toggle the Switch: While the simulation is running, toggle the Manual Switch to simulate the attack. You’ll see the system respond to the false input, 	trying to reach the incorrect target speed.

	3.	Analyze: Observe how the vehicle’s speed control system attempts to adjust based on the spoofed speed value, demonstrating how an attack on sensor data can destabilize CPS.



# Expected Results

    
First Switch Configuration and Scope Output:

	When the Manual Switch is toogled in the first scenario to the desired speed, the vehicle control system will receive real feedback from the Transfer Function (actual speed of the vehicle).
	Scope Output: The curve is gradually increasing and approaching a stable speed, indicating that the PID controller is working to reach the desired speed (50 km/h). This response suggests normal operation 	without interference.

 
Second Switch Configuration and Scope Output:

	When the Manula Switch is toogled again to the spoofed sensor data (the lower, spoofed speed input).
	Scope Output: The plot shows a significant linear increase, suggesting the control system is reacting to the spoofed data, interpreting it as a low speed. Consequently, it increases the throttle 		excessively in an attempt to reach the desired speed, even though the feedback is incorrect.



 Summary of Elements and Their Functions.

	- Constant (Desired Speed): Sets the target speed, e.g., 50 km/h, which the system tries to reach.
	- Sum Block: Calculates the error by subtracting the feedback speed from the desired speed. This error guides the system's adjustments.
	- PID Controller: Processes the error and generates a control signal to adjust the vehicle's speed, aiming to reduce the error to zero.
	- Transfer Function (Vehicle Dynamics): Simulates the vehicle's response to the control signal, providing a real-time output speed.
	- Constant1 (Spoofed Speed): Represents a fake (lower) speed used to simulate a cyberattack (sensor spoofing).
	- Manual Switch: Allows toggling between real feedback (from the Transfer Function) and the spoofed feedback. Switching to spoofed feedback simulates a cyberattack.
	- Scope: Displays the vehicle’s speed over time, helping observe system behavior with real vs. spoofed feedback.


 Overall Operation:

 	The system takes a target speed and compares it with the actual or spoofed speed to calculate an error. The PID controller uses this error to adjust the throttle, aiming to match the actual speed to the 	target. The Manual Switch allows testing of system stability by toggling between real and spoofed sensor data, showing how a cyberattack can affect performance.


## How to Use
1. Open `CPS_SpeedControlModel.slx` in Simulink.
2. Run the model to observe the vehicle's speed response on the Scope.
3. Adjust the PID parameters in the model to see different behaviors.


## Requirements
- Matlab R2024b or later with Simulink.


## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.







# Complete Procedure


