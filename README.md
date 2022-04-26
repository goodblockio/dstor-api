This repo is the source for documentation regarding using the api for uploads to dStor. 
## dStor API documentation 

04.2022 Folder Upload process
To upload files/folder using new upload process:
1. You should get an upload token. Send a POST request to the `v1/upload/get-token`. The request should:
- have an `Authorization` header provided
- have both `chunks_number` and `folder_path` in its body.
If everything is ok, you'll get the response containing message: 'ok' and token: <upload token>
2. For every chunk you've got (for example, you had 10000 files to upload and you divided them into 100 chunks 100 files each), send a POST request to the `v1/upload/`. The request should:
- be of `multipart/form-data` content-type
- have an `Authorization` header provided
- have a `x-dstor-upload-token` header specified with the token value you've got from 1.
- have its body (in the frontend code, which is React.js code, we use a FormData object) consisting of one or multiple files. Here's the example of what we're doing in the frontend code:
```
const fd = new FormData()
for (const acceptedFile of chunk) {
    fd.append('file', acceptedFile.content, acceptedFile.path)
}
```
It is not required to put your files into the `file` field. You might even use any random field for each file, as we don't use this field name in our backend code for any purpose and process any field in the form data as a file field.

While you're uploading those files, they are saved to the temporary folder. Only after all of your chunks are uploaded (number of upload requests should be the same as you've specified in 1.) files are uploaded to ipfs and their data is saved to the database.  
3. So after you've uploaded all of your chunks you might send requests to get updates about your upload. To do so, send GET requests to the `v1/upload/get-status/`. The request should:
- have an `Authorization` header provided
- have a `x-dstor-upload-token` header specified with the token value you've got from 1.  
As the response you will get an object describing your upload process. If an upload process finishes successfully you get the `DONE` status. If there's an error you get the `ERROR` status with the `errorExplanation` and `errorAtStage` fields filled.
