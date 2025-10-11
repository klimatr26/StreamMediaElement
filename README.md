# StreamMediaElement — Play Streams in `MediaElement`

This helper adds a single extension method that lets you feed any seekable Stream (e.g., FileStream, MemoryStream, pipe, interop-backed stream) directly into the `CommunityToolkit.Maui.MediaElement`, on Windows, Android, iOS, and Mac Catalyst.

## Usage

One method is provided:

```csharp
using StreamMediaElement;

await mediaElement.SetStreamMediaSource(stream, contentType: "video/mp4");
```
**Content type tips**
| Platform | Expected type string                              | Examples                                                   |
| -------: | ------------------------------------------------- | ---------------------------------------------------------- |
|  Windows | MIME                                              | `video/mp4`, `audio/mpeg`, `video/quicktime`               |
|  Android | MIME (Media3 / ExoPlayer)                         | `video/mp4`, `audio/mpeg`                                  |
|  iOS/mac | **UTType identifier** is safest for `ContentType` | `public.mpeg-4`, `public.mp3`, `com.apple.quicktime-movie` |

## What it does

`SetStreamMediaSource(this MediaElement mediaElement, Stream stream, string contentType = "video/mp4", bool throwIfNotSeekable = false)`
Adapts your .NET Stream to the native media pipeline:

- Windows: wraps with IRandomAccessStream and uses MediaSource.CreateFromStream.
- Android: implements a DataSource for AndroidX Media3 ExoPlayer and plays via a ProgressiveMediaSource.
- iOS/macOS: supplies bytes via AVAssetResourceLoaderDelegate to an AVUrlAsset.


> [!IMPORTANT]
> Requires seekable streams (stream.CanSeek == true). (The throwIfNotSeekable parameter is present for future flexibility; currently a non-seekable stream throws.)

## Note
I have not tested de iOS/MacCatalyst version, but it *may*™ work. Also, I have not permormed any form of thorough testing. I created this just to see if it was possible to do, and it was - at least *on my machine*™.

Just copy and paste the code into your project. :D
