package org.firstinspires.ftc.teamcode.teleop;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.eventloop.opmode.Disabled;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.Servo;
import com.qualcomm.robotcore.hardware.DcMotorSimple;
import com.qualcomm.robotcore.util.ElapsedTime;
import com.qualcomm.robotcore.util.Range;

// version 3 of taro's driver control code
// basic drivetrain opmode w/ other components (& servo claw) and split gamepads

// @Disabled
@TeleOp(name="teleop_v5", group="Linear Opmode")
public class teleop_v5 extends LinearOpMode
{
    private ElapsedTime runtime = new ElapsedTime();

    //name motor variables
    private DcMotor fldrive, frdrive, brdrive, bldrive, slideleft, slideright, turret;
    double  MIN_POSITION = 0, MAX_POSITION = 1;

    @Override
    public void runOpMode()
    {
        telemetry.addData("Status", "Initialized");
        telemetry.update();

        // map the motor variables to actual motors
        fldrive = hardwareMap.get(DcMotor.class, "fldrive");
        frdrive = hardwareMap.get(DcMotor.class, "frdrive");
        brdrive = hardwareMap.get(DcMotor.class, "brdrive");
        bldrive = hardwareMap.get(DcMotor.class, "bldrive");
        slideleft = hardwareMap.get(DcMotor.class, "slideleft");
        slideright = hardwareMap.get(DcMotor.class, "slideright");
        turret = hardwareMap.get(DcMotor.class, "turret");


        // set direction of motors
        fldrive.setDirection(DcMotor.Direction.FORWARD);
        frdrive.setDirection(DcMotor.Direction.REVERSE);
        brdrive.setDirection(DcMotor.Direction.REVERSE);
        bldrive.setDirection(DcMotor.Direction.FORWARD);
        slideleft.setDirection(DcMotor.Direction.FORWARD);
        slideright.setDirection(DcMotor.Direction.FORWARD);
        turret.setDirection(DcMotor.Direction.FORWARD);

        // wait for the game to start (driver presses PLAY)
        waitForStart();
        runtime.reset();

        // slowmode
        boolean slowmode = false;
        boolean xControl = false;

        while (opModeIsActive())
        {
            double speed = gamepad1.left_stick_y;
            double turn = gamepad1.right_stick_x;
            double strafe = gamepad1.left_stick_x;
            double tfor = gamepad2.right_trigger;
            double tback = gamepad2.left_trigger;
            double ls = gamepad2.left_stick_y;

            //determine power for each motor
            double fl = speed+turn+strafe;
            double fr = speed-turn-strafe;
            double br = speed-turn+strafe;
            double bl = speed+turn-strafe;
            double t = tfor - tback;

            // slow mode
            if (slowmode){
                fl /= 10;
                fr /= 10;
                bl /= 10;
                br /= 10;
                ls /= 5;
            }

            //set power to motors with range of -1 to 1
            fldrive.setPower(Range.clip(fl, -1.0, 1.0));
            frdrive.setPower(Range.clip(fr, -1.0, 1.0));
            brdrive.setPower(Range.clip(br, -1.0, 1.0));
            bldrive.setPower(Range.clip(bl, -1.0, 1.0));
            slideleft.setPower(Range.clip(ls, -0.5, 0.5));
            slideright.setPower(Range.clip(ls, -0.5, 0.5));
            turret.setPower(Range.clip(t, -0.5, 0.5));

            xControl = !gamepad1.x;

            //debug messages for each motor
            telemetry.addData("fldrive",Double.toString(fldrive.getPower()));
            telemetry.addData("frdrive",Double.toString(frdrive.getPower()));
            telemetry.addData("brdrive",Double.toString(brdrive.getPower()));
            telemetry.addData("bldrive",Double.toString(bldrive.getPower()));
            telemetry.addData("slideleft",Double.toString(slideleft.getPower()));
            telemetry.addData("slideright",Double.toString(slideright.getPower()));
            telemetry.addData("turret",Double.toString(turret.getPower()));
            // telemetry.addData("claw position",Double.toString(clawServo.getPosition()));
            // telemetry.addData("claw position",Double.toString(clawPosition));

            telemetry.update();
        }
    }
}
