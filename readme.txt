ICDB Selections Mixer

2018-03-29
v1.3

Overall:

	This is an application written in python using the Tkinter module to create a GUI-driven application
	that helps a user create selections lists for the ICDB - an application of the California Historical Resource Information System

Background:
	The ICDB allows a user to save and load 'selection sets' of either Reports (with S-numbers) or Resources (with P-numbers).
	These 'selection sets' are useful for allowing a given set of selected reports or resources to be
	used as a means of handing off to other users, or as input to additional tools that operate on a given set of selections.
	One useful activity is 'map reading', whereby a user is studying a 7.5' or 15' quad map and reading either S-numbers or P-numbers
	off the map - for the purpose of working with them as a set in both the ICDB and in the GIS.

	Thus, this is a tool to allow a user to create and manipulate selection sets of S-numbers and P-numbers

Basic operation:
	The basic concept in the tool is that the user is manipulating a 'current set' of selections.
	This 'current set' is shown in a text box on the left side of the application's main window.
		it displays the list of S-numbers or P-numbers (but *not* both simultaneously), scrolling if necessary
		The 'current set' is always maintained in a sorted and de-duped condition.
		And the 'current set' is tagged internally as being either a list of Reports or a list of Resources - it cannot be *both*
	
	In the right side of the application's main window is a 'log' of the activity the user has done;
	such as adding lists, entering individual values, deleting individual values, saving lists, etc.
	
	Between these 2 windows are some control buttons, a field to enter values and a display of the current number of entries in the 'current set'
		- 'Add List' - prompts the user via a 'standard' windows file dialog box to specify one or more existing saved selections files
			and then it adds all the entires from all files to the current set
			it should be obviouis that Windows does not know about ICDB selection files, so any .xlsx file could be selected.
			the program will examine upon opening each .xlsx file whether or not it is a valid ICDB saved selections file
			and should quietly ignore invalid files (i.e., not crash the app)
		- 'Remove List' - prompts the user for one or more existing saved selections files
			and then opens each one, and removes matching entries from the current set
		- 'Intersect' - prompts the user of one or more saved selections files (i.e. .xlsx files)
			and then removes from the current set all entries that are not in the selected files
			(currently, at v1.3, to be of any use, this requires the current set not be empty; a the intersection of any set with the null set produces the null set)
		- a small text box where the user types in and entry to be added to the current set
			the program tries to be accommodating and not require the presence of the standard "S-" or "P-", but they may be present
			thus, simply typing '123' and pressing the Enter key will assume the user is attempting to add S-000123 to the current set
			or, typing '8-234' and pressing the Enter key will assume the user is intending to add "P-08-000234" to the current set
			upon entering a value, the current set is updated, a line is added to the log window, and the field is cleared for the next entry
		- 'Add Single' - a button that basically performs the same operation as pressing Enter in the above small text box
			
		- 'Del Selected' - a button that will remove the currently selected entries in the list window on the left.
			this button works by finding the currently selected text in the list window, extracting the S-# or P-# values that are selected
			and then removing them from the current set
			Note; this does not work by having the user enter a value in the field and then clicking on this button.
		- the word 'Count' is displayed as a UI heading to the text value below...
		- a numeric value showing the number of entires in the current list
		- 'Clear' - remove all values from the current list
			
	Underneath the log window are 3 buttons to:
		- 'Save Selections' saves the current set to a ICDB compatible saved selections excel file (.xlsx)
		- 'Quit' quit the application (obvious?)
		- 'Save Log' save the text of the log window to a file (.txt)
	
		Saving the log window to a text file is useful when map reading, because...
		... the maps are hard to read and it's not uncommon to mis-read some value.
		Having a log that shows the order you entered values can be useful
			when you find that the S-# or P-# you entered seems to be in a completely separate geography,
			having a list you can use to see where you saw it in your visual map scanning can be useful
			to go back and try to re-read the map; maybe improving your chances of getting the S-# or P-# the second time.
			
Things to consider doing:

make the 'Intersect' button work more intuitively when the current set is empty
	by performing an 'Add' operation on the first filename opened
	and then performing 'Intersect' operations on all subsequent files selected.

maybe allos values to be entered in the small box and then click on 'Delete' to delete the entry from the current list
	this would have to gracefully allow values entered but not found in the current set to be ignored, while adding a line to the log window
	

alternative configuration:
	it could be useful to deploy this app to researchers at the IC who need to provide lists of S-#'s and P-#"s to staff
	for obtaining outputs from the GIS and from the ICDB.
	But the interface would need to be simplified for such usage
	because saving log files, and operating on previous lists (add, remove, intersect) is probably of no interest to researchers.
	my initial thoughts go to having the app read 'command line arguments' to configure how it sets itself up
	and then the same code could present a slightly different interface depending on command line arguments stored in
	the properties of a desktop icon
	
longer term problem:
	map reading often involves reading trinomial values
	but there is no concept in the ICDB of saved selection sets of trinomials


		
