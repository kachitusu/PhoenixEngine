# PhoenixEngine
Framework for VEX sonar controlled robot

# Premise
  The whole premise of the sonar framework is to create a virtual grid onto the field, and to assign absolute posistions to every point onto the field, thus creating great versatility in autonomous controlled competitions. The framework is designed exclusivly around mecanum wheels, as per the motorSet method
  
# Indexing loop structure
  The entirity of the code is written in a singular loop, to add the looping functionality of programing, namely to get constant feedback and updates to many methods, such as the ones controlling the output to the motor of the control or the methods which modify the sonar distances through trignometry. All user defined method calls will be passed an index value in which to execute, and as soon as the method is done executing, it will raise the value of the global index, so to allow the next step to execute
  
# API
  StrafeX (float, int, bool)
The purpose of this method is to assign the proper values to the virtual x axis so that the framework can later commit the values to the motors and thus produces motion left and right relativily to the bot
The first float value is the expectedLocation variable, which is the absolute posistion on the field in the x direction for the bot to try and move too. Based off of the motor intervals defined on the task, a scenario of harmonic motion is possible, so be wary
The second int represents the index value for which the method will execute, as explained under the header "Indexing loop structure"
The bool is the waitOnY variable. Due to the structure of the sister functions, strafeX and strafeY, they can execute simultaneouslly on the same index value. This value represents if the method should wait to increase the global task index until its sister function has indicated that it is done executing.
