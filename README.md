# PhoenixEngine
Phoenix Engine is a framework for VEX sonar controlled robots.

# Premise
  The whole premise of the sonar framework is to create a virtual grid onto the field, and to assign absolute positions to every point onto the field, thus creating great versatility in autonomous controlled competitions. The framework is designed exclusively around mecanum wheels, as per the motorSet method.
  
# Indexing loop structure
  The entirity of the code is written in a singular loop, namely to get constant feedback and updates to many methods, such as the ones controlling the output to the motor of the control or the methods which modify the sonar distances through trigonometry. All user defined method calls will be passed an index value in which to execute, and as soon as the method is done executing, it will raise the value of the global index, so to allow the next step to execute.
  
# API
  StrafeX (float, int, bool)
The purpose of this method is to assign the proper values to the virtual x-axis so that the framework can later commit the values to the motors and thus produce motion left and right relatively to the bot.
The first float value is the expectedLocation variable, which is the absolute posistion on the field in the x direction for the bot to try and move too. Based off of the motor intervals defined on the task, a scenario of harmonic motion is possible, so be wary. On strafing left and right, the high amounts of friction causes the motors to stall, and the weight ditrubution of the bot causes arcing in the bot's trajectory, hence the reason that the motorset values per interval are much greater than in strafeX's sister method, strafeY.
The first int represents the index value for which the method will execute, as explained under the header "Indexing loop structure".
The bool is the waitOnY variable. Due to the structure of the sister functions, strafeX and strafeY, they can execute simultaneouslly on the same index value. This value represents if the method should wait to increase the global task index until its sister function has indicated that it is done executing.

  StrafeY (float, int, bool)
The purpose of this method is to assign the proper values to the virtual y-axis so that the framework can later commit the values to the motors and thus produce motion forwards and backwards relativily to the bot.
The first float value is the expectedLocation variable, which is the absolute posistion on the field in the y direction for the bot to try and move too. Based off of the motor intervals defined on the task, a scenario of harmonic motion is possible, so be wary.
The first int represents the index value for which the method will execute, as explained under the header "Indexing loop structure".
The bool is the waitOnX variable. Due to the structure of the sister functions, strafeX and strafeY, they can execute simultaneouslly on the same index value. This value represents if the method should wait to increase the global task index until its sister function has indicated that it is done executing.

  rotate (int, int)
The purpose of this method is to assign the proper values to the virtual rotate axis so that the framework can later commit the values to the motors and thus produce angular motion relative to the spinning of the control box.
The first int represents the equilbrium angle of the bot, that the method will try to reach.
The second int represents the taskIndex value on which the method should execute, as explained under the header "Indexing loop structure".

  lift (int, int)
The lift method is designed is change the height of the lift so that multiple heights can be used during autonomous.
The first int is the expected height, so the bot will try to reach an equilibrium height at that passed value.
The second int represents the taskIndex value on which the method should execute, as explained under the header "Indexing loop structure".

  jerk (int, bool)
The jerk method is designed for times in which the bot is facing the wall and needs to move forward or backwords enough so that the cube can be placed onto either a skyrise tower, or one of the scoring posts. So the method is only designed to move the bot from a rotating distance from the wall to being able to drop the cube, or vice versa. It is highly recommended that both strafeX and strafeY are called immediatly afterwards so that the posistion of the bot is exactly where it needs to be, due to the inconsistencies with the jerk method.
The first int represents the index value for which the method will execute, as explained under the header "Indexing loop structure".
The first bool is for changing the direction, if true, the bot will jerk forwards, and if it is false, than the bot will jerk backwards.

