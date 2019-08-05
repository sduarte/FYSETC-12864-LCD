# FYSETC-12864-LCD
How to Setup Graphic LCD from FYSETC on Anycubic i3 Mega

Since the LCD that comes with the original Anycubic i3 Mega is not an open source hardware and has very few functions and lots of limitations I decided to upgrade my printer to use a standard Prusa-like LCD.
I found a very reasonable one at: 
https://www.aliexpress.com/item/33029483516.html?spm=a2g0s.9042311.0.0.4effb90aoEFDRE
And this is a simple guide about removing the original LCD from the Anycubic i3 Mega and installing a new one. 

This is my first attempt at GitHub also my first attempt to write a tutorial about anything. So keep in mind this is a work in progress.

For Basic documentation about this LCD please look at:  
https://wiki.fysetc.com/Generic_12864_Panel/

Some steps at this wiki were changed in order to work with my Anycubic i3 Mega using Marlin Firmware: https://github.com/davidramiro/Marlin-AI3M/releases

FIRST STEP - Invert EXP1 and EXP2 connectors. To do that you don't need to desolder anything, just gently push the plastic part away from the board and invert it. 

CHANGES IN Configuration.h:

Comment:

        // Enable Anycubic TFT
        //#define ANYCUBIC_TFT_MODEL
        //#define ANYCUBIC_FILAMENT_RUNOUT_SENSOR
        //#define ANYCUBIC_TFT_DEBUG

Uncomment:

        #define MINIPANEL

Keep This commented (conflict with FYSETC documentation):

        //#define NEOPIXEL_LED

CHANGES IN Ramps.h - Use the chages on FYSECT Wiki

CHANGES IN pins_TRIGORILLA_14.h:

Find: 

        #elif defined(MULTIPANEL)

below #define SD_DETECT_PIN 49 (mine is line 216) insert:

        #elif defined(MINIPANEL)
        // Pins for DOGM SPI LCD Support
        #define DOGLCD_A0           16
        #define DOGLCD_CS           17
        #define LCD_BACKLIGHT_PIN   27 
        #define LCD_RESET_PIN       23
        #define LCD_CONTRAST        127
        #define SDSS                53
        #define BEEPER_PIN          37
        #define BTN_EN1             31
        #define BTN_EN2             33
        #define BTN_ENC             35
        #define SD_DETECT_PIN       49
        #define KILL_PIN            -1
        
 
 CHANGES IN Configuration_adv.h - Use the chages on FYSECT Wiki
 
 CHANGES IN ultralcd_impl_DOGM.h - Use the chages on FYSECT Wiki
