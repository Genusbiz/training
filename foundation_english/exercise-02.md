# Introduction to modeling
The first part of these exercises will concern the creation of new object classes. A Genus application delivered to a customer will typically support all or parts of its business model. For instance, an application model may cover a large part of an employment agency's business model by supporting case management, reporting, document archiving, communication (e-mail/SMS) and integration towards external systems. Some clients may focus heavily on the reporting part of the business, while others have their main focus on data search.

Common to all application models - whether this is full-scaled case management solutions, Business Intelligence solutions (corporate governance with focus on reports and analysis) or technical integration solutions - they all have an object model.
An object model is simply the business objects of the customer, inter-connected. The object model often corresponds to the model in the database, but is also modelled/reflected in Genus Apps, and can have additional logical connections, information and even object classes that doesn't exist in the database. The advantage of creating the object model in Genus Apps, is that Genus Apps maintains connections, dependencies, primary keys, data consistency, data types, creation, modification and deletion of data. Deletion rules, duplication rules, validation rules, automatic rules (equivalent to "triggers" in the computer language) can all be controlled in Genus Apps.

The object model is exposed to the end user through tables or "forms", combined with actions, searches and other functionality, in the Genus Desktop client (exercise 1). The developer sets up the object model, the logic of actions, the search properties and the GUI using Genus Studio, which you now will get to know even better.

In Genus Studio, we refer to an object (e.g. Company) as an «Object Class». The properties of the object (e.g. "Name" or "Org No") are called «Object Class Property» or just «Property».
The proposed Genus CRM solution has a simple object model outlined in the Case-description. What is missing in your EDU-solution is Contact, Contact Log, Document and Request. Initially, you will have to expand the object model with Contact and Contact Log.

 
Fig.1.1.: The initial version of the Genus CRM object model. Click on «Object Class Diagram» in the menu on the left to open the diagram. Here we see 5 Object Classes, each with several Object Class Properties. 
NOTE: A diagram is just a drawing board where it is possible to visualize a selection of objects in the solution (all existing objects are listet under «Object Classes»). Here you will automatically see the object relations. If you delete an object from the diagram, it will only disappear from this particular view. The object itself is not deleted from the solution.


##Exercise 2
Your first task will be to model/create Object Class "Contact" with all its required and essential Object Class Properties. To construct an Object Class in Genus Studio, an equivalent table that the object class can refer to must exist in the database.

There are two ways of making new Object Classes: 

- **Alt 1:** If you have experience with SQL, you can write a SQL statement from scratch to create the database tables and columns directly in SQL Server Management Studio. By referencing these tables, you can build the objects (Object Class/Object Class Properties) in Genus Studio.
- **Alt 2:** You wish to make a draft of the object in Genus Studio first, and then get the needed SQL statements generated. For this you will have to use the Object Class Diagram view. Here you can generate «Draft» Object Classes and «Draft» Object Class Properties that don't exist in the database yet. This feature can be very useful when you are in an object model design-phase, and want the model to be QAed before the tables are actually created in the database. It is easier to modify Draft-objects in Genus Studio than tables after they have been created and associated with Object Classes. If you want to add or remove an attribute/field, the latter requires changes in 2 places; both in the database and in Genus Studio.

In the first exercise, you will use alternative 2 to get familiar with this option. However, in later exercises, you will create tables with alternative 1 (first make tables and/or columns in the database, secondly model the objects in Genus Studio).

1. Create a Draft Object Class for «Contact».
   *Guidance: Navigate to «Object Class Diagram». Right-click -> Insert -> Class (Draft). In the dialog box that pops up, you'll set the Logical Name equal to the object in Genus ("Contact") and the Physical Name equal to the name of the table that is to be made in the database ("Contact").*
  ![oppg2fig2.JPG](media/oppg2fig2.JPG)
 
   The drafted object «Contact» is now made. Notice that the new object is gray-colored unlike the Object Classes that were already there. A property named «ID» is auto-generated for the object, and is the primary key of the table / object.
   
2. Add the following Properties to Contact:
   1. FirstName (varchar(60))
   2. LastName (varchar(60))
   3. Company (Outbound reference to object “Company”)
   4. Mail (varchar(120))
   5. Mobile (varchar(20))
   6. Position (varchar(100))
   7. State (Outbound reference to object / code domain “Object State”. This is an internal code domain consisting of «Active» and «Inactive»)
   8. Created Date (datetime)
   9. Created By (Outbound reference to object «User»)
   10. Modified Date (datetime)
   11. Modified By (Outbound reference to object «User»)

