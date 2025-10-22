# monteporzio_ergocub_demo
Demo instructions for starting ergoCubSN000 in Monteporzio

# ErgoCub Robot Basics

These instructions aim to explain the robot basics on how the PC configuration is done, and how to turn it on.

> [!CAUTION]
> When you use the robot you need to have all the safety precaution put in place, i.e.- the crane, emergency button and so on

# ergoCubSN000

> [!TIP]
> While typing the commands, you can use `TAB` to autocomplete them and be quicker

## Power on

> [!IMPORTANT]  
> The robot needs to be suspended on the crane

0. Check the connections:
   
   Be assured that the power cables are properly tightened and connected to the robot as shown in the following pictures of this section.

2. Turn on the power supply:
   
![ergoCub_PowerSupply](https://github.com/hsp-iit/demos/assets/86918431/83eefd8e-1f9f-4ebf-a7e2-e1c5cc95231d)

4. Power on the robot PCs and Motors:

Both LEDs need to be Green and not blinking

![ergoCub_back_description](https://github.com/hsp-iit/demos/assets/86918431/833d000f-287d-4655-bc7a-38a2b0a2f220)

## YARP setup

0. Launch the `yarpmanager` from a terminal on the laptop.
1. In the *cluster* section, start the `yarpserver` (Nameserver Node)

![yarpmanager_cluster](https://github.com/hsp-iit/demos/assets/86918431/580798a3-4897-4354-a3b1-99ed0b982d38)

2. Start the following `yarpserver` nodes, under the `Nodes` section: `ergocubXXX-lap`, `ergocub-torso`, `ergocub-head`

## Connectivity

**Table with the PCs IPs and aliases:**

### ergoCubSN000
| Alias | IP | location |
| ----- | --- | ------ |
|`ergocub-laptop` | `10.0.2.4` | Alienware laptop outside the robot |
|`ergocub-head` | `10.0.2.3` | Nvidia Xavier on the robot head |
|`ergocub-torso` | `10.0.2.2` | Internal PC in the robot torso |
| | `10.0.2.1` | External server for connectivity and network access management |

> [!TIP]
> If you don't know the robot password, ask it on the relative Microsoft Teams channel

To connect to one of the PCs, just type: `ssh <alias name>` like: `ssh ergocub-torso`

## Start-up the Robot and set it up

> [!WARNING]  
> **Do the following steps while the robot is suspended on the crane.**

**3. Launch the YarpRobotInterface on the robot torso:**
   
> [!IMPORTANT]
> Before running the next command, verify that the robot is in a resting position, the joints need to be far away from their limits, like in the picture:
> 
> ![ergoCub_standing](https://github.com/hsp-iit/demos/assets/86918431/b2d7bea3-5f8c-4198-8504-b51087696caa)

On the TORSO run:
   ```
   yarprobotinterface --config ergocub.xml
   ```

**4. Launch the yarpmotorgui:**

On the laptop run:
```
yarpmotorgui --from custom_positions.ini
```
And home all the parts into `TwoFeetStanding` position.

**5. Calibrate the FT sensors:**
Once the robot is completely staying still, run on a terminal:
   ```
   yarp rpc /wholeBodyDynamics/rpc
   >> calib all 300
   ```
