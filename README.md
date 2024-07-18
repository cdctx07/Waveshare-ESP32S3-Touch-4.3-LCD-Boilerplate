# Waveshare-ESP32S3-Touch-4.3-LCD-Boilerplate
Boilerplate to make Waveshare show standard Squareline UI export

Using the examples and libraries offered by Waveshare's wiki (https://www.waveshare.com/wiki/ESP32-S3-Touch-LCD-4.3), I was able to get the Waveshare screen to work with minimal changes.

The ui.ino file is a copy of Waveshare's Arduino lvgl_Porting.ino file (download the ESP32-S3-Touch-LCD-4.3_Code.zip file from the aforementioned wiki). I removed all the LVGL example program references, then I added ui_init() (exported function from ui.h/ui.c files in the Squareline exported library folder) and lv_timer_handler() between lvgl_port_lock(-1) and lvgl_port_unlock().

This is all in the main ui.ino file, so you should be able to do the following to get your Waveshare ESP32S3 LCD 4.3" touch display to work:
****Note: I deviate from Waveshare's methodology. They have you put the library files in your main Arduino folder. Since I have numerous devices with various libraries, I make my own Arduino folders for them (e.g., Arduino - Waveshare). Even then, I don't have one library folder for all Waveshare projects. Instead, each project has its own library folder, just as how Squareline exports the projects. SO, you will need to go to Arduino's preferences and change your "Sketchbook location" to your project's main folder... more below.

1) Create a Squareline project with whatever display stuff you want.
  - Remember to set the display as 800x480 (with whatever rotation)
  - Use Arduino v1.1.2 with whatever LVGL 8.3.x (I used 8.3.11)
  - My Project Export Root resides in a dedicated C:/.../Documents/Arduino - Waveshare subfolder (e.g., C:/Users/username/OneDrive/Documents/Arduino - Waveshare/myprogram)
  - The UI Files Exports Path is the same above, but './libraries/ui/src' added on (so C:/Users/username/OneDrive/Documents/Arduino - Waveshare/myprogram/./libraries/ui/src)
2) In Squareline, go to Export then Create Template Project.
3) Once complete, go to Export then Export UI Files.
4) Go to the project folder and open the libraries folder.
5) Drag and drop all of the library files provided by the aforementioned Waveshare wiki site (ESP32-S3-Touch-LCD-4.3 libraries.zip) into this folder. You can remove TFT_eSPI; make sure the ui folder remains.
6) Download the files in this repository and put them in the project folder's ui folder (and allow the override of the original ui.ino file provided by Squareline). When done, copy "ESP_Panel_Conf.h" to the project folder's library folder.
7) Open ui.ino in Arduino, then go to File -> Preferences. For sketchbook location, click Browse and find your project's folder (the one that has the "libraries" and "ui" folders). In the above folder example, this would be C:/Users/username/OneDrive/Documents/Arduino - Waveshare/myprogram. Click OK.
8) For board, select ESP32S3 Dev Module, ensure the proper board settings (again, see the Waveshare wiki), then compile/upload to board.

This should compile with your UI files, as the ui.ino is mainly there to setup the boot session and call ui_init (then let lvgl do its thing). You can add your own custom functions and C externs to the ui.ino as needed (such as WiFi connect, HTTP server, scale functions, etc.), or you can make these separate imported files. But just keep the core things where they are.

Bonus note: Squareline will override your lvgl.h file, so once you adjust any settings (e.g., font), make a backup of it so you can simply copy and rename to lvgl.h when you reexport ui files.