*Guidance: Add Object Class Properties to the draft object by right-clicking it:*

   «Contact» -> Insert -> Property (Draft) (or CTRL -Shift - +). 
  
References to other classes can easily be made by pressing the Alt-key while selecting an object and dragging it into the drafted Object Class. If you do that, you will automatically get an outbound reference with correct data type set for you.

  ![oppg2fig3.JPG](media/oppg2fig3.JPG)
  ![oppg2fig4.JPG](media/oppg2fig4.JPG)

When you add a new draft Property, you define its Logical Name (the name of the field in Genus CRM), Physical Name (the name of the field in the database), Outbound reference (the object that the field is pointing at, e.g. «Company») and Data type (e.g. «varchar(120)» for text where 120 is the number of characters, «int» for integer, uniqueidentifier for primary keys or ID-reference, and so on. The data type is set automatically if you choose an Outbound Reference). Press OK.

Best Practice when it comes to naming a database column (Physical Name) is to use the "camel cased" version of the Logical Name. E.g. a field with Logical Name «First Name» should be «FirstName» in the database (Physical Name). The exception is references to other objects. The property "Company" should have Physical Name "CompanyID" to indicate that the field is refering to another object's ID.

3. Open the «Actions» menu (at the top), and push «Forward Engineering». Select object «Contact» and click Next twice. This will generate a SQL script that can be used to create the «Contact»-table in the database. Copy the scrupt and run it in SQL Server Management Studio against the database (GenusCRM_EDUXY_Data).

You have now made the table «Contact» in the database, and will soon model the associated Object Class for Contact in Genus.

Once again, we emphasize that you don't have to build Draft object classes, but that it can be a good thing whenever you want to verify the object model against others (internally / customers) before creating tables in the database and modeling actual object classes. It is easier to change a drafted object model than an actual object model. We always use a fairly large portion of time on the object model when we design business applications, since it is a well known fact that changes made on an application's "data layer" is more costly once GUI and logic has been added.

4. Build object class «Contact» in Studio.
  *Guidance: Navigate to Object Classes in Studio (left pane) and right-click -> New -> Object Domain. Go through the wizard.*
   1. First step: Select the database from which the table will be read (it will be set by default if there is only one database, but an application in Genus might have tables in several databases).
   2. Second step: Select the table you will be modeling («Contact»). Here you have the oportunity to override the object's name as shown in Genus CRM (e.g. if the table has a technical name).
   3. Step «Table columns»: Choose which columns you want to model. By default, all of them are selected. Click on Next.
   4. Step «Primary key»: Select property «Contact ID» and check the «generate identifier automatically». The latter allows Genus to handle uniqueness and the creation of primary keys.
   5. Step «Property definitions»: Double-click on each row/propery to verify, and change if needed, the data type and data interpretation. It is important that Data interpretation is changed wherever needed. For instance, the field «Created by» is supposed to be a reference to the object «User». Genus will not be able to figure this out unless you specify it yourself. Double-click on the row and change the data interpretation to «User» (when you do this, the Display name is also changed to "User". Call it "Created by" instead). Repeat the process for properties Company (interpretation «Company»), State (interpretation «Object State»), Modified By (interpretation «User») og Mail (interpretation «E-mail»). The latter will give you free validation of e-mail addresses, as the E-mail object is built in object in Genus.
   6. Step «Naming»: This is the attribute that sets the standard naming of the object. Here you can press Add.. and add First Name and Last Name. Click on Finish.

If you expand the node «Object Classes» in Studio, you should now see the Contact-object. If you expand Contact further and click on Properties, you will find the list of Object Class Properties belonging to Contact.

5. Modify the following settings on the Properties of Contact (double-click on a Property):
   1. Company, First Name and Last Name: Tab «Data Validation», uncheck «Allow blank value». In other words, the fields become mandatory.
   2. Created Date:
      1. Tab «Security», check «Read». The field becomes Read Only for the end user.
      2. Tab «Data Calculation»: Set Default = Time Stamp. The value of the field is set to the server's current time when the Contact object is created, and cannot be edited later.
   3. Created By: Add the same Security as Created Date, but set default value to «Active User Account Stamp». The value of the field is set to the logged in user that creates the object, and cannot be editet later.
   4. Modified Date:
      1. Tab «Security», check «Read».
      2. Tab «Data Calculation», set Formula = Time Stamp. Formulas are updated everytime an object is changed. In other words, Modified Date is updated automatically everytime a user saves a change made on a Contact.
   5. Modified By: Same Security as Modified Date, but set Formula = Active User Account Stamp. The value of the field is set to the logged in user everytime a change on a Contact is saved.
   6. State: Tab «Data Calculation»: Set Default = Active. The state of the Contact is set to Active when it is created. The state can be changed later. Note also that the field is of Data Type int. The state is stored in the database as an integer, but is mapped to the Code Domain in Genus called «Object State», which translates 1 to «Active» and 2 to «Inactive». You will be able to see this by right-clicking the object class «Object State» -> Open -> Data Entries.
   7. Mail: We want this field to be blank, but at the same time we want a message - "field should have value" - to be shown when it is.
      1. Tab «Data Validations», click «Add»
      2. Legg til en Condition «Contact.Mail has no value»
	  2. Add a Condition «Contact.Mail has no value».
      3. Check Impact = "Notify user and ask for confirmation for proceed" and "Notification Message" (type in a suitable response, e.g. "Mail should be set" or something similar).

