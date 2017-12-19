# PROBLEM DESCRIPTION

- Developing blender addons can be a serious pain, especially
when the code base is large.

- Blenders internal text-editor is quite lacking and although there
are some powerful addons out there to improve the experience, sometimes
you just want to work in an IDE that you love.

- There is no obvious way to link up your IDE to blender that allows 
a fast workflow

# PROPOSAL

- This document showcases a blender-pycharm workflow that I have 
personally stumbled upon that may or may not ease your troubles.

# Solution

1. Obviously you should have both blender and Pycharm installed on
your machine

2. Find a suitable folder where you can put all your addon development
work. This folder will have a special format that will allows us to link
it to blender.

3. Once you've made the folder, add three sub-folders into it - addons, modules
and startup.

    - Here's how mine looks
![Alt text](/res/folders.png?raw=true "Folder Layout")
    
4. Next we will link this folder to blender. i.e Blender will always know how to find
this folder

    - Open blender
    - Goto File -> User Preferences 
    - Under the file tab 
    - Find the scripts path and point it to the folder we just made
    
    - Here's mine
![Alt text](/res/user-prefs.png?raw=true "User Preferences")  


5. Now we are going to setup PyCharm. Hold on to your socks

6. First of we want to create some pre-definitions for pycharm , so that it won't
bother us with loads of errors when developing addons for blender

7. Create another folder somewhere you like and download the pypredef_gen.py file
that is in this repo into that folder.
    - You can click on the file 
    - Click Raw
    - Save it into the folder you just made
    
    - Have something like this
![Alt text](/res/predef-folder.png?raw=true "Predef-folder") 
    
    
8. Now we are going to run this script, but we will do it with blender.

9. Find the path to your Blender executable.
    
    Something like :
        - 'C:\program files\blender\blender.exe',
                or
        - '/usr/bin/blender'
        
        
10. Run this command:
    path/to/blender/executable -b -P "path/to/pypredef_gen.py"
    
    replace 'path/to/blender/executable' with path from step 9
    replace 'path/to/pypredef_gen.py' with path to that file
     
11. Step 10 will create some folders like this:

![Alt text](/res/predef-generated.png?raw=true "Predef-Generated")
 
12. Now that we have pre-definitions, we can go over the steps you will have to take
to develop blender addons with pycharm

13. Create a new pycharm project - this will be your addon.
    - Now this is important. You will want to create this project in the first
      folder that we created, under addons. This is where you will develop all
      your addons.
      
      i.e:
      if your first-folder was called 'blender-addons', your project should be
      under : "blender-addons/addons/<Your Project Name>" 
      

14. To set the pre-definitions for the project:
    - Go to File -> Settings
    - Under Project:<Your Project Name> -> Project Structure
    - Select Add Content Root
    - Navigate to pypredef folder
    
    - Like This:   
![Alt text](/res/predef-setup.png?raw=true "Predef-Setup")

    - Now pycharm will autocomplete blender python API
    
NOTE: You will have to do this for all your blender-addon projects

15. Now we will finalize the setup and smoothen the workflow.

    -- First up is  -> How to run the addon.
    
    a) If you set up the first folder properly, anytime you create a new addon
      project as in step 13, The addon will automatically be imported to blender.
      - thats the magic of the first folder.
      
    b) If you open blender, go to the user preferences under addons, you can
       enable it. It will remain enabled for the entire development.
       
    c) To keep refreshing the addon while you develop, you will need to keep
       restarting blender. Luckily we can create a run configuration in pycharm
       for exactly this.
       
    d) In your pycharm project root folder, create a new script called start_blender.py
    
    e) Add the following 2 lines:
    
        import os 
        os.system("path/to/blender/executable")
        
    f) Right-click on the file in the project tree and navigate to "Create 'start_blender.py'"
    
    g) Now anytime you run the project <shift-f10>, it will open blender which will reload
       your addon.
       
    h) For some more goodies, you may want to start blender with some given settings every time
        e.g a layout.
        
        Create a start.blend file with all your settings and save it in the root of your project
        Now modify your start_blender.py:
            
            import os
            os.system("path/to/blender/executable  start.blend")
            
        Now everytime you run blender, it will open the .blend file with your settings.
        
16. Finally make your cool addon.

    - Here's a sample
![Alt text](/res/blender-pycharm.gif?raw=true "Sample Workflow")    
    

# CONCLUSION 

This is certainly alot of work to do,  which is why its not for everyone. 
If you are working with a huge multiple file/ multiple package addon, you should be able
to appreciate the value of this workflow like I have.

Some Caveats:
    - If your blender has slow starup time - <Your screwed>
    - All blender output is delayed by pycharm until the program exits
    - No debugging - obviously.
    
    
    
