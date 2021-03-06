# Firestore for Google Apps Scripts
### A Google Apps Script library for accessing Google Cloud Firestore.

This library allows a user (or service account) to authenticate with Firestore and edit their Firestore database within a Google Apps Script.

Read how this project was started [here](http://grahamearley.website/blog/2017/10/18/firestore-in-google-apps-script.html).

## Installation
In the Google online script editor, select the `Resources` menu item and choose `Libraries...`. In the "Add a library" input box, enter `MX2_NUfxVpaA1XPcZ_N-3wWb_Hp7BVbw3` and click "Add." Choose the most recent version number.


## Quick start with a service account
Follow [these instructions](https://developers.google.com/identity/protocols/OAuth2ServiceAccount#creatinganaccount) (just the "Creating a service account" section) to obtain a service account email address and private key. Ensure you have given the account full read/write access to the `https://www.googleapis.com/auth/datastore` scope.

Now, with your service account email address `email` and private key `privateKey`, we will create a document with a field `name` with value `test!`. You will need your project ID to do this (we'll assume you've stored the ID in a variable called `projectId`).

We encode these fields as a JSON object:
```javascript
const data = {
  "name": "test!"
}
```

Now, we can create a document called `FirstDocument` at a  collection called "FirstCollection":
```javascript
FirestoreApp.createDocumentWithId("FirstCollection", "FirstDocument", data, email, key, projectId)
```

To update the document at this location, we can use the `updateDocument` function:
```javascript
FirestoreApp.updateDocument("FirstCollection/FirstDocument", data, email, key, projectId)
```

**Note:** Although you can call `updateDocument` without using `createDocument` to create the document, any documents in your path will not be created and thus you can only access the document by using the path explicitly.

## Contributions
Contributions are welcome -- send a pull request! This library is a work in progress and currently only supports creating and updating documents with fields (whose values are strings, numbers, booleans, arrays, or objects).
