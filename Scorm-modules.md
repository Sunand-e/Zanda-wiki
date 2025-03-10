The SCORM functionality of the platform uses three main concepts:

*   **Scorm Packages** - the files generated by the SCORM authoring tool (e.g. Articulate Rise).
*   **Scorm Modules** - the content item which contains a SCORM package, and allows for tracking of overall progress and score of a SCORM package. The SCORM package belonging to a scorm module can be replaced.
*   **Sco Attempts** - the model which stores the CMI data for a user's attempt of a scorm package.

**Note:** There is an additional model which is currently unused, `ScormSco`. This was generated due to the fact that SCORM packages can sometimes contain more than one 'SCO'. For more information on this, see: [https://scorm.com/scorm-explained/technical-scorm/run-time/](https://scorm.com/scorm-explained/technical-scorm/run-time/)

### How it works

The platform supports both Articulate Rise and Storyline SCORM packages. The zip files are uploaded via the `upload_scorm` method of the `UploadsController`, and saved in the `ScormPackage` model. SCORM attempts are saved in the `ScoAttempt` model. Each time the SCORM package changes the CMI data on the frontend (when the user is interacting with the SCORM package), the whole CMI object is posted to the rails app via the `upsertScoAttempt` graphql mutation, and the existing saved data is overwritten with this for the user's current attempt. When a user loads a SCORM module, the system will use graphQL to retrieve the latest ScoAttempt data for the user, if one exists.