# 📄 Google Docs API Documentation

This document provides an overview of selected **Google Docs API** methods.  
It is designed to demonstrate structured **API documentation writing**. 

---

## Table of Contents
- [1. Method: `documents.create`](#1-method-documentscreate)
- [2. Method: `documents.get`](#2-method-documentsget)
- [3. Method: `documents.batchUpdate`](#3-method-documentsbatchupdate)
- [Additional Resources](#-additional-resources)

---

## 1. Method: `documents.create`

**Creates a new blank Google Document.**

### HTTP Request

```http
POST https://docs.googleapis.com/v1/documents
```

### Request Body Parameters

| Field   | Type   | Description                    |
| ------- | ------ | ------------------------------ |
| `title` | string | The title of the new document. |

### Response Body

| Field        | Type   | Description                             |
| ------------ | ------ | --------------------------------------- |
| `documentId` | string | Unique identifier for the new document. |
| `title`      | string | Title of the new document.              |
| `revisionId` | string | Revision ID of the document.            |

### Authorization Scopes
- ```https://www.googleapis.com/auth/documents```

###Example Request

```
POST https://docs.googleapis.com/v1/documents
{
  "title": "Sample Document"
}
```

### Example Response

```
{
  "documentId": "1A2B3C4D5E",
  "title": "Sample Document",
  "revisionId": "abcdef12345"
}
```

---
## 2. Method: `documents.get`

**Retrieves the content and metadata of a Google Document.**

### HTTP Request

```
GET https://docs.googleapis.com/v1/documents/{documentId}
```

### Path Parameters
| Field        | Type   | Description                         |
| ------------ | ------ | ----------------------------------- |
| `documentId` | string | The ID of the document to retrieve. |

### Response Body

| Field     | Type   | Description                       |
| --------- | ------ | --------------------------------- |
| `title`   | string | The title of the document.        |
| `body`    | object | The body content of the document. |
| `headers` | object | The document headers.             |
| `footers` | object | The document footers.             |

### Authorization Scopes

- `https://www.googleapis.com/auth/documents.readonly`

### Example Request

```
GET https://docs.googleapis.com/v1/documents/1A2B3C4D5E
```

### Example Response

```
{
  "title": "Sample Document",
  "body": {
    "content": [
      {
        "paragraph": {
          "elements": [
            { "textRun": { "content": "Hello, world!" } }
          ]
        }
      }
    ]
  }
}
```

## 3. Method: `documents.batchUpdate`
**Applies one or more updates to a document.**

### HTTP Request

```
POST https://docs.googleapis.com/v1/documents/{documentId}:batchUpdate
```

### Path Parameters

| Field        | Type   | Description                       |
| ------------ | ------ | --------------------------------- |
| `documentId` | string | The ID of the document to update. |

### Request Body Parameters

| Field      | Type  | Description                                                                                                                |
| ---------- | ----- | -------------------------------------------------------------------------------------------------------------------------- |
| `requests` | array | A list of update requests. See [Update Types](https://developers.google.com/docs/api/reference/rest/v1/documents/request). |

### Example Request

```
POST https://docs.googleapis.com/v1/documents/1A2B3C4D5E:batchUpdate
{
  "requests": [
    {
      "insertText": {
        "location": {
          "index": 1
        },
        "text": "This is inserted text."
      }
    }
  ]
}

```
### Example Response

```
{
  "documentId": "1A2B3C4D5E",
  "replies": [
    {
      "insertText": {
        "location": { "index": 1 },
        "text": "This is inserted text."
      }
    }
  ]
}

```
## Additional Resources

- [Google Docs API Overview](https://developers.google.com/docs/api/quickstart/js)  
- [Document Structure Guide](https://developers.google.com/docs/api/concepts/structure)  
- [Batch Update Requests](https://developers.google.com/docs/api/reference/rest/v1/documents/request)  

