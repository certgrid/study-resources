# Lab 04 - Explore Blob Storage

Blob storage is the answer to most "where do we put unstructured data" questions on the exam. This lab makes containers, blobs, and access tiers concrete.

## Time Needed

15-20 minutes.

## What You Will Learn

- How containers organize blobs
- How to upload a blob and view its URL
- What the Hot, Cool, Cold, and Archive tiers change
- Why blob "folders" are just name prefixes

## DP-900 Concepts Covered

| Concept           | Where you see it in the lab                    |
| ----------------- | ---------------------------------------------- |
| Unstructured data | You upload files as blobs                      |
| Container         | You create the grouping for blobs              |
| Block blob        | Your uploaded file's blob type                 |
| Access tiers      | You change a blob's tier and read the warnings |

## Steps

### 1. Create a container

1. Open the storage account from Lab 03.
2. Select **Containers**, then **+ Container**.
3. Name:

```text
lab-blobs
```

4. Leave access level as **Private**.

### 2. Upload a blob

1. Open the container and select **Upload**.
2. Pick any small file from your computer (an image or text file).
3. Expand **Advanced** before uploading and note the **Blob type** is Block blob and the **Access tier** dropdown.
4. Upload the file.

### 3. Inspect the blob

1. Click the uploaded blob.
2. Note the **URL**: every blob is an object with its own address.
3. Note the properties: blob type, access tier, size.

### 4. Simulate a folder

1. Select **Upload** again, expand **Advanced**, and set "Upload to folder" to `reports/2026`.
2. After upload, notice the "folder" navigation. The blob's real name is just prefixed with `reports/2026/`; the namespace is flat.

### 5. Change the access tier

1. Open a blob and select **Change tier**.
2. Read the options: Hot, Cool, Cold, Archive.
3. Set it to **Cool** and note the warning about early deletion periods and access costs.
4. Do not set Archive on anything you want to open again quickly: archived blobs must be rehydrated before reading, which can take hours.

## Clean Up

Keep the storage account for Lab 05. If you uploaded large files, delete them now; small lab files can wait for [09 - Clean Up Resources](09-clean-up-resources.md).

## Success Criteria

You are done when you can explain:

- What a container is and what a blob is
- Why every blob has a URL and what that implies (object storage)
- When you would pick Hot, Cool, Cold, or Archive
- What is actually happening when the portal shows blob "folders"
