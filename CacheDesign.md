# Cache Design
1. Get a cache path in cache document
```
    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);
    _diskCachePath = [paths[0] stringByAppendingPathComponent:fullNamespace];
    dispatch_sync(_ioQueue, ^{
        _fileManager = [NSFileManager new];
    });
```
2. Save Data
```
    dispatch_async(self.ioQueue, ^{
        NSData *data = imageData;
            if (data) {
            if (![_fileManager fileExistsAtPath:_diskCachePath]) {
                [_fileManager createDirectoryAtPath:_diskCachePath withIntermediateDirectories:YES attributes:nil error:NULL];
            }
            [_fileManager createFileAtPath:[self defaultCachePathForKey:key] contents:data attributes:nil];
            }
        });
```
