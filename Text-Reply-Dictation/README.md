# Text Reply Dictation
This profile is activated when you receive a text and have something already plugged into the headphone jack.
Will check if spotify is running and pause it, ask to read text, read text, ask to reply or call, reply with speech-to-text (or call), and if spotify was running before hand, it will resume spotify after everything is over (replying, calling, cancelling, etc.)

### Requirements
1. [Secure Settings](https://play.google.com/store/apps/details?id=com.intangibleobject.securesettings.plugin)

### Command Descriptions
```
Profile: Aux Text (16)
Event: Received Text [ Type:Any Sender:* Content:* ]
State: Headset Plugged [ Type:Any ]
Enter: Read Text (15)
A1: Variable Clear [ Name:%STD_OUT Pattern Matching:Off ] 
A2: Secure Settings [ Configuration:runcheck Package:com.intangibleobject.securesettings.plugin Name:Secure Settings Timeout (Seconds):0 ] 
A3: Wait [ MS:0 Seconds:3 Minutes:0 Hours:0 Days:0 ] 
A4: If [ %STD_OUT ~ *spotify* ]
A5: Send Intent [ Action:com.spotify.mobile.android.ui.widget.PLAY Cat:None Mime Type: Data: Extra: Extra: Package:com.spotify.music Class: Target:Broadcast Receiver ] 
A6: End If 
A7: Say [ Text:Read? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
<t4>
A8: Get Voice [ Title:Read Language Model:Free Form Maximum Results:1 Timeout (Seconds):30 ] 
A9: If [ %VOICE ~ *yes*/*read*/*yep*/*yeah*/*message* ]
A10: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A11: Say [ Text:%SMSRN said %SMSRB Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:On ] 
A12: Popup [ Title:%SMSRN Text:%SMSRB Background Image: Layout:Popup Timeout (Seconds):10 Show Over Keyguard:On ] 
A13: Say [ Text:Reply or call back? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A14: Get Voice [ Title:Reply or call back? Language Model:Free Form Maximum Results:1 Timeout (Seconds):20 ] 
A15: If [ %VOICE ~ *call* ]
A16: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A17: Variable Set [ Name:%call To:1 Do Maths:Off Append:Off ] 
A18: If [ %STD_OUT ~ *spotify* ]
A19: Wait [ MS:500 Seconds:0 Minutes:0 Hours:0 Days:0 ] 
A20: Send Intent [ Action:com.spotify.mobile.android.ui.widget.PLAY Cat:None Mime Type: Data: Extra: Extra: Package:com.spotify.music Class: Target:Broadcast Receiver ] 
A21: End If 
A22: Wait [ MS:500 Seconds:0 Minutes:0 Hours:0 Days:0 ] 
A23: Call [ Number:%SMSRF Auto Dial:On ] 
A24: Else 
A25: If [ %VOICE !~ *send*/*message*/*reply*/*tell*/ ]
A26: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A27: Say [ Text:Cancelled Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A28: Else 
A29: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
<t3>
A30: Say [ Text:What's your message? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
<t1>
A31: Get Voice [ Title:What's your message? Language Model:Free Form Maximum Results:1 Timeout (Seconds):30 ] 
A32: If [ %VOICE !Set ]
A33: Say [ Text:Didn't catch that. Let's try again. Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A34: Goto [ Type:Action Label Number:22 Label:t1 ] 
A35: Else 
A36: Variable Set [ Name:%MessageContent To:%VOICE Do Maths:Off Append:Off ] 
A37: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A38: Say [ Text:Your said %MessageContent. Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:7 Respect Audio Focus:On Network:Off Continue Task Immediately:On ] 
A39: Popup [ Title:You said Text:%MessageContent Background Image: Layout:Popup Timeout (Seconds):8 Show Over Keyguard:On ] 
A40: Say [ Text:Do you want to send it? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:7 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
<t2>
A41: Get Voice [ Title:Send the message? Language Model:Free Form Maximum Results:1 Timeout (Seconds):30 ] 
A42: If [ %VOICE ~ *send*/*yes*/*ok*/*yup*/*yeah*/*go ahead* ]
A43: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A44: Send SMS [ Number:%SMSRF Message:%MessageContent Store In Messaging App:Off ] 
A45: Say [ Text:Message sent Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A46: Else 
A47: If [ %VOICE !~ *no*/*nah*/*nope*/*cancel*/*go home*/*nevermind* ]
A48: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A49: Say [ Text:Didn't catch that. Do you want me to send the message? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A50: Goto [ Type:Action Label Number:25 Label:t2 ] 
A51: Else 
A52: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A53: Say [ Text:Do you want to rewrite the message? Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A54: Get Voice [ Title:Re-enter the message? Language Model:Free Form Maximum Results:1 Timeout (Seconds):30 ] 
A55: If [ %VOICE ~ *yes*/*ok*/*yup*/*yeah*/*go ahead* ]
A56: Variable Clear [ Name:%VOICE Pattern Matching:Off ] 
A57: Goto [ Type:Action Label Number:14 Label:t3 ] 
A58: End If 
A59: End If 
A60: End If 
A61: End If 
A62: End If 
A63: End If 
A64: Else If [ %VOICE !~ *no*/*nope*/*cancel*/*exit* ]
A65: Say [ Text:Didn't catch that. Let's try again. Engine:Voice:com.google.android.tts:eng-usa Stream:3 Pitch:5 Speed:5 Respect Audio Focus:On Network:Off Continue Task Immediately:Off ] 
A66: Goto [ Type:Action Label Number:22 Label:t4 ] 
A67: End If 
A68: If [ %STD_OUT ~ *spotify* & %call !~ 1 ]
A69: Wait [ MS:500 Seconds:0 Minutes:0 Hours:0 Days:0 ] 
A70: Send Intent [ Action:com.spotify.mobile.android.ui.widget.PLAY Cat:None Mime Type: Data: Extra: Extra: Package:com.spotify.music Class: Target:Broadcast Receiver ] 
A71: End If
```
