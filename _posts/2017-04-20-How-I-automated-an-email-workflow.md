---
layout: post
title: Automating an email management system
subtitle: How to stop doing boring tasks at work, sit back and relax
---

When I started my job in the Committee on World Food Security, at FAO, I was asked to maintain the very convoluted mailing list system they had. It was all over the place and in text format (sic!). Even when moved to a more manageable Excel format, I was spending 5-7 hours at week working on it - not exactly the most exciting part of my job. So I decided that I had to do something about it!

First, I listed all the perks of our mailing lists:

* The mailing list was comprised of two sub-groups. 
    * In the first group there are participants of open meetings the Committee organizes and should receive meeting notifications for just a handle of workstreams they follow. Anyone can subscribe to these meeting notifications. 
    *  The second group is our 'executive board'. They get special notifications plus open meeting notifications. You get on the list only if you're appointed as a member!
* Most people in our lists works in embassies or international organizations and in these places people come and go. This is why we take attendance lists, so we're always updated on who's following what.
* Different people in my team send emails to these mailing lists using our corporate email on Outlook.

At this point I knew what features I wanted:
* A system as simple as possible, so that my teammates do not struggle when sending an email.
* People should be able to sign up by themselves to a mailing list, but we should get a notification if someone tries to signup to the 'special' subgroup.
* Recording the attendance during meeting should be easy

The breakthrough arrived when I discovered that I could do all the above with Google Sheets, Forms and a bit of Javascript scripting. Now, I know that out there there must be wonderful ready-made email marketing software that would do the job more efficiently, but I had zero budget and I wanted to keep the stack as simple as possible for my teammates' sake. Besides, what would be the fun in it?

So, here's what I did instead: 
1) First, import all old mailing list into a master spreadsheet, along with indication on their group of appartenence. I ended up with something like this:

| Name  | Email             | Group  |
|-------|-------------------|--------|
| John  | john@example.com  | GroupA |
| Jane  | jane@example.com  | GroupB |

2) Then I created a sign up form with Google Forms for all groups, to be imported in the master spreadsheet. You can collect the answers from a Google Form by creating the form inside a spreadsheet and import into the master spreadsheet using the ```IMPORTRANGE()``` function.

3) The third step was to divide the master spreadsheet in single thematic lists. The general formula to do this is 
```
=SORT(QUERY(IMPORTRANGE("sheet_id", "Column range"), "query")),1, true)
```

Google Sheets has its own query language, which is actually very easy to learn being very similar to spoken English. A sample query I used is 
```
select Col3 where Col4 contains 'GroupA' or select Col3 where Col4 contains 'GroupB' 
```

At this point I had the basic functionality implemented, but I wanted also to implement a function to remove people if they wished to do so and receive notification whenever someone subscribed to our 'special group'.

Removing people from the list was the hardest part, but I ended up adding one option to the sign-up form - "Delete me" - and inserted this script in all spreadsheet handling Forms.

```javascript 
/*
Google App Script function to remove all rows matching a criteria in Google Sheets with Google Apps Script
*/

function upForDeletion() {

    var sheet = SpreadsheetApp.getActiveSheet(); // Sheet type
    var data = sheet.getDataRange().getValues(); // Range type

    var delMe = "Unsubscribe me from all CFS communications";

    // Creates an array and appends all emails marked as to delete
    var toDelete = new Array();

    for (var i = 0; i < data.length; i++) {
        if (data[i][3] == delMe) {
            toDelete.push(data[i][2]);
        }
    }

    // Remove all rows that contains the emails listed in toDelete
   for(var j = data.length-1; j >=0; j-- ) {
        for (var k = 0; k < toDelete.length; k++) {
            if(data[j][2] == toDelete[k]){
              sheet.deleteRow(j + 1);
            } 
        }
    }
}
```

This script runs every couple of hours, so the list is regularly cleaned. 

For the notification, I ended up using an add-on for Google Forms, [Email Notifications from Forms](https://chrome.google.com/webstore/detail/email-notifications-for-f/acknfdkglemcidajjmehljifccmflhkm?hl=en), which does exactly what I wanted: it sends me an email notification with the details of people who signed up to our 'special group' mailing list.

As a last touch, we ordered a couple of tablets to get emails during meeting. These emails are again sorted and imported into the various thematic mailing lists, ensuring that the lists are always updated all the time. 

Voilà! A simple (and hackish) email management system, at zero budget, and super-easy to use :) 