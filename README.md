# VRCTT-VEXcode
Please read the latest code created. Thanks in advance!

/*----------------------------------------------------------------------------*/
/*                                                                            */
/*    Module:       main.cpp                                                  */
/*    Author:       C:\Users\admin                                            */
/*    Created:      Fri Oct 04 2019                                           */
/*    Description:  V5 project                                                */
/*                                                                            */
/*----------------------------------------------------------------------------*/
#include "vex.h"

using namespace vex;

// A global instance of vex::brain used for printing to the V5 brain screen
vex::brain       Brain;
// A global instance of vex::competition
vex::competition Competition;

// define your global instances of motors and other devices here
vex::motor        LeftTop(PORT10, gearSetting::ratio18_1, true);
vex::motor        RightTop(PORT20, gearSetting::ratio18_1, false);
vex::motor        LeftBottom(PORT6, gearSetting::ratio18_1, true);
vex::motor        RightBottom(PORT16, gearSetting::ratio18_1, false);
vex::motor        Motor19(PORT19, gearSetting::ratio36_1, false);
vex::motor        Motor9(PORT9, gearSetting::ratio36_1, true);
vex::motor        Snapper(PORT11, gearSetting::ratio18_1, false);
vex::controller   Controller1;

/*---------------------------------------------------------------------------*/
/*                          Pre-Autonomous Functions                         */
/*                                                                           */
/*  You may want to perform some actions before the competition starts.      */
/*  Do them in the following function.  You must return from this function   */
/*  or the autonomous and usercontrol tasks will not be started.  This       */
/*  function is only called once after the cortex has been powered on and    */ 
/*  not every time that the robot is disabled.                               */
/*---------------------------------------------------------------------------*/

void pre_auton( void ) {
  // All activities that occur before the competition starts
  // Example: clearing encoders, setting servo positions, ...
  
}

/*---------------------------------------------------------------------------*/
/*                                                                           */
/*                              Autonomous Task                              */
/*                                                                           */
/*  This task is used to control your robot during the autonomous phase of   */
/*  a VEX Competition.                                                       */
/*                                                                           */
/*  You must modify the code to add your own robot specific commands here.   */
/*---------------------------------------------------------------------------*/

void autonomous( void ) {
  // ..........................................................................
  // Insert autonomous user code here.
  // ..........................................................................

}

/*---------------------------------------------------------------------------*/
/*                                                                           */
/*                              User Control Task                            */
/*                                                                           */
/*  This task is used to control your robot during the user control phase of */
/*  a VEX Competition.                                                       */
/*                                                                           */
/*  You must modify the code to add your own robot specific commands here.   */
/*---------------------------------------------------------------------------*/

void usercontrol( void ) {
  // User control code here, inside the loop
  while (1) {
    // This is the main execution loop for the user control program.
    // Each time through the loop your program should update motor + servo 
    // values based on feedback from the joysticks.

    // ........................................................................
    // Insert user code here. This is where you use the joystick values to 
    // update your motors, etc.
    // ........................................................................
if(abs(Controller1.Axis2.position(percentUnits::pct))>5) {
RightTop.spin(directionType::fwd,Controller1.Axis2.position(percentUnits::pct),velocityUnits::pct);
RightBottom.spin(directionType::fwd,Controller1.Axis2.position(percentUnits::pct),velocityUnits::pct);
}
else {
RightTop.stop();
RightBottom.stop();
}
if(abs(Controller1.Axis3.position(percentUnits::pct))>5) {
LeftTop.spin(directionType::fwd,Controller1.Axis3.position(percentUnits::pct),velocityUnits::pct);
LeftBottom.spin(directionType::fwd,Controller1.Axis3.position(percentUnits::pct),velocityUnits::pct);
}
else {
  LeftTop.stop();
  LeftBottom.stop();
}
if(Controller1.ButtonL1.pressing()){
  Motor9.spin(directionType::fwd, 50, velocityUnits::pct);
  Motor19.spin(directionType::fwd, 50, velocityUnits::pct);
}
else if(Controller1.ButtonL2.pressing()){
  Motor9.spin(directionType::rev, 50, velocityUnits::pct);
  Motor19.spin(directionType::rev, 50, velocityUnits::pct); 
}
else{
  Motor19.stop(brakeType::hold);
  Motor9.stop(brakeType::hold);
}
if(Controller1.ButtonR1.pressing()){
  Snapper.spin(directionType::fwd, 50, velocityUnits::pct);
}
else if(Controller1.ButtonR2.pressing()){
  Snapper.spin(directionType::rev, 50, velocityUnits::pct);
}
else{
  Snapper.stop(brakeType::hold);
}


    vex::task::sleep(20); //Sleep the task for a short amount of time to prevent wasted resources. 
  }
}

//
// Main will set up the competition functions and callbacks.
//
int main() {
    //Set up callbacks for autonomous and driver control periods.
    Competition.autonomous( autonomous );
    Competition.drivercontrol( usercontrol );
    
    //Run the pre-autonomous function. 
    pre_auton();
       
    //Prevent main from exiting with an infinite loop.                        
    while(1) {
      vex::task::sleep(100);//Sleep the task for a short amount of time to prevent wasted resources.
    }    
       
}
