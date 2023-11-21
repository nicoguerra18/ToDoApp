# To-Do List Web Application
Use cases:
- use#105	update button binding	if the user checks the 'is complete' checkbox the update button disappears from the tuple
- use#106	added tuple display	the new tuple added will display the provided entries from the dialog including the task, description, deadline, and priority as formatted and 
  shown on the preview
- use#107	successful update	if the user clicks update on the dialog and the dialog is valid and the tuple is updated properly a success toaster will display saying that the 
  task was updated successfully
- use#108	successful delete	if the user clicks the delete button on the tuple the tuple will be deleted from the table and a success toaster will display saying that the task 
  was deleted successfully
- use#109	dialog reusability	the task dialog must be a component of its own separate from the page component and be triggered and recycled from the update and add button
- use#110	successful add	if user clicks add button and all entries are filled out properly the dialog will close and a new tuple is added to the table with all fields 
  formatted like shown on the preview of the instruction sheet and a success toaster will display saying that the task was added successfully
- use#111	is complete checkbox	the new tuple will display a checkbox under the 'is complete' column that is not checked by default
- use#112	empty validation	the title and description textboxes must validate for empty entries and if empty, the textbox will turn red and display a small error message underneath the textbox
- use#113	date picker	the date picker must display a calender when clicked just like on the preview allowing the user to pick any day of the year and display in the format 
  mm/dd/yyyy
- use#114	update/delete button	the new tuple will display an update and delete button under the action column
- use#115	update dialog	if the user clicks the 'update' button on a tuple, the task dialog appears updating the title from 'add task' to 'edit task' and changing the icon from 
  a plus icon to an edit icon as shown on the preview, populating all the provided fields from the tuple selected and hiding the title textbox (this is because titles should 
  not be editable after they are created because of distinction)
- use#116	validation return	if user clicks add button but the form is not valid i.e. the title or description textboxes are empty, or the title is not unique, or the deadline 
  is not selected, or the priority radio is not selected, the dialog stays open and the textbox that is invalid shows the error accordingly
- use#117	radio button	the priority radio button must allow user to mutually exclusively select between low med and high
- use#118	cancel button	if user clicks the cancel button the dialog closes and the to do table does not change
- use#119	notifications	all notifications must look like a toaster and be on the lower right side of the app to avoid covering the buttons on top
- use#120	distinct validation	the title textbox must also be unique from the existing titles added to the table and if the title is not unique then the textbox will turn red 
  and display a small error message underneath the textbox
- use#121	banner bar	page has an upper banner with a title labeled 'FRAMEWORKS' and on the right side of the banner there is an add button with an add icon to the left side of 
  the label as shown on the preview in the instruction sheet
- use#122	add dialog	when user clicks the add button, a dialog prompts with a header that contains a title 'add task', a body that contains a title textbox, a description 
  textbox, a deadline date picker, a priority radio button, and a footer that contains an 'add' and 'cancel' button with icons in front of each of those buttons (the radio 
  button and date picker can be pre-populated as shown on the preview but not required)
- use#124	tools	application uses an SPA framework like React, Vue, Angular and a materials library like MUI, Vuetify, Bootstrap 5

#Screenshots

<img width="871" alt="Screenshot 2023-11-21 at 11 05 54 AM" src="https://github.com/nicoguerra18/ToDoApp/assets/139820627/cd1b11b5-8c0a-458c-8ca2-d233777afc1e">

<img width="869" alt="Screenshot 2023-11-21 at 11 11 14 AM" src="https://github.com/nicoguerra18/ToDoApp/assets/139820627/0c2775f5-c0a6-4cf0-8696-8a5a034171ba">

<img width="864" alt="Screenshot 2023-11-21 at 11 11 26 AM" src="https://github.com/nicoguerra18/ToDoApp/assets/139820627/74528355-a74f-4a57-9bf5-e54909949449">

<img width="864" alt="Screenshot 2023-11-21 at 11 06 38 AM" src="https://github.com/nicoguerra18/ToDoApp/assets/139820627/18c09372-a371-4273-88cf-5e8affa5ba26">

<img width="867" alt="Screenshot 2023-11-21 at 11 06 20 AM" src="https://github.com/nicoguerra18/ToDoApp/assets/139820627/3c037449-0c7d-433a-b69f-6f0bc6d12322">
