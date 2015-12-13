
package org.usfirst.frc.team5534.robot;


import edu.wpi.first.wpilibj.SampleRobot;


//This can be used for sensors and/or limit switches
//import edu.wpi.first.wpilibj.DigitalInput;

/**
 * This is a demo program showing the use of the RobotDrive class. 
 * The SampleRobot class is the base of a robot application that will 
 * automatically call your 
 * Autonomous and OperatorControl methods at the right time as controlled by 
 * the switches on 
 * the driver station or the field controls.
 * 
 * The VM is configured to automatically run this class, and to call the
 * functions corresponding to each mode, as described in the SampleRobot
 * documentation. If you change the name of this class or the package after
 * creating this project, you must also update the manifest file in the
 * resource directory.
 * 
 * WARNING: While it may look like a good choice to use for your code if
 * you're inexperienced, don't. Unless you know what you are doing, complex code will be much more
 * difficult under this system. Use IterativeRobot or Command-Based instead if you're new.
 * /
public class Robot extends SampleRobot {
  // RobotDrive myRobot;
  Joystick stick = new Joystick(1);

  Victor driveL;
  Victor driveR;
  
  Victor lift;
  
  Buttonb1 = new JoystickButton(stick, 1);
  
// DigitalInput limitSwitch;
//
//  public void robotInit() {
//          ^ The INT is the PWM digitalinput number
//    limitSwitch = new DigitalInput(1);
//  }
//
//  public void operatorControl() {
//      //more code here
//  while (limitSwitch.get()) {
//      Timer.delay(10);
//  }
//      //more code here
//  }


  public Robot() {
  
    // 'lift' more on PWM 2
//  lift = new Victor(2);
  }
  /**
  * AUTONOMOUS MODE
  * 
  * A. Reading inputs is disabled in autonomous mode. If you wish to test joystick, button, or other input,
  * it must be done in teleoperator mode or test mode.
  * /
public void autonomous() {
  // Set up instances here and other settings that do not change while
  // in autonomous mode.
  // Left and Right PWM ports
  // myRobot = new RobotDrive(0, 1);

  // Research what these do ...
  // myRobot.setExpiration(0.1);
  // myRobot.setSafetyEnabled(false);
  
  // Define the motor controller instances
  driveL = new Victor (1);
  driveR = new Victor (0);
  
  // Flag used to stop the while loop
  boolean isActive = true;
  
  // This loop is used to continue looping in autonomous mode assuming
  // that what we are doing more than one thing at a time.
// while ( isActive && isAutonomous() && isEnabled() ) {
//
//    // Break out at the next opportunity
//    isActive = false;
//    }

//  Drive forward at half speed
//    // also: myRobot.drive(-0.5, 0.0);
    driveL.set(0.5);
    driveR.set(-0.55);
    Timer.delay(3.0);
    
    // Stop for 2 seconds
    driveL.set(0.0);
    driveR.set(-0.0);
    Timer.delay(2.0);
    
    // Turn Left for 1/2 second
    driveL.set(-0.5);
    driveR.set(-0.55);
    Timer.delay(0.5);
    
    // Drive forward for 1.5 second on north side of column
    driveL.set(0.5);
    driveR.set(-0.55);
    Timer.delay(1.5);
    
    // Pause for 2 seconds before turning
    driveL.set(0.0);
    driveR.set(-0.0);
    Timer.delay(2.0);
    
    // Turn right for 1/4 second
    driveL.set(0.5);
    driveR.set(0.55);
    Timer.delay(.25);
    
    
    
    
    
    // Drive forward using a gyroscope
    // Gyro gyro;
    // static final double Kp = o.03;
    
    // RobotInit
    // gyro = new Gyro(1);
    
    // double angle = gyro.getAngle();
    // myRobot.arcadeDrive(-1.0, -angle*Kp );
    // Timer.delay(0.01);
    
    
    // Stop the robot as a last command
    // also: myRobot.drive(0.0, 0.0);
    driveL.set (0.0);
    driveR.set (0.0);
  }
  
  /**
   * Runs the motors with arcade steering.
   * /
  public void operatorControl() {
    
    //
    // INITIAL VALUES. Here we define the initial values for the various
    // components of the robot.
    //

        //  CHASSIS MOTORS
        double drivespeed = 0;
        double turnspeed = 0;
        
        driveR = new Victor(0);
        double Rdrivespeed = 0;
        
        driveL = new Victor(1);
        double Ldrivespeed = 0;
        
        
        // LIFT MECHANISM
        // NB: determine if a negative value makes the lift go up or down.
        
        lift = new Victor(2);
        double liftspeed = 0;
        
        
    //
    //  LOOP. This section of code is a continual loop as long as
    //  the driver station is set to Operator controlled and is
    //  also Enabled.
    //
        while (isOperatorControl() && isEnabled()) {
        
          //
          //  BUTTON. Determine whether the 
          //
              //  BUTTON PUSHED. Run lift motor until a limit switch
              //  is activated.
              liftspeed = stick.getRawButton(7) ? -0.30 : 0.00;
              
              
                  //  CHECK IF LIMITS REACHED.
                  //  If the lift has reached its upper or lower limit
                  //  then we need to set the lift speed to zero to protect
                  //  the motor from burning out or stripping the shaft.
                  
              //
              //  CHASSIS SPEED CONTROL
              //
                  // This code reads the joy stick and makes adjustments to 
                  // the drive speed. Initially we base the left and right
                  // motor speeds on the Y-axis of the joy stick. Then,
                  // these values are adjusted based upon the X-axis to
                  // determine an amount of turn. No use is currently made of the
                  // twist to the joy stick.
                      
                      drivespeed = stick.getY();
                      
                      // SET BASE SPEED FOR EACH SIDE OF CHASSIS. If we
                      // need to reduce the maximum speed of the robot, this can
                      // be done here. For example, the following code reduces the
                      // maximum speed of the robot by half.
                      
                      Ldrivespeed = drivespeed / 2;
                      Rdrivespeed = drivespeed / 2;
                      
                    // DETERMINE AMOUNT OF TURN. The amount of turn ranges
                    // from -1 to +1. If a negative value is LEFT, then this is 
                    // added to Left drive speed and subtracted from the Right 
                    // drive speed.
                        
                        turnspeed = stick.getX();
                        
                        // ADJUST DRIVE SPEED FOR EACH SIDE OF CHASSIS. This
                        // code makes each side of the robot turn at a different
                        // rate thus making the robot change direction.
                        Ldrivespeed += turnspeed / 2;
                        
                          Rdrivespeed -= turnspeed / 2;
                        
                        // ENSURE MAXIMUM VALUES ARE NOT EXCEEDED. If no
                        // reduction is applied to the drive speed and turn speed variables
                        // then the robot could potentially have its speed set to a value
                        // beyond -1 to +1. The code below will provide scaling to ensure that
                        // this does not happen. CURRENTLY NOT IMPLEMENTED.
                        
                        
                    //
                    // Code below this point actually sets motor speeds to their desired value.
                    // Prior to this we set the values that are used here.
                    //
                    //
                    
                        // LIFT MOTOR
                        lift.set( liftspeed );
                        
                        // CHASSIS DRIVE
                        driveL.set( Ldrivespeed );
                        driveR.set( Rdrivespeed );
                        
                        // DELAY FOR MOTOR UPDATE
                        // 0.005 seconds is 5 milliseconds
                        Timer.delay( 0.005 );
                        
                    }
              }
              
              /**
               * Runs during test mode
               */
              public void test() {
              }
}
    