The object «Contact» is now almost done. The last step is to assign a few properties to the object class «Contact» itself.

6. Right-click on Object Class «Contact» -> Open.
   1. Tab «Events»: Check "Enable auditing" and then "Mandatory" on "Modify". Press Apply. This allows the user to right-click on a Contact in the client to look at its change history (which user has done what). 
   2. Tab «Data Sorting»: Click Add.. and select First Name and Last Name. This will by default sort Contacts automatically by their first name and last name wherever Contacts are listed (e.g. tables, grids) without any sorting specified.
   3. Tab «Data Filtering»: Under "Auto Complete", click Add.. and select First Name, Last Name and Mail. This allows the user to type in a part of a Contact's first name, last name or e-mail in any field of type Contact, and hit Tab to lookup contact persons that match the written text.
   4. Tab «Data Integrity»: Click on Change under "Uniqueness Constraint", and then Add. In the window that opens you can set uniqueness requirements for the creation of contacts. Here you can for example say that "if e-mail has a value", check if another contact person with the same e-mail exists, and if so, qive a warning to the user.

    *Guidance: See screenshot below*
    ![oppg2fig5.JPG](media/oppg2fig5.JPG)
 
   This is where you meet Genus' "Condition editor" for the first time. It is used everytime you want to conditionalize something. In this case it will generate a SQL query that checks (prior to saving) whether a Contact in the database has the same e-mail address as the one you want to store, or not. If the query returns true, the user will get a warning. Notice that we have allowed the user to store the Contact nevertheless, as the "Notify user and ask for confimation to proceed"-box has been checked. By selecting the option above, however, you will deny users to store Contacts with identical e-mail addresses. 
   5. Tab «Search»: In the Search Properties section, click Modify and add the properties that you want to be searchable (at least Company, First Name and Last Name). This is where you define which properties should be visible in the search panel at the top of the client when you want to find certain Contacts.
   
  **Click OK.** The object «Contact» is now complete and ready to be included in the interace (and optionally get additional functionality).

Note that you can go back and modify the properties of an Object Class/Object Class Property at any time, with a few exceptions (e.g. Data Interpretation of an Object Class Property; if you want to change this, you will have to delete the property and add it again). You can obviously also add new Object Class Properties to an Object Class after creation (e.g. you want to add Photo to Contact). Then you will have to run the wizard «Add object class properties», which is available in Studio by right-clicking on an Object Class. Remember to expand the table in the database first.

7. We just realized that we forgot to add a field Responsible (user) to Contact.
   1. Create a new field called Responsible on Contact.
   *Guidance: A column must be added to the database first. Do this by running the SQL statement «alter table Contact add ResponsibleUserID uniqueidentifier». Navigate to object class «Contact» -> Right-click -> «Add Object Class Properties..». Click Next in the first dialog window. In the second, Genus reads all columns from the table that has not modelled yet. Click Next. Under «Property Definitions», double-click on the row and change the Data Interpretation to «User» (make sure you change the Display Name to «Responsible» afterwards). Click OK and Finish.*
   2. Set Default value of Responsible to «User (User Account)» (Active User Account).
*Guidance: Note that this is not the same as «Active User Account Stamp». «Active User Account Stamp», like «Time Stamp», means that the default value is set server-side, and can hence not be changed from the client. Choose instead F3 (see screenshot below) and pick «User (User Account)» which corresponds to the logged in user on the client.

  ![oppg2fig6.JPG](media/oppg2fig6.JPG)
 

8. The Draft-object that you made in Exercise 2.2 is no longer needed. Navigate to Object Class Diagram -> Right-click on Draft-object «Contact» -> «Replace Draft». In the dialog box, select object class «Contact». This will remove the Draft-object from the view and replaced it with modeled object class «Contact».