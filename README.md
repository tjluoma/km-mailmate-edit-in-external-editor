km-mailmate-edit-in-external-editor
===================================

**Summary: Keyboard Maestro macro to edit email message from MailMate in another editor, such as MultiMarkdown Composer**

[MailMate] is a great email client which supports [Markdown]. If you want to write your emails in a Markdown-aware editor such as [MultiMarkdown Composer], then you'll need a way to easily move text between the two apps.

I mean, sure, you could do:

1.	Select All in MailMate
2.	Cut
3.	Switch to MultiMarkdown Composer
4.	Create a new file
5.	Paste
6.	Save it, just in case something happens
7.	Write the email
8.	Select All
9.	Cut
10.	Switch back to MailMate
11.	Paste

You could do that *like an animal*™ but wouldn't you rather:

1.	Press a keyboard shortcut, have your email automatically saved to a temporary file, have that file opened in MultiMarkdown Composer (or any other text editor you prefer)
2.	Write the email
3.	When finished, save the file
4.	Quit MultiMarkdown Composer

and have the contents of that temporary file pasted back into your MailMate compose window?

Of course you would. That's 4 steps instead of 11. If you remove "Write the email" from both lists, it is ***three*** steps instead of ***ten***.


## Installation and Configuration ##

* Download [MailMate-Edit-in-External-App.kmmacros] and import it into [Keyboard Maestro].

* If you want to change the keyboard shortcut from <kbd>Control</kbd> + <kbd>Option</kbd> + <kbd>M</kbd>  to something else, you can set that within the Keyboard Maestro macro.

* If you want to use a different editor, look for the "Execute Shell Script" portion of the macro, and edit this line:

		MM_APP="MultiMarkdown Composer"

Change 'MultiMarkdown Composer' to the name of the app that you want to use instead.

* Temporary files are stored in ~/Library/Application Support/MailMate/ but you can change that by changing the `MM_TEMP_DIR=` line in the shell script. By default it is:

		MM_TEMP_DIR="$HOME/Library/Application Support/MailMate"

n.b. If the macro detects that the temporary file was successfully copied back onto the pasteboard, the temporary file will automatically be moved to the Trash. If you want to keep them for some reason or you want to move them to a different directory, edit or remove this line in the script:

		/bin/mv -n "$TEMPFILE" "$HOME/.Trash/"

For example, if you wanted to move it to the Desktop instead, use this:

		/bin/mv -n "$TEMPFILE" "$HOME/Desktop/"

Or if you do not want to move it anywhere, just put a '#' at the ***start*** of the line to make it into a comment:

		# /bin/mv -n "$TEMPFILE" "$HOME/.Trash/"

That is all you should have to change, but if you want to use MultiMarkdown Composer you don't have to change the shell script part at all.

### One Last Thing…

The only special instruction to remember is that when you are done using the external editor (MultiMarkdown Composer or whatever) you must ***quit*** the app (after saving, of course). That is because the shell script waits for that app to quit before it knows to continue.

[MultiMarkdown Composer]: http://multimarkdown.com/
[Markdown]: http://daringfireball.net/projects/markdown/.
[MailMate]: http://freron.com/
[Keyboard Maestro]: http://www.keyboardmaestro.com/main/
[MailMate-Edit-in-External-App.kmmacros]: https://raw.github.com/tjluoma/km-mailmate-edit-in-external-editor/master/MailMate-Edit-in-External-App.kmmacros

