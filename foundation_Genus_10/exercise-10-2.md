## Exercise 10-2 - Request
  
####4. Create Object Class «Request» 

In the New Object Domain wizard, remember to set correct Data Interpretations.

*Comment: The SQL script for creating table «Request» has already been run against your database. This is because we wanted to genereate some data in advance for making reports/analysis in later exercises.*
   
   1. Set default value for field «Order No». Select «Custom Id Generator» and «Order No Counter» from the list. Make Subject, State and Type mandatory. Also, agreed Delivery Date and Expected Delivery Date should have Data Interpretation "Date" (not "Date and Time"), as we don't want the user to care about the time of the delivery.
      
      After creating the object class, sett Default values for the «Created» fields and Formula values for the «Modified» fields. Default values for State and Type should also be defined. In addition, set the default value of Received Date to "Now", but let it be possible to change.
      
      *Comment: Default locks the values after creation (i.e. they remain unchanged after creation), while Formula allows the values to be automatically set whenever the Request object is modified.*
   
   2. Open Object Class «Request» (right-click -> Open) and define the following properties:
      - Search (set search properties, under «Search Properties» in tab «Search»).
      - Events -> Auditing (want to log all changes made on Request objects, check «Enable Auditing» in tab «Events»).
      - Display -> Naming (field «Subject» should at least be a part of the naming, in tab «Display»).
      -	Data Sorting (default sorting on «Company» ascending and «Received Date» descending, in tab «Data Sorting»).
  
You have now created the object itself. Next, you will make it possible to drag documents and e-mail into a Request.

####5. Add property "Request" on object classes Mail and Document

*Guidance: Use the following SQL query to create a new column in the Document table:*

```
ALTER TABLE Document
 ADD RequestID uniqueidentifier 
```

*Run the equivalent query against the Mail Table. Add the two fields to their corresponding Object Classes in Studio.*

####6. Create actions «Paste new Mail from file (Request)» and «Paste new Document from file (Request)»

Both actions should take Request as input.

*Guidance: Copy the corresponding Paste-actions for Company, and substitute the data source Company with Request. Make sure that the reference to Request is correctly set on Mail/Document creation (Mail.Request = Request (input) and Document.Request = Request (input)).*

You are now ready to add Request to the interface, i.e. make a Request-form and list Requests under Company. In addition, you will be asked to make a list (table) of Requests that is accessible from the Navigation Pane.

####7. Create a Form for Request

Add commands+events for creating Mail and Documents (by Paste) in the corresponding Grids. Do the same for deletion and opening of e-mail/documents.

*Tip: Add a Tab Sheets container with tabs "General", "Documents" and "Mail" in that respective order. To get a meaningful Ribbon (optional), you should place the commands on the tabs. Remember to give the commands good names and symbols.*
   
####8. Make a "Requests"-tab in the Company-form

Add a list of Requests to the Company-form in a separate Request-tab. Remember to create commands+events for creating new and opening existing requests through the Request-form. It should not be possible to delete Requests. However, the grid should filter out Requests with State="Canceled".

*Comment: Feel free to add the "New" command to the Ribbon. Find a meaningful symbol for Request.*
  
####9. Create a Table for Requests

Model a Request-table with a view that displays all Requests with State="Open". Name the view "Open Requests".

*Guidance: If needed, take a look at the earlier Table exercise. Make sure you include columns, define the Data Filter and enable Search. Under Events, add one "Open a Form" event with menu item = "New" (remember Create Data) and one with menu item = "Open in New Window (remember Data Filter).*
   
####10. Make a View Button in the Navigation Pane

Add a shortcut (name "Requests") to the Navigation Pane that points to the "Open Requests"-table. Remember to define the security of the View Button first, so that the security is inherited by all its elements. Choose a suitable symbol (e.g. 1972).
![oppg9fig3.JPG](media/oppg9fig3.JPG)
  
####11. OPTIONAL: Make a rule "Set Closed Date and Canceled Date when State changed"

This rule should change Closed Date if State is set to "Closed" (and NULL otherwise) and Canceled Date if State is set to "Canceled" (and NULL otherwise).

####12. OPTIONAL: Make actions "Close Request", "Reopen Request" and "Cancel Request"

Force field Request.State to be "Read Only" by changing the Read Only property in the Request form/grid/table, and make actions "Close Request", "Reopen Request" and "Cancel Request" to set the State of a Request. Publish the actions through buttons in the Request-form (e.g. next to State) and in the Company-form (below the grid). Furthermore, add enabling conditions to the buttons, so that "Close Request" is enabled when State="Open", "Re-open Request" is enabled when State="Canceled"/"Closed", and "Cancel Request" is enabled when State="Open".

####13. OPTIONAL: Make Request "read-only" if State <> "Open"

Force all fields in the Request-form to be "Read Only" if State is not equal to "Open".

*Tip: You can determine when a Control is "Read Only" and not by defining conditions in the menu on the left-hand side of the editor. Luckily, you don't have to define one condition per field, you can also do it per Group. Everything placed within the Group will be "Read Only" if the condition is true.*
	
####14. OPTIONAL: Define dynamic labels for tabs "Mail" and "Documents"

Give tabs «Mail» and «Documents» in the Request-form dynamic labels which counts the number of objects listed (e.g. "Mail (3)" and "Documents (1)").

*Guidance: It may be necessary to use the provided solution for aid.*
    
   1. You will need a data source of type Local Object (name: "Labels") in the Request-form. Create two fields "Mail Label" and "Document Label" of Type = Function. For Data Calculation, use Formula (e.g. "Mail  (" + Misc.ifNull(mail.count(),0).toString() + ")"  )
   2. The local object's Data Filter can't be read from the database, but you can set Data Filter = "Create Single Object". This will create a Labels object when the form is opened.
   3. Bind the Label properties of tabs «Documents» and «Mail» to fields «Label Values.Documents Label» and «Label Values.Mail Label», respectively. 

Deploy and verify! Check the naming of the tabs.


<table>
   <tr><td><a href="exercise-10-1.md"><- Previous</a></td><td align="right"><a href="exercise-11-1.md">Next -></a></td></tr>
</table>
