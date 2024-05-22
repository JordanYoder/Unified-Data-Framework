# Unified-Data-Framework

## Purpose
This Unified Data Framework is to, as closely as possible align, the common data across Engage's clients. Common fields 
will include identifying information (i.e., Finder Number, Keycode, etc) as well as customer data (i.e., name, address, 
employee, etc).

Clients will have fields that are not common between them. These will be recorded for the client but aren't necessarily 
a field we are interested in tracking as a whole.


## Structure
We are transitioning having each client's dataset being in their own silo to instead have a common bucket that contains 
all the client data. Instead of breaking data up into clients, instead data will be broken up into functionalities. For 
example every client has certain clearly defined functionality.

### Staging Data
Previously known as Data Entry. This is where the data is 'staged', a temporary state where we have taken the keyed 
data and perform automated transformations to the data. In addition to any changes made programmatically a user will 
provide additional changes depending on the client, this may be include something such as adding flags or verifying the 
populated data for the customer matches the signature on the check. When complete the data is moved to the Committed 
Data database.

This is also where the daily export files and reports are generated from to send to clients.

### Batch Data
Batch data is a way to track the data in any given import. Tracked data includes overviews of records, amount, various 
dates (such as date imported, the Remit Run Date, etc), and additional information.


### Committed Data
Formerly known as Archives. This is where data that has been staged is moved to for 'storage'. Upon client request we 
can pull this data to send to them again. Any large analsysis of data, either a single client or all clients, would be 
performed on this dataset.

This database will hold the bulk of the data we collect.


### Export Layouts
Exports Layouts is a table that holds the 'layout' for each client's spreadsheet. The translates what we call a field 
to what a client calls this field. When we create a spreadsheet in Staging Data for a client we actually import the 
data from that database to this database. The Import Script step will map our fieldnames to what the client wants to 
use as a header for their data. Each import for a client will erase the data previously held there and import the new 
dataset.

Some clients may have multiple layouts. Each of these layouts will be a table in the Export Layouts database named 
sequentiall as ClientCode_Export1, ClientCode_Export2, etc.


### Flag Data
Clients tend to have different flags. This database will hold each client's flagcode and flagdescription.


### Finder Data
While we have moved a majority of clients finder data to SQL Server, there are still some that are unable to be 
moved from FileMaker Finder files. Ideally we will consolidate all the finder data to the Finder Data database, though 
there may be exceptions for very large files.