# Outlook Web

## Showing declined meetings or events

* Go to your Calendar.
* Select 'View' followed by 'Calendar settings'.
* Select 'Events and invitations'.
* Under 'Save declined events' check 'Show declined events on your calendar'.

## Checking if you are member of a certain group

You can do it as follows:

* Start a new email
* In the To-field, fill in the group.
* Then you have two options:
  * Click on the plus-sign.  All names in the To-field will be expanded.
  * Rightclick on the group and then select 'Open contact card' which will show you all members.

## Searching

### General info

* Outlook uses what's called prefix matching when searching. So if you type ray into the Search box, Outlook will return messages that contain ray, Ray, Raymond, and rays, but not disarray or tray. Also, the search treats numbers that are connected to words (no spaces between the word and the number) as part of the word. Searching for "365" will NOT find messages that contain "Microsoft365".

* Strings of numbers less than five (or two???) digits are ignored. If you want to search for 98101, entering 9810 will not return any results.  TODO: check this!

### Examples

* To find all mails which have Discrepancy or Questions in the subject line:

  ```text
  subject:Discrepancy OR subject:Questions
  ```

* To search for exact phrases, put things between double quotes:

  ```text
  "bob"
  ```
  
  This will show items containing the exact phrase *bob* and not the variations such as *bobby* or *bobbin*.

### References

* [How to search in Outlook](https://support.microsoft.com/en-us/office/how-to-search-in-outlook-d824d1e9-a255-4c8a-8553-276fb895a8da)
