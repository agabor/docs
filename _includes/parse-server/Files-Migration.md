In order of priority and easiest to hardest, here's how we should allow files migration from Hosted MSG to MSG Server:

### In Flight

Parse Server knows how to access and read existing files in Hosted MSG S3. We should make so that whenever we have a request for a file still on Hosted MSG, MSG Server downloads the original, uploads it to your file store and updates the reference in Mongo. This should probably be an option, maybe not everyone wants to allow this?

* Pros: Easy to implement, seamless for users
* Cons: Small latency hit the first time we copy the file (although we could just redirect and defer the download), could potentially miss some never accessed files, how to deal with concurrency?

### Mongo Objects

Have a helper script in MSG Server that looks up the Schema places with known file objects, iterates over all those object and copies them to the new data store using the file adapter.

* Pros: guaranties that all referenced files are copied, would allow you to migrate from one file adapter to another
* Cons: can be costly and take a long time to iterate on all Mongo objects for large apps, what to do for file objects within objects/arrays?

### S3 Listing

We could have an API on Hosted MSG that once authenticated, returns the list of all the files an app has in S3 by doing a listing on the bucket.

* Pros: users control how they want to sync their files, ability to download all files even those deleted in Mongo
* Cons: need to implement some API on Hosted MSG for security, listing job can take a long time for apps with lots of files