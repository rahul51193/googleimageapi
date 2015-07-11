# Google Image Search API (Deprecated)

<p align="center">
  <img src="https://raw.githubusercontent.com/lukegeiger/googleimageapi/master/1.png">
  <img src="https://raw.githubusercontent.com/lukegeiger/googleimageapi/master/2.png">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/lukegeiger/googleimageapi/master/3.png">
  <img src="https://raw.githubusercontent.com/lukegeiger/googleimageapi/master/4.png">
</p>

# Overview & Goals

The purpose of this project was to use the deprecated Google Image Search API, found [here](https://developers.google.com/image-search/). Below are the goals.

- 3 images in a row using a UIScrollView.
- Save search history.
- Incremental loading when a user scrolls to the bottom of the page.

# API

I created a Singleton wrapper that fetches photos from the API, below is a sample of how it works.

```objective-c

  [[GImageAPI sharedAPI]fetchPhotosForQuery:search.query onCompletion:^(NSArray*gimages,NSError*error){
        
  }];
    
```

# Models

There are two model objects in this project, the *GImage* which is a Cocoa Touch Representation of a Google Image, and a *Search* which is a user search.

```GImage.h
@interface GImage : NSObject

/*
 Supplies the title of the image, which is usually the base filename (for example, monkey.png.)
*/
@property (nonatomic, readonly) NSString *imageTitle;

/*
 Supplies a brief snippet of information from the page associated with the image result.
 */
@property (nonatomic, readonly) NSString *content;

/*
 Unique ID
 */
@property (nonatomic, readonly) NSString *imageId;

/*
 Supplies the height and width, in pixels, of the image.
 */
@property (nonatomic, readonly) CGSize size;

/*
 Supplies the URL of a image.

 */
@property (nonatomic, readonly) NSURL* url;

/*
 Supplies the URL of a thumbnail image.
 */
@property (nonatomic, readonly) NSURL* thumbURL;

/*
 Supplies the height and width, in pixels, of the image thumbnail.
 */
@property (nonatomic, assign) CGSize thumbSize;

/*
 Turns a Google Image JSON dictionary into a Cocoa Touch Object
 @param dict a json dictionary
 @return a cocoa touch representation of a google image
 */
+(GImage*)gImageFromDict:(NSDictionary*)dict;

@end

```

```Search.h
@interface Search : NSManagedObject

/*
 The search text.
 */
@property (nonatomic, retain) NSString * query;

/*
 The last time this search was searched.
 */
@property (nonatomic, retain) NSDate * lastSearchDate;

/*
 Returns a new search, or an existing search if the query paramter matches a previous query
*/
+(Search*)searchForQuery:(NSString*)query inContext:(NSManagedObjectContext*)context;

@end

```

# CocoaPods

I used a few CocoaPods in this project, including one of my own. Below is the list.

- AFNetworking
- MBProgressHUD
- LGSemiModalNavController (This is my pod)
- SDWebImage

# Possible Improvements

- Stop using the Deprecated API.
- Rework the GImageAPI singleton.
- Empty data sets images.
