# SOCsheets
I have a google script(in google sheets) that lets me email one selected row. But now I want to email multiple, different rows in one email. Can it be done? 

function sendEmail() {
  // define a couple constants for the function
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const ui = SpreadsheetApp.getUi();

  // Make sure the selected row has text
  if(sheet.getActiveCell().isBlank()) {
    ui.alert("Please select a row ");
    return;
  }
  
for(i = 0; i <3; i++){
   
  // if valid, get the correct row of data.
    var row = sheet.getActiveCell().getRow();

  // get the range for that row
    var rowRange = sheet.getRange(row, 1, 1, 10).getValues();

  // Build the object to use in MailApp
    var cameraIp = rowRange[0][0];
    var up = rowRange[0][1];
    var down = rowRange[0][2];
    var permenetlyDown = rowRange[0][3];
    var recording = rowRange[0][4];
    var issue = rowRange[0][5];
    var socComments = rowRange[0][6];
    var time = rowRange[0][7];
    var itComment = rowRange[0][8];
    
   

    var msg = "Camera Name: " + cameraIp + "\nCamera is Up : " + up + "\nCamera is down : " + down +   "\nPermanently Down :  " + permenetlyDown +   "\nRcording :  " + recording+  "\nIssue :  " + issue +
     "\nSOC Comments :  " + socComments + "\nTime : " + time + "\nIT Comments :  " + itComment  ;
      

  // Here for popup message only
    ui.alert(msg, ui.ButtonSet.OK)

 
 

    // MailApp.sendEmail(address, subj, body);
MailApp.sendEmail({
    to:  "my.vo@jaxport.com" ,
    subject: "My's Super Camera Report",
    body :  msg,
})
}
    
}
