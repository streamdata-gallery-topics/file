---
swagger: "2.0"
x-collection-name: Box
x-complete: 0
info:
  title: Box Get File's Comments
  description: Retrieves the comments on a particular file, if any exist.
  version: 1.0.0
host: api.box.com
basePath: /2.0
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /files/{FILE_ID}:
    get:
      summary: Get File's Info, Get Embed Link
      description: Used to retrieve the metadata about a file.
      operationId: getFile
      x-api-path-slug: filesfile-id-get
      parameters:
      - in: query
        name: fields
        description: Attribute(s) to include in the response
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
    put:
      summary: Update File Info, Lock and Unlock, Create Shared Link
      description: |-
        Used to update individual or multiple fields in the file object, including renaming the file, changing its description, and creating a shared link for the file. To move a file, change the ID of its parent folder. An optional If-Match header can be included to prevent race conditions.

        To lock and unlock files, you execute a PUT operation on the /files/{file id} endpoint and set or clear the lock properties on the file.

        Used to create a shared link for this particular file. Please see here for more information on the permissions available for shared links. In order to get default shared link status, set it to an empty access level, i.e. {"shared_link": {}}. In order to disable a shared link, send this same type of PUT request with the value of shared_link set to null, i.e. {"shared_link": null}
      operationId: updateFileInfo
      x-api-path-slug: filesfile-id-put
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: path
        name: FILE_ID
      - in: header
        name: If-Match
        description: The etag of the file can be included as an ???If-Match??? header
          to prevent race conditions
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
    delete:
      summary: Delete File
      description: Discards a file to the trash. The etag of the file can be included
        as an ???If-Match??? header to prevent race conditions.
      operationId: deleteFile
      x-api-path-slug: filesfile-id-delete
      parameters:
      - in: path
        name: FILE_ID
      - in: header
        name: If-Match
        description: The etag of the file
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
    post:
      summary: Restore Item
      description: Restores an item that has been moved to the trash. Default behavior
        is to restore the item to the folder it was in before it was moved to the
        trash. If that parent folder no longer exists or if there is now an item with
        the same name in that parent folder, the new parent folder and/or new name
        will need to be included in the request.
      operationId: restoreTrashedFile
      x-api-path-slug: filesfile-id-post
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
  /files/{FILE_ID}/content:
    get:
      summary: Download File
      description: Retrieves the actual data of the file. An optional version parameter
        can be set to download a previous version of the file.
      operationId: getFileContent
      x-api-path-slug: filesfile-idcontent-get
      parameters:
      - in: header
        name: BoxApi
        description: The shared link for this item
      - in: path
        name: FILE_ID
      - in: header
        name: Range
        description: The range value in bytes
      - in: query
        name: version
        description: The ID specific version of this file to download
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Content
  /files/{FILE_ID}/versions:
    get:
      summary: View Versions
      description: If there are previous versions of this file, this method can be
        used to retrieve information about the older versions. (Versions are only
        tracked for Box users with premium accounts.)
      operationId: getFileVersions
      x-api-path-slug: filesfile-idversions-get
      parameters:
      - in: query
        name: fields
        description: Attribute(s) to include in the response
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Versions
  /files/{FILE_ID}/versions/current:
    post:
      summary: Promote Version
      description: If there are previous versions of this file, this method can be
        used to promote one of the older versions to the top of the stack. This actually
        mints a copy of the old version and puts it on the top of the versions stack.
        The file will have the exact same contents, the same SHA1/etag, and the same
        name as the original. Other properties such as comments do not get updated
        to their former values.
      operationId: promotoeFileVersion
      x-api-path-slug: filesfile-idversionscurrent-post
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Versions
      - Current
  /files/{FILE_ID}/versions/{VERSION_ID}:
    delete:
      summary: Delete Old Version
      description: Discards a specific file version to the trash. (Depending on the
        enterprise settings for this user, the item will either be actually deleted
        from Box or moved to the trash.)
      operationId: deleteFileVersion
      x-api-path-slug: filesfile-idversionsversion-id-delete
      parameters:
      - in: path
        name: FILE_ID
      - in: header
        name: If-Match
        description: The etag of the file
      - in: path
        name: VERSION_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Versions
      - Version
  /files/{FILE_ID}/copy:
    post:
      summary: Copy File
      description: Used to create a copy of a file in another folder. The original
        version of the file will not be altered.
      operationId: copyFile
      x-api-path-slug: filesfile-idcopy-post
      parameters:
      - in: body
        name: body
        schema:
          $ref: '#/definitions/holder'
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Copy
  /files/{FILE_ID}/thumbnail.{EXTENSION}:
    get:
      summary: Get Thumbnail
      description: Retrieves a thumbnail, or smaller image representation, of this
        file. Sizes of 32x32,64x64, 128x128, and 256x256 can be returned in the .png
        format and sizes of 32x32, 94x94, 160x160, and 320x320 can be returned in
        the .jpg format. Thumbnails can be generated for the image and video file
        formats listed here.
      operationId: getFileThumbnail
      x-api-path-slug: filesfile-idthumbnail-extension-get
      parameters:
      - in: path
        name: EXTENSION
        description: The preview format, e
      - in: path
        name: FILE_ID
      - in: query
        name: max_height
        description: The maximum height of the thumbnail
      - in: query
        name: max_width
        description: The maximum width of the thumbnail
      - in: query
        name: min_height
        description: The minimum height of the thumbnail
      - in: query
        name: min_width
        description: The minimum width of the thumbnail
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Thumbnail.
      - Extension
  /files/{FILE_ID}/trash:
    get:
      summary: Get Trashed File
      description: Retrieves an item that has been moved to the trash.
      operationId: getTrashedFile
      x-api-path-slug: filesfile-idtrash-get
      parameters:
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Trash
    delete:
      summary: Permanently Delete
      description: Permanently deletes an item that is in the trash. The item will
        no longer exist in Box. This action cannot be undone.
      operationId: deleteTrashedFile
      x-api-path-slug: filesfile-idtrash-delete
      parameters:
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Trash
  /files/{FILE_ID}/comments:
    get:
      summary: Get File's Comments
      description: Retrieves the comments on a particular file, if any exist.
      operationId: getFileComments
      x-api-path-slug: filesfile-idcomments-get
      parameters:
      - in: query
        name: fields
        description: Attribute(s) to include in the response
      - in: path
        name: FILE_ID
      responses:
        200:
          description: OK
      tags:
      - Documents
      - Files
      - File
      - ""
      - Comments
x-streamrank:
  polling_total_time_average: 0
  polling_size_download_average: 0
  streaming_total_time_average: 0
  streaming_size_download_average: 0
  change_yes: 0
  change_no: 0
  time_percentage: 0
  size_percentage: 0
  change_percentage: 0
  last_run: ""
  days_run: 0
  minute_run: 0
---