# Overview
ArchiveIt serves as a wrapper for a database that enables users to view, store, and manage collections from an intuitive frontend.  The database can be either local or remote but must be a MySQL server or equivalent (for example, Azure servers are also compatible for most functions).

## Basic Concepts
The highest level object is an Archive, which is a file containing the necessary connection information and metadata regarding the database that is being connected to.  The program can handle multiple archives, with a connection screen.

Archives contain multiple Collections.  A collection is an object in a database that contains entries as well as important information regarding the Collection that is set by the user.  Examples of this information are Departments, Managers, Contacts, etc.  

Entries are the actual individual objects within a Collection.  Collections can hold as many Entries as allowed by the database service.

## Schema
The schema of the database is designed around individual tables for Collections, with a few other tables allowing for other metadata.  The schemas for the individual tables (for example, the Collection schema) contains some required information followed by whatever user-defined data is entered.

A list of all collections within an Archive is stored in the Collections table.  Each collection must be given a separate name, as it is the primary key.  In addition to the name, some other information is included and automatically filled:

 - ID : A numeric ID that represents the collection, used for enumeration.
 - DateCreated : The date and time that the collection was initialized in the archive.
 - EntryCount : A constantly updated value representing the number of entries currently contained within the collection.

The individual schema of Collections is decided by the user, but contains:

 - ID : A string ID for the Entry.  ID's are a composed of XXXXX-#####, with the X values being the first five values of the MD5 hash for the Collection name, and the five #'s being the number of the entry.  This allows for entries to be searched across all Collections by simply passing in an entry ID.
 - DateCreated : The date and time that the Entry was added to the Collection.
 - EntryDescription : A description of the Entry (maximum 256 characters).