# Create a Program Shortcut on the Desktop

1. Create a `.desktop` file

   Create a file with the `.desktop` extension and add the following content. Edit the fields as needed:

   ```text
   [Desktop Entry]
   Version=1.0
   Type=Application
   Name=Program Name
   Exec=/path/to/your/program
   Icon=/path/to/your/icon
   Terminal=false
   Categories=Program
   StartupNotify=true
   ```

2. Make the file executable

Right-click the `.desktop` file and select **"Allow Launching"**.

## Reference

- [How to make a desktop shortcut on Ubuntu 20.04? - Ask Ubuntu](https://askubuntu.com/questions/1232612/how-to-make-a-desktop-shortcut-on-ubuntu-20-04/1232616#1232616)
