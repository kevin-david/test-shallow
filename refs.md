# Git refs

## Get a list of references

```httprequest
GET https://{account}.VisualStudio.com/DefaultCollection/git[/{project}]/repositories/{repository}/refs[/{filter}]
```

| Parameter  | Type   | Notes
|:-----------|:------:|:----------------------------------------------------------------------------------------------------------------------------
| account    | string | Your Visual Studio Online account, or use http://{server}:{port}/tfs/{collection} if you use TFS on-premises.
| project    | string | Name or ID of the project that contains the [repository](repositories).
| repository | string | Name or ID of the [repository](repositories). If you identify the repository by name, you have to specify the project, too.
| filter     | string | The reference name always starts with "heads/". "heads/ma" would return "heads/master" and "heads/main", for example.

### Unfiltered

<div id="GET__git_repositories__repositoryId__refs_json"></div>

### Filtered

<div id="GET__git_repositories__repositoryId__refs__filter__json"></div>

## Update or create references
Updates or creates references based on the input parameters. Returns the status of each request. 
```httprequest
POST https://{account}.VisualStudio.com/DefaultCollection/git[/{project}]/repositories/{repository}/refs
```
| URL Parameter   | Type   | Notes
|:------------|:------:|:----------------------------------------------------------------------------------------------------------------------------
| account     | string | Your Visual Studio Online account, or use http://{server}:{port}/tfs/{collection} if you use TFS on-premises.
| project     | string | Name or ID of the project that contains the [repository](repositories).
| repository  | string | Name or ID of the [repository](repositories). If you identify the repository by name, you have to specify the project, too.

| Request Body <br /> Parameter | Type   | Notes
|:---------|:------:|:----------------------------------------------------------------------------------------------------------------------------
| Name        | string | Name of the ref to update. Currently, only refs/{heads,notes,tags}/... are supported.
| oldObjectId | string | Old object id as a 40-character SHA1 hash. All zeros if creating a new ref.
| newObjectId | string | New object id as a 40-character SHA1 hash. All zeros if deleting a ref.


### Examples
<b>Example 1</b> Create a tag in a non-existent namespace (refs/currently/unsupported - currently unsupported on the server), delete a tag (refs/tags/first_tag), and update a branch (refs/heads/master)

#### Before (Using Get refs above)

```json
{
    "count": 3,
    "value": [
        {
            "name": "refs/heads/master",
            "objectId": "08eddb2a7d206a8678f5b0913e3ba1572d401617"
        },
        {
            "name": "refs/heads/second_branch",
            "objectId": "f540d74a1c50ada11d2912b24cd94c5613637b59"
        },
        {
            "name": "refs/tags/first_tag",
            "objectId": "08eddb2a7d206a8678f5b0913e3ba1572d401617"
        }
    ]
}
```

<div id="POST_refs_ex1_json"></div>

#### After (Using Get refs above)
```json
{
    "count": 2,
    "value": [
        {
            "name": "refs/heads/master",
            "objectId": "f540d74a1c50ada11d2912b24cd94c5613637b59"
        },
        {
            "name": "refs/heads/second_branch",
            "objectId": "f540d74a1c50ada11d2912b24cd94c5613637b59"
        }
    ]
}
```
