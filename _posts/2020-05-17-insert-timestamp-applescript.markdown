---
title: "Keyboard shortcut to insert current timestamp as text using AppleScript"
layout: post
date: 2020-05-17 18:04
image: 
headerImage: false
tag:
- macOS
- applescript
- timestamp
- automator
- keyboard-shortcut
- productivity
star: false
category: blog
author: prashant
hidden: false
description: Creating keyboard shortcut to insert current timestamp as text using AppleScript.
---

<img src="../assets/images/2020-05-17-insert-timestamp-applescript/quick-action-workflow.png" alt="Quick Action Workflow" style="width:100%;">

I often find myself adding timestamps in various documents, notes, readme and personal logs. Typing it manually is quite a hassle, so, I thought why not create a shortcut for this. If you too frequently insert timestamps in documents, this post might help you reduce the toil in your workflow.

1. Create a new `Quick Action` in `Automator.app`.

2. Set `Workflow receives current` option to `no input`. Leave others unchanged.

3. Drag `Run AppleScript` action from `Library -> Utilities` present in left panel to the center of the screen where it says `Drag actions or files here to build your workflow`.

4. Now to insert the current timestamp, first we need to get it and then ask our computer to type it. Here is the applescript to achieve this:

   ```applescript
   on run {input, parameters}
      set timestamp to (current date) as string
      tell application "System Events"
         keystroke timestamp
      end tell
   end run
   ```

   Paste it into the `Run AppleScript` code box.

5. Save the file with whatever name you like.

6. Goto `System Preferences -> Keyboard -> Shortcuts -> Services`, find the service with same name from previous step and assign a shortcut to it.

7. Goto an open file in your editor or to test box in Chrome or any other application where you can type and press the keyboard shortcut you created in previous step and current timestamp should appear like `Sunday, May 17, 2020 18:14:04`. When you use this shortcut in an application for the first time, it will ask access to control `System Events.app`. Click ok and then goto `System Preferences -> Security & Privacy -> Privacy` and enable that application to control your computer.

8. While this does the job, I wanted a more compactly formatted timestamp. I found this [Github Gist](https://gist.github.com/Glutexo/78c170e2e314f0eacc1a) which outputs current timestamp in `YYYY-MM-DD HH:MM:SS` format. We just need to plug this script into the workflow we created.

9. So, the updated script is:

   ```applescript
   on zero_pad(value, string_length)
      set string_zeroes to ""
      set digits_to_pad to string_length - (length of (value as string))
      if digits_to_pad > 0 then
         repeat digits_to_pad times
            set string_zeroes to string_zeroes & "0" as string
         end repeat
      end if
      set padded_value to string_zeroes & value as string
      return padded_value
   end zero_pad

   on run {input, parameters}
      set now to (current date)
      
      set result to (year of now as integer) as string
      set result to result & "-"
      set result to result & zero_pad(month of now as integer, 2)
      set result to result & "-"
      set result to result & zero_pad(day of now as integer, 2)
      set result to result & " "
      set result to result & zero_pad(hours of now as integer, 2)
      set result to result & ":"
      set result to result & zero_pad(minutes of now as integer, 2)
      set result to result & ":"
      set result to result & zero_pad(seconds of now as integer, 2)

      tell application "System Events"
         keystroke result
      end tell
   end run
   ```

   Paste it into the `Run AppleScript` code box.

10. Now when you press the keyboard shortcut you created, current timestamp should appear like `2020-05-17 18:29:15`.

Voila! Now you have a shortcut to insert timestamp anywhere.
