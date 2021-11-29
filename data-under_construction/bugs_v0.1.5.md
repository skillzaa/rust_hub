## Bugs version 0.1.5

1. Once ./data folder is created it should never be over-written. Only the user can remove files from it manually.
2. There should never be a panic just accurate messages. There should be some app level error number and appropriate messages with it.Have your own Error object and make it available at app level.
3. Always over-write the ./site folder before gen since it may have old files remaining in it which has been removed from data folder. 