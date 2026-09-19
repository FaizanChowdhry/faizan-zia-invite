# Gmail RSVP Setup for the Wedding Invite

This page is now configured to send RSVP data to a Google Apps Script endpoint. Replace the placeholder in the HTML with your real deployed Apps Script URL before going live.

## 1) Create a Google Apps Script
1. Open https://script.google.com/
2. Create a new project
3. Paste this code:

```javascript
function doPost(e) {
  const payload = JSON.parse(e.postData.contents || '{}');
  const to = 'chowdhary.faizan60@gmail.com';
  const subject = 'Wedding RSVP: Faizan & Zia';
  const body = [
    'Name: ' + (payload.guestName || ''),
    'Attendance: ' + (payload.attendance || ''),
    'Guests: ' + (payload.guests || ''),
    'Message: ' + (payload.message || '')
  ].join('\n');

  GmailApp.sendEmail(to, subject, body);

  return ContentService.createTextOutput(JSON.stringify({ ok: true }));
}
```

4. Save the project and deploy it as a Web App.
5. Set access to Anyone.
6. Copy the deployed Web App URL.

## 2) Update the invitation
In `wedding-invite.html`, replace:

```javascript
const RSVP_ENDPOINT = 'https://script.google.com/macros/s/PASTE_YOUR_DEPLOYED_SCRIPT_ID/exec';
```

with your real deployed URL.

## 3) Publish the page
After this, host the HTML on GitHub Pages or Netlify and test the live URL.

## 4) Test
Submit a sample RSVP from the hosted page and check Gmail inbox.
