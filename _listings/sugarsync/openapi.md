swagger: "2.0"
x-collection-name: SugarSync
x-complete: 1
info:
  title: SugarSync  API
  description: the-sugarsync-service-presents-a-set-of-resources-that-your-application-can-access-through-the-platform-api--
  version: "1"
host: api.sugarsync.com
basePath: /
schemes:
- http
produces:
- application/json
consumes:
- application/json
paths:
  /file:
    get:
      summary: Retrieving File Data
      description: To retrieve file data, an application submits an HTTP GET request
        to then          file data resource that represents the data for the file.
      operationId: retrieving-file-data
      x-api-path-slug: file-get
      responses:
        200:
          description: OK
      tags:
      - File
    put:
      summary: Uploading File Data
      description: An application can upload data to a file by issuing an HTTP PUT
        request to thenfile data resource that represents the data for the file.n
      operationId: uploading-file-data
      x-api-path-slug: file-put
      responses:
        200:
          description: OK
      tags:
      - File
  /file/:
    delete:
      summary: Deleting a File
      description: An application can permanently delete a file by issuing an HTTP
        DELETE request to the URL of thenfile resource.nIts a good idea to precede
        DELETE requests like this with a caution note in your applications user interface.n
      operationId: deleting-a-file
      x-api-path-slug: file-delete
      responses:
        200:
          description: OK
      tags:
      - File
    get:
      summary: Retrieving File Information
      description: To retrieve information about a file, an application submits an
        HTTP GET request to then          file resource that represents the file.
      operationId: retrieving-file-information
      x-api-path-slug: file-get
      responses:
        200:
          description: OK
      tags:
      - File
    post:
      summary: Creating a New File Version
      description: nAn application can create a new version of a file by submitting
        an HTTP POST request to the URL that represents the version history. The version
        history URL is returned in the &lt;versions&gt; element whenn retrieving information
        about a file.n
      operationId: creating-a-new-file-version
      x-api-path-slug: file-post
      responses:
        200:
          description: OK
      tags:
      - File
    put:
      summary: Updating File Information
      description: An application can update various attributes of a file by issuing
        an HTTP PUT request to the URL thatnrepresents the file resource. In addition,
        the app needs to provide as input, XML that identifies the new attribute values
        for the file. Upon receiving the PUT request, the SugarSync service examines
        the input and updates any of the attributes that have been modified.
      operationId: updating-file-information
      x-api-path-slug: file-put
      parameters:
      - in: header
        name: Authorization
        description: The access token
      - in: header
        name: Content-Length
        description: The length of the request body
      - in: header
        name: Content-Type
        description: The content type and character encoding of the response
      - in: header
        name: Host
        description: The domain name of the server
      - in: header
        name: User-Agent
        description: The client application implementing the network protocol for
          communication between          the client and server
      responses:
        200:
          description: OK
      tags:
      - File