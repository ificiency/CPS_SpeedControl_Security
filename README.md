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





## Complete Procedure


   # Step 1: Set Up the Speed Control System

  
	1.	Open Simulink: Launch Matlab, then open Simulink from the toolbar.

	2.	Create a New Model: In Simulink, create a new blank model. This will be the basic control system of an autonomous vehicle.
		


			Add Blocks:

				Add a Constant block to represent the desired speed (target speed).
				Add a Sum block to calculate the error between the desired speed and the actual speed.
				Add a PID Controller block to adjust the throttle based on the error.
				Add a Transfer Function block to simulate the vehicle’s response (you can use a simple first-order model with a transfer function: (1)/(1+s)
				Add a Scope block to display the vehicle’s speed output.


			Connect the Blocks:
				Connect the Constant block to the Sum block (positive input).
				Connect the output of the Transfer Function to the negative input of the Sum block.
				Connect the Sum block to the PID Controller block.
				Connect the PID Controller block to the Transfer Function.
				Connect the output of the Transfer Function to the Scope block.



			Set Parameters:
				In the Constant block, set the desired speed (e.g., 50 km/h).
				Configure the PID Controller parameters as needed (e.g., P=1, I=0.5, D=0.1).
				Set the Transfer Function’s parameters to simulate the vehicle dynamics.






    # Step 2: Simulate a Cyberattack – Sensor Spoofing


               
	               1.	Add a Manual Switch: Insert a Manual Switch block to toggle between the real speed and a spoofed speed.

                       2.	Add a Constant Block for the Spoofed Value: Add another Constant block to represent the spoofed sensor reading (e.g., set it to a lower value like 30 km/h 																					to simulate an          																attack where the sensor falsely reports a slower speed).


	

              Integrate the Spoofed Sensor Data:
	

                   Connect the output of the Spoofed Constant block to one input of the Manual Switch.
	           Connect the Transfer Function output (real speed) to the other input of the Manual Switch.
	           Connect the output of the Manual Switch to the feedback input of the Sum block.
	           Configure the Switch: The Manual Switch will now let you toggle between the real sensor data and the spoofed sensor data. When toggled to the spoofed value, the control  				system receives incorrect speed data.




     #Step 3: Run and Observe the Results

			1.	Run the Simulation: Start the simulation and observe the output on the Scope.

			2.	Toggle the Switch: While the simulation is running, toggle the Manual Switch to simulate the attack. You’ll see the system respond to the false input, 					trying to reach the incorrect target speed.

			3.	Analyze: Observe how the vehicle’s speed control system attempts to adjust based on the spoofed speed value, demonstrating how an attack on sensor data can 				destabilize CPS.


   





## How to Use
1. Open `CPS_SpeedControlModel.slx` in Simulink.
2. Run the model to observe the vehicle's speed response on the Scope.
3. Adjust the PID parameters in the model to see different behaviors.


## Requirements
- Matlab R2024b or later with Simulink.


## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.







# Complete Procedure


