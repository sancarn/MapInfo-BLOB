# General layout

## `MapInfo-BLOB.mb`

This is to be compiled to `MapInfo-BLOB.mbx`. The MBX will implement a ribbon button on the TABLE tab in 64-bit MapInfo. In 32-Bit MapInfo a dropdown menu item in the Table drop down menu will be used instead. The button will execute the `BlobManager`.

## `BlobManager.mb`

* This opens a very simple GUI for managing BLOB data.
* The vision is to have this like a TreeView control displaying blobs in their individual folders (indicated by the name of the blob). Empty folders could be implemented with a zero-sized blob if wanted.
* The BlobManager GUI will contain buttons to add, remove, rename, copy, open and move blob data from the BLOB file to anywhere on the file system.
* The BlobManager simply wraps `MapInfo-BLOB-API.mb` in a GUI. No functionality which exists in `BlobManager.mb` GUI but not in the API should be trivial implementation details. The goal is to make `BlobManager` an implementation example of how to use the API.

## `MapInfo-BLOB-API.mb`

* The core library of `MapInfo-BLOB`. The API is not only supposed to give `MapInfo-BLOB` it's functionality, but also allows other developers to use the API to manipulate their own table's BLOBs.

### Planned Functions:

`sTOFN` stands for 'string Table or File Name'. If `sTOFN` is the name of an open table then the action will be performed on this table. Otherwise if `sTOFN` is a file path, the BLOB file relative to that of the table selected file path is operated on instead.

#### BLOB_GetDict(ByVal sTOFN as string) as string

##### Description

Returns the Blob descriptions for an open table or TAB/BLOB file as a readonly table.

#### BLOB_Add(ByVal sTOFN as string, ByVal ID as LargeInt, ByVal sName as string, ByVal sFilePath as string)

##### Description

Adds a BLOB to an existing table.

#### BLOB_Remove(ByVal sTOFN as string, ByVal ID as LargeInt, ByVal sName as string)

##### Description

Removes a BLOB from an existing table.

#### BLOB_Copy(ByVal sTOFN as string, ByVal ID as LargeInt, ByVal sName as string, ByVal sToPath as string) as string

##### Description

Copies a BLOB from an existing table to a new destination.

#### BLOB_Move(ByVal sTOFN as string, ByVal ID as LargeInt, ByVal sName as string, ByVal sToPath as string) as string

##### Description

Moves a BLOB from an existing table to a new destination.
