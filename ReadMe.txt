WordMap-System Access Violation
is a C# 2019 app that uses a backgroundWorker to generate bitmap representations of a word's location on a given RichTextBox.  This app was developed to reproduce an error that has been recurring in a Creative Writer's Word Processor that I wrote and published onto the CodeProject website https://www.codeproject.com/Articles/5246733/Creative-Writers-Word-Processor-Csharp2022

The backgroundWorker needs to reproduce the state of the RichTextBox but threading violations prevent it from accessing the actual RichTextBox.  The 'state' of the RTX is recorded and sent to the BackgroundWorker as an input parameter which is then used by the BackgroundWorker when it instantiates the RichTextBoxes that it needs to generate the graphic representation of a given word's location in the text.

The method by which the Bitmap is generated works, however, after repeatedly(from dozens to several thousand iterations) executing this function the BackgroundWorker encounters a System-Access-Violation error which the Try-Catch does not detect and the entire application simply quits (or the debugger stops and complains until you Ctrl-F10 back to the top again and F5 it back to life).

This app, repeatedly picks a random word in a provided text then draws the Bitmap to 'map' its location where it appears in the source RichTextBox.  

As I have been testing to see how often it can complete its job before crashing, 
every time the BackgroundWorker is executed it updates the content of a local file 
 		: WordMap_Result_MostRecent.txt
with a running count of how many times it has started to draw a bitmap.

At the moment when it runs for the last time before crashing, its count is recorded on that file so that when the app is launched again it reads the same file and appends its content (number of times it was called before it crashed during the last test run) into a separate file
		: Word_Results_List.txt

which, after several Crash-Tests, now reads 


421
1907
2389
672
384
604
332
278
91
120
320
993
2100
1438
1038
295
352
1714
858
46
500
2479
1083
170
501
61
2898
1618
3356
5420
444
1000
188
942
243
1961
1253
3659
774
1397

indicating that there is no obvious pattern and the crashing may as well be random.

The purpose for including this app here on GitHub is to enlist the help of other more experienced programmers who can better understand what the problem is.
